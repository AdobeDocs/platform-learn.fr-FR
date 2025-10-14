---
title: Offer Decisioning - Configuration de vos offres et de votre identifiant de décision
description: Offer Decisioning - Configuration de vos offres et de votre identifiant de décision
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 13%

---

# 3.7.2 Configuration de vos offres et de votre décision

## 3.7.2.1 Créer vos offres personnalisées

Dans cet exercice, vous allez créer quatre **Offres personnalisées**. Voici les détails à prendre en compte lors de la création de ces offres :

| Nom | Période | Lien d’image pour l’e-mail | Lien de l’image pour le Web | Texte | Priorité | Admissibilité | Langue | Fréquence de limitation | Nom de l’image |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | aujourd’hui - 1 mois plus tard | https://bit.ly/4a9RJ5d | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | all - Clientes | Anglais (États-Unis) | 3 | Apple AirPods Max- Femme.jpg |
| `--aepUserLdap-- - Galaxy S24` | aujourd’hui - 1 mois plus tard | https://bit.ly/3W8yuDv | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | all - Clientes | Anglais (États-Unis) | 3 | Galaxy S24 - Femme.jpg |
| `--aepUserLdap-- - Apple Watch` | aujourd’hui - 1 mois plus tard | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | all - Clients | Anglais (États-Unis) | 3 | Apple Watch - Masculin.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | aujourd’hui - 1 mois plus tard | https://bit.ly/4gTrkeo | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | all - Clients | Anglais (États-Unis) | 3 | Galaxy Watch7 - Homme.jpg |

{style="table-layout:auto"}

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Étapes suivantes

Accédez à [3.7.3 Configuration de Web SDK pour Experience Decisioning](./ex3.md){target="_blank"}

Revenez à [&#x200B; Experience Decisioning &#x200B;](ajo-decisioning.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
