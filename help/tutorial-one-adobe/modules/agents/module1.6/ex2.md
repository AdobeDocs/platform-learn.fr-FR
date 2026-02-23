---
title: Serveurs et curseur AEM MCP
description: Serveurs et curseur AEM MCP
kt: 5342
doc-type: tutorial
source-git-commit: 1abfd8d1f270a810dd65d9921c69834df2a9147d
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 1%

---

# 1.6.2 Serveurs et curseur AEM MCP

>[!IMPORTANT]
>
>Pour réaliser cet exercice, vous devez avoir accès à un environnement AEM Sites et Assets CS avec services de développement intégré (EDS) fonctionnel, et les différents agents AEM doivent être activés pour l’organisation IMS que vous utilisez.
>
>Si vous ne disposez pas encore d’un tel environnement, passez à l’exercice [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Sites et Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.


Voici tous les serveurs AEM MCP disponibles :

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly (opérations de contenu en lecture seule)
- https://mcp.adobeaemcloud.com/adobe/mcp/content-updater (expose les compétences correspondantes depuis l’agent de production Experience)
- https://mcp.adobeaemcloud.com/adobe/mcp/experience-governance (Expose les compétences pour obtenir et vérifier la politique de marque d’une page)
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery (Expose les compétences pour découvrir du contenu dans un environnement AEM)

Dans cet exercice, vous trouverez des instructions sur l’utilisation de ces serveurs MCP spécifiques :

- https://mcp.adobeaemcloud.com/adobe/mcp/content
- https://mcp.adobeaemcloud.com/adobe/mcp/discovery

Vous pouvez utiliser les instructions ci-dessous pour configurer des serveurs MCP similaires pour les autres serveurs MCP AEM disponibles, car le processus est très similaire.

## Configuration du serveur MCP du curseur de l’agent de production 1.6.2.1 Experience

Créez un dossier vide sur votre bureau.

![Curseur + AEM](./images/cursorai1.png)

Ouvrez le curseur. Cliquez sur **Ouvrir le projet**.

![Curseur + AEM](./images/cursorai2.png)

Sélectionnez le dossier que vous avez créé précédemment et cliquez sur **Ouvrir**.

![Curseur + AEM](./images/cursorai3.png)

Cliquez sur **Oui, je fais confiance aux auteurs**.

![Curseur + AEM](./images/cursorai4.png)

Vous devriez alors voir ceci. Utilisez le raccourci clavier `Cmd + Shift + J` pour ouvrir les paramètres du curseur. Vous devriez alors voir ceci. Accédez à **Outils et MCP**.

![Curseur + AEM](./images/cursorai5.png)

Cliquez sur **+ Nouveau serveur MCP**.

![Curseur + AEM](./images/cursorai6.png)

Ajoutez le serveur MCP suivant au fichier **mcp.json**. D&#39;autres serveurs MCP sont peut-être déjà spécifiés dans ce fichier. Ne les supprimez pas et ajoutez simplement les nouvelles lignes ci-dessous. Enregistrez vos modifications.

```json
"aem": {
	"url": "https://mcp.adobeaemcloud.com/adobe/mcp/content"
	}
```

![Curseur + AEM](./images/cursorai7.png)

Revenez à l’onglet **Paramètres du curseur**. Vous devriez maintenant voir un outil appelé **aem** ajouté à la liste des serveurs MCP. Cliquez sur **se connecter** pour vous authentifier à l’aide de votre compte Adobe.

![Curseur + AEM](./images/cursorai8.png)

Cliquez sur **Ouvrir** au cas où ce message s’afficherait. Vous devez ensuite vous authentifier dans votre navigateur.

![Curseur + AEM](./images/cursorai9.png)

Une fois l’authentification réussie, vous devriez voir un élément similaire à ceci.

![Curseur + AEM](./images/cursorai10.png)

Fermez les onglets **Cursor Settings** et **mcp.json**. Collez l’invite suivante dans la conversation et cliquez sur **envoyer**.

```
I just created a new custom mcp server named 'aem'. what can I do with that?
```

![Curseur + AEM](./images/cursorai11.png)

Cliquez sur **Exécuter**.

![Curseur + AEM](./images/cursorai12.png)

Vous devriez alors voir une réponse similaire.

![Curseur + AEM](./images/cursorai13.png)

![Curseur + AEM](./images/cursorai14.png)

Comme vous pouvez le constater, des fonctionnalités similaires sont exposées via le serveur MCP dans Cursor par rapport à ce qui était possible à l’aide de l’assistant AI dans l’exercice précédent.

Saisissez l’invite suivante et cliquez sur **Envoyer**.

```javascript
List AEM Author instances
```

![Curseur + AEM](./images/cursorai15.png)

Vous devriez alors voir quelque chose comme ça. Recherchez l’environnement à utiliser, puis saisissez l’invite suivante et cliquez sur **Envoyer**.

```javascript
use environment number X
```

![Curseur + AEM](./images/cursorai16.png)

Vous devriez alors voir ceci.

![Curseur + AEM](./images/cursorai17.png)

Collez l’invite suivante et cliquez sur **envoyer**. Remplacez XXX dans cette invite par l’URL que vous avez copiée dans l’exercice précédent.

```
On the page https://author-p185022-e1936676.adobeaemcloud.com/content/CitiSignal/fiber-max.html, please make the following changes:

- change the word 'winter' to 'summer'
- change the text 'be as fast as a leopard' to 'dominate your internet like a gorilla'
- change the image in the hero block to use the image 'citisignal_gorilla.png'
- change the text '99.9% network reliability' to '99.998% network reliability'
```

![Curseur + AEM](./images/cursorai18.png)

Après 1-2 minutes, vous devriez obtenir une réponse similaire. Copiez l’URL et ouvrez la page dans votre navigateur.

![Curseur + AEM](./images/cursorai19.png)

Vous devriez alors voir ceci.

![Curseur + AEM](./images/cursorai20.png)

Saisissez l’invite suivante et cliquez sur **Envoyer**.

```javascript
promote the changes by creating a new launch and promoting it
```

![Curseur + AEM](./images/cursorai21.png)

Après 1 à 2 minutes, les modifications ont été promues.

![Curseur + AEM](./images/cursorai22.png)

Les modifications sont maintenant visibles en direct sur votre site web.

![Curseur + AEM](./images/cursorai23.png)

N’hésitez pas à découvrir les autres fonctionnalités du serveur MCP AEM.

## Configuration du serveur MCP du curseur de l&#39;agent Discovery 1.6.2.2

Utilisez le raccourci clavier `Cmd + Shift + J` pour ouvrir les paramètres du curseur. Vous devriez alors voir ceci. Accédez à **Outils et MCP**. Cliquez sur **+ Nouveau serveur MCP**.

![Curseur + AEM](./images/cursoraiz5.png)

Ajoutez le serveur MCP suivant au fichier **mcp.json**. D&#39;autres serveurs MCP sont peut-être déjà spécifiés dans ce fichier. Ne les supprimez pas et ajoutez simplement les nouvelles lignes ci-dessous. Enregistrez vos modifications.

```
,
"aem-discovery": {
	"url": "https://mcp.adobeaemcloud.com/adobe/mcp/discovery"
}
```

![Curseur + AEM](./images/cursoraiz7.png)

Revenez à l’onglet **Paramètres du curseur**. Vous devriez maintenant voir un outil appelé **aem** ajouté à la liste des serveurs MCP. Cliquez sur **se connecter** pour vous authentifier à l’aide de votre compte Adobe.

![Curseur + AEM](./images/cursoraiz8.png)

Après l’authentification, vous devriez voir ceci.

![Curseur + AEM](./images/cursoraiz9.png)

Fermez les onglets **Cursor Settings** et **mcp.json**. Collez l’invite suivante dans la conversation et cliquez sur **envoyer**.

```
I just created a new custom mcp server named 'aem-discovery'. what can I do with that?
```

![Curseur + AEM](./images/cursoraiz10.png)

```
for the environment https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/, list all assets tagged with 'Spring 2026'
```

![Curseur + AEM](./images/cursoraiz11.png)

Vous devriez alors voir quelque chose comme ça.

![Curseur + AEM](./images/cursoraiz12.png)

## Étapes suivantes

Revenir à [AEM et agents](./aemagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}