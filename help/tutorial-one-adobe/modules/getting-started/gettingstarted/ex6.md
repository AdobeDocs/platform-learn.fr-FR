---
title: Prise en main - Adobe I/O
description: Prise en main - Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: cc8efbdbcf90607f5a9bc98a2e787b61b4cd66d9
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 4%

---

# Configuration de votre projet Adobe I/O

## Création de votre projet Adobe I/O

Dans cet exercice, Adobe I/O est utilisé pour interroger divers points d’entrée Adobe. Pour configurer Adobe I/O, procédez comme suit.

Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nouvelle intégration Adobe I/O](./images/iohome.png){zoomable="yes"}

Veillez à sélectionner l’instance appropriée dans le coin supérieur droit de l’écran. Votre instance est `--aepImsOrgName--`.

>[!NOTE]
>
> La capture d’écran ci-dessous montre une organisation spécifique sélectionnée. Lorsque vous parcourez ce tutoriel, il est très probable que votre organisation porte un nom différent. Lorsque vous vous êtes inscrit à ce tutoriel, les détails de l’environnement à utiliser vous ont été fournis. Veuillez suivre ces instructions.

Sélectionnez ensuite **Créer un projet**.

![Nouvelle intégration Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API FIREFLY SERVICES

Vous devriez alors voir ceci. Sélectionnez **+ Ajouter au projet** et choisissez **API**.

![Nouvelle intégration Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Votre écran devrait ressembler à ceci.

![Nouvelle intégration Adobe I/O](./images/api1.png){zoomable="yes"}

Sélectionnez **Creative Cloud** puis choisissez **Firefly - Firefly Services**, puis sélectionnez **Suivant**.

![Nouvelle intégration Adobe I/O](./images/api3.png){zoomable="yes"}

Attribuez un nom à vos informations d’identification : `--aepUserLdap-- - One Adobe OAuth credential`, puis sélectionnez **Suivant**.

![Nouvelle intégration Adobe I/O](./images/api4.png){zoomable="yes"}

Sélectionnez le profil par défaut **Configuration Firefly Services par défaut** et sélectionnez **Enregistrer l’API configurée**.

![Nouvelle intégration Adobe I/O](./images/api9.png){zoomable="yes"}

Vous devriez alors voir ceci.

![Nouvelle intégration Adobe I/O](./images/api10.png){zoomable="yes"}

### API PHOTOSHOP SERVICES

Sélectionnez **+ Ajouter au projet** puis sélectionnez **API**.

![ Stockage Azure ](./images/ps2.png){zoomable="yes"}

Sélectionnez **Creative Cloud** puis **Photoshop - Firefly Services**. Sélectionnez **Suivant**.

![ Stockage Azure ](./images/ps3.png){zoomable="yes"}

Sélectionnez **Suivant**.

![ Stockage Azure ](./images/ps4.png){zoomable="yes"}

Ensuite, vous devez sélectionner un profil de produit qui définit les autorisations disponibles pour cette intégration.

Sélectionnez **Configuration Firefly Services par défaut** et **Configuration des services d’automatisation de Creative Cloud par défaut**.

Sélectionnez **Enregistrer l’API configurée**.

![ Stockage Azure ](./images/ps5.png){zoomable="yes"}

Vous devriez alors voir ceci.

![Nouvelle intégration Adobe I/O](./images/ps7.png){zoomable="yes"}

### API ADOBE EXPERIENCE PLATFORM

Sélectionnez **+ Ajouter au projet** puis sélectionnez **API**.

![ Stockage Azure ](./images/aep1.png){zoomable="yes"}

Sélectionnez **Adobe Experience Platform** puis **API Experience Platform**. Sélectionnez **Suivant**.

![ Stockage Azure ](./images/aep2.png){zoomable="yes"}

Sélectionnez **Suivant**.

![ Stockage Azure ](./images/aep3.png){zoomable="yes"}

Ensuite, vous devez sélectionner un profil de produit qui définit les autorisations disponibles pour cette intégration.

Sélectionnez **Adobe Experience Platform - Tous les utilisateurs - PROD**.

Sélectionnez **Enregistrer l’API configurée**.

![ Stockage Azure ](./images/aep4.png){zoomable="yes"}

Vous devriez alors voir ceci.

![Nouvelle intégration Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nom du projet

Cliquez sur le nom de votre projet.

![Nouvelle intégration Adobe I/O](./images/api13.png){zoomable="yes"}

Sélectionnez **Modifier le projet**.

![Nouvelle intégration Adobe I/O](./images/api14.png){zoomable="yes"}

Saisissez un nom convivial pour votre intégration : `--aepUserLdap-- One Adobe tutorial`et sélectionnez **Enregistrer**.

![Nouvelle intégration Adobe I/O](./images/api15.png){zoomable="yes"}

La configuration de votre projet Adobe I/O est maintenant terminée.

![Nouvelle intégration Adobe I/O](./images/api16.png){zoomable="yes"}

## Étapes suivantes

Accédez à [Option 1 : configuration de Postman](./ex7.md){target="_blank"}

Accédez à [Option 2 : configuration de PostBuster](./ex8.md){target="_blank"}

Revenir à [Prise en main](./getting-started.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
