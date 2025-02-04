---
title: PostBuster - Adobe Employés
description: PostBuster - Adobe Employés
doc-type: multipage-overview
exl-id: a798e9d7-bb99-4390-885f-5fbd2ef4cee9
source-git-commit: 9c1b30dc0fcca6b4324ec7c8158699fa273cdc90
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Les instructions ci-dessous sont destinées uniquement aux employés Adobes.

>[!IMPORTANT]
>
>En suivant les instructions ci-dessous, vous disposerez déjà de toutes les collections d’API requises qui seront utilisées dans ces exercices :
>
>- [2.1.3 Visualiser votre propre profil client en temps réel - API](./modules/rtcdp-b2c/module2.1/ex3.md)
>- [2.3.6 Destinations SDK](./modules/rtcdp-b2c/module2.3/ex6.md)
>- [3.3.6 Tester votre décision à l’aide de l’API ](./modules/ajo-b2c/module3.3/ex6.md)
>- [5.1.8 API Query Service](./modules/datadistiller/module5.1/ex8.md)

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

Sélectionnez le fichier **aep_tutorial.json**. Cliquez sur **Ouvrir**.

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
		"read_organizations",
		"additional_info.projectedProductContext",
		"session",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"QS_QUERY_ID": "",
	"SANDBOX_NAME": ""
}
```

Tu devrais avoir ça.

![PostBuster](./assets/images/pb12.png)

Après avoir créé votre projet d’E/S d’Adobe, votre environnement doit se présenter comme suit : Vous n’avez pas besoin de le faire maintenant, nous y reviendrons plus tard.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./overview.md)
