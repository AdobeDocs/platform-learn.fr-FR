---
title: Structuration de vos données
description: Structuration de vos données
exl-id: 8d176389-25a4-4718-afff-efd2f87204ed
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# Structuration de vos données

Les entreprises ont leur propre langue pour communiquer sur leur domaine. Les concessionnaires automobiles s&#39;occupent des marques, des modèles et des cylindres. Les compagnies aériennes traitent des numéros de vol, des classes de service et des assignations de places. Certains de ces termes sont propres à une entreprise spécifique, d’autres sont partagés entre les secteurs d’activité et d’autres sont partagés par presque toutes les entreprises. Pour les termes partagés dans un secteur industriel vertical ou même au-delà, vous pouvez commencer à utiliser vos données de manière puissante lorsque vous nommez et structurez ces termes de manière commune.

Par exemple, de nombreuses entreprises traitent des commandes. Et si, collectivement, ces entreprises décidaient de modéliser une commande de la même manière ? Par exemple, que se passe-t-il si le modèle de données est constitué d’un objet avec une `priceTotal` qui représentait le prix total de la commande ? Et si les propriétés de cet objet étaient également nommées `currencyCode` et `purchaseOrderNumber`? Peut-être que l’objet order contient une propriété nommée `payments` qui serait un tableau d&#39;objets de paiement. Chaque objet représente un paiement pour la commande. Par exemple, un client a peut-être payé une partie de la commande avec une carte-cadeau et payé le reste avec une carte de crédit. Vous pouvez commencer à construire un modèle qui ressemble à ceci :

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

## XDM

C&#39;est l&#39;objectif de l&#39;Adobe [Modèle de données d’expérience](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM fournit une modélisation descriptive pour les données courantes dans le secteur, tout en vous permettant d’étendre le modèle en fonction de vos besoins spécifiques. Adobe Experience Platform est conçu autour de XDM et, en tant que tel, les données envoyées à Experience Platform doivent être dans XDM. Plutôt que de réfléchir à où et comment transformer vos modèles de données actuels en XDM avant d’envoyer les données à l’Experience Platform, envisagez d’adopter XDM de manière plus systématique à l’échelle de votre organisation afin que la traduction ait rarement lieu.

[Suivant : ](configure-the-server/create-a-schema.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
