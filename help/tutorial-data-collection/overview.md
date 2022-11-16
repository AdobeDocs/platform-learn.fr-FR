---
title: Aperçu
description: Aperçu
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 2%

---

# Utilisation de la collecte de données Adobe Experience Platform

La collecte de données sur les événements se produisant dans le navigateur d’un utilisateur est un principe fondamental de la stratégie marketing. Adobe propose plusieurs outils pour vous aider à gérer ces données. Bien que vous puissiez vous familiariser avec chacun de ces outils individuellement, ce tutoriel tente de fournir une vue plus large de ce que chacun de ces outils font et de la manière dont ils travaillent ensemble pour atteindre un objectif commun.

Dans ce tutoriel, nous abordons une stratégie pour :

1. Structurer et conserver vos données dans Adobe Experience Platform,
1. Gestion de vos données dans le navigateur et communication de l’existence de certains événements, et
1. Réagir à ces événements en envoyant les données appropriées à Adobe Experience Platform.

Bien que ce tutoriel utilise la couche de données client Adobe, le SDK Web Adobe Experience Platform et le [!DNL Tags] pour une mise en oeuvre plus prescriptive et transparente, vous pouvez également mélanger ces outils à des outils tiers ou internes pour une flexibilité ultime.

## Exemple de scénario

Au cours de ce tutoriel, vous implémentez la collecte de données pour une page de produit simple sur un site de commerce électronique :

1. La page du produit est chargée dans le navigateur. Vous pouvez effectuer ici le suivi de l’utilisateur qui a consulté le produit.
1. L’utilisateur décide d’acheter le produit, il clique donc sur un bouton pour ajouter le produit à son panier. Ici, vous pouvez vérifier que l’utilisateur a ouvert un nouveau panier et ajouté le produit au panier en envoyant des événements d’expérience à Adobe Experience Platform.
1. Enfin, l’utilisateur clique sur un _Téléchargement de l’application_ car votre application mobile les intéresse. Vérifiez que l’utilisateur a cliqué sur le lien.

C’est parti !

[Suivant : ](structuring-your-data.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
