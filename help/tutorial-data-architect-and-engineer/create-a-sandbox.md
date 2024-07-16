---
title: Création d’un sandbox
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création d’un sandbox
description: Dans cette leçon, vous allez créer un environnement de test d’environnement de développement que vous pourrez utiliser pour le reste du tutoriel.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---

# Créer un sandbox

<!--25min-->

Dans cette leçon, vous allez créer un environnement de test d’environnement de développement que vous utiliserez pour le reste du tutoriel.

Les environnements de test fournissent des environnements isolés dans lesquels vous pouvez tester la fonctionnalité sans mélanger les ressources et les données à votre environnement de production. Pour plus d’informations, consultez la [documentation des environnements de test](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=fr).

**Les architectes de données** et **les ingénieurs de données** devront créer des environnements de test en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les environnements de test :
>[!VIDEO](https://video.tv.adobe.com/v/29838/?learn=on)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Création d’un environnement de test

Créons un environnement de test :

1. Connectez-vous à l’interface [Adobe Experience Platform](https://experience.adobe.com/platform)
1. Accédez à **[!UICONTROL Sandbox]** dans le volet de navigation de gauche.
1. Sélectionnez **[!UICONTROL Créer un environnement de test]** en haut à droite.
   ![Sélectionner Créer un environnement de test](assets/sandbox-createSandbox.png)

1. Sélectionnez **[!UICONTROL Development]** comme **[!UICONTROL Type]**
1. Nommez votre environnement de test `luma-tutorial` (pensez à ajouter votre nom à la fin).
1. Nommez votre tutoriel `Luma Tutorial` (pensez à ajouter votre nom à la fin).
1. Sélectionnez le bouton **[!UICONTROL Créer]**
   ![Créez votre environnement de test](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Bien que vous puissiez utiliser n’importe quelle valeur arbitraire pour votre nom et votre titre d’environnement de test, il est recommandé de respecter les valeurs suggérées, car nous nous référerons à ces étiquettes tout au long du tutoriel. Si plusieurs personnes de votre entreprise suivent ce tutoriel, pensez à ajouter votre nom à la fin du titre et du nom de l’environnement de test, par exemple luma-tutorial-ignatiusjreilly.

La création des environnements de test prend environ 30 secondes, au cours de laquelle un état &quot;[!UICONTROL Création]&quot; s’affiche. Une fois l’environnement de test entièrement créé, il s’affiche comme &quot;[!UICONTROL Actif]&quot; :
![État actif](assets/sandbox-active.png)

Patientez jusqu’à ce que l’environnement de test soit &quot;[!UICONTROL Actif]&quot; avant de poursuivre l’exercice suivant.

## Ajouter le nouvel environnement de test au rôle

Une fois que l’environnement de test est actif, vous devez l’inclure dans votre rôle pour pouvoir l’utiliser. Pour l’ajouter à votre rôle (nécessite des privilèges d’administrateur système ou d’administrateur de produit) :

1. Accédez à l’écran [!UICONTROL Autorisations]
1. Ouvrez le rôle `Luma Tutorial Platform`
1. Éventuellement _supprimez_ l’environnement de test `Prod` du rôle
1. Ajout de l’environnement de test `Luma Tutorial`
1. Sélectionnez **[!UICONTROL Save]**
1. Sur la ligne [!UICONTROL Sandbox], sélectionnez **[!UICONTROL Modifier]**

   ![Ajout du tutoriel Luma](assets/sandbox-addLumaTutorial.png)

1. Rechargez (ou rechargez-la) la page et vous devriez maintenant vous trouver dans l’environnement de test `Luma Tutorial` ou elle devrait apparaître dans la liste déroulante de votre environnement de test.
1. Passez à l’environnement de test `Luma Tutorial` si vous ne l’êtes pas déjà.

   ![Confirmer l’environnement de test](assets/sandbox-confirmDropdown.png)

Super, vous avez créé votre environnement de test et êtes prêt à [configurer Developer Console et Postman](set-up-developer-console-and-postman.md) !
