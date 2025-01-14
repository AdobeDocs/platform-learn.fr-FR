---
title: Migration des règles de lien personnalisées
description: Découvrez comment migrer des règles qui envoient des accès à des liens personnalisés (par opposition aux pages vues).
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16765
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# Migration des règles de lien personnalisées

Dans cet exercice, vous apprendrez à migrer les règles qui envoient des accès à des liens personnalisés (par opposition aux pages vues).

## Vue d’ensemble

Lorsque vous envoyez un accès à un lien personnalisé à l’aide de l’extension Analytics ou d’un code d’AppMeasurement, lorsque vous configurez l’action **Envoyer la balise**, vous choisissez également d’envoyer un accès à une page vue ou un accès à un lien personnalisé, et si vous choisissez un accès à un lien personnalisé, il vous demandera le **Nom du lien** et le **Type de lien** pour cet accès. Si vous n’envoyez pas d’autres données de variable que le nom et le type du lien, vous n’avez pas besoin d’une action supplémentaire qui définit des variables (props, eVars et événements).
Pour cette raison, lorsque vous migrez des règles qui sont des règles de lien personnalisées, vous aurez **l’un des deux** scénarios suivants dans les règles :

1. La règle existante contiendra une action **Adobe Analytics - Définir les variables** qui définit les props, les eVars, les événements, etc., puis contient une action **Adobe Analytics - Envoyer la balise** qui définit l’accès à un accès à un lien personnalisé (A.K.A. un accès s.tl()), définit le nom et le type du lien, puis envoie les données.
   1. Dans ce cas, il contiendra probablement également une action finale appelée **Adobe Analytics - Effacer les variables** afin de « zéro » la valeur des variables après l’envoi des données aux serveurs d’Adobe.
1. La règle existante contiendra uniquement l’action **Adobe Analytics - Envoyer la balise** qui définit l’accès sur un accès à un lien personnalisé, définit le nom et le type du lien et envoie les données.

### Un changement important

La raison pour laquelle cela est important lorsque vous migrez votre implémentation Adobe Analytics vers le SDK Web est la suivante :
Le paramètre du nom et du type du lien, qui est obligatoire pour que l’accès soit un accès à un lien personnalisé, ne se trouve PAS dans l’action « Envoyer l’équivalent d’une balise » (événement d’envoi). Ce paramètre du nom et du type de lien se trouve plutôt dans l’action « Définir des variables équivalentes » (mettre à jour la variable).
Par conséquent, que vous ayez le scénario 1 ou le scénario 2 ci-dessus, vous devrez obtenir à la fois une action Mettre à jour la variable et une action Envoyer l’événement.

Vous trouverez ci-dessous une représentation visuelle de cette différence dans les implémentations .

![Migration des règles de lien personnalisées](assets/migrate-custom-link-rule-2.jpg)

## Étapes de migration

Ouvrez votre règle de lien personnalisé et déterminez si elle ressemble au scénario 1 ou au scénario 2 ci-dessus.
**Si votre règle ressemble au scénario 1:**

1. Ouvrez l’action Définir les variables et notez toutes les variables (props, eVars, événements, etc.) définies dans cette action (par exemple, dans l’image ci-dessus, event10 est défini).
1. Ouvrez l’action Envoyer la balise et vérifiez qu’elle est définie pour envoyer un accès s.tl(). Notez les valeurs Type de lien et Nom du lien.
1. Dans la section Actions de votre règle de lien personnalisée, cliquez sur l’icône plus pour ajouter une autre règle.

   ![Ajouter une nouvelle action](assets/add-new-action-3.jpg)

1. Configuration de l’action
   1. Définissez la variable **Extension** sur Adobe Experience Platform Web SDK
   1. Définissez le **Type d’action** sur Mettre à jour la variable
   1. Sélectionnez l’objet **Analytics**
   1. Définissez vos props, eVars et événements à partir de votre action Analytics Définir les variables (dans cet exemple, event10).

      ![Définition des variables à migrer](assets/set-variables-to-migrate.jpg)

   1. Dans la même règle, faites défiler l’écran jusqu’au champ déroulant **Propriété supplémentaire**, puis ajoutez le champ **Nom du lien** en le définissant sur la valeur que vous avez extraite de votre règle Envoyer la balise. Dans l’image ci-dessous, l’exemple définit le nom sur la valeur de chaîne « clic sur le menu ».
   1. Ajoutez également le champ **Type de lien** dans la même liste déroulante, en ajoutant « o » comme valeur (en supposant que votre type de lien dans l’action Envoyer la balise soit « Lien personnalisé »). Cette opération envoie le type de lien « autre », ce qui équivaut à un lien personnalisé. Si votre type de lien était un lien de téléchargement, choisissez « d » pour la valeur de ce champ nouveau type de lien et si votre type de lien était un lien de sortie, choisissez « e » pour la valeur de ce champ nouveau type de lien.

      ![Nom et type du lien ](assets/link-name-and-type.jpg)

1. Sous les propriétés supplémentaires, une case à cocher intitulée **Effacer la valeur existante** s’affiche. Si votre règle existante comporte une action **Adobe Analytics - Effacer les variables** (comme indiqué ci-dessus à l’étape 3), il vous suffit de cocher cette case, et vous n’aurez pas besoin d’ajouter une action d’effacement des variables pour le SDK Web.

   ![effacer les variables](assets/clear-existing-value.jpg)

1. Ajoutez une autre action en cliquant sur l’icône plus.
1. Configurer votre action d’événement d’envoi
   1. Définissez la variable **Extension** sur Adobe Experience Platform Web SDK
   1. Définissez le **Type d’action** sur Événement envoyé
   1. Cliquez sur l’icône de l’élément de données et sélectionnez l’élément de données **Variable de données de page vue**

   ![Configurer l’événement d’envoi](assets/configure-send-event.jpg)

1. **Conserver les modifications**, **Enregistrer dans la bibliothèque** et vous pouvez **Créer** la bibliothèque à partir de cette même page, puisque nous avons déjà défini une bibliothèque de travail.

## Tirer une conclusion importante en matière de migration

* Dans cette leçon, vous avez appris à migrer des règles de lien personnalisées.
* Dans l’exercice [Migrer votre règle de chargement de page par défaut](migrate-your-default-page-load-rule.md), vous avez appris à migrer les règles qui définissent des variables et envoient également une balise Analytics.
* Dans la leçon [ Migration de règles de page supplémentaires ](migrate-additional-page-rules.md) , vous avez appris à migrer vos règles qui définissent des variables mais n’envoient pas de balise dans Adobe Analytics.

Comme vous pouvez l’imaginer, les mêmes méthodes peuvent être utilisées dans de nombreuses règles différentes pour migrer votre extension Analytics vers Web SDK.
Dans la plupart des cas, vous mettez simplement **à jour les actions** dans les règles. Vous ne modifiez pas l’événement ni les conditions de déclenchement. Vous ne modifiez ce qui se passe dans la section Actions que lorsque les règles se déclenchent.
La plupart, voire la totalité, de vos règles appartiennent à ces catégories. Si une règle ne fonctionne pas correctement, envisagez le même paradigme de migration de l’action, et non pas celui qui a déclenché la règle.
