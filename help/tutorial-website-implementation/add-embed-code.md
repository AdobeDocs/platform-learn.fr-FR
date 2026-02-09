---
title: Ajouter le code incorporé
description: Découvrez comment obtenir les codes incorporés de votre propriété de balise et les implémenter dans votre site web. Cette leçon fait partie du tutoriel Implémentation d’Experience Cloud dans les sites web .
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 43%

---

# Ajouter le code incorporé

Dans cette leçon, vous allez implémenter le code incorporé asynchrone de l’environnement de développement de votre propriété de balise. Vous découvrirez ainsi deux concepts principaux relatifs aux balises : les environnements et les codes incorporés.


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

* Obtention du code incorporé pour la propriété de balise
* différencier environnement de développement, d’évaluation et de production ;
* Ajout d’un code intégré de balise à un document HTML
* Expliquez l’emplacement optimal du code incorporé de balise par rapport à d’autres codes dans la `<head>` d’un document HTML

## Copie du code intégré

Le code incorporé est une balise `<script>` que vous placez sur vos pages web pour charger et exécuter la logique que vous créez dans les balises. Si vous chargez la bibliothèque de manière asynchrone, le navigateur continue à charger la page, récupère la bibliothèque de balises et l’exécute en parallèle. Dans ce cas, il n’y a qu’un seul code intégré à placer dans l’élément `<head>`. (Lorsque les balises sont déployées de manière synchrone, il existe deux codes incorporés, l’un que vous placez dans le `<head>` et l’autre avant le `</body>`).

Dans l’écran de présentation de la propriété, cliquez sur **[!UICONTROL Environnements]** dans le volet de navigation de gauche pour accéder à la page Environnements. Notez que les environnements de développement, d’évaluation et de production ont déjà été créés pour vous.

![Clic sur Environnements dans la barre de navigation supérieure](images/launch-environments.png)

Les environnements de développement, d’évaluation et de production correspondent aux environnements typiques du processus de développement et de mise à jour du code. Le code est d’abord écrit par un développeur dans un environnement de développement. Lorsqu’ils ont terminé leur travail, les développeurs envoient le code à un environnement d’évaluation où il est révisé par des équipes d’assurance qualité et d’autres équipes. Une fois que les équipes d’assurance qualité et les autres équipes sont satisfaites, le code est publié dans l’environnement de production, qui est l’environnement sur lequel les visiteurs arrivent lorsqu’ils se connectent à votre site web.

Les balises permettent d’ajouter des environnements de développement, ce qui s’avère utile pour les grandes organisations dans lesquelles plusieurs développeurs travaillent sur différents projets en même temps.

Ce sont les seuls environnements nécessaires pour suivre jusqu’au bout ce tutoriel. Les environnements vous permettent de disposer de différentes versions de travail de vos bibliothèques de balises hébergées à différentes URL. Vous pouvez ainsi ajouter en toute sécurité de nouvelles fonctionnalités et les mettre à la disposition des utilisateurs appropriés (par exemple, les développeurs, les ingénieurs en assurance qualité, le public, etc.) au bon moment.

Copions maintenant le code intégré :

1. Dans la ligne **[!UICONTROL Développement]**, cliquez sur l’icône Installer ![icône Installer](images/launch-installIcon.png) pour ouvrir la boîte de dialogue modale.

1. Notez que les balises utilisent par défaut les codes incorporés asynchrones

1. Cliquez sur l’icône Copier ![icône Copier](images/launch-copyIcon.png) pour copier le code intégré dans le presse-papiers.

1. Cliquez sur **[!UICONTROL Fermer]** pour fermer la boîte de dialogue modale.

   ![Icône Installer](images/launch-copyInstallCode.png)

## Mise en œuvre du code intégré dans l’élément `<head>` de la page HTML d’exemple

Le code intégré doit être mis en œuvre dans l’élément `<head>` de toutes les pages HTML qui partageront la propriété. Vous pouvez avoir un ou plusieurs fichiers de modèle qui contrôlent la `<head>` globalement sur le site, ce qui facilite le processus d’ajout de balises.

Si ce n’est pas déjà fait, copiez l’exemple de code de page HTML et collez-le dans un éditeur de code. Si vous en avez besoin, [Brackets](https://brackets.io/) est un éditeur libre et open source.

+++Exemple de code de page HTML

```html
<!doctype html>
<html lang="en">
<head>
    <title>Tags: Sample HTML Page</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags: Sample HTML Page</h1>
    <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
    <p>See <a href="https://docs.adobe.com/content/help/fr-FR/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
</body>
</html>
```

+++

Remplacez le code intégré existant sur la ligne 34, ou autour de celle-ci, par le code du presse-papiers et enregistrez la page. Ouvrez ensuite la page dans un navigateur web. Si vous chargez la page à l’aide du protocole `file://`, vous devez ajouter « https: » au début de l’URL du code intégré dans l’éditeur de code. Les lignes 33 à 36 de votre page d’exemple devraient ressembler à ceci :

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

Ouvrez les outils de développement de votre navigateur web et accédez à l’onglet Réseau. À ce stade, une erreur 404 devrait s’afficher pour l’URL de l’environnement de balises :
Erreur ![404](images/samplepage-404.png)

L’erreur 404 est attendue, car vous n’avez pas encore créé de bibliothèque dans cet environnement Balises. Ce point sera abordé dans la leçon suivante. Si un message d’erreur « fail » s’affiche à la place d’une erreur 404, vous avez probablement oublié d’ajouter le protocole `https://` au code intégré. Là encore, il suffit d’ajouter `https://` si vous chargez la page d’exemple à l’aide du protocole `file://`. Effectuez cette modification et rechargez la page jusqu’à ce que l’erreur 404 s’affiche.

## Bonnes pratiques d’implémentation des balises

Prenons quelques instants pour passer en revue certaines des bonnes pratiques d’implémentation des balises qui sont illustrées dans l’exemple de page :

* **Couche de données** :

   * Nous *vivement* recommandons de créer une couche de données sur votre site contenant tous les attributs nécessaires pour renseigner les variables dans Analytics, Target et d’autres solutions marketing. Cette page d’exemple ne contient qu’une couche de données très simple, mais une véritable couche de données peut contenir beaucoup plus de détails à propos de la page, du visiteur, des informations sur son panier, etc. Pour plus d’informations sur les couches de données, consultez le document [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf).

   * Définissez votre couche de données avant le code incorporé de balise afin d’optimiser l’utilisation des solutions Experience Cloud.

* **Bibliothèques d’assistance JavaScript** : si vous disposez déjà d’une bibliothèque telle que JQuery implémentée dans le `<head>` de vos pages, chargez-la avant les balises afin d’exploiter sa syntaxe dans les balises et Target

* **Doctype HTML5** : Target a besoin du doctype HTML5.

* **preconnect et dns-prefetch** : utilisez preconnect and dns-prefetch pour améliorer le temps de chargement de la page. Voir aussi : [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **fragment de code de masquage préalable pour les implémentations Target asynchrones** : vous en apprendrez plus à ce sujet dans la leçon Target. Cependant, lorsque Target est déployé via des codes incorporés de balises asynchrones, vous devez coder en dur un fragment de code de masquage préalable sur vos pages avant les codes incorporés de balises afin de gérer le scintillement du contenu

Voici un résumé des bonnes pratiques décrites ci-dessus dans l’ordre conseillé. Notez qu’il existe des espaces réservés pour les détails spécifiques au compte :

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
    <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
    <link rel="preconnect" href="//dpm.demdex.net">
    <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//techmarketingdemos.demdex.net">
    <link rel="preconnect" href="//cm.everesttech.net">
    <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
    <link rel="dns-prefetch" href="//dpm.demdex.net">
    <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
    <link rel="dns-prefetch" href="//cm.everesttech.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
    <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
    <!--/Preconnect and DNS-Prefetch-->
    <!--Data Layer to enable rich data collection and targeting-->
    <script>
    var digitalData = {
        "page": {
            "pageInfo" : {
                "pageName": "Home"
                }
            }
    };
    </script>
    <!--/Data Layer-->
    <!--jQuery or other helper libraries-->
    <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
    <!--/jQuery-->
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

Vous savez maintenant comment ajouter le code incorporé de balise à votre site.

[Suite : « Ajouter un élément de données, une règle et une bibliothèque » >](add-data-elements-rules.md)
