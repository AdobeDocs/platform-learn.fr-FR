---
title: Changement d’environnements de balise avec le débogueur Adobe Experience Cloud
description: Découvrez comment utiliser l’Experience Cloud Debugger pour charger différents codes incorporés de balise. Cette leçon fait partie du tutoriel Mise en oeuvre de l’Experience Cloud sur les sites web .
exl-id: 29972a00-e5e0-4fe0-a71c-c2ca106938be
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 40%

---

# Changement d’environnements de balise avec l’Experience Cloud Debugger

Dans cette leçon, vous utiliserez la variable [Extension Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) pour remplacer la propriété de balise codée en dur sur la propriété [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) avec votre propre propriété.

Cette technique, appelée changement d’environnement, vous sera utile ultérieurement lorsque vous utiliserez des balises sur votre propre site web. Vous pourrez charger votre site web de production dans votre navigateur, mais avec votre *development* environnement de balises. Cela vous permet d’effectuer et de valider des modifications de balises en toute confiance, indépendamment de vos mises à jour de code standard.  Après tout, cette séparation entre les mises à jour de balises marketing et les mises à jour de code standard est l’une des principales raisons pour lesquelles les clients utilisent des balises en premier lieu !

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été apportées à l’interface que vous devez connaître lors de l’utilisation de ce contenu :
>
> * Le platform launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Le platform launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**


## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Utilisez Debugger pour charger un autre environnement de balises.
* Utilisez Debugger pour vérifier que vous avez chargé un autre environnement de balises.

## Obtention de l’URL de votre environnement de développement

1. Dans la propriété de balise, ouvrez le `Environments` page

1. Sur la ligne **[!UICONTROL Développement]**, cliquez sur l’icône Installer ![icône Installer](images/launch-installIcon.png) pour ouvrir le modal.

1. Cliquez sur l’icône Copier ![icône Copier](images/launch-copyIcon.png) pour copier le code incorporé dans le presse-papiers.

1. Cliquez sur **[!UICONTROL Fermer]** pour fermer le modal.

   ![Icône Installer](images/launch-copyInstallCode.png)

## Remplacez l’URL de balise sur le site de démonstration Luma.

1. Ouvrez le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome.

1. Ouvrez l’[extension Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) en cliquant sur l’icône ![icône Debugger](images/icon-debugger.png).

   ![Clic sur l’icône Debugger](images/switchEnvironments-openDebugger.png)

1. Notez que la propriété de balise actuellement mise en oeuvre s’affiche dans l’onglet Résumé .

   ![Environnement de balises affiché dans Debugger](images/switchEnvironments-debuggerOnWeRetail-prod.png)

1. Accédez à l’onglet Outils.
1. Accédez à la section **[!UICONTROL Remplacement du code incorporé Launch]**.
1. Assurez-vous que l’onglet Chrome avec le site Luma est mis en évidence derrière le débogueur (et non l’onglet avec ce tutoriel ou l’onglet avec l’interface Collecte de données).  Collez le code incorporé présent dans le presse-papiers dans le champ de saisie.
1. Activez la fonction &quot;Appliquer sur luma.enablementadobe.com&quot; afin que toutes les pages du site Luma soient mappées à votre propriété de balise.
1. Cliquez sur le bouton **[!UICONTROL Enregistrer]**.

   ![Environnement de balises affiché dans Debugger](images/switchEnvironments-debugger-save.png)

1. Chargez à nouveau le site Luma et vérifiez l’onglet Résumé du débogueur. Sous la section Launch, vous devriez constater que votre propriété de développement est en cours d’utilisation. Vérifiez que le nom de la propriété correspond à celui de la vôtre et que l’environnement indique « development ».

   ![Environnement de balises affiché dans Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

>[!NOTE]
>
>Le débogueur enregistrera cette configuration et remplacera les codes incorporés de balise chaque fois que vous reviendrez sur le site Luma. Cela n’a aucune incidence sur les autres sites que vous visitez dans les autres onglets ouverts. Pour empêcher le débogueur de remplacer le code incorporé, cliquez sur le bouton **[!UICONTROL Supprimer]** en regard du code incorporé dans l’onglet Outils du débogueur.

À mesure que vous poursuivez le tutoriel, vous utiliserez cette technique pour mapper le site Luma sur votre propre propriété de balise afin de valider votre mise en oeuvre de balises. Lorsque vous commencez à utiliser des balises sur votre site web de production, vous pouvez utiliser cette même technique pour valider les modifications.

[Suite : « Ajout d’Adobe Experience Platform Identity Service » >](id-service.md)
