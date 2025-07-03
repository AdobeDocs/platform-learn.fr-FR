---
title: Adobe Journey Optimizer - Configuration du parcours et du message
description: Adobe Journey Optimizer - Configuration du parcours et du message
kt: 5342
doc-type: tutorial
exl-id: 687eb818-2d50-4293-88e6-7e5945b91db6
source-git-commit: e3d3b8e3abdea1766594eca53255df024129cb2c
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 4%

---

# 3.2.4 Création de parcours et de messages

Dans cet exercice, vous allez créer un parcours et plusieurs messages texte à l&#39;aide de Adobe Journey Optimizer.

Pour ce cas d’utilisation, l’objectif est d’envoyer différents messages en fonction des conditions météorologiques de l’emplacement de votre client. 3 scénarios ont été définis :

- Plus froid que 10 °C
- Entre 10 et 25 °C
- Plus chaud que 25 °C

Pour ces 3 conditions, vous devez définir 3 messages dans Adobe Journey Optimizer.

## 3.2.4.1 Créer votre parcours

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Dans le menu de gauche, accédez à **Parcours** puis cliquez sur **Créer un Parcours** pour commencer à créer votre Parcours.

![Démonstration](./images/jocreate.png)

Vous devriez donner un prénom à votre parcours.

Comme nom pour le parcours, utilisez `--aepUserLdap-- - Geofence Entry Journey`. Aucune autre valeur ne doit être définie pour le moment. Cliquez sur **Enregistrer**.

![Démonstration](./images/joname.png)

Sur le côté gauche de l’écran, regardez **Événements**. Vous devriez voir votre événement créé précédemment dans cette liste, qui est nommée `--aepUserLdap--GeofenceEntry`. Sélectionnez-la, puis faites-la glisser et déposez-la sur la zone de travail du parcours. Votre parcours ressemble alors à ceci.

![Démonstration](./images/joevents.png)

Cliquez ensuite sur **Orchestration**. Les fonctionnalités **Orchestration** disponibles s’affichent à présent. Sélectionnez **Condition**, puis faites-la glisser et déposez-la sur la zone de travail du Parcours.

![Démonstration](./images/jo2.png)

Vous devez maintenant configurer trois chemins pour cette condition :

- Il fait plus froid que 10° Celsius
- C&#39;est entre 10 et 25 degrés Celsius
- Il fait plus chaud que 25 degrés Celsius

Définissons la première condition.

### Condition 1 : plus froid que 10 °C

Cliquez sur la **Condition**.  Cliquez sur **Path1** et modifiez le nom du chemin en **Plus froid que 10 C**. Cliquez sur l’icône **Modifier** pour l’expression de Path1.

![Démonstration](./images/jo5.png)

Un écran **Éditeur simple** vide s’affiche alors. Votre requête sera un peu plus avancée, vous aurez donc besoin du **Mode avancé**. Cliquez sur **Mode avancé**.

![Démonstration](./images/jo7.png)

Vous verrez ensuite l’**Éditeur avancé** qui permet la saisie de code.

![Démonstration](./images/jo9.png)

Sélectionnez le code ci-dessous et collez-le dans l’**Éditeur avancé**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 10`

Tu verras ça.

![Démonstration](./images/jo10.png)

Pour récupérer la température dans le cadre de cette condition, vous devez indiquer la ville dans laquelle se trouve actuellement le client.
Le **City** doit être lié au `q` de paramètres dynamique, comme vous l’avez vu précédemment dans la documentation de l’API Open Weather.

Cliquez sur le champ **val dynamique : q** comme indiqué dans la capture d’écran.

![Démonstration](./images/jo11.png)

Vous devez ensuite trouver le champ qui contient la ville actuelle du client dans l’une des sources de données disponibles. Dans ce cas, vous devez le trouver sous **Contexte**.

![Démonstration](./images/jo12.png)

Vous pouvez trouver le champ en accédant à `--aepUserLdap--GeofenceEntry.placeContext.geo.city`.

En cliquant sur ce champ ou sur **+**, il sera ajouté comme valeur dynamique pour le paramètre `q`. Ce champ est renseigné, par exemple, par le service de géolocalisation que vous avez implémenté dans votre application mobile. Dans ce cas, vous allez simuler cette opération à l’aide de la propriété de collecte de données du site web de démonstration. Cliquez sur **OK**.

![Démonstration](./images/jo13.png)

### Condition 2 : entre 10° et 25° Celsius

Après avoir ajouté la première condition, vous verrez cet écran. Cliquez sur **Ajouter un chemin**.

![Démonstration](./images/joc2.png)

Double-cliquez sur **Chemin1** et modifiez le nom du chemin en **Entre 10 et 25 C**. Cliquez sur l’icône **Modifier** correspondant à l’expression de ce chemin d’accès.

![Démonstration](./images/joc6.png)

Un écran **Éditeur simple** vide s’affiche alors. Votre requête sera un peu plus avancée, vous aurez donc besoin du **Mode avancé**. Cliquez sur **Mode avancé**.

![Démonstration](./images/jo7.png)

Vous verrez ensuite l’**Éditeur avancé** qui permet la saisie de code.

![Démonstration](./images/jo9.png)

Sélectionnez le code ci-dessous et collez-le dans l’**Éditeur avancé**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 10 and #{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} <= 25`

Tu verras ça.

![Démonstration](./images/joc10.png)

Pour récupérer la température dans le cadre de cette condition, vous devez indiquer la ville dans laquelle se trouve actuellement le client.
Le paramètre **City** doit être lié au paramètre dynamique **q**, comme vous l’avez vu précédemment dans la documentation de l’API Open Weather.

Cliquez sur le champ **val dynamique : q** comme indiqué dans la capture d’écran.

![Démonstration](./images/joc11.png)

Vous devez ensuite trouver le champ qui contient la ville actuelle du client dans l’une des sources de données disponibles.

![Démonstration](./images/jo12.png)

Vous pouvez trouver le champ en accédant à `--aepUserLdap--GeofenceEntry.placeContext.geo.city`. En cliquant sur ce champ, il est ajouté comme valeur dynamique pour le paramètre **q**. Ce champ est renseigné, par exemple, par le service de géolocalisation que vous avez implémenté dans votre application mobile. Dans ce cas, vous allez simuler cette opération à l’aide de la propriété de collecte de données du site web de démonstration. Cliquez sur **OK**.

![Démonstration](./images/jo13.png)

Ensuite, vous allez ajouter la troisième condition.

### Condition 3 : plus chaud que 25 °C

Après avoir ajouté la deuxième condition, vous verrez cet écran. Cliquez sur **Ajouter un chemin**.

![Démonstration](./images/joct2.png)

Double-cliquez sur Path1 pour remplacer le nom par **Plus chaud que 25 C**.
Cliquez ensuite sur l’icône **Modifier** correspondant à l’expression de ce chemin d’accès.

![Démonstration](./images/joct6.png)

Un écran **Éditeur simple** vide s’affiche alors. Votre requête sera un peu plus avancée, vous aurez donc besoin du **Mode avancé**. Cliquez sur **Mode avancé**.

![Démonstration](./images/jo7.png)

Vous verrez ensuite l’**Éditeur avancé** qui permet la saisie de code.

![Démonstration](./images/jo9.png)

Sélectionnez le code ci-dessous et collez-le dans l’**Éditeur avancé**.

`#{--aepUserLdap--WeatherApi.--aepUserLdap--WeatherByCity.main.temp} > 25`

Tu verras ça.

![Démonstration](./images/joct10.png)

Pour récupérer la température dans le cadre de cette condition, vous devez indiquer la ville dans laquelle se trouve actuellement le client.
Le paramètre **City** doit être lié au paramètre dynamique **q**, comme vous l’avez vu précédemment dans la documentation de l’API Open Weather.

Cliquez sur le champ **val dynamique : q** comme indiqué dans la capture d’écran.

![Démonstration](./images/joct11.png)

Vous devez ensuite trouver le champ qui contient la ville actuelle du client dans l’une des sources de données disponibles.

![Démonstration](./images/jo12.png)

Vous pouvez trouver le champ en accédant à ```--aepUserLdap--GeofenceEntry.placeContext.geo.city```. En cliquant sur ce champ, il est ajouté comme valeur dynamique pour le paramètre **q**. Ce champ est renseigné, par exemple, par le service de géolocalisation que vous avez implémenté dans votre application mobile. Dans ce cas, vous allez simuler cette opération à l’aide de la propriété de collecte de données du site web de démonstration. Cliquez sur **OK**.

![Démonstration](./images/jo13.png)

Vous disposez désormais de trois chemins configurés. Cliquez sur **Enregistrer**.

![Démonstration](./images/jo3path.png)

Comme il s’agit d’un parcours à des fins d’apprentissage, vous allez maintenant configurer quelques actions pour présenter la variété des options dont disposent désormais les professionnels du marketing pour diffuser des messages.

## 3.2.4.2 Envoyer des messages pour le chemin : moins de 10° Celsius

Pour chacun des contextes de température, vous tenterez d&#39;envoyer un message texte à un client. Pour cet exercice, vous allez envoyer un message réel à un canal Slack plutôt qu’à un numéro de téléphone mobile.

Concentrons-nous sur le chemin **plus froid que 10°C**.

![Démonstration](./images/p1steps.png)

Dans le menu de gauche, revenez à **Actions**, sélectionnez l’`--aepUserLdap--TextSlack` Action, puis faites-la glisser après l’action **Message**.

![Démonstration](./images/joa18.png)

Faites défiler jusqu’à **Paramètres de requête** et cliquez sur l’icône **Modifier** pour le `textToSlack` de paramètre.

![Démonstration](./images/joa19.png)

Dans la fenêtre contextuelle, cliquez sur **Mode avancé**.

![Démonstration](./images/joa20.png)

Sélectionnez le code ci-dessous, copiez-le et collez-le dans l’**Éditeur de mode avancé**. Cliquez sur **OK**.

`"Brrrr..." + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + ",  it's cold and freezing outside. Get comfortable at home with a 20% discount on a Disney+ subscription!"`

![Démonstration](./images/joa21.png)

L’action terminée s’affiche. Faites défiler vers le haut et cliquez sur **Enregistrer**.

![Démonstration](./images/joa22.png)

Ce chemin d’accès du parcours est maintenant prêt.

## 3.2.4.3 Envoyer des messages pour le chemin : entre 10° et 25° Celsius

Pour chacun des contextes de température, vous tenterez d&#39;envoyer un message à votre client. Pour cet exercice, vous allez envoyer un message réel à un canal Slack plutôt qu’à un numéro de téléphone mobile.

Concentrons-nous sur le chemin **entre 10 et 25 C**.

![Démonstration](./images/p2steps.png)

Dans le menu de gauche, revenez à **Actions**, sélectionnez l’`--aepUserLdap--TextSlack` Action, puis faites-la glisser après l’action **Message**.

![Démonstration](./images/jop18.png)

Faites défiler jusqu’à **Paramètres de requête** et cliquez sur l’icône **Modifier** pour le `textToSlack` de paramètre.

![Démonstration](./images/joa19z.png)

Dans la fenêtre contextuelle, cliquez sur **Mode avancé**.

![Démonstration](./images/joa20.png)

Sélectionnez le code ci-dessous, copiez-le et collez-le dans l’**Éditeur de mode avancé**. Cliquez sur **OK**.

`"What nice weather for the time of year, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + " 20% discount on Apple AirPods so you can go for a walk and listen to your favorite podcast!"`

![Démonstration](./images/jop21.png)

L’action terminée s’affiche. Faites défiler vers le haut et cliquez sur **Enregistrer**.

![Démonstration](./images/jop22.png)

Ce chemin d’accès du parcours est maintenant prêt.

## 3.2.4.4 Envoyer des messages pour le chemin : plus chaud que 25° Celsius

Pour chacun des contextes de température, vous tenterez d&#39;envoyer un message à votre client. Pour cet exercice, vous allez envoyer un message réel à un canal Slack plutôt qu’à un numéro de téléphone mobile.

Concentrons-nous sur le chemin **plus chaud que 25 C**.

![Démonstration](./images/p3steps.png)

Dans le menu de gauche, revenez à **Actions**, sélectionnez l’`--aepUserLdap--TextSlack` Action, puis faites-la glisser après l’action **Messages**.

![Démonstration](./images/jod18.png)

Faites défiler jusqu’à **Paramètres de requête** et cliquez sur l’icône **Modifier** pour le `textToSlack` de paramètre.

![Démonstration](./images/joa19zzz.png)

Dans la fenêtre contextuelle, cliquez sur **Mode avancé**.

![Démonstration](./images/joa20.png)

Sélectionnez le code ci-dessous, copiez-le et collez-le dans l’**Éditeur de mode avancé**. Cliquez sur **OK**.

`"So warm, " + #{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName} + "! 20% discount on adding 10GB of extra data so you can get online at the beach!"`

![Démonstration](./images/jod21.png)

L’action terminée s’affiche. Cliquez sur **Enregistrer**.

![Démonstration](./images/jod22.png)

Ce chemin d’accès du parcours est maintenant prêt.

## 3.2.4.5 Publier votre parcours

Votre parcours est maintenant entièrement configuré. Cliquez sur **Publier**.

![Démonstration](./images/jodone.png)

Cliquez de nouveau sur **Publier**.

![Démonstration](./images/jopublish1.png)

Votre parcours est maintenant publié.

![Démonstration](./images/jopublish2.png)

## Étapes suivantes

Accédez à [3.2.5 Déclencher votre parcours ](./ex5.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : sources de données externes et actions personnalisées](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
