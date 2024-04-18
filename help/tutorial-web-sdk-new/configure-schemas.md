---
title: Création d’un schéma XDM pour les données web
description: Découvrez comment créer un schéma XDM pour les données web dans l’interface de collecte de données. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK,Schemas
exl-id: 159f914a-43d4-4808-b6af-01136386e25c
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# Création d’un schéma XDM pour les données web

Découvrez comment créer un schéma XDM pour les données web dans l’interface de collecte de données.

Les schémas de modèle de données d’expérience (XDM) sont les blocs de création, les principes et les bonnes pratiques pour la collecte de données dans Adobe Experience Platform.

Le SDK Web Platform utilise votre schéma pour normaliser vos données d’événement web, les envoyer à l’Edge Network Platform et, en fin de compte, transférer les données à toute application Experience Cloud configurée dans le flux de données. Cette étape est essentielle, car elle définit un modèle de données standard requis pour ingérer des données d’expérience client dans Experience Platform et permet aux services et applications en aval de fonctionner conformément à ces normes.

## Pourquoi modéliser les données ?

Les entreprises ont leur propre langue pour communiquer sur leur domaine. Les concessionnaires automobiles s&#39;occupent des marques, des modèles et des cylindres. Les compagnies aériennes traitent des numéros de vol, des classes de service et des assignations de places. Certains de ces termes sont propres à une entreprise spécifique, d’autres sont partagés entre les secteurs d’activité et d’autres sont partagés par presque toutes les entreprises. Pour les termes partagés dans un secteur industriel vertical ou même au-delà, vous pouvez commencer à utiliser vos données de manière puissante lorsque vous nommez et structurez ces termes de manière commune.

Par exemple, de nombreuses entreprises traitent des commandes. Et si, collectivement, ces entreprises décidaient de modéliser une commande de la même manière ? Par exemple, que se passe-t-il si le modèle de données est constitué d’un objet avec une `priceTotal` qui représentait le prix total de la commande ? Que se passe-t-il si cet objet possède également des propriétés nommées `currencyCode` et `purchaseOrderNumber`? L’objet order peut contenir une propriété nommée `payments` qui serait un tableau d&#39;objets de paiement. Chaque objet représente un paiement pour la commande. Par exemple, un client a peut-être payé une partie de la commande avec une carte-cadeau et payé le reste avec une carte de crédit. Vous pouvez commencer à construire un modèle qui ressemble à ceci :

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

Si toutes les entreprises qui traitent des commandes décidaient de modéliser leurs données de commande de manière cohérente pour des termes courants dans le secteur, des choses magiques pourraient commencer à se produire. Les informations pourraient être échangées plus couramment à l&#39;intérieur et à l&#39;extérieur de votre organisation au lieu d&#39;interpréter et traduire constamment les données (props et evars, qui que ce soit ?). L’apprentissage automatique pourrait plus facilement comprendre vos données. _signifie_ et fournissent des informations exploitables. Les interfaces utilisateur pour l’affichage de données pertinentes pourraient devenir plus intuitives. Vos données peuvent être intégrées de manière transparente avec des partenaires et des fournisseurs qui suivent la même modélisation.

C&#39;est l&#39;objectif de l&#39;Adobe [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM fournit une modélisation descriptive pour les données courantes dans le secteur, tout en vous permettant d’étendre le modèle en fonction de vos besoins spécifiques. Adobe Experience Platform est conçu autour de XDM et, en tant que tel, les données envoyées à Experience Platform doivent être dans XDM. Plutôt que de réfléchir à où et comment transformer vos modèles de données actuels en XDM avant d’envoyer les données à l’Experience Platform, envisagez d’adopter XDM de manière plus systématique à l’échelle de votre organisation afin que la traduction ait rarement lieu.


>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon créent un exemple de schéma pour capturer le contenu consulté et les produits achetés par les clients dans la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Bien que vous puissiez utiliser ces étapes pour créer un schéma différent à vos propres fins, il est recommandé de suivre d’abord la création de l’exemple de schéma pour découvrir les fonctionnalités de l’éditeur de schémas.

Pour en savoir plus sur les schémas XDM, suivez le cours [Modèle de vos données d’expérience client avec XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=fr) ou voir la [Présentation du système XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr).

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Création d’un schéma XDM dans l’interface de collecte de données
* Ajout de groupes de champs à votre schéma XDM
* Création de schémas XDM pour les données d’événement web à l’aide des bonnes pratiques

## Conditions préalables

Toutes les autorisations d’utilisateur et d’approvisionnement nécessaires pour la collecte de données et Adobe Experience Platform décrites dans la section [aperçu](overview.md) page.

## Créer un schéma XDM

Les schémas XDM sont la méthode standard pour décrire les données en Experience Platform, ce qui permet à toutes les données conformes aux schémas d’être réutilisées dans une organisation sans conflit, voire partagées entre plusieurs organisations. Pour en savoir plus, voir la section [Principes de base de la composition des schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr).

Au cours de cet exercice, vous allez créer un schéma XDM à l’aide des groupes de champs de ligne de base recommandés pour capturer les données d’événement web sur la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Ouvrez le [Interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Vérifiez que vous vous trouvez dans le bon environnement de test. Localisation de l’environnement de test dans le coin supérieur droit

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un environnement de test de développement pour ce tutoriel. Si ce n’est pas le cas, utilisez le **[!UICONTROL Prod]** sandbox.

1. Accédez à **[!UICONTROL Schémas]** dans la navigation de gauche
1. Sélectionnez la variable **[!UICONTROL Création d’un schéma]** en haut à droite

   ![Création d’un schéma](assets/schema-xdm-create-schema.png)
1. Sélectionner **[!UICONTROL Événement d’expérience]** dans l’écran suivant
1. Sélectionner **[!UICONTROL Suivant]**

   ![Événement d’expérience de schéma](assets/schema-experience-event.png)

1. Saisissez le nom de votre schéma sous **[!UICONTROL Nom d’affichage du schéma]** champ, dans ce cas `Luma Web Event Data`

   >[!TIP]
   >
   >Une convention d’affectation des noms courante pour les schémas XDM consiste à nommer le schéma après la source des données.


1. Sélectionner Terminer

   ![Fin de l’événement d’expérience de schéma](assets/schema-name-schema.png)

## Ajouter des groupes de champs

Comme nous l’avons déjà mentionné, XDM est le cadre de base qui normalise les données d’expérience client en fournissant des structures et des définitions communes à utiliser dans les services Adobe Experience Platform en aval. En adhérant aux normes XDM, _toutes les données d’expérience client_ peut être intégré à une représentation commune. Cette approche vous permet d’obtenir des informations précieuses à partir des actions des clients, de définir des audiences de clients par le biais de segments et d’exprimer les attributs du client à des fins de personnalisation à l’aide de données provenant de plusieurs sources. Voir [Bonnes pratiques relatives à la modélisation des données](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) pour plus d’informations.

Dans la mesure du possible, il est recommandé d’utiliser des groupes de champs existants et de respecter un modèle et des conventions d’affectation des noms indépendant du produit. Pour toute donnée propre à votre organisation qui ne correspond pas aux groupes de champs prédéfinis ci-dessus, vous pouvez créer un groupe de champs personnalisé. Voir [Création d’un schéma à l’aide de l’éditeur de schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) pour obtenir des instructions plus détaillées sur les schémas personnalisés.

>[!TIP]
> 
>Dans cet exercice, vous ajoutez les groupes de champs prédéfinis recommandés pour la collecte de données web : _**[!UICONTROL ExperienceEvent du SDK Web AEP]**_ et _**[!UICONTROL Événement d’expérience client]**_.
>
>
> Si vous implémentez uniquement **Adobe Analytics** avec le SDK Web et sans envoyer de données à **Experience Platform**, utilisez le [!UICONTROL Modèle ExperienceEvent Adobe Analytics] groupe de champs pour définir le schéma XDM. Elle sera utilisée dans la variable [Configuration d’Analytics](setup-analytics.md) leçon.

1. Dans le **[!UICONTROL Groupes de champs]** , sélectionnez **[!UICONTROL Ajouter]**

   ![Nouveau groupe de champs](assets/schema-new-field-group.png)

1. Recherchez [!UICONTROL `AEP Web SDK ExperienceEvent`].
1. Cochez la case
1. Recherchez [!UICONTROL `Consumer Experience Event`].
1. Cochez la case
1. Sélectionner **[!UICONTROL Ajouter des groupes de champs]**

   ![Ajouter un groupe de champs](assets/schema-add-field-group.png)

Avec les deux groupes de champs, notez que vous avez accès aux paires clé-valeur les plus couramment utilisées requises pour la collecte de données sur le Web. La variable [!UICONTROL nom d&#39;affichage] de chaque champ s’affiche pour les spécialistes du marketing dans l’interface du créateur de segments des applications basées sur Platform. Vous pouvez modifier le nom d’affichage des champs standard en fonction de vos besoins. Vous pouvez également supprimer les champs que vous ne souhaitez pas. Lorsque vous cliquez sur l’un des noms de groupe de champs, l’interface met en évidence les regroupements de paires clé-valeur qui lui appartiennent. Dans l’exemple ci-dessous, vous pouvez voir à quels groupes appartiennent. **[!UICONTROL Événement d’expérience client]**.

![Groupes de champs de schéma](assets/schema-consumer-experience-event.png)

Cette leçon n&#39;est qu&#39;un point de départ. Lors de la création de votre propre schéma d’événements web, vous devez explorer et documenter les besoins de votre entreprise. Ce processus est similaire à la création d’une [Document sur les besoins de l’entreprise](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=fr) et [Référence de conception de solution](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html?lang=fr) pour une mise en oeuvre Adobe Analytics, mais doit inclure des exigences pour _tous les destinataires de données en aval_ telles que les destinations de transfert de Platform, de Target et d’événement.


### Objet identityMap

Un champ spécial est utilisé pour identifier les utilisateurs web appelés `[!UICONTROL identityMap]`.

![Données d’événement web Luma](assets/schema-identityMap.png)

Il s’agit d’un objet obligatoire pour toute collecte de données Web, car il contient l’identifiant Experience Cloud requis pour identifier les utilisateurs sur le Web. C’est également la clé de la définition des ID de client internes pour les utilisateurs authentifiés. `[!UICONTROL identityMap]` est abordé plus en détail dans la section [Configuration des identités](configure-identities.md) leçon. Elle est automatiquement incluse dans tous les schémas à l’aide de la variable **[!UICONTROL XDM ExperienceEvent]** classe .


>[!IMPORTANT]
>
> Il est possible d’activer **[!UICONTROL Profil]** pour un schéma avant d’enregistrer votre schéma. **Ne pas** l’activer à ce stade. Une fois qu’un schéma est activé pour Profile, il ne peut pas être désactivé ni supprimé. Les champs ne peuvent pas non plus être supprimés des schémas à ce stade, bien qu’il soit possible de [Champs obsolètes dans l’interface utilisateur](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation-ui.html?lang=en#deprecate). Il est important de tenir compte de ces implications ultérieurement lorsque vous travaillez avec vos propres données dans votre environnement de production.
>
>
>Ce paramètre est abordé plus en détail au cours de la [Configuration d’un Experience Platform](setup-experience-platform.md) leçon.
>![Schéma de profil](assets/schema-profile.png)

Pour terminer cette leçon, sélectionnez **[!UICONTROL Enregistrer]** en haut à droite.

![Enregistrer le schéma](assets/schema-select-save.png)


Vous pouvez maintenant référencer ce schéma lorsque vous ajoutez l’extension SDK Web à votre propriété de balise.


[Suivant : ](configure-identities.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
