---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Exigences du schéma XDM dans Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Exigences du schéma XDM dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 1.1.7 Exigences relatives aux schémas XDM dans Adobe Experience Platform

Pour que le SDK Web puisse ingérer des données dans Adobe Experience Platform, un mixin XDM spécifique doit faire partie du schéma XDM dans Adobe Experience Platform.

Accédez à [https://experience.adobe.com/platform](https://experience.adobe.com/platform) et connectez-vous.

![&#x200B; Débogueur AEP &#x200B;](./images/exp1.png)

Après vous être connecté, sélectionnez le sandbox approprié en cliquant sur le texte **Production Prod** dans la ligne bleue en haut de votre écran. Sélectionnez l’`--aepSandboxName--` Sandbox .

Après avoir sélectionné votre sandbox, la modification de l’écran s’affiche et vous êtes maintenant dans votre sandbox.

![&#x200B; Débogueur AEP &#x200B;](./images/exp2.png)

Dans le menu de gauche, accédez à **Schémas** et ouvrez le schéma **Système de démonstration - Schéma d’événement pour le site web (global v1.1)** .

![&#x200B; Débogueur AEP &#x200B;](./images/exp3.png)

Dans ce schéma, vous verrez que le groupe de champs **AEP Web SDK ExperienceEvent** a été ajouté. Ce groupe de champs ajoute tous les champs obligatoires au minimum au schéma. Chaque schéma d’événement d’expérience dans Adobe Experience Platform qui sera utilisé par Web SDK nécessite toujours que ce groupe de champs fasse partie du schéma.

![&#x200B; Débogueur AEP &#x200B;](./images/exp4.png)

Dans [Module 1.2](./../module1.2/data-ingestion.md) vous apprendrez à ajouter des groupes de champs aux schémas.

Étape suivante : [Résumé et avantages](./summary.md)

[Retour au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
