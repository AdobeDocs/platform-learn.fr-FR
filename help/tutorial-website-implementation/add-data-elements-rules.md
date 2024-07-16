---
title: Ajout d’un élément de données, d’une règle et d’une bibliothèque
description: Découvrez comment créer des éléments de données, des règles et une bibliothèque dans des balises. Cette leçon fait partie du tutoriel Mise en oeuvre de l’Experience Cloud sur les sites web .
exl-id: 4d9eeb52-144a-4876-95d3-83d8eec4832f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 54%

---

# Ajout d’un élément de données, d’une règle et d’une bibliothèque

Au cours de cette leçon, vous allez créer votre premier élément de données, votre première règle et votre première bibliothèque.

Les éléments de données et les règles sont les blocs de création de base des balises. Les éléments de données stockent les attributs que vous souhaitez envoyer à vos solutions de marketing et publicitaires, tandis que les règles déclenchent les requêtes vers ces solutions dans les bonnes conditions. Les bibliothèques sont les fichiers JavaScript qui se chargent sur la page pour effectuer toutes les tâches. Dans cette leçon, vous utiliserez les trois pour faire fonctionner notre page d’exemple.

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été apportées à l’interface que vous devez connaître lors de l’utilisation de ce contenu :
>
> * Le platform launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Le platform launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* créer un élément de données ;
* créer une règle ;
* créer une bibliothèque ;
* ajouter des modifications à une bibliothèque ;
* valider le chargement de la bibliothèque dans votre navigateur web ;
* utiliser la fonction « Bibliothèque de travail » pour travailler plus efficacement.

## Création d’un élément de données pour le nom de page

Les éléments de données sont la version des balises d’une couche de données. Ils peuvent stocker des valeurs de votre propre objet de couche de données, de cookies, d’objets de stockage local, de paramètres de chaîne de requête, d’éléments de page, de balises META, etc. Au cours de cet exercice, vous allez créer un élément de données pour le nom de page, que vous utiliserez ultérieurement pour les implémentations de Target et Analytics.

**Création d’un élément de données**

1. Dans le volet de navigation de gauche, cliquez sur **[!UICONTROL Data Elements]**

1. Comme vous n’avez pas encore créé d’éléments de données dans cette propriété, une courte vidéo s’affiche et vous montre des informations supplémentaires sur cette rubrique. Regardez cette vidéo si vous le souhaitez.

1. Cliquez sur le bouton **[!UICONTROL Créer un élément de données]** :

   ![Créer un élément de données](images/launch-newDataElement.png)

1. Nommez l’élément de données. Par exemple, `Page Name`.

1. Utilisez le type d’élément de données [!UICONTROL Variable JavaScript] pour pointer vers une valeur dans la couche de données de votre page d’exemple : `digitalData.page.pageInfo.pageName`.

1. Cochez les cases correspondant à **[!UICONTROL Forcer l’utilisation de minuscules pour la valeur]** et **[!UICONTROL Clean text]** pour normaliser la casse et supprimer les espaces superflus.

1. Laissez **[!UICONTROL None]** comme paramètre **[!UICONTROL Durée de stockage]** , car cette valeur sera généralement différente sur chaque page.

1. Cliquez sur le bouton **[!UICONTROL Enregistrer]** pour enregistrer l’élément de données.

   ![Création de l’élément de données Nom de page](images/launch-dataElement.png).

>[!NOTE]
>
>Les fonctionnalités d’élément de données _peuvent être étendues avec les extensions_. Par exemple, l’extension ContextHub vous permet d’ajouter des éléments de données à l’aide de fonctionnalités de l’extension.

## Création d’une règle

Vous utiliserez ensuite cet élément de données dans une règle simple. Les règles sont l’une des fonctionnalités les plus puissantes des balises et vous permettent de spécifier ce qui doit se produire lorsque le visiteur interagit avec votre site web. Lorsque les critères définis dans une règle sont satisfaits, celle-ci déclenche l’action indiquée.

Vous allez créer une règle transmettant la valeur de l’élément de données Nom de page à la console du navigateur.

**Création d’une règle**

1. Dans le volet de navigation de gauche, cliquez sur **[!UICONTROL Règles]**

1. Comme vous n’avez pas encore créé de règle dans cette propriété, une courte vidéo s’affiche et vous montre des informations supplémentaires sur cette rubrique. Regardez cette vidéo si vous le souhaitez.

1. Cliquez sur le bouton **[!UICONTROL Créer une règle]** :

   ![Clic sur le bouton Créer une règle](images/launch-newRule.png)

1. Attribuez un nom à la règle `All Pages - Library Loaded`. Cette convention d’affectation des noms indique où et quand la règle se déclenchera, ce qui facilite l’identification et la réutilisation à mesure que votre propriété de balise se développe.

1. Sous Événements, cliquez sur **[!UICONTROL Ajouter]**. L’événement indique aux balises quand la règle doit se déclencher et peut être de nombreux éléments, y compris un chargement de page, un clic, un événement JavaScript personnalisé, etc.

   ![Attribution d’un nom à la règle et ajout d’un événement](images/launch-addEventToRule.png)

   1. Comme type d’événement, sélectionnez **[!UICONTROL Chargé par bibliothèque Haut de page]**. Notez que lorsque vous sélectionnez le type d’événement, les balises prérenseignent le nom de l’événement à l’aide de votre sélection. Notez également que l’ordre par défaut de l’événement est 50. La commande est une puissante fonctionnalité des balises qui vous permet de contrôler précisément la séquence d’actions lorsque plusieurs règles sont déclenchées par le même événement. Vous utiliserez cette fonctionnalité plus loin dans le tutoriel.

   1. Cliquez sur le bouton **[!UICONTROL Conserver les modifications]**

   ![Sélection d’un événement](images/launch-ruleSelectEvent.png)

1. Puisque cette règle doit se déclencher sur toutes les pages, laissez vide **[!UICONTROL Conditions]**. Si vous ouvrez le modal Conditions, vous verrez que les conditions peuvent ajouter des restrictions aussi bien que des exclusions en fonction d’une grande variété d’options, y compris les URL, les valeurs d’élément de données, les périodes, etc.

1. Sous Actions, cliquez sur **[!UICONTROL Ajouter]**

1. Sélectionnez **[!UICONTROL Type d’action > Code personnalisé]**, qui est à ce stade la seule option. Plus loin dans le tutoriel, au fur et à mesure que vous ajouterez des extensions, plus d’options deviennent disponibles.

1. Sélectionnez **[!UICONTROL &lt;/> Ouvrir l’éditeur]** pour ouvrir l’éditeur de code.

   ![Sélection d’une action](images/launch-selectAction.png)

1. Ajoutez l’élément ci-dessous à l’éditeur de code. Ce code génère la valeur de l’élément de données Nom de page dans la console du navigateur afin que vous puissiez confirmer son fonctionnement :

   ```javascript
   console.log('The page name is '+_satellite.getVar('Page Name'));
   ```

1. Enregistrez l’éditeur de code.

   ![Saisie d’un code personnalisé](images/launch-customCodeAction.png)

1. Dans l’écran Configuration de l’action, cliquez sur **[!UICONTROL Conserver les modifications]**

1. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer la règle.

Sur la page Règles , la nouvelle règle doit s’afficher :
![La règle apparaît sur la page](images/launch-savedRule.png)

## Enregistrer des modifications effectuées dans une bibliothèque

Après avoir configuré une collection d’extensions, d’éléments de données et de règles dans l’interface Collecte de données, vous devez regrouper ces fonctionnalités et logiques dans un ensemble de codes JavaScript que vous pouvez déployer sur votre site web afin que les balises marketing se déclenchent lorsque les visiteurs se connectent au site. Une bibliothèque est un ensemble de codes JavaScript qui effectue cette opération.

Dans une précédente leçon, vous avez mis en œuvre le code incorporé de votre environnement de développement sur la page d’exemple. Lorsque vous avez chargé la page d’exemple, une erreur 404 s’est affichée pour l’URL du code incorporé, car aucune bibliothèque de balises n’avait été créée et affectée à l’environnement. Vous allez maintenant placer votre nouvel élément de données et votre nouvelle règle dans une bibliothèque pour que votre page d’exemple puisse faire quelque chose.

**Ajout et création d’une bibliothèque**

1. Dans le volet de navigation de gauche, cliquez sur **[!UICONTROL Flux de publication]**

1. Cliquez sur **[!UICONTROL Ajouter une nouvelle bibliothèque]**

   ![Ajout d’une bibliothèque](images/launch-addNewLibrary.png)

1. Nommez la bibliothèque, par exemple `Initial Setup`.

1. Sélectionnez **[!UICONTROL Environnement > Développement]**

1. Cliquez sur **[!UICONTROL Ajouter toutes les ressources modifiées]**

   ![Ajout de toutes les ressources modifiées](images/launch-addAllChangedResources.png)

1. Notez qu’après avoir cliqué sur **[!UICONTROL Ajouter toutes les ressources modifiées]** , les balises résument les modifications que vous venez d’effectuer.

1. Cliquez sur **[!UICONTROL Enregistrer et créer pour le développement]**

   ![Enregistrement et génération pour le développement](images/launch-saveAndBuild.png)

Après quelques moments, l’état devient vert, ce qui indique que la bibliothèque a été créée.

![Bibliothèque créée](images/launch-libraryBuilt.png)

## Validation de votre travail

Vérifiez maintenant que votre règle fonctionne comme prévu.

Rechargez votre page d’exemple. Si vous consultez l’onglet Outils de développement -> Réseau , vous devriez maintenant voir une réponse 200 pour votre bibliothèque de balises !

![Chargements de bibliothèque avec réponse 200](images/samplepage-200.png)

Si vous consultez Outils de développement > Console, le texte « Le nom de la page est la page d’accueil » s’affiche.

![Message de la console](images/samplepage-console.png)

Félicitations, vous avez créé votre premier élément de données et votre première règle et créé votre première bibliothèque de balises !

## Utilisation de la fonctionnalité Bibliothèque de travail

Lorsque vous effectuez de nombreuses modifications dans les balises, il n’est pas pratique d’avoir à accéder à l’onglet Publication, d’ajouter des modifications et de créer la bibliothèque chaque fois que vous souhaitez voir le résultat.  Une fois votre bibliothèque de configuration initiale créée, vous pouvez utiliser la fonctionnalité Bibliothèque de travail pour enregistrer rapidement vos modifications et recréer la bibliothèque en une seule étape.

Apportez un petit changement à la règle « Toutes les pages - Bibliothèque chargée ». Dans le volet de navigation de gauche, cliquez sur **[!UICONTROL Rules]** , puis sur la règle `All Pages - Library Loaded` pour l’ouvrir.

![Réouverture de la règle](images/launch-reopenRule.png)

Sur la page `Edit Rule`, cliquez sur la liste déroulante ***[!UICONTROL Working Library]*** (Bibliothèque de travail) et sélectionnez votre bibliothèque `Initial Setup`.

![Sélection de la bibliothèque Configuration initiale comme bibliothèque de travail](images/launch-setWorkingLibrary.png)

Une fois la bibliothèque sélectionnée, vous devriez constater que le bouton **[!UICONTROL Enregistrer]** est désormais **[!UICONTROL Enregistrer dans la bibliothèque]** par défaut. Lorsque vous effectuez une modification des balises, vous pouvez utiliser cette option pour ajouter automatiquement la modification à votre bibliothèque de travail et/ou la recréer.

Faites le test. Ouvrez votre action Code personnalisé et ajoutez un point-virgule après le texte « Le nom de page est » afin que le bloc de code entier soit :

```javascript
console.log('The page name is: '+_satellite.getVar('Page Name'));
```

Enregistrez le code, conservez les modifications dans l’action, puis cliquez sur le bouton **[!UICONTROL Enregistrer dans la bibliothèque et créer]** .

![L’option Enregistrer et créer existe désormais](images/launch-workingLibrary-saveAndBuild.png)

Patientez jusqu’à ce que le point vert réapparaisse en regard de la liste déroulante [!UICONTROL Bibliothèque de travail]. Maintenant, chargez à nouveau votre page d’exemple. Vous devriez voir votre modification se refléter dans le message de la console (vous devrez peut-être pour cela vider le cache de votre navigateur et le charger à nouveau) :

![Message de la console avec deux points](images/samplepage-consoleWithColon.png)

C’est une façon beaucoup plus rapide de travailler et ce sera la méthode utilisée pour le reste du tutoriel.

[Suite : &quot;Changement d’environnements avec l’Experience Cloud Debugger&quot; >](switch-environments.md)
