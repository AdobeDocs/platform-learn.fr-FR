---
title: Prétravail
description: Prétravail
doc-type: multipage-overview
source-git-commit: 7b76e7714d2a390d84393ce21a19063b56508ac1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Les instructions ci-dessous sont destinées uniquement aux employés Adobes.

## Installer PostBuster

Accédez à [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Cliquez pour télécharger la dernière version de **PostBuster**.

![PostBuster](./assets/images/pb1.png)

Téléchargez la version adaptée à votre système d’exploitation.

![PostBuster](./assets/images/pb2.png)

Une fois le téléchargement terminé et installé, ouvrez PostBuster. Vous devriez alors voir ceci. Cliquez sur **Importer**.

![PostBuster](./assets/images/pb3.png)

Téléchargez [postbuster.json.zip](./assets/postman/postbuster.json.zip) et extrayez-le sur votre bureau.

![PostBuster](./assets/images/pbpb.png)

Cliquez sur **Choisir un fichier**.

![PostBuster](./assets/images/pb4.png)

Sélectionnez le fichier **postbuster.json**. Cliquez sur **Ouvrir**.

![PostBuster](./assets/images/pb5.png)

Vous devriez alors voir ceci. Cliquez sur **Scan**.

![PostBuster](./assets/images/pb6.png)

Cliquez sur **Importer**.

![PostBuster](./assets/images/pb7.png)

Vous devriez alors voir ceci. Cliquez pour ouvrir la collection importée.

![PostBuster](./assets/images/pb8.png)

Maintenant, vous voyez votre collection. Vous devez toujours configurer un environnement pour contenir certaines variables d’environnement.

![PostBuster](./assets/images/pb9.png)

Cliquez sur **Environnement de base** puis sur l’icône **Modifier**.

![PostBuster](./assets/images/pb10.png)

Vous devriez alors voir ceci.

![PostBuster](./assets/images/pb11.png)

Copiez l’espace réservé d’environnement ci-dessous et collez-le dans l’**Environnement de base**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

Tu devrais avoir ça.

![PostBuster](./assets/images/pb12.png)

Après avoir parcouru le module **Services de Firefly**, votre environnement doit ressembler à ceci. Vous n’avez pas besoin de le faire maintenant, nous y reviendrons plus tard.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./overview.md)
