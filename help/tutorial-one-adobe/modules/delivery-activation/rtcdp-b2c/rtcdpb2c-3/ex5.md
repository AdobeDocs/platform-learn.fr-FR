---
title: Real-time CDP - Créez une audience et effectuez une action - Envoyez votre audience à Adobe Target
description: Real-time CDP - Créez une audience et effectuez une action - Envoyez votre audience à Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 2a9a982b-0ffd-468d-9b71-77224e2c7e1d
source-git-commit: 15adbf950115f0b6bb6613e69a60b310f25de058
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 3%

---

# 2.3.5 Agir : envoyez votre audience à Adobe Target

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la [!UICONTROL sandbox] appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

## Vérifier le flux de données

La destination Adobe Target dans Real-Time CDP est connectée au flux de données utilisé pour ingérer des données dans Adobe Edge Network. Si vous souhaitez configurer votre destination Adobe Target, vous devez d’abord vérifier si votre flux de données est déjà activé pour Adobe Target. Votre flux de données a été configuré dans [Exercice 0.2 : créer votre flux de données](./../../../modules/../getting-started/gettingstarted/ex2.md) et a été nommé `--aepUserLdap-- - Demo System Datastream`.

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Flux de données**. Dans Flux de données, recherchez le flux de données nommé `--aepUserLdap-- - Demo System Datastream`. Cliquez sur votre flux de données pour l’ouvrir.

![Ingestion des données](./images/atdestds1.png)

Vous verrez alors ceci, cliquez sur **...** en regard de **Adobe Experience Platform** puis cliquez sur **Modifier**.

![Ingestion des données](./images/atdestds4.png)

Cochez les cases pour **Segmentation Edge** et **Destinations Personalization**. Cliquez sur **Enregistrer**.

![Ingestion des données](./images/atdestds4a.png)

Cliquez ensuite sur **+ Ajouter un service**.

![Ingestion des données](./images/atdestds4b.png)

Sélectionnez le service **Adobe Target**. Cliquez sur **Enregistrer**.

![Ingestion des données](./images/atdestds5.png)

Votre flux de données est maintenant configuré pour Adobe Target.

![Ingestion des données](./images/atdestds5a.png)

## Configurer votre destination Adobe Target

Adobe Target est disponible en tant que destination depuis Real-Time CDP. Pour configurer votre intégration Adobe Target, accédez à **Destinations**, puis à **Catalogue**.

Cliquez sur **Personalization** dans le menu **Catégories**. La carte de destination **(v2) Adobe Target** s’affiche alors.

![À](./images/atdest1.png)

Cliquez sur **Se connecter à la destination**.

![À](./images/atdest1a.png)

Tu verras ça. Vous devez créer votre propre destination Adobe Target, suivez ces instructions :

- Nom : utilisez le nom `--aepUserLdap-- - Adobe Target v2  (Web)`.
- Identifiant du flux de données : vous devez sélectionner le flux de données que vous avez configuré dans [Exercice 0.2 : créer votre flux de données](./../../../modules/../getting-started/gettingstarted/ex2.md). Le nom de votre flux de données doit être : `--aepUserLdap-- - Demo System Datastream`.
- Workspace : relatif aux espaces de travail Adobe Target. Si aucun espace de travail spécifique ne doit être utilisé, sélectionnez **Workspace par défaut**.

Cliquez sur **Suivant**.

![À](./images/atdest5.png)

Vous pouvez désormais éventuellement sélectionner une politique de gouvernance des données. Cliquez sur **Suivant**.

![À](./images/atdest2.png)

Dans la liste des audiences disponibles, sélectionnez l’audience que vous avez créée dans l’exercice précédent [Créer une audience](./ex1.md), qui est nommée `--aepUserLdap-- - Interest in Galaxy S24`. Cliquez ensuite sur **Suivant**.

![À](./images/atdest8.png)

Sur l’écran **Mappage**, vous pouvez mapper les attributs de profil pour qu’ils soient disponibles dans Adobe Target. Cela vous permet d’ajouter une couche de personnalisation supplémentaire à votre site web. Cliquez sur **Ajouter un nouveau champ**.

![À](./images/atdest9.png)

Pour le nouveau champ, sélectionnez le champ **person.name.firstName**. Cliquez sur **Enregistrer**.

![À](./images/atdest9a.png)

Tu auras alors ceci. Cliquez sur **Suivant**.

![À](./images/atdest9b.png)

Cliquez sur **Terminer**.

![À](./images/atdest10.png)

Votre audience est maintenant activée vers Adobe Target.

![À](./images/atdest11.png)

>[!IMPORTANT]
>
>Lorsque vous venez de créer votre destination Adobe Target dans Real-Time CDP, la mise en ligne de la destination peut prendre jusqu’à une heure. Il s’agit d’un temps d’attente unique, en raison de la configuration du serveur principal. Une fois le temps d’attente initial d’une heure et la configuration du serveur principal terminés, les nouvelles audiences ajoutées à la destination Adobe Target seront disponibles pour le ciblage en temps réel.

## Configuration de votre activité Adobe Target basée sur les formulaires

Maintenant que votre audience Real-Time CDP est configurée pour être envoyée à Adobe Target, vous pouvez configurer votre activité de ciblage d’expérience dans Adobe Target. Dans cet exercice, vous allez configurer une activité basée sur des formulaires.

Accédez à la page d’accueil de Adobe Experience Cloud en vous rendant sur [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Cliquez sur **Target** pour l’ouvrir.

![RTCDP](./images/excl.png)

Sur la page d’accueil **Adobe Target**, toutes les activités existantes s’affichent. Cliquez sur **Créer une activité**, puis sur **Ciblage d’expérience**.

![RTCDP](./images/exclatov.png)

Sélectionnez **Web**, **Formulaire** et **Aucune restriction de propriété**. Cliquez sur **Créer**.

![RTCDP](./images/exclatcrxtdtlform.png)

Vous êtes maintenant dans le compositeur d’activité basé sur les formulaires.

![RTCDP](./images/atform1.png)

Pour le champ **EMPLACEMENT 1**, sélectionnez **target-global-mbox**.

![RTCDP](./images/atform2.png)

L’audience par défaut est actuellement **Tous les visiteurs**. Cliquez sur les points **3** à côté de **Tous les visiteurs** et cliquez sur **Modifier l’audience**.

![RTCDP](./images/atform3.png)

La liste des audiences disponibles s’affiche maintenant. L’audience Adobe Experience Platform que vous avez créée précédemment et envoyée à Adobe Target fait désormais partie de cette liste. Sélectionnez l’audience que vous avez précédemment créée dans Adobe Experience Platform. Cliquez sur **Attribuer l’audience**.

![RTCDP](./images/exclatvecchaud.png)

Votre audience Adobe Experience Platform fait maintenant partie de cette activité de ciblage d’expérience.

![RTCDP](./images/atform4.png)

Changeons maintenant l’image principale sur la page d’accueil du site web. Cliquez pour ouvrir la liste déroulante en regard de **Contenu par défaut** puis cliquez sur **Créer une offre HTML**.

![RTCDP](./images/atform5.png)

Collez le code suivant.

```javascript
<script>document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Image > img").src="https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/citisignal-new-hero.png"; document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Banner__content > div > div > h1").innerHTML="Hi there ";
document.querySelector("#SpectrumProvider > div.App > div > div.Page.home > main > div.Banner.Banner--alignment-right.Banner--verticalAlignment-middle.main-banner > div.Banner__content > div > div > div > div > p").innerHTML="What about 10% off of your next Galaxy S24 smartphone?";
</script>
```

![RTCDP](./images/atform6.png)

Vous devez ensuite ajouter un jeton de personnalisation à partir des attributs de profil Adobe Experience Platform. N’oubliez pas que lorsque vous avez activé l’audience dans Adobe Target, vous sélectionnez également le champ **person.name.firstName** à partager avec Adobe Target. Pour récupérer le champ, sélectionnez la source **Adobe Experience Platform**, sélectionnez votre sandbox (qui doit être `--aepSandboxName--`), puis sélectionnez l’attribut **person.name.firstName**.

![RTCDP](./images/atform6a.png)

Avant de cliquer sur le bouton **Ajouter**, assurez-vous d&#39;aller à la ligne où vous voyez `... > h1").innerHTML="Hi there ";` et de mettre votre curseur à l&#39;intérieur des crochets après le mot `there`, comme suit :

```
... > h1").innerHTML="Hi there ";
```

Cliquez ensuite sur le bouton **Ajouter** qui doit alors ajouter le jeton, ce qui mettra à jour le code comme suit :

```
... > h1").innerHTML="Hi there ${aep.person.name.firstName}";
```


Cliquez sur **Suivant**.

![RTCDP](./images/atform6b.png)

Vous verrez ensuite un aperçu de votre expérience avec la nouvelle image, pour l’audience sélectionnée. Cliquez sur **Suivant**.

![RTCDP](./images/atform7.png)

Cliquez sur le titre de votre activité dans le coin supérieur gauche pour la renommer, comme suit : `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Sur la page **Objectifs et paramètres** - , accédez à **Mesures d’objectif**. Définissez l’objectif du Principal sur **Engagement** - **Temps passé sur le site**. Cliquez sur **Enregistrer et fermer**.

![RTCDP](./images/vec3.png)

Vous êtes maintenant sur la page **Aperçu de l’activité**. Vous devez encore activer votre activité. Cliquez sur le champ **Inactif** et sélectionnez **Activer**.

![RTCDP](./images/atform10.png)

Vous obtiendrez alors une confirmation visuelle de la mise en ligne de votre activité.

![RTCDP](./images/atform12.png)

Votre activité est maintenant en ligne et peut être testée sur le site web de démonstration.

>[!IMPORTANT]
>
>Lorsque vous venez de créer votre destination Adobe Target dans Real-Time CDP, la mise en ligne de la destination peut prendre jusqu’à une heure. Il s’agit d’un temps d’attente unique, en raison de la configuration du serveur principal. Une fois le temps d’attente initial d’une heure et la configuration du serveur principal terminés, les nouvelles audiences Edge ajoutées qui sont envoyées à la destination Adobe Target seront disponibles pour le ciblage en temps réel.

Si vous revenez maintenant à votre site web de démonstration et consultez la page produit pour Galaxy S24, vous serez alors éligible à l’audience que vous avez créée et l’activité Adobe Target s’affichera sur la page d’accueil en temps réel.

![RTCDP](./images/atform13.png)

## Étapes suivantes

Accédez à [2.3.6 Destinations SDK](./ex6.md){target="_blank"}

Revenez à [Real-time CDP - Créer une audience et prendre des mesures](./real-time-cdp-build-a-segment-take-action.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
