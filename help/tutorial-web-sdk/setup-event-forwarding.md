---
title: Configuration d’un transfert d’événement avec les données du SDK Web Platform
description: Découvrez comment utiliser la propriété de transfert d’événement à l’aide des données Experience Platform du SDK Web. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Event Forwarding
jira: KT-15414
exl-id: 5a306609-2c63-42c1-8beb-efa412b8efe4
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '1873'
ht-degree: 4%

---

# Configuration du transfert d’événement avec les données du SDK Web Platform

Découvrez comment utiliser le transfert d’événement avec les données du SDK web d’Adobe Experience Platform.

Le transfert d’événement est un nouveau type de propriété disponible dans la collecte de données. Le transfert d’événements vous permet d’envoyer des données à des fournisseurs tiers non Adobes directement à partir de l’Edge Network Adobe Experience Platform au lieu du navigateur côté client traditionnel. Découvrez les avantages du transfert d’événement dans la [présentation du transfert d’événement](https://experienceleague.adobe.com/fr/docs/experience-platform/tags/event-forwarding/overview).


![ Diagramme SDK Web et transfert d’événement ](assets/dc-websdk-eventforwarding.png)

Pour utiliser le transfert d’événement dans Adobe Experience Platform, les données doivent d’abord être envoyées à Adobe Experience Platform Edge Network à l’aide d’une ou de plusieurs des trois options suivantes :

* [SDK web Adobe Experience Platform](overview.md)
* [ SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/home/)
  <!--* [Server-to-Server API](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s)-->


>[!NOTE]
>Le SDK Web Platform et le SDK Mobile Platform ne nécessitent pas de déploiement par le biais de balises. Toutefois, il est recommandé d’utiliser des balises pour déployer ces SDK.

Après avoir suivi les leçons précédentes de ce tutoriel, vous devriez envoyer des données à Platform Edge Network à l’aide du SDK Web. Une fois que les données se trouvent dans l’Edge Network Platform, vous pouvez activer le transfert d’événement et utiliser une propriété de transfert d’événement pour envoyer des données à des solutions non-Adobes.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous serez en mesure de :

* Création d’une propriété de transfert d’événement
* Associer une propriété de transfert d’événement à un flux de données SDK Web Platform
* Comprendre les différences entre les éléments de données et les règles de propriété de balise et les éléments de données et les règles de propriété de transfert d’événement
* Création d’un élément de données de transfert d’événement
* Configuration d’une règle de transfert d’événement
* Validation de l’envoi de données par une propriété de transfert d’événement


## Conditions préalables

* Une licence logicielle qui inclut le transfert d’événement. Le transfert d’événement est une fonctionnalité payante de la collecte de données. Pour plus d’informations, contactez votre équipe de compte d’Adobe.
* Le transfert d’événement est activé dans votre organisation Experience Cloud.
* Autorisation de l’utilisateur pour le transfert d’événement. (Dans [Admin Console](https://adminconsole.adobe.com/), sous le produit Adobe Experience Platform Launch, les éléments d’autorisation pour[!UICONTROL Plateformes] > [!UICONTROL Edge] et tous les [!UICONTROL Droits de propriété]). Une fois accordée, vous devriez voir [!UICONTROL Transfert d’événement] dans le volet de navigation de gauche de l’interface de collecte de données :
  ![Propriétés de transfert d’événement](assets/event-forwarding-menu.png)

* Le SDK Adobe Experience Platform Web ou Mobile est configuré pour envoyer des données à l’Edge Network. Vous devez avoir terminé les leçons suivantes de ce tutoriel :

   * Configuration initiale

      * [Configurer un schéma XDM](configure-schemas.md)
      * [Configuration d’un espace de noms d’identité](configure-identities.md)
      * [Configurer un trains de données](configure-datastream.md)

   * Configuration des balises

      * [Installer l’extension SDK Web](install-web-sdk.md)
      * [Création d’éléments de données](create-data-elements.md)
      * [Création d’identités](create-identities.md)
      * [Création de règles de balise](create-tag-rule.md)
      * [Validation avec le débogueur Adobe Experience Platform](validate-with-debugger.md)


## Création d’une propriété de transfert d’événement

Commencez par créer une propriété de transfert d’événement :

1. Ouvrez l’ [interface de collecte de données](https://experience.adobe.com/#/data-collection)
1. Sélectionnez **[!UICONTROL Transfert d’événement]** dans la navigation de gauche.
1. Sélectionnez **[!UICONTROL Nouvelle propriété]**.
   ![Propriétés de transfert d’événement](assets/event-forwarding-new.png)

1. Attribuez un nom à la propriété. Dans ce cas, `Server-Side - Web SDK Course`

1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![enregistrement de propriété de transfert d’événement](assets/event-forwarding-save.png)

## Configuration du flux de données

Pour que le transfert d’événement utilise les données que vous envoyez à l’Edge Network Platform, vous devez lier la propriété de transfert d’événement nouvellement créée à la même structure de données que celle utilisée pour envoyer des données à des solutions Adobe.

Pour configurer Target dans le flux de données :

1. Accédez à l’interface [Collecte de données](https://experience.adobe.com/#/data-collection){target="blank"}
1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Datastreams]**
1. Sélectionnez le flux de données `Luma Web SDK: Development Environment` créé précédemment.

   ![Sélectionnez la banque de données du SDK Web Luma](assets/datastream-luma-web-sdk-development.png)

1. Sélectionnez **[!UICONTROL Ajouter un service]**
   ![Ajouter un service à la banque de données](assets/event-forwarding-datastream-addService.png)
1. Sélectionnez **[!UICONTROL Event Forwarding]** comme **[!UICONTROL Service]**

1. Dans la liste déroulante **[!UICONTROL ID de propriété]**, sélectionnez le nom que vous avez donné à votre propriété de transfert d’événement, dans ce cas `Server-Side - Web SDK Course`

1. Dans la liste déroulante **[!UICONTROL ID d’environnement]**, sélectionnez l’environnement de balise auquel vous liez l’environnement de transfert d’événement, dans ce cas `Development`

   >[!TIP]
   >
   >    Pour envoyer des données à un environnement de transfert d’événement en dehors de l’organisation d’Adobe, sélectionnez **[!UICONTROL Saisir manuellement les identifiants]** et collez-les dans un identifiant. L’identifiant est fourni lorsque vous créez une propriété de transfert d’événement.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Activation du transfert d’événement vers le serveur de données](assets/event-forwarding-datastream-enable.png)

Répétez ces étapes pour les flux de données d’évaluation et de production lorsque vous êtes prêt à promouvoir vos modifications par le biais du flux de publication.

## Transfert de données de l’Edge Network Platform vers une solution non Adobe

Dans cet exercice, vous apprendrez à configurer un élément de données de transfert d’événement, à configurer une règle de transfert d’événement et à valider à l’aide d’un outil tiers appelé [Webhook.site](https://webhook.site/).

>[!NOTE]
>
>Un webhook est un moyen d’intégrer différents systèmes en temps semi-réel. [Webhook.site](https://webhook.site/) est un outil tiers qui vous permet d’inspecter, de tester et d’automatiser facilement (avec le générateur d’actions personnalisées visuel ou WebhookScript) toute requête HTTP ou tout e-mail entrant.

>[!IMPORTANT]
>
>Vous devez avoir déjà créé et mappé des éléments de données à un objet XDM, ainsi que configuré des règles de balise et créé ces modifications dans une bibliothèque dans un environnement de balise pour continuer. Si ce n&#39;est pas le cas, reportez-vous aux étapes **Configuration des balises** de la section [Conditions préalables](setup-event-forwarding.md#prerequisites) . Ces étapes garantissent que les données sont envoyées à l’Edge Network Platform. Vous pouvez ensuite configurer une propriété de transfert d’événement pour transférer des données vers une solution non-Adobe.


### Création d’un élément de données de transfert d’événement

L’objet XDM que vous avez précédemment configuré à l’aide de l’extension de balise SDK Web Platform devient la source de données pour les éléments de données dans une propriété de transfert d’événement. Vous utilisez les mêmes données que celles que vous avez déjà configurées dans la propriété de balise comme source de données pour le transfert d’événement.

>[!IMPORTANT]
>
>Il existe une différence de syntaxe clé lors du référencement des champs XDM dans le transfert d’événement par rapport à d’autres contextes. Pour référencer les données dans une propriété de transfert d’événement, le chemin d’accès de l’élément de données doit inclure le préfixe `arc.event` :
>
> * `arc` désigne Adobe Response Context.
> * Par exemple : `arc.event.xdm.web.webPageDetails.URL`
>
>Si ce chemin dʼaccès nʼest pas spécifié correctement, les données ne sont pas collectées.

Au cours de cet exercice, vous allez transférer la hauteur de la fenêtre d’affichage du navigateur et l’identifiant Experience Cloud de l’objet XDM vers un webhook. Le chemin d’accès au champ XDM est déterminé par le schéma XDM créé lors de la leçon [Configuration d’un schéma XDM](configure-schemas.md) .

>[!TIP]
>
>Vous pouvez également trouver le chemin d’accès de l’objet XDM en utilisant les outils réseau de votre navigateur web, en filtrant les requêtes `/ee`, en ouvrant la balise [!UICONTROL **Payload**] et en descendant vers la variable que vous recherchez. Cliquez avec le bouton droit de la souris et sélectionnez &quot;Copier le chemin de la propriété&quot;. Voici un exemple pour la hauteur de la fenêtre d’affichage du navigateur :
> ![Chemin XDM de transfert d’événement](assets/event-forwarding-xdm-path.png)

1. Accédez à la propriété **[!UICONTROL Event Forwarding]** que vous avez récemment créée.

1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Data Elements]**

1. Sélectionnez **[!UICONTROL Créer un élément de données]**

   ![Transfert d’événement d’un nouvel élément de données](assets/event-forwarding-new-dataelement.png)

1. **[!UICONTROL Nommer]** l’élément de données `environment.browserDetails.viewportHeight`

1. Sous **[!UICONTROL Extension]**, laissez `CORE`

1. Sous **[!UICONTROL Type d’élément de données]**, sélectionnez `Path`

1. Saisissez le chemin d’accès de l’objet XDM contenant la hauteur de la fenêtre d’affichage du navigateur `arc.event.xdm.environment.browserDetails.viewportHeight`.

1. Sélectionnez **[!UICONTROL Save]**

   ![Chemin d’accès ECID de transfert d’événement](assets/event-forwarding-browser-viewpoirt-height.png)


1. Création d’un autre élément de données

1. **[!UICONTROL Nom]** it `ecid`

1. Sous **[!UICONTROL Extension]**, laissez `CORE`

1. Sous **[!UICONTROL Type d’élément de données]**, sélectionnez `Path`

1. Saisissez le chemin d’accès à l’objet XDM contenant l’identifiant Experience Cloud `arc.event.xdm.identityMap.ECID.0.id`.

1. Sélectionnez **[!UICONTROL Save]**

   ![Chemin d’accès ECID de transfert d’événement](assets/event-forwarding-ecid.png)

   >[!CAUTION]
   >
   > Veillez à inclure le préfixe `arc.event.` dans le chemin d’accès. Veillez également à respecter la casse exacte en tant que nom du champ d’objet XDM : l’espace de noms ECID doit être en majuscules.


   >[!TIP]
   >
   >Lorsque vous utilisez votre propre site web, vous pouvez trouver le chemin d’accès de l’objet XDM avec les outils réseau de votre navigateur web, en filtrant les requêtes `/ee`, en ouvrant la balise [!UICONTROL **Payload**] et en descendant vers la variable que vous recherchez. Cliquez avec le bouton droit de la souris et sélectionnez &quot;Copier le chemin de la propriété&quot;. Voici un exemple pour la hauteur de la fenêtre d’affichage du navigateur :
   > ![Chemin XDM de transfert d’événement](assets/event-forwarding-xdm-path.png)

### Installation de l’extension Adobe Cloud Connector

Pour envoyer des données à des emplacements tiers, vous devez d’abord installer l’extension [!UICONTROL Adobe Cloud Connector].

1. Sélectionnez **[!UICONTROL Extensions]** dans le volet de navigation de gauche

1. Sélectionnez l’onglet **[!UICONTROL Catalogue]**

1. Recherchez **[!UICONTROL Adobe Cloud Connector]**, sélectionnez **[!UICONTROL Install]**

   ![Chemin d’accès ECID de transfert d’événement](assets/event-forwarding-adobe-cloud-connector.png)

Aucune configuration d’extension n’est nécessaire. Avec cette extension, vous pouvez désormais transférer des données vers une solution autre qu’Adobe !

### Création d’une règle de transfert d’événement

Il existe quelques différences principales entre la configuration des règles dans une propriété de balise et une règle dans une propriété de transfert d’événement :

* **[!UICONTROL Événements] et [!UICONTROL Conditions]** :

   * **Balises** : toutes les règles sont déclenchées par un événement qui doit être spécifié dans la règle, par exemple, `Library Loaded - Page Top`. Les conditions sont facultatives.
   * **Transfert d’événement** : on suppose que chaque événement envoyé à l’Edge Network Platform est un déclencheur pour transférer des données. Par conséquent, aucun [!UICONTROL événement] ne doit être sélectionné dans les règles de transfert d’événement. Pour gérer les événements qui déclenchent une règle de transfert d’événement, vous devez configurer des conditions.

* **Jeton d’élément de données** :

   * **Balises** : les noms des éléments de données sont segmentés en unités lexicales avec un `%` au début et à la fin du nom de l’élément de données lorsqu’ils sont utilisés dans une règle. Par exemple : `%viewportHeight%`.

   * **Transfert d’événement** : les noms des éléments de données sont segmentés en unités lexicales avec `{{` au début et `}}` à la fin du nom de l’élément de données lorsqu’ils sont utilisés dans une règle. Par exemple : `{{viewportHeight}}`.

* **Séquence d’actions de règle** :

   * La section Actions d’une règle de transfert d’événement est toujours exécutée de manière séquentielle. Assurez-vous que l’ordre des actions est correct lorsque vous enregistrez une règle. Cette séquence d’exécution ne peut pas être exécutée de manière asynchrone, à la différence des balises.

<!--
  * **Tags**: Rule actions can easily be reordered using drag-and-drop functionality.
  * **Event forwarding**: Rule actions are always executed sequentially. Make sure the order of actions is correct when you save a rule.
-->

Pour configurer une règle de transfert de données vers votre webhook, vous devez d’abord obtenir votre webhook personnel :

1. Accédez à [Webhook.site](https://webhook.site)

1. Recherchez **votre URL unique**. Utilisez-la comme requête d’URL dans votre règle de transfert d’événement.

1. Sélectionnez **[!UICONTROL Copier vers le presse-papiers]**

1. Laissez cette fenêtre ouverte, car vous pourrez valider les données de transfert d’événement en temps réel capturées par Webhook.

   ![Copier l’URL Webhook](assets/event-forwarding-webhook.png)

1. Revenez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Transfert d’événement]** > **[!UICONTROL Règles]** à partir du volet de navigation de gauche.

1. Sélectionnez **[!UICONTROL Créer une règle]**

   ![Transfert d’événement Nouvelle règle](assets/event-forwarding-new-rules.png)

1. Nommez-le `all events - ad cloud connector - webhook`

1. Ajout d’une action

1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Adobe Cloud Connector]**

1. Sous **[!UICONTROL Action Type]**, sélectionnez **[!UICONTROL Make Fetch Call]**

1. Collez l’URL de webhook dans le champ **[!UICONTROL URL]**

   ![Copier l’URL Webhook](assets/event-forwarding-rule.png)

1. Sous **[Params de requête]**, vous allez ajouter les deux éléments de données que vous avez créés précédemment.

1. Sur le type de colonne **[!UICONTROL Key]** dans `viewPortHeight`. Dans la colonne **[!UICONTROL Valeur]**, saisissez l’élément de données `{{environment.browserDetails.viewportHeight}}` en le saisissant ou en le sélectionnant à partir de l’icône du sélecteur d’éléments de données.

1. Sélectionnez [!UICONTROL **+ Ajouter un autre**] pour ajouter un autre paramètre de requête

1. Sur le type de colonne **[!UICONTROL Key]** dans `ecid`. Dans la colonne Valeur , saisissez l’élément de données `{{ecid}}`.

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Ajouter un paramètre de requête](assets/event-forwarding-rule-query-parameter.png)

1. Votre règle doit ressembler à ci-dessous.

1. Sélectionnez **[!UICONTROL Save]**

   ![Enregistrer la règle de transfert d’événement](assets/event-forwarding-rule-save.png)

### Création et création de la bibliothèque

Créez une bibliothèque et générez toutes les modifications dans votre environnement de développement de transfert d’événement comme vous le feriez normalement dans une propriété de balise.

>[!NOTE]
>
>Si vous n’avez pas lié les propriétés d’évaluation et de transfert d’événement de production à votre flux de données, vous verrez l’environnement de développement comme la seule option vers laquelle créer une bibliothèque.

![Enregistrer la règle de transfert d’événement](assets/event-forwarding-initial-build.png)

## Validation de la règle de transfert d’événement

Vous pouvez maintenant valider votre propriété de transfert d’événement à l’aide de Platform Debugger et de Webhook.site :

1. Suivez les étapes pour [changer la bibliothèque de balises](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en/men.html) vers la propriété de balise du SDK Web vers laquelle vous avez mappé votre propriété de transfert d’événement dans le flux de données.

1. Avant de recharger la page, sur le débogueur Experience Platform, ouvrez **[!UICONTROL Journaux]** dans le volet de navigation de gauche.

1. Sélectionnez l’onglet **[!UICONTROL Edge]** , puis sélectionnez **[!UICONTROL Se connecter]** pour afficher les demandes de l’Edge Network Platform.

   ![Session réseau de périphérie de transfert d’événement](assets/event-forwarding-edge-session.png)

1. Recharger la page

1. D’autres requêtes s’affichent, vous donnant ainsi une vue d’ensemble des requêtes côté serveur envoyées par l’Edge Network Platform à WebHook.

1. La requête sur laquelle se concentrer la validation est celle qui montre l’URL entièrement construite envoyée par le réseau Edge.

   ![Débogueur de transfert d’événement](assets/event-forwarding-debugger.png)


1. Notez les paramètres de chaîne de requête viewPortHeight et ecid

   ![Chaînes de requête de validation de transfert d’événement](assets/event-forwarding-validate-data.png)

1. Ils correspondent aux données affichées dans l’objet XDM.

   ![Transfert d’événement correspondant aux données](assets/event-forwarding-matching-data.png)

1. Enfin, validez les correspondances de données dans [Webhook.site](https://webhook.site) en affichant votre fenêtre Webhook ouverte.

   ![Données du site webhook de transfert d’événement](assets/event-forwarding-webhook-data.png)

Félicitations ! Vous avez configuré le transfert d’événement !

[Suivant : ](conclusion.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
