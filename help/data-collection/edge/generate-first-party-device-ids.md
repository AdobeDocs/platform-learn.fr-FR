---
title: Générer des identifiants d’appareil propriétaires
description: Découvrez comment générer des identifiants d’appareil propriétaires
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: fd60f7ad338c81f5b32e7951d5a00b49c5aa1756
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Générer des identifiants d’appareil propriétaires

Les applications Adobe Experience Cloud génèrent traditionnellement des cookies pour stocker les identifiants d’appareils à l’aide de différentes technologies, notamment :

1. Cookies tiers
1. Cookies propriétaires définis par un serveur Adobe à l’aide de la configuration CNAME d’un nom de domaine
1. Cookies propriétaires définis par JavaScript

Des modifications récentes apportées au navigateur limitent la durée de ces types de cookies. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur détenu par le client à l’aide d’un enregistrement DNS A/AAAA plutôt que d’un CNAME DNS. La fonctionnalité [Identifiant d’appareil interne (FPID)](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/identity/first-party-device-ids) permet aux clients implémentant Adobe Experience Platform Web SDK d’utiliser les identifiants d’appareil dans les cookies des serveurs à l’aide des enregistrements DNS A/AAAA. Ces identifiants peuvent ensuite être envoyés à Adobe et utilisés comme adresses de contrôle pour générer des identifiants Experience Cloud (ECID), qui restent l’identifiant principal dans les applications Adobe Experience Cloud.

Voici un exemple rapide de la manière dont cette fonctionnalité fonctionne :

![Identifiants d’appareils propriétaires (FPID) et identifiants Experience Cloud (ECID)](../assets/kt-9728.png)

1. Le navigateur d’un utilisateur final demande une page web au serveur web ou au réseau CDN d’un client.
1. Le client génère un identifiant d’appareil (FPID) sur son serveur web ou réseau CDN (le serveur web doit être lié à l’enregistrement DNS A/AAAA du nom de domaine).
1. Le client définit un cookie propriétaire pour stocker le FPID dans le navigateur de l’utilisateur final.
1. L’implémentation de Adobe Experience Platform Web SDK du client envoie une requête à Platform Edge Network et :
   1. Inclut le FPID dans le mappage d’identités.
   1. Configure un CNAME pour ses requêtes Web SDK et configure son flux de données avec le nom de son cookie FPID.
1. Experience Platform Edge Network reçoit le FPID et l’utilise pour générer un Experience Cloud ID (ECID).
1. La réponse de Platform Web SDK renvoie l’ECID au navigateur de l’utilisateur final.
1. Si le `idMigrationEnabled=true` est , Platform Web SDK utilise JavaScript pour stocker l’ECID en tant que cookie `AMCV_` dans le navigateur de l’utilisateur final.
1. Dans le cas où le cookie `AMCV_` expire, le processus se répète. Tant que le même identifiant d’appareil interne est disponible, un nouveau cookie `AMCV_` est créé avec la même valeur ECID qu’auparavant.

>[!NOTE]
>
>Il n’est pas nécessaire de définir le `idMigrationEnabled` sur `true` pour utiliser le FPID. Toutefois, avec `idMigrationEnabled=false`, vous ne verrez peut-être pas de cookie `AMCV_` et devrez rechercher la valeur ECID dans la réponse réseau.


Pour ce tutoriel, un exemple spécifique utilisant le langage de script PHP est utilisé pour montrer comment :

* Générer un UUIDv4
* Écrire la valeur UUIDv4 dans un cookie
* Inclure la valeur du cookie dans le mappage d’identités
* Valider la génération d’ECID

Vous trouverez plus d’informations sur les identifiants d’appareils propriétaires dans la documentation du produit.

## Générer un UUIDv4

PHP n&#39;a pas de bibliothèque native pour la génération d&#39;UUID, donc ces exemples de code sont plus étendus que ce qui serait nécessaire si un autre langage de programmation était utilisé. PHP a été choisi pour cet exemple parce que c&#39;est un langage côté serveur largement pris en charge.


Lorsque la fonction suivante est appelée, elle génère un UUID aléatoire version-4 :

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

## Écrire la valeur UUIDv4 dans un cookie

Le code suivant envoie une requête à la fonction ci-dessus pour générer un UUID. Il définit ensuite les indicateurs de cookie décidés par votre organisation. Si un cookie a déjà été généré, l’expiration est prolongée.

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
>Le cookie qui contient l’identifiant d’appareil propriétaire peut avoir n’importe quel nom.

## Inclure la valeur du cookie dans le mappage d’identités

La dernière étape consiste à utiliser PHP pour faire écho à la valeur du cookie dans le mappage d&#39;identité.


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
>Le symbole d’espace de noms d’identité utilisé dans le mappage d’identités doit être appelé `FPID`.
>
> `FPID` est un espace de noms d’identité réservé qui n’est pas visible dans les listes d’interface des espaces de noms d’identité.


## Valider la génération d’ECID

Validez la mise en œuvre en confirmant que le même ECID est généré à partir de votre identifiant d’appareil interne :

1. Générez un cookie FPID.
1. Envoyez une requête à Platform Edge Network à l’aide de Platform Web SDK.
1. Un cookie au format `AMCV_<IMSORGID@AdobeOrg>` est généré. Ce cookie contient l’ECID.
1. Notez la valeur du cookie généré, puis supprimez tous les cookies de votre site, à l’exception du cookie `FPID`.
1. Envoyez une autre requête à Platform Edge Network.
1. Vérifiez que la valeur dans le cookie `AMCV_<IMSORGID@AdobeOrg>` est la même `ECID` que dans le cookie `AMCV_` qui a été supprimé. Si la valeur du cookie est identique pour un FPID donné, le processus d’amorçage de l’ECID a réussi.

Pour plus d’informations sur cette fonctionnalité, consultez [la documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
