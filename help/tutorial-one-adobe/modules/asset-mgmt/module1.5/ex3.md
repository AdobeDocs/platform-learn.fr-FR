---
title: Connexion d’ACCS au serveur de collecte de données AEM Assets
description: Connexion d’ACCS au serveur de collecte de données AEM Assets
kt: 5342
doc-type: tutorial
source-git-commit: 16229700449660a085549a37013e015a5e20ba9e
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---

# 1.5.3 Connexion d’ACCS à AEM Assets CS

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement AEM Sites et Assets CS avec EDS fonctionnel.
>
>Si vous ne disposez pas encore d’un tel environnement, passez à l’exercice [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Sites et Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

![ACCS+AEM Assets](./images/accsaemassets1.png)


## 1.5.3.4 Update config.json

Ajoutez le fragment de code ci-dessous sous la ligne 6 `"ac-environment-id":XXX` :

```json
 "commerce-assets-enabled": "true",
```



Étape suivante : [Résumé et avantages](./summary.md){target="_blank"}

Revenir à [Adobe Commerce as a Cloud Service](./accs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
