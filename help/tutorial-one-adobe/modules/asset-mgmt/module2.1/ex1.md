---
title: Création de votre programme Cloud Manager
description: Création de votre programme Cloud Manager
kt: 5342
doc-type: tutorial
exl-id: fda247eb-1865-4936-b46e-84128ccab357
source-git-commit: 490bc79332bb84520ba084ec784ea3ef48a68fb5
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 3%

---

# 1.1.1 Création de votre programme Cloud Manager

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`. Vous verrez alors quelque chose comme ceci. Cliquez sur **Ajouter un programme**.

![ AEMCS ](./images/aemcs1.png)

Pour le **Nom du programme**, utilisez `--aepUserLdap-- - CitiSignal AEM+ACCS`. Sélectionnez l’option **Configurer un sandbox**. Cliquez sur **Continuer**.

![ AEMCS ](./images/aemcs2.png)

Assurez-vous que les options suivantes sont sélectionnées :

- Sites
- Formulaires
- Ressources

Cliquez sur la flèche de **Assets** pour afficher la liste des options.

![ AEMCS ](./images/aemcs3.png)

Assurez-vous que les options suivantes sont sélectionnées :

- Content Hub

Faites défiler la liste vers le bas.

![ AEMCS ](./images/aemcs3a.png)

Assurez-vous que les options suivantes sont sélectionnées :

- Edge Delivery Services
- Dynamic Media

Cliquez sur **Créer**.

![ AEMCS ](./images/aemcs3b.png)

La création de votre environnement prendra du temps, entre 10 et 20 minutes.

![ AEMCS ](./images/aemcs4.png)

Une fois les environnements créés et prêts à l’emploi, vous recevrez un e-mail de confirmation avant de revenir ici.

![ AEMCS ](./images/aemcs5.png)

Une fois que vous avez reçu votre confirmation par e-mail, revenez sur [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Vous verrez alors que le statut de votre programme est passé à **Prêt**. Cliquez sur votre programme pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png)

Consultez l’onglet **Pipelines**. Cliquez sur le **de 3 points...**, puis sur **Exécuter**.

![ AEMCS ](./images/aemcs7.png)

Cliquez sur **Exécuter**.

![ AEMCS ](./images/aemcs8.png)

Cliquez ensuite sur le **de 3 points...** dans l’onglet **Environnements** et cliquez sur **Afficher les détails**.

![ AEMCS ](./images/aemcs9.png)

Vous verrez ensuite les détails de votre environnement, y compris l’URL de votre environnement **de création**, dont vous aurez besoin dans l’exercice suivant.

Jetez un coup d’œil à la ligne **Content Hub**, puis sélectionnez **Cliquer pour activer**.

![ AEMCS ](./images/aemcs10.png)

Cliquez sur **Activer**.

![ AEMCS ](./images/aemcsact1.png)

L&#39;activation de **Content Hub** a maintenant commencé. Cela peut prendre 10 minutes ou plus.

![ AEMCS ](./images/aemcsact2.png)

Au bout d’environ 10 minutes, l’activation de **Content Hub** sera terminée.
Ensuite, jetez un coup d’œil à la ligne **Dynamic Media** et sélectionnez **Cliquer pour activer**.

![ AEMCS ](./images/aemcsact3.png)

Cliquez sur **Activer**.

![ AEMCS ](./images/aemcsact4.png)

L’activation de **Dynamic Media** a maintenant commencé. Cela peut prendre 10 minutes ou plus.

![ AEMCS ](./images/aemcsact5.png)

Au bout d’environ 10 minutes, l’activation de **Dynamic Media** est terminée.

![ AEMCS ](./images/aemcsact6.png)

Une fois l’exécution du pipeline terminée, vous pouvez passer à l’exercice suivant.

Étape suivante : [Configuration de votre environnement AEM CS](./ex3.md){target="_blank"}

Revenir à [Adobe Experience Manager Cloud Service et Edge Delivery Services](./aemcs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
