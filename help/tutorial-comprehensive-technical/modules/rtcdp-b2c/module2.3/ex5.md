---
title: CDP en temps réel - Créer une audience et agir - Envoyer votre audience à Adobe Target
description: CDP en temps réel - Créer une audience et agir - Envoyer votre audience à Adobe Target
kt: 5342
doc-type: tutorial
exl-id: b041897b-4ee8-4ff8-a3bc-d953e2e42a1a
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 3%

---

# 2.3.5 Action : envoyez votre audience à Adobe Target

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

## Vérification de la structure de données

La destination Adobe Target dans Real-Time CDP est connectée à la banque de données utilisée pour ingérer des données dans le réseau Edge d’Adobe. Si vous souhaitez configurer votre destination Adobe Target, vous devez d’abord vérifier si votre flux de données est déjà activé pour Adobe Target. Votre jeu de données a été configuré dans l’ [exercice 0.2 de création de votre flux de données](./../../../modules/gettingstarted/gettingstarted/ex2.md) et a été nommé `--aepUserLdap-- - Demo System Datastream`.

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Datastreams**. Dans les flux de données, recherchez votre flux de données nommé `--aepUserLdap-- - Demo System Datastream`. Cliquez sur votre flux de données pour l’ouvrir.

![Ingestion des données](./images/atdestds1.png)

Vous verrez alors ceci, cliquez sur **...** en regard de **Adobe Experience Platform**, puis cliquez sur **Modifier**.

![Ingestion des données](./images/atdestds4.png)

Cochez les cases correspondant à la **segmentation Edge** et aux **destinations Personalization**. Cliquez sur **Enregistrer**.

![Ingestion des données](./images/atdestds4a.png)

Cliquez ensuite sur **+ Ajouter un service**.

![Ingestion des données](./images/atdestds4b.png)

Sélectionnez le service **Adobe Target**. Cliquez sur **Enregistrer**.

![Ingestion des données](./images/atdestds5.png)

Votre flux de données est maintenant configuré pour Adobe Target.

![Ingestion des données](./images/atdestds5a.png)

## Configuration de votre destination Adobe Target

Adobe Target est disponible en tant que destination depuis Real-Time CDP. Pour configurer votre intégration Adobe Target, accédez à **Destinations**, à **Catalogue**.

Cliquez sur **Personalization** dans le menu **Catégories** . Vous verrez ensuite la carte de destination **(v2) Adobe Target**.

![AT](./images/atdest1.png)

Cliquez sur **Se connecter à la destination**.

![AT](./images/atdest1a.png)

Vous verrez alors ceci. Vous devez créer votre propre destination Adobe Target. Suivez les instructions suivantes :

- Nom : utilisez le nom `--aepUserLdap-- - Adobe Target v2  (Web)`.
- Identifiant de la banque de données : vous devez sélectionner la banque de données que vous avez configurée dans l’ [exercice 0.2 Création de la banque de données](./../../../modules/gettingstarted/gettingstarted/ex2.md). Le nom de votre flux de données doit être : `--aepUserLdap-- - Demo System Datastream`.
- Workspace : il est lié aux espaces de travail Adobe Target. S’il n’existe aucun espace de travail spécifique que vous devez utiliser, sélectionnez **Workspace par défaut**.

Cliquez sur **Suivant**.

![AT](./images/atdest5.png)

Vous pouvez désormais sélectionner une stratégie de gouvernance des données (facultatif). Cliquez sur **Suivant**.

![AT](./images/atdest2.png)

Dans la liste des audiences disponibles, sélectionnez l’audience que vous avez créée lors de l’exercice précédent [Créer une audience](./ex1.md), qui s’appelle `--aepUserLdap-- - Interest in Galaxy S24`. Cliquez ensuite sur **Suivant**.

![AT](./images/atdest8.png)

Sur l’écran **Mapping**, vous pouvez mapper les attributs de profil pour qu’ils soient disponibles dans Adobe Target. Vous pouvez ainsi ajouter une couche supplémentaire de personnalisation sur votre site web. Cliquez sur **Ajouter un nouveau champ**.

![AT](./images/atdest9.png)

Pour le nouveau champ, sélectionnez le champ **person.name.firstName**. Cliquez sur **Enregistrer**.

![AT](./images/atdest9a.png)

Vous aurez alors ceci. Cliquez sur **Suivant**.

![AT](./images/atdest9b.png)

Cliquez sur **Terminer**.

![AT](./images/atdest10.png)

Votre audience est maintenant activée vers Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Lorsque vous venez de créer votre destination Adobe Target dans Real-Time CDP, la mise en service de cette destination peut prendre jusqu’à une heure. Il s’agit d’un temps d’attente ponctuel, en raison de la configuration du serveur principal. Une fois la configuration initiale du temps d’attente d’une heure et du serveur principal terminée, les audiences nouvellement ajoutées envoyées à la destination Adobe Target seront disponibles pour le ciblage en temps réel.

## Configuration de votre activité Adobe Target basée sur les formulaires

Maintenant que votre audience Real-Time CDP est configurée pour être envoyée à Adobe Target, vous pouvez configurer votre activité de ciblage d’expérience dans Adobe Target. Dans cet exercice, vous allez configurer une activité d’après les formulaires.

Accédez à la page d’accueil de Adobe Experience Cloud en vous rendant sur [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Cliquez sur **Target** pour l’ouvrir.

![RTCDP](./images/excl.png)

Sur la page d’accueil **Adobe Target**, vous verrez toutes les activités existantes. Cliquez sur **Créer une activité**, puis sur **Ciblage d’expérience**.

![RTCDP](./images/exclatov.png)

Sélectionnez **Web**, **Formulaire** et **Aucune restriction de propriété**. Cliquez sur **Créer**.

![RTCDP](./images/exclatcrxtdtlform.png)

Vous vous trouvez maintenant dans le compositeur d’activité d’après les formulaires.

![RTCDP](./images/atform1.png)

Pour le champ **LOCATION 1**, sélectionnez **target-global-mbox**.

![RTCDP](./images/atform2.png)

L’audience par défaut est actuellement **Tous les visiteurs**. Cliquez sur le **3 points** en regard de **Tous les visiteurs** et cliquez sur **Changer d’audience**.

![RTCDP](./images/atform3.png)

La liste des audiences disponibles s’affiche désormais. L’audience Adobe Experience Platform que vous avez créée précédemment et envoyée à Adobe Target fait désormais partie de cette liste. Sélectionnez l’audience que vous avez précédemment créée dans Adobe Experience Platform. Cliquez sur **Attribuer une audience**.

![RTCDP](./images/exclatvecchaud.png)

Votre audience Adobe Experience Platform fait désormais partie de cette activité de ciblage d’expérience.

![RTCDP](./images/atform4.png)

Changeons maintenant l&#39;image du héros sur la page d&#39;accueil du site web. Cliquez pour ouvrir la liste déroulante en regard de **Contenu par défaut** et cliquez sur **Créer une offre d’HTML**.

![RTCDP](./images/atform5.png)

Collez le code suivant.

```javascript
<script>document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Image > img").src="https://tech-insiders.s3.us-west-2.amazonaws.com/citisignal-new-hero.png"; document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Banner__content > div > div > h1").innerHTML="Hi there ";
document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Banner__content > div > div > div > div > p").innerHTML="What about 10% off of your next Galaxy S24 smartphone?";
</script>
```

![RTCDP](./images/atform6.png)

Vous devez ensuite ajouter un jeton de personnalisation à partir des attributs de profil Adobe Experience Platform. Souvenez-vous que lorsque vous avez activé l’audience dans Adobe Target, vous sélectionnez également le champ **person.name.firstName** à partager avec Adobe Target. Pour récupérer le champ, sélectionnez la source **Adobe Experience Platform**, sélectionnez votre environnement de test (qui doit être `--aepSandboxName--`), puis sélectionnez l’attribut **person.name.firstName**.

![RTCDP](./images/atform6a.png)

Avant de cliquer sur le bouton **Ajouter** , veillez à accéder à la ligne où se trouve `... > h1").innerHTML="Hi there ";` et placez le curseur entre les crochets après le mot `there`, comme suit :

`... > h1").innerHTML="Hi there ";`

Cliquez ensuite sur le bouton **Ajouter** , qui doit ensuite ajouter le jeton, ce qui met à jour le code comme suit :

`... > h1").innerHTML="Hi there ${aep.person.name.firstName}";`

Cliquez sur **Suivant**.

![RTCDP](./images/atform6b.png)

Vous verrez ensuite la présentation de votre expérience avec la nouvelle image, pour le public sélectionné. Cliquez sur **Suivant**.

![RTCDP](./images/atform7.png)

Cliquez sur le titre de votre activité dans le coin supérieur gauche pour la renommer, comme suit : `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Sur la page **Objectifs et paramètres** - , accédez à **Mesures d’objectif**. Définissez l’objectif Principal sur **Engagement** - **Temps passé sur le site**. Cliquez sur **Enregistrer et fermer**.

![RTCDP](./images/vec3.png)

Vous vous trouvez maintenant sur la page **Aperçu de l’activité**. Vous devez toujours activer votre activité. Cliquez sur le champ **Inactif** et sélectionnez **Activer**.

![RTCDP](./images/atform10.png)

Vous obtiendrez alors une confirmation visuelle que votre activité est maintenant active.

![RTCDP](./images/atform12.png)

Votre activité est maintenant en ligne et peut être testée sur le site web de démonstration.

>[!IMPORTANT]
>
>Lorsque vous venez de créer votre destination Adobe Target dans Real-Time CDP, la mise en service de cette destination peut prendre jusqu’à une heure. Il s’agit d’un temps d’attente ponctuel, en raison de la configuration du serveur principal. Une fois la configuration initiale du temps d’attente d’une heure et du serveur principal terminée, les audiences Edge nouvellement ajoutées envoyées à la destination Adobe Target seront disponibles pour le ciblage en temps réel.

Si vous revenez maintenant à votre site web de démonstration et que vous visitez la page de produit de Galaxy S24, vous serez alors admissible pour l’audience que vous avez créée, et l’activité Adobe Target s’affichera sur la page d’accueil en temps réel.

![RTCDP](./images/atform13.png)

Étape suivante : [2.3.6 External Audiences](./ex6.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
