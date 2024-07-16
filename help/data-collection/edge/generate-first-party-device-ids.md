---
title: Génération d’identifiants d’appareil propriétaires
description: Découvrez comment générer des identifiants d’appareil propriétaires
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Génération d’identifiants d’appareil propriétaires

Les applications Adobe Experience Cloud ont traditionnellement généré des cookies pour stocker les identifiants d’appareil à l’aide de différentes technologies, notamment :

1. Cookies tiers
1. Cookies propriétaires définis par un serveur Adobe à l’aide de la configuration CNAME d’un nom de domaine
1. Cookies propriétaires définis par JavaScript

Les modifications récentes du navigateur limitent la durée de ces types de cookies. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur détenu par le client à l’aide d’un enregistrement DNS A/AAAA plutôt que d’un CNAME DNS. La fonctionnalité d’identifiant d’appareil propriétaire (FPID) permet aux clients implémentant le SDK Web de Adobe Experience Platform d’utiliser les identifiants d’appareil dans les cookies des serveurs utilisant des enregistrements DNS A/AAAA. Ces identifiants peuvent ensuite être envoyés à Adobe et utilisés comme graines pour générer des identifiants Experience Cloud (ECID), qui reste l’identifiant principal dans les applications Adobe Experience Cloud.

Voici un exemple rapide du fonctionnement de cette fonctionnalité :

![ ID d’appareils propriétaires (FPID) et ID Experience Cloud (ECID)](../assets/kt-9728.png)

1. Le navigateur d’un utilisateur final demande une page Web au serveur Web ou au réseau de diffusion de contenu d’un client.
1. Le client génère un identifiant d’appareil (FPID) sur son serveur web ou CDN (le serveur web doit être associé à l’enregistrement DNS A/AAAA du nom de domaine).
1. Le client définit un cookie propriétaire pour stocker le FPID dans le navigateur de l’utilisateur final.
1. L’implémentation du SDK Web Adobe Experience Platform du client émet une requête à l’Edge Network Platform, y compris le FPID dans la carte d’identité.
1. L’Edge Network Experience Platform reçoit le FPID et l’utilise pour générer un identifiant Experience Cloud (ECID).
1. La réponse du SDK Web Platform envoie l’ECID à son navigateur.
1. Si le `idMigrationEnabled=true`, le SDK Web de Platform utilise JavaScript pour stocker l’ECID en tant que cookie `AMCV_` dans le navigateur de l’utilisateur final.
1. Dans le cas où le cookie `AMCV_` expire, le processus se répète. Tant que le même identifiant d’appareil propriétaire est disponible, un nouveau cookie `AMCV_` est créé avec la même valeur ECID qu’auparavant.

>[!NOTE]
>
>`idMigrationEnabled` n’a pas besoin d’être défini sur `true` pour utiliser FPID. Avec `idMigrationEnabled=false`, vous ne verrez peut-être pas de cookie `AMCV_` et devrez rechercher la valeur ECID dans la réponse réseau.


Dans ce tutoriel, un exemple spécifique utilisant le langage de script PHP est utilisé pour montrer comment :

* Génération d’un UUIDv4
* Écrire une valeur UIDv4 dans un cookie
* Inclure la valeur du cookie dans la carte d’identité
* Validation de la génération d’ECID

Vous trouverez plus d’informations sur les ID d’appareils propriétaires dans la documentation du produit.

## Génération d’un UUIDv4

PHP n’a pas de bibliothèque native pour la génération d’UUID. Par conséquent, ces exemples de code sont plus étendus que ce qui serait probablement nécessaire si un autre langage de programmation était utilisé. PHP a été choisi pour cet exemple car il s’agit d’un langage côté serveur largement pris en charge.


Lorsque la fonction suivante est appelée, elle génère un UUID aléatoire version 4 :

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## Écrire une valeur UIDv4 dans un cookie

Le code suivant émet une requête à la fonction ci-dessus pour générer un UUID. Il définit ensuite les indicateurs de cookie décidés par votre organisation. Si un cookie a déjà été généré, l’expiration est étendue.

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>Le cookie qui contient l’identifiant d’appareil propriétaire peut porter n’importe quel nom.

## Inclure la valeur du cookie dans la carte des identités

La dernière étape consiste à utiliser PHP pour faire écho à la valeur du cookie dans la carte des identités.


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>Le symbole de l’espace de noms d’identité utilisé dans la carte d’identité doit être appelé `FPID`.
>
> `FPID` est un espace de noms d’identité réservé qui n’est pas visible dans les listes d’interface des espaces de noms d’identité.


## Validation de la génération d’ECID

Validez l’implémentation en confirmant que le même ECID est généré à partir de votre identifiant d’appareil propriétaire :

1. Générez un cookie FPID.
1. Envoyez une requête à l’Edge Network Platform à l’aide du SDK Web Platform.
1. Un cookie au format `AMCV_<IMSORGID@AdobeOrg>` est généré. Ce cookie contient l’ECID.
1. Notez la valeur du cookie qui est générée, puis supprimez tous les cookies de votre site, à l’exception du cookie `FPID`.
1. Envoyez une autre requête à l’Edge Network Platform.
1. Vérifiez que la valeur du cookie `AMCV_<IMSORGID@AdobeOrg>` est la même valeur `ECID` que dans le cookie `AMCV_` qui a été supprimé. Si la valeur du cookie est identique pour un FPID donné, le processus d’ensemencement de l’ECID a réussi.

Pour plus d’informations sur cette fonctionnalité, voir [la documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
