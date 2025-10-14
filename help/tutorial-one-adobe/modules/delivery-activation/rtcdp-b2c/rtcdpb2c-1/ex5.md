---
title: Voir votre profil client en temps réel en action dans le centre d’appels
description: Voir votre profil client en temps réel en action dans le centre d’appels
kt: 5342
doc-type: tutorial
exl-id: d3bd34a1-5577-4da7-a5a5-0f186b1a73c2
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 3%

---

# 2.1.5 Consultez votre profil client en temps réel en action dans le centre d’appels

Dans cet exercice, l’objectif est de vous faire parcourir le parcours client et d’agir comme un véritable client.

Sur ce site web, nous avons implémenté Adobe Experience Platform. Chaque action est considérée comme un événement d’expérience et est envoyée à Adobe Experience Platform en temps réel, ce qui complète le profil client en temps réel.

Dans un exercice précédent, vous avez commencé en tant que client anonyme qui navigue sur le site et, après quelques étapes, vous êtes devenu un client connu.

Lorsque ce même client décroche son téléphone et appelle votre centre d’appels, il est essentiel que les informations provenant d’autres canaux soient disponibles immédiatement, afin que l’expérience du centre d’appels puisse être pertinente et personnalisée.

## Utilisation de l’application CX

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **3 points...** de votre projet d&#39;application CX, puis cliquez sur **Modifier** pour l&#39;ouvrir.

![Démonstration](./images/cxapp3.png)

Dans votre projet d’application CX, accédez à **Intégrations**. Cliquez sur **Sélectionner l’environnement**.

![Démonstration](./images/cxapp3a.png)

Sélectionnez la propriété Collecte de données Adobe Experience Platform qui a été créée dans Prise en main. Vous devez sélectionner la propriété dont le nom contient **(cx-app)**.

![Démonstration](./images/cxapp4.png)

Tu verras ça. Cliquez sur **Exécuter**.

![Démonstration](./images/cxapp4a.png)

Ensuite, vous devez sélectionner l’une de vos identités et l’espace de noms correspondant, puis cliquer sur le **icône-de-recherche**.

![Profil client](./images/identities.png)

| Identité | Espace de noms |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 79943948563923140522865572770524243489 |
| Experience Cloud ID (ECID) | 70559351147248820114888181867542007989 |
| ID d’e-mail | woutervangeluwe+18112024-01@gmail.com |
| ID du numéro de mobile | +32473622044+18112024-01 |

![Démonstration](./images/19.png)

Vous verrez maintenant les informations qui seraient idéalement affichées dans le centre d’appels, de sorte que les agents du centre d’appels disposent de toutes les informations pertinentes immédiatement lorsqu’ils parlent à un client.

![Démonstration](./images/20.png)

## Étapes suivantes

Accédez à [&#x200B; Résumé et avantages &#x200B;](./summary.md){target="_blank"}

Revenez au [profil client en temps réel](./real-time-customer-profile.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
