---
title: Remplacement de la bibliothèque - Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment migrer une mise en oeuvre Adobe Target d’at.js 2.x vers le SDK Web Adobe Experience Platform. Les rubriques incluent un aperçu de la bibliothèque, des différences de mise en oeuvre et d’autres légendes dignes d’intérêt.
exl-id: dfafa132-376a-475d-a467-9bc2f0a414cf
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 3%

---

# Remplacement de la bibliothèque at.js par le SDK Web Platform

Découvrez comment remplacer votre implémentation Adobe Target sur la page pour migrer d’at.js vers le SDK Web Platform. Un remplacement de base comprend les étapes suivantes :

* Vérifiez vos paramètres d’administration Target et notez votre identifiant de l’organisation IMS.
* Remplacez la bibliothèque at.js par le SDK Web Platform.
* Mise à jour du fragment de code de masquage préalable pour les implémentations de bibliothèques synchrones
* Configuration du SDK Web de Platform

>[!NOTE]
>
>Les exemples fournis sont fournis à titre d’illustration et votre mise en oeuvre réelle de Target peut varier. Si votre mise en oeuvre Target existante utilise le gestionnaire de balises de collecte de données d’Adobe, vous pouvez également vous reporter au [tutoriel de mise en oeuvre du SDK Web Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=fr) pour plus d’informations.


## Vérification des paramètres d’administration de Target

La première étape de la migration de Target vers le SDK Web Platform consiste à passer en revue vos paramètres dans la section **[!UICONTROL Administration]** de l’interface Target.

### [!UICONTROL Mise en œuvre]

#### [!UICONTROL Détails du compte]

* **[!UICONTROL Identifiant de l’organisation IMS]** - Notez cette valeur, car elle est requise pour configurer le SDK Web Platform.
* **[!UICONTROL Prise de décision sur l’appareil]** - Cette fonctionnalité n’est pas prise en charge par le SDK Web Platform. Ce paramètre peut être désactivé après la migration et si vous n’utilisez plus at.js sur l’un de vos sites web ou si vous avez des cas d’utilisation côté serveur pour la prise de décision sur le périphérique.

#### [!UICONTROL Méthodes de mise en œuvre]

Tous les paramètres modifiables de la section **[!UICONTROL Méthodes d’implémentation]** s’appliquent uniquement à at.js. Ces paramètres sont utilisés pour générer une bibliothèque at.js personnalisée pour votre implémentation. Vérifiez ces paramètres pour vérifier si vous disposez d’un code personnalisé ou si vous définissez des cookies propriétaires et tiers pour des cas d’utilisation inter-domaines.

Le paramètre **[!UICONTROL Durée de vie du profil]** ne peut être modifié que par l’assistance clientèle d’Adobe. La durée de vie du profil du visiteur Target n’est pas affectée par votre approche de mise en oeuvre. at.js et le SDK Web Platform utilisent la même durée de vie de profil du visiteur.

#### [!UICONTROL Confidentialité]

* **[!UICONTROL Obscurcir les adresses IP des visiteurs]** - Ce paramètre a un impact sur les fonctionnalités de géociblage. at.js et le SDK Web Platform utilisent les mêmes paramètres d’obscurcissement d’IP du serveur principal à des fins de géociblage.

### [!UICONTROL Environnements]

Le SDK Web Platform utilise une configuration de flux de données qui vous permet de définir explicitement un [!UICONTROL ID d’environnement] pour les flux de données de développement, d’évaluation et de production distincts. Le principal cas d’utilisation de cette configuration concerne les mises en oeuvre d’applications mobiles pour lesquelles les URL n’existent pas afin de distinguer facilement les environnements. Le paramètre est facultatif, mais peut être utilisé pour s’assurer que toutes les requêtes sont correctement associées à l’environnement spécifié. Cela diffère d’une implémentation d’at.js dans laquelle vous devez affecter des environnements Target en fonction des domaines et des règles du groupe d’hôtes.

>[!NOTE]
>
>Si aucun ID d’environnement n’est spécifié dans la configuration du flux de données, Target utilise le mappage domaine-environnement comme indiqué dans la section **Hôtes** .

Pour plus d’informations, reportez-vous au guide [configuration du flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html?lang=fr#target) et à la documentation de Target [Hôtes](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=fr).

## Déploiement du SDK Web de Platform

La fonctionnalité Target est fournie par at.js et le SDK Web Platform. Si les deux bibliothèques sont utilisées en même temps, vous pouvez rencontrer des problèmes de rendu et de suivi. Pour réussir la migration vers le SDK Web Platform, la première étape consiste à supprimer at.js et à le remplacer par le SDK Web Platform (alloy.js).

Prenons l’exemple d’une mise en oeuvre simple de Target avec at.js :

* Une couche de données située en haut de la page fournit des informations pour Target et d’autres applications.
* Une ou plusieurs bibliothèques d’assistance tierces dont les fonctionnalités peuvent être utilisées dans des activités Target (jQuery, par exemple)
* Fragment de prémasquage pour atténuer le scintillement
* La bibliothèque at.js de Target se charge de manière asynchrone avec les paramètres par défaut pour demander et générer automatiquement les activités :

+++Exemple d’implémentation d’at.js sur une page d’HTML

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Pour mettre à niveau Target afin d’utiliser le SDK Web Platform, commencez par supprimer at.js :

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

Et remplacez par la bibliothèque JavaScript alliée ou votre code incorporé de balises et l’extension SDK Web Adobe Experience Platform :

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

>[!TAB Balises]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

Dans la propriété tag, ajoutez l’extension SDK Web Adobe Experience Platform :

![Ajout de l’extension Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable="yes"}


>[!ENDTABS]

La version autonome prédéfinie nécessite un &quot;code de base&quot; ajouté directement à la page, qui crée une fonction globale nommée alloy. Utilisez cette fonction pour interagir avec le SDK. Si vous souhaitez donner un autre nom à la fonction globale, modifiez le nom `alloy`.

Pour plus d’informations et d’options de déploiement, reportez-vous à la documentation [Installation du SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=fr) .


## Mise à jour de l’approche de prémasquage du contenu

L’implémentation du SDK Web Platform peut nécessiter un fragment de code de masquage préalable selon que la bibliothèque est chargée de manière asynchrone ou synchrone.

### Mise en oeuvre asynchrone

Tout comme avec at.js, si la bibliothèque SDK Web Platform se charge de manière asynchrone, le rendu de la page peut se terminer avant que Target n’effectue un échange de contenu. Ce comportement peut entraîner un &quot;scintillement&quot;, dans lequel le contenu par défaut s’affiche brièvement avant d’être remplacé par le contenu personnalisé spécifié par Target. Si vous souhaitez éviter ce scintillement, Adobe recommande d’ajouter un fragment de code de masquage préalable spécial juste avant la référence de script SDK Web de Platform asynchrone ou le code intégré des balises.

Si votre mise en oeuvre est asynchrone comme dans les exemples ci-dessus, remplacez le fragment de code de masquage préalable d’at.js par la version ci-dessous compatible avec le SDK Web Platform :

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Le fragment de code de masquage préalable crée une balise de style dans l’en-tête de la page avec la définition CSS de votre choix. Cette balise de style est supprimée lorsqu’une réponse de Target est reçue ou que le délai d’expiration est atteint.

Le comportement de masquage préalable est contrôlé par deux configurations à la fin du fragment de code.

* `body { opacity: 0 !important }` spécifie la définition CSS à utiliser pour le masquage préalable jusqu’au chargement de Target. Par défaut, la page entière est masquée. Vous pouvez mettre à jour cette définition avec les sélecteurs que vous souhaitez pré-masquer, ainsi que la manière dont vous souhaitez les masquer. Vous pouvez inclure plusieurs définitions, car cette valeur est simplement insérée dans la balise de style de masquage préalable. Si vous disposez d’un élément de conteneur facilement identifiable encapsulant le contenu sous votre navigation, vous pouvez utiliser ce paramètre pour limiter le masquage préalable à cet élément de conteneur.

* `3000` spécifie le délai d’expiration en millisecondes pour le masquage préalable. Si aucune réponse de Target n’est reçue avant le délai d’expiration, la balise de style de masquage préalable est supprimée. Il devrait être rare d’atteindre ce délai.

>[!IMPORTANT]
>
>Veillez à utiliser le fragment de code correct pour le SDK Web Platform, car il utilise un autre ID de style `alloy-prehiding`. Si le fragment de code de masquage préalable d’at.js est utilisé, il se peut qu’il ne fonctionne pas correctement.

### Mise en oeuvre synchrone

Adobe recommande de mettre en oeuvre le SDK Web de Platform de manière asynchrone pour optimiser les performances globales de la page. Cependant, si la bibliothèque alloy.js ou le code incorporé des balises est chargé de manière synchrone, le fragment de code de masquage préalable n’est pas requis. Le style de masquage préalable est spécifié dans la configuration du SDK Web Platform.

Le style de prémasquage pour les implémentations synchrones peut être configuré à l’aide de l’option [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr#prehidingStyle) . La configuration du SDK Web Platform est traitée dans la section suivante.

Pour en savoir plus sur la façon dont le SDK Web Platform peut gérer le scintillement, consultez la section du guide : [gestion du scintillement pour les expériences personnalisées](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html?lang=fr)

## Configuration du SDK Web de Platform

Le SDK Web Platform doit être configuré à chaque chargement de page. L’exemple suivant suppose que l’ensemble du site est mis à niveau vers le SDK Web Platform dans le cadre d’un seul déploiement :

>[!BEGINTABS]

>[!TAB JavaScript]

La commande `configure` doit toujours être la première commande de SDK appelée. Le `edgeConfigId` est l’ [!UICONTROL &#x200B; ID de flux de données]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Balises]

Dans les mises en oeuvre de balises, de nombreux champs sont automatiquement renseignés ou peuvent être sélectionnés dans les menus déroulants. Notez que différentes plateformes [!UICONTROL sandbox] et [!UICONTROL datastreams] peuvent être sélectionnées pour chaque environnement. Le flux de données change en fonction de l’état de la bibliothèque de balises dans le processus de publication.

![configuration de l’extension de balise SDK Web](assets/tags-config.png){zoomable="yes"}
>[!ENDTABS]

Si vous prévoyez de migrer page par page d’at.js vers le SDK Web Platform, les options de configuration suivantes sont requises :


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB Balises]

![configuration des options de migration de l’extension de balise SDK Web](assets/tags-config-migration.png){zoomable="yes"}

>[!ENDTABS]

Les options de configuration dignes d’intérêt liées à Target sont décrites ci-dessous :

| Option | Description | Exemple de valeur |
| --- | --- | --- |
| `edgeConfigId` | Identifiant de la banque de données | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | ID d’organisation Adobe Experience Cloud | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Utilisez cette option pour permettre au SDK Web de lire et d’écrire les cookies mbox et mboxEdgeCluster hérités utilisés par at.js. Vous pouvez ainsi conserver le profil du visiteur lors du passage d’une page qui utilise le SDK Web à une page qui utilise la bibliothèque at.js et de la manière opposée. | `true` |
| `idMigrationEnabled` | Si la valeur est true, le SDK lit et définit les anciens cookies AMCV. Cette option permet de passer à l’utilisation du SDK Web Platform, tandis que certaines parties du site peuvent toujours utiliser Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Active le paramètre des cookies tiers Adobe. Le SDK peut conserver l’identifiant visiteur dans un contexte tiers afin de permettre l’utilisation du même identifiant visiteur sur plusieurs sites. Utilisez cette option si vous disposez de plusieurs sites. Toutefois, cette option n’est parfois pas souhaitée pour des raisons de confidentialité. | `true` |
| `prehidingStyle` | Permet de créer une définition de style CSS qui masque les zones de contenu de votre page web pendant le chargement du contenu personnalisé à partir du serveur. Il n’est utilisé qu’avec les déploiements synchrones du SDK. | `body { opacity: 0 !important }` |

Pour obtenir la liste complète des options, reportez-vous au guide [Configuration du SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=fr) .

## Exemple d’implémentation

Une fois que le SDK Web Platform est correctement en place, la page d’exemple ressemble à ceci.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB Balises]

Code de page :

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

Dans les balises, ajoutez l’extension SDK Web Adobe Experience Platform :

![Ajout de l’extension Adobe Experience Platform Web SDK](assets/library-tags-addExtension.png){zoomable="yes"}

Ajoutez ensuite les configurations souhaitées :
![configuration des options de migration de l’extension de balise SDK Web](assets/tags-config-migration.png){zoomable="yes"}


>[!ENDTABS]



Il est important de noter que l’inclusion et la configuration simples de la bibliothèque SDK Web Platform comme illustré ci-dessus n’exécutent aucun appel réseau au réseau Adobe Edge.

Ensuite, découvrez comment [demander et appliquer des activités basées sur le VEC](render-vec-activities.md) à la page.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
