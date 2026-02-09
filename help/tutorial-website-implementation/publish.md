---
title: Publication de la propriété de balise
description: Découvrez comment publier votre propriété de balise de l’environnement de développement vers les environnements d’évaluation et de production. Cette leçon fait partie du tutoriel Implémentation d’Experience Cloud dans les sites web .
exl-id: dec70472-cecc-4630-b68e-723798f17a56
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 55%

---

# Publication de la propriété de balise

Maintenant que vous avez mis en œuvre certaines solutions clés d’Adobe Experience Cloud dans votre environnement de développement, il est temps d’apprendre le processus de publication.


>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été déployées dans l’interface. Vous devez en être conscient lors de l’utilisation de ce contenu :
>
> * Platform Launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Platform Launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

1. publier une bibliothèque de développement dans l’environnement d’évaluation ;
1. faire correspondre une bibliothèque d’évaluation à votre site web de production à l’aide du débogueur ;
1. publier une bibliothèque d’évaluation dans l’environnement de production.

## Publication dans l’environnement d’évaluation

Maintenant que vous avez créé et validé votre bibliothèque dans l’environnement de développement, il est temps de la publier dans l’environnement d’évaluation.

1. Accédez à la page **[!UICONTROL Flux de publication]**

1. Ouvrez la liste déroulante en regard de votre bibliothèque et sélectionnez **[!UICONTROL Envoyer pour approbation]**

   ![Envoyer pour approbation](images/publishing-submitForApproval.png)

1. Cliquez sur le bouton **[!UICONTROL Envoyer]** dans la boîte de dialogue :

   ![Clic sur Envoyer dans le modal](images/publishing-submit.png)

1. Votre bibliothèque apparaît désormais dans la colonne [!UICONTROL Envoyé] à l’état non créée :

1. Ouvrez la liste déroulante et sélectionnez **[!UICONTROL Créer pour l’évaluation]** :

   ![Créer à des fins d’évaluation](images/publishing-buildForStaging.png)

1. Lorsque l’icône en forme de point vert s’affiche, la bibliothèque peut être prévisualisée dans l’environnement d’évaluation.

Dans un scénario réel, l’étape suivante du processus consisterait à demander aux membres de votre équipe d’assurance qualité de valider les modifications dans la bibliothèque d’évaluation. Cela est possible à l’aide du débogueur.

**Validation des modifications dans la bibliothèque d’évaluation**

1. Dans la propriété de balise, ouvrez la page [!UICONTROL &#x200B; Environnements &#x200B;]

1. Sur la ligne [!UICONTROL Évaluation], cliquez sur l’icône Installer ![icône Installer](images/launch-installIcon.png) pour ouvrir le modal.

   ![Accès à la page Environnements et clic pour ouvrir le modal](images/publishing-getStagingCode.png)

1. Cliquez sur l’icône Copier ![icône Copier](images/launch-copyIcon.png) pour copier le code intégré dans le presse-papiers.

1. Cliquez sur **[!UICONTROL Fermer]** pour fermer la fenêtre modale

   ![Icône Installer](images/publishing-copyStagingCode.png)

1. Ouvrez le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome.

1. Ouvrez l’extension [Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) en cliquant sur l’icône ![icône Debugger](images/icon-debugger.png)

   ![Clic sur l’icône Debugger](images/switchEnvironments-openDebugger.png)

1. Accédez à l’onglet Outils.

1. Dans la section **[!UICONTROL Adobe Launch > Remplacer le code intégré de Launch]** collez le code intégré intermédiaire qui se trouve dans votre presse-papiers
1. Activez le commutateur **[!UICONTROL Appliquer sur luma.enablementadobe.com]**

1. Cliquez sur l’icône de disquette pour enregistrer.

   ![environnement de balise affiché dans Debugger](images/switchEnvironments-debugger-save.png)

1. Actualisez et consultez l’onglet Résumé du débogueur. Sous la section Launch , vous devriez maintenant voir votre propriété d’évaluation mise en œuvre, affichant le nom de votre propriété (c’est-à-dire « Tutoriel sur les balises » ou le nom de votre propriété) !

   ![environnement de balise affiché dans Debugger](images/publishing-debugger-staging.png)

En situation réelle, une fois que l’équipe d’assurance qualité a examiné et validé les modifications dans l’environnement d’évaluation, il est temps de publier la propriété dans l’environnement de production.

## Publication dans l’environnement de production

1. Accédez à la page [!UICONTROL Publication].

1. Dans la liste déroulante, cliquez sur **[!UICONTROL Approuver pour publication]** :

   ![Approuver pour publication](images/publishing-approveForPublishing.png)

1. Cliquez sur le bouton **[!UICONTROL Approuver]** dans la boîte de dialogue :

   ![Clic sur Approuver](images/publishing-approve.png)

1. La bibliothèque apparaît désormais dans la colonne [!UICONTROL Approuvé] à l’état non créée (point jaune) :

1. Ouvrez la liste déroulante et sélectionnez **[!UICONTROL Créer et publier en production]** :

   ![Créer et publier dans l’environnement de production](images/publishing-buildAndPublishToProduction.png)

1. Cliquez sur le bouton **[!UICONTROL Publier]** dans la boîte de dialogue :

   ![Clic sur Publier.](images/publishing-publish.png)

1. La bibliothèque s’affiche désormais dans la colonne [!UICONTROL Publié] :

   ![Publié](images/publishing-published.png)

Vous avez terminé. Vous avez terminé le tutoriel et publié votre première propriété dans les balises.
