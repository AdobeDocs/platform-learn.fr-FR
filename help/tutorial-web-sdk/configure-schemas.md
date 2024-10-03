---
title: Création d’un schéma XDM pour les données web
description: Découvrez comment créer un schéma XDM pour les données web dans l’interface de collecte de données. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Schemas
jira: KT-15398
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 3%

---

# Création d’un schéma XDM pour les données web

Découvrez comment créer un schéma XDM pour les données web dans l’interface de collecte de données d’Adobe Experience Platform.

Les schémas de modèle de données d’expérience (XDM) sont les blocs de création, les principes et les bonnes pratiques pour la collecte de données dans Adobe Experience Platform.

Le SDK Web Platform utilise votre schéma pour normaliser vos données d’événement web, les envoyer à l’Edge Network Platform et, en fin de compte, transférer les données à toute application Experience Cloud configurée dans le flux de données. Cette étape est essentielle, car elle définit un modèle de données standard requis pour ingérer des données d’expérience client dans Experience Platform et permet aux services et applications en aval de fonctionner conformément à ces normes.

>[!NOTE]
>
>Un schéma XDM est _non requis_ pour implémenter Adobe Analytics, Adobe Target ou Adobe Audience Manager avec SDK Web (les données peuvent être transmises dans l’objet `data` au lieu de l’objet `xdm` comme vous le verrez plus loin). Un schéma XDM est requis pour les implémentations les plus performantes des applications natives à Platform telles que Journey Optimizer, Real-Time Customer Data Platform, Customer Journey Analytics. Bien que vous puissiez décider de ne pas utiliser un schéma XDM dans votre propre mise en oeuvre, vous devez le faire dans le cadre de ce tutoriel.

## Pourquoi modéliser les données ?

Les entreprises ont leur propre langue pour communiquer sur leur domaine. Les concessionnaires automobiles s&#39;occupent des marques, des modèles et des cylindres. Les compagnies aériennes traitent des numéros de vol, des classes de service et des assignations de places. Certains de ces termes sont propres à une entreprise spécifique, d’autres sont partagés entre les secteurs d’activité et d’autres sont partagés par presque toutes les entreprises. Pour les termes partagés dans un secteur industriel vertical ou même au-delà, vous pouvez commencer à utiliser vos données de manière puissante lorsque vous nommez et structurez ces termes de manière commune.

Par exemple, de nombreuses entreprises traitent des commandes. Et si, collectivement, ces entreprises décidaient de modéliser une commande de la même manière ? Par exemple, que se passe-t-il si le modèle de données est constitué d’un objet avec une propriété `priceTotal` qui représentait le prix total de la commande ? Que se passe-t-il si cet objet possède également des propriétés appelées `currencyCode` et `purchaseOrderNumber` ? Peut-être que l’objet order contient une propriété nommée `payments` qui serait un tableau d’objets de paiement. Chaque objet représente un paiement pour la commande. Par exemple, un client a peut-être payé une partie de la commande avec une carte-cadeau et le reste avec une carte de crédit. Vous pouvez commencer à construire un modèle qui ressemble à ceci :

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Si toutes les entreprises qui traitent des commandes décidaient de modéliser leurs données de commande de manière cohérente pour des termes courants dans le secteur, des choses magiques pourraient commencer à se produire. Les informations pourraient être échangées plus couramment à l&#39;intérieur et à l&#39;extérieur de votre organisation au lieu d&#39;interpréter et traduire constamment les données (props et evars, qui que ce soit ?). L’apprentissage automatique peut comprendre plus facilement ce que vos données _signifient_ et fournir des informations exploitables. Les interfaces utilisateur pour l’affichage de données pertinentes pourraient devenir plus intuitives. Vos données peuvent être intégrées de manière transparente avec des partenaires et des fournisseurs qui suivent la même modélisation.

C’est l’objectif du [modèle de données d’expérience](https://business.adobe.com/products/experience-platform/experience-data-model.html) de l’Adobe. XDM fournit une modélisation descriptive pour les données courantes dans le secteur, tout en vous permettant d’étendre le modèle en fonction de vos besoins spécifiques. Adobe Experience Platform est conçu autour de XDM et, en tant que tel, les données envoyées à Experience Platform doivent être dans XDM. Plutôt que de réfléchir à où et comment transformer vos modèles de données actuels en XDM avant d’envoyer les données à l’Experience Platform, envisagez d’adopter XDM de manière plus systématique à l’échelle de votre organisation afin que la traduction ait rarement lieu.


>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon créent un exemple de schéma pour capturer le contenu affiché et les produits achetés par les clients sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Bien que vous puissiez utiliser ces étapes pour créer un schéma différent à vos propres fins, il est recommandé de suivre d’abord la création de l’exemple de schéma pour découvrir les fonctionnalités de l’éditeur de schémas.

Pour en savoir plus sur les schémas XDM, consultez la playlist [Model Your Customer Experience Data with XDM](https://experienceleague.adobe.com/en/playlists/experience-platform-model-your-customer-experience-data-with-xdm) ou consultez la [présentation du système XDM](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/home).

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Création d’un schéma XDM dans l’interface de collecte de données
* Ajout de groupes de champs à votre schéma XDM
* Création de schémas XDM pour les données d’événement web à l’aide des bonnes pratiques

## Conditions préalables

Toutes les autorisations d’utilisateur et de mise en service nécessaires pour la collecte de données et Adobe Experience Platform sont décrites sur la page [overview](overview.md) .

## Créer un schéma XDM

Les schémas XDM sont la méthode standard pour décrire les données en Experience Platform, ce qui permet à toutes les données conformes aux schémas d’être réutilisées dans une organisation sans conflit, voire partagées entre plusieurs organisations. Pour en savoir plus, consultez les [ principes de base de la composition des schémas](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/schema/composition).

Au cours de cet exercice, vous allez créer un schéma XDM à l’aide des groupes de champs de ligne de base recommandés pour capturer les données d’événement web sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} :

1. Ouvrez l’ [ interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Vérifiez que vous vous trouvez dans le bon environnement de test. Localisation de l’environnement de test dans le coin supérieur droit

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un environnement de test de développement pour ce tutoriel. Si ce n&#39;est pas le cas, utilisez l&#39;environnement de test **[!UICONTROL Prod]**.

1. Accédez à **[!UICONTROL Schémas]** dans le volet de navigation de gauche
1. Sélectionnez le bouton **[!UICONTROL Créer un schéma]** en haut à droite.

   ![Créer un schéma](assets/schema-xdm-create-schema.png)
1. Sélectionnez **[!UICONTROL Experience Event]** dans l’écran suivant
1. Sélectionnez **[!UICONTROL Suivant]**

   ![Événement d’expérience de schéma](assets/schema-experience-event.png)

1. Saisissez le nom de votre schéma sous le champ **[!UICONTROL Nom d’affichage du schéma]**, ici `Luma Web Event Data`

   >[!TIP]
   >
   >Une convention d’affectation des noms courante pour les schémas XDM consiste à nommer le schéma après la source des données.


1. Sélectionner Terminer

   ![Finch de l’événement d’expérience de schéma](assets/schema-name-schema.png)

## Ajouter des groupes de champs

Comme nous l’avons déjà mentionné, XDM est le cadre de base qui normalise les données d’expérience client en fournissant des structures et des définitions communes à utiliser dans les services Adobe Experience Platform en aval. En adhérant aux normes XDM, _toutes les données d’expérience client_ peuvent être intégrées dans une représentation commune. Cette approche vous permet d’obtenir des informations précieuses à partir des actions des clients, de définir des audiences de clients par le biais de segments et d’exprimer les attributs du client à des fins de personnalisation à l’aide de données provenant de plusieurs sources. Voir [Bonnes pratiques pour la modélisation des données](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/best-practices) pour plus d’informations.

Dans la mesure du possible, il est recommandé d’utiliser des groupes de champs existants et de respecter un modèle et des conventions d’affectation des noms indépendant du produit. Pour toute donnée propre à votre organisation qui ne correspond pas aux groupes de champs prédéfinis ci-dessus, vous pouvez créer un groupe de champs personnalisé. Voir [Création d’un schéma à l’aide de l’éditeur de schémas](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/create-schema-ui#create) pour obtenir des instructions plus détaillées sur les schémas personnalisés.

>[!TIP]
> 
>Dans cet exercice, vous ajoutez les groupes de champs prédéfinis recommandés pour la collecte de données web : _**[!UICONTROL AEP Web SDK ExperienceEvent]**_ et _**[!UICONTROL Consumer Experience Event]**_.
>


1. Dans la section **[!UICONTROL Groupes de champs]**, sélectionnez **[!UICONTROL Ajouter]**

   ![Nouveau groupe de champs](assets/schema-new-field-group.png)

1. Rechercher [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Cochez la case
1. Rechercher [!UICONTROL `Consumer Experience Event`]
1. Cochez la case
1. Sélectionnez **[!UICONTROL Ajouter des groupes de champs]**

   ![Ajouter un groupe de champs](assets/schema-add-field-group.png)

Avec les deux groupes de champs, notez que vous avez accès aux paires clé-valeur les plus couramment utilisées requises pour la collecte de données sur le Web. Le [!UICONTROL nom d’affichage] de chaque champ s’affiche pour les marketeurs dans l’interface du créateur de segments des applications basées sur Platform. Vous pouvez modifier le nom d’affichage des champs standard en fonction de vos besoins. Vous pouvez également supprimer les champs que vous ne souhaitez pas. Lorsque vous cliquez sur l’un des noms de groupe de champs, l’interface met en évidence les regroupements de paires clé-valeur qui lui appartiennent. Dans l’exemple ci-dessous, vous voyez les champs appartenant à **[!UICONTROL Consumer Experience Event]**.

![Groupes de champs de schéma](assets/schema-consumer-experience-event.png)

Cette leçon n&#39;est qu&#39;un point de départ. Lors de la création de votre propre schéma d’événements web, vous devez explorer et documenter les besoins de votre entreprise. Ce processus est similaire à la création d’un [document sur les exigences de l’entreprise](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document) et d’une [référence sur la conception de la solution](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr) pour une mise en oeuvre Adobe Analytics, mais doit inclure des exigences pour _tous les destinataires de données en aval_ tels que les destinations Platform, Target et de transfert d’événement.


### Objet identityMap

Un champ spécial est utilisé pour identifier les utilisateurs web appelés `[!UICONTROL identityMap]`.

![Luma Web Event Data](assets/schema-identityMap.png)

Il s’agit d’un objet obligatoire pour toute collecte de données Web, car il contient l’identifiant Experience Cloud requis pour identifier les utilisateurs sur le Web. C’est également la clé de la définition des ID de client internes pour les utilisateurs authentifiés. `[!UICONTROL identityMap]` est abordé plus en détail dans la leçon [Configurer les identités](configure-identities.md). Elle est automatiquement incluse dans tous les schémas à l’aide de la classe **[!UICONTROL XDM ExperienceEvent]**.


>[!IMPORTANT]
>
> Il est possible d’activer **[!UICONTROL Profile]** pour un schéma avant d’enregistrer votre schéma. **Ne l’activez pas** à ce stade. Une fois qu’un schéma est activé pour Profile, il ne peut pas être désactivé ni supprimé sans réinitialiser l’ensemble de l’environnement de test. Les champs ne peuvent pas être supprimés des schémas à ce stade non plus, bien qu’il soit possible de [Champs obsolètes dans l’interface utilisateur](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/tutorials/field-deprecation-ui#deprecate). Il est important de tenir compte de ces implications ultérieurement lorsque vous travaillez avec vos propres données dans votre environnement de production.
>
>
>Ce paramètre est abordé plus en détail lors de la leçon [Configuration de l’Experience Platform](setup-experience-platform.md).
>![Schéma de profil](assets/schema-profile.png)

Pour terminer cette leçon, sélectionnez **[!UICONTROL Enregistrer]** en haut à droite.

![Enregistrer le schéma](assets/schema-select-save.png)


Désormais, vous pouvez référencer ce schéma lorsque vous ajoutez l’extension SDK Web à votre propriété de balise.


[Suivant : ](configure-identities.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
