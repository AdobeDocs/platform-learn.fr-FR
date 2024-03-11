---
title: Configuration d’un espace de noms d’identité
description: Découvrez comment configurer les espaces de noms d’identité à utiliser avec le SDK Web de Adobe Experience Platform. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK,Tags,Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 8%

---

# Configuration d’un espace de noms d’identité


>[!CAUTION]
>
>Nous prévoyons de publier les modifications majeures de ce tutoriel le vendredi 15 mars 2024. Après ce point, de nombreux exercices changeront et vous devrez peut-être redémarrer le tutoriel dès le début pour terminer toutes les leçons.

Découvrez comment configurer les espaces de noms d’identité à utiliser avec le SDK Web de Adobe Experience Platform.

La variable [Service Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr) définit un identifiant visiteur commun à toutes les solutions Adobe afin d’optimiser les fonctionnalités Experience Cloud telles que le partage d’audience entre les solutions. Vous pouvez également envoyer vos propres ID de client au service pour permettre le ciblage entre appareils et les intégrations avec d’autres systèmes, tels que votre système de gestion de la relation client (CRM).

Si votre site web utilise déjà le service d’ID Experience Cloud sur votre site web (via l’API visiteur ou l’extension de balise du service d’ID Experience Cloud) et que vous souhaitez continuer à l’utiliser lors de la migration vers le SDK Web Adobe Experience Platform, vous devez utiliser la dernière version de l’API visiteur ou l’extension de balise du service d’ID Experience Cloud. Voir [Migration des identifiants](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) pour plus d’informations.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon vous permettent de capturer les détails d’identité d’un client fictif connecté à la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) à l&#39;aide des informations d&#39;identification, **utilisateur : test@adobe.com / password: test**. Bien que vous puissiez utiliser ces étapes pour créer une identité différente à vos propres fins, pour découvrir les fonctionnalités de la carte des identités dans l’interface de collecte de données, il est recommandé de suivre d’abord pour capturer l’exemple d’identité.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Présentation des espaces de noms d’identité
* Création d’un espace de noms d’identité personnalisé pour capturer un identifiant CRM interne


## Conditions préalables

Vous devez avoir terminé les leçons précédentes :

* [Configuration des autorisations](configure-permissions.md)
* [Configuration des schémas](configure-schemas.md)

>[!IMPORTANT]
>
>La variable [Extension d’ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) n’est pas nécessaire lors de l’implémentation du SDK Web de Adobe Experience Platform, car la bibliothèque JavaScript du SDK Web contient la fonctionnalité du service d’identification des visiteurs.

## Création d’un espace de noms d’identité

Dans cet exercice, vous créez un espace de noms d’identité pour le champ d’identité personnalisé de Luma, `lumaCrmId`. Les espaces de noms d’identité jouent un rôle essentiel dans la création de profils clients en temps réel, car deux valeurs correspondantes dans le même espace de noms permettent à deux sources de données de former un graphique d’identité.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur l’identité dans Adobe Experience Platform :
>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Maintenant, créez un espace de noms pour l’ID de gestion de la relation client Luma :

1. Ouvrez le [Interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Sélectionnez l’environnement de test que vous utilisez pour le tutoriel

   >[!NOTE]
   >
   >Si vous êtes le client d’une application basée sur Platform comme Real-Time CDP, nous vous recommandons d’utiliser un environnement de test de développement pour ce tutoriel. Si ce n’est pas le cas, utilisez le **[!UICONTROL Prod]** sandbox.

1. Sélectionner **[!UICONTROL Identités]** dans la navigation de gauche
1. Sélectionner **[!UICONTROL Parcourir]**

   Une liste d’espaces de noms d’identité s’affiche dans l’interface principale de la page, indiquant leurs noms, symboles d’identité, la date de la dernière mise à jour et s’ils sont des espaces de noms standard ou personnalisés. Le rail de droite contient des informations sur la force du graphique d’identités.

1. Sélectionner **[!UICONTROL Créer un espace de noms d’identité]**

   ![Affichage des identités](assets/configure-identities-screen.png)

1. Indiquez les détails suivants et sélectionnez **[!UICONTROL Créer]**.

   | Champ | Valeur |
   |---------------|-----------|
   | Nom d’affichage | Identifiant Luma CRM |
   | Symbole d’identité | lumaCrmId |
   | Type | Identifiant multi-appareils |


   ![Création d’espaces de noms.](assets/identities-create-namespace.png)


   L’espace de noms Identity est renseigné dans la variable **[!UICONTROL Identités]** écran.

   ![Création d’espaces de noms.](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> Dans le [Création d’éléments de données](create-data-elements.md) leçon : vous apprendrez à utiliser cet espace de noms lors de l’envoi d’identités à Platform Edge Network.

## Création de l’espace de noms d’identité dans votre environnement de test de production

En raison d’une limitation actuelle de l’extension SDK Web, les espaces de noms d’identité doivent également être créés dans l’environnement de test de production afin d’utiliser l’espace de noms pour envoyer des données à un environnement de test de développement. Ainsi, si vous avez utilisé un environnement de test de développement pour ce tutoriel, créez également la variable `Luma CRM ID` dans votre environnement de test de production.

## Ressources supplémentaires

* [Documentation d’Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr)
* [API Service d’identités](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Maintenant que les identités sont en place, le flux de données peut être configuré.

[Suivant : ](configure-datastream.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
