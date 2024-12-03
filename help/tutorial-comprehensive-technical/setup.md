---
title: Configuration
description: Configuration de votre instance AEP
doc-type: multipage-overview
hide: false
source-git-commit: c0649aeacdce00e09c993f2130de3423efc352fa
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 5%

---

# Configuration

>[!IMPORTANT]
>
>Cette page est destinée uniquement aux rôles d’administrateur système. Vous avez besoin des droits d’accès Administrateur système pour que votre instance spécifique puisse suivre les étapes ci-dessous. Si vous n’êtes pas administrateur système de votre organisation Adobe Experience Cloud, contactez votre administrateur système et demandez-lui d’approuver et d’aider avant de passer à l’une des étapes ci-dessous.

## Vue d’ensemble

Pour mettre en pratique tous ces tutoriels, les applications Adobe Experience Cloud suivantes doivent être configurées dans votre organisation IMS :

- Adobe de la plateforme CDP en temps réel
- Collecte de données dʼAdobe Experience Platform
- Adobe Journey Optimizer
- Customer Journey Analytics
- Data Distiller
- Composition d’audiences fédérées

Si un service d’application spécifique n’est pas configuré pour votre organisation IMS, vous ne pourrez pas effectuer cet exercice pratique.

## Créer un environnement de test

Pour passer en revue le tutoriel dans votre propre instance AEP, il est conseillé de commencer par configurer un nouvel environnement de test de développement. Pour créer un nouvel environnement de test, accédez à [https://experience.adobe.com/platform](https://experience.adobe.com/platform), aux environnements de test, puis à **Parcourir**. Cliquez sur **Créer un environnement de test**.

![Créer un environnement de test](./assets/images/sandbox1.png)

Créez votre environnement de test comme suit :

- Type : **Développement**
- Nom : **aep-tutorial**
- Titre : **Tutoriel AEP**

Cliquez sur **Créer**.

![Créer un environnement de test](./assets/images/sandbox2.png)

Votre environnement de test va maintenant être créé. Au bout de quelques minutes, vous verrez ceci.

![Créer un environnement de test](./assets/images/sandbox3.png)

## Configuration des autorisations

Accédez à **Permissions**, puis à **Roles**.

Cliquez pour ouvrir le **rôle** spécifique qui sera utilisé par les apprenants qui suivront ce tutoriel. Cliquez sur **Créer un rôle**.

![Créer un environnement de test](./assets/images/perm1.png)

Donnez un nom à votre rôle, par exemple **Tutoriel AEP**, cliquez sur **Confirmer**.

![Créer un environnement de test](./assets/images/perm2.png)

Dans le menu déroulant **Sandbox**, sélectionnez l’environnement de test que vous venez de créer et assurez-vous de supprimer tout autre environnement de test (supprimez également **Prod**).

![Créer un environnement de test](./assets/images/perm3.png)

Ajoutez les différentes ressources et définissez les autorisations. Veillez à ne pas ajouter d’autorisations pour **Sandbox Administration**.

![Créer un environnement de test](./assets/images/perm4.png)

Ajoutez d’autres ressources comme indiqué et définissez les autorisations.

![Créer un environnement de test](./assets/images/perm5.png)

Ajoutez d’autres ressources comme indiqué et définissez les autorisations. Cliquez sur **Enregistrer**. Cliquez ensuite sur **Fermer**.

![Créer un environnement de test](./assets/images/perm6.png)

## Configuration de l’Adobe I/O

Accédez à
[https://developer.adobe.com/console/integrations](https://developer.adobe.com/console/integrations). Vérifiez que vous vous trouvez dans la bonne instance. Cliquez sur **Créer un projet**.

![Créer un environnement de test](./assets/images/io1.png)

Cliquez sur **+ Ajouter au projet**, puis sur **API**.

![Créer un environnement de test](./assets/images/io2.png)

Cliquez sur **Adobe Experience Platform**, puis activez **API Experience Platform**. Cliquez sur **Suivant**.

![Créer un environnement de test](./assets/images/io3.png)

Pour le **nom d’identification**, utilisez le **tutoriel DSN AEP**. Cliquez sur **Suivant**.

![Créer un environnement de test](./assets/images/io4.png)

Sélectionnez l’un des profils de produit disponibles. Ce profil de produit ne détermine pas les autorisations pour ce projet d’Adobe I/O. Cette opération sera effectuée à l’étape suivante. Cliquez sur **Enregistrer l’API configurée**.

![Créer un environnement de test](./assets/images/io5.png)

Cliquez sur **+ Ajouter au projet**, puis de nouveau sur **API**.

![Créer un environnement de test](./assets/images/io6.png)

Cliquez sur **Adobe Experience Platform**, puis activez **API Experience Platform Launch**. Cliquez sur **Suivant**.

![Créer un environnement de test](./assets/images/io7.png)

Cliquez sur **Suivant**.

![Créer un environnement de test](./assets/images/io8.png)

Sélectionnez un profil de produit qui permet de créer et de gérer des propriétés de collecte de données. Cliquez sur **Enregistrer l’API configurée**.

![Créer un environnement de test](./assets/images/io9.png)

Vous verrez alors ceci. Cliquez sur le nom actuel du **Projet XXX**.

![Créer un environnement de test](./assets/images/io10.png)

Cliquez sur **Modifier le projet**.

![Créer un environnement de test](./assets/images/io11.png)

Saisissez un nouveau **Titre du projet**, tel que **Tutoriel AEP DSN**. Cliquez sur **Enregistrer**.

![Créer un environnement de test](./assets/images/io12.png)

Votre projet d’Adobe I/O est maintenant prêt.

## Lier le projet Adobe I/O au rôle

Accédez à **Permissions**, à **Roles**, puis cliquez sur le nouveau rôle que vous avez créé précédemment.

![Créer un environnement de test](./assets/images/role1.png)

Accédez à **Informations d’identification de l’API**. Cliquez sur **+ Ajouter les informations d’identification d’API**.

![Créer un environnement de test](./assets/images/role2.png)

Vous verrez ensuite les informations d’identification d’Adobe I/O que vous avez créées à l’étape précédente. Sélectionnez-le et cliquez sur **Enregistrer**.

![Créer un environnement de test](./assets/images/role3.png)

Votre projet Adobe I/O est maintenant configuré avec les autorisations requises pour accéder aux API Adobe Experience Platform.

![Créer un environnement de test](./assets/images/role4.png)

>[!IMPORTANT]
>
>Vous devez attendre au moins 10 minutes avant de poursuivre les étapes suivantes dans Demo System Next.

## Configuration de votre environnement dans Demo System Next

Accédez à [https://dsn.adobe.com/tools/org-admin](https://dsn.adobe.com/tools/org-admin). Cliquez sur **+ Ajouter une organisation**.

![Créer un environnement de test](./assets/images/dsnorg1.png)

Renseignez les champs requis :

- Identifiant de l’organisation IMS
- Nom
- ID de tenant (n’incluez pas de **trait de soulignement**)
- Région

Votre administrateur système doit pouvoir vous aider à définir les valeurs de ces champs.

Cliquez sur **Enregistrer**.

![Créer un environnement de test](./assets/images/dsnorg2.png)

Votre environnement fera désormais partie de la liste. Recherchez-le dans la liste et cliquez sur l&#39;icône **link** .

![Créer un environnement de test](./assets/images/dsnorg3.png)

Vous devez maintenant saisir les valeurs que vous avez créées dans le cadre des informations d’identification de votre projet Adobe I/O. Vous trouverez **Client ID**, **Client Secret** et **Portées** ici :

![Créer un environnement de test](./assets/images/dsnorg4.png)

**ID du compte technique** :

![Créer un environnement de test](./assets/images/dsnorg5.png)

Copiez-collez-les ici, cliquez sur **Enregistrer**.

![Créer un environnement de test](./assets/images/dsnorg6.png)

Votre environnement DSN est maintenant configuré correctement.

## Configuration de votre accès à l’environnement du DSN

Accédez à [https://dsn.adobe.com/tools/environment-admin](https://dsn.adobe.com/tools/environment-admin). Sélectionnez l’organisation IMS que vous venez de créer, sélectionnez votre utilisateur, puis cliquez sur **+ Attribuer** sous **Environnements de test**.

![Créer un environnement de test](./assets/images/dsnorg7.png)

Saisissez le **nom sandbox** que vous avez défini à la première étape ci-dessus. Il doit ressembler à ceci :

- Nom : **aep-tutorial**

Cliquez sur **Confirmer**.

![Créer un environnement de test](./assets/images/dsnorg8.png)

Votre environnement de test est désormais disponible pour l’utilisateur que vous avez sélectionné.

![Créer un environnement de test](./assets/images/dsnorg9.png)

## Configuration rapide du DSN

Accédez à [https://dsn.adobe.com/quick-setup](https://dsn.adobe.com/quick-setup). Ouvrez le menu déroulant **Environnement** et sélectionnez votre organisation IMS/sandbox.

![Créer un environnement de test](./assets/images/dsnorg10.png)

Pour **Configuration**, sélectionnez **Global v2.0**.

![Créer un environnement de test](./assets/images/dsnorg11.png)

Faites défiler l’écran jusqu’à **Industry - Telco** et sélectionnez **Citi Signal - Advanced**.

![Créer un environnement de test](./assets/images/dsnorg12.png)

Faites défiler l’écran vers le haut et cliquez sur **Démarrer**.

![Créer un environnement de test](./assets/images/dsnorg13.png)

Saisissez un **Titre** et cliquez sur **Démarrer**.

![Créer un environnement de test](./assets/images/dsnorg14.png)

>[!NOTE]
>
>Vous pouvez obtenir des erreurs si aucune stratégie de fusion par défaut n’a été créée dans l’environnement de test. Si tel est le cas, attendez un peu plus que la stratégie de fusion soit créée automatiquement ou accédez manuellement à Adobe Experience Platform, à Profils > Stratégies de fusion et créez une nouvelle stratégie de fusion par défaut.

Vous verrez ensuite la progression de l’installation en cours, qui prendra quelques minutes.

![Créer un environnement de test](./assets/images/dsnorg15.png)

Une fois que tout a été terminé, votre instance AEP est correctement configurée et prête pour que les apprenants puissent suivre le tutoriel.

>[!NOTE]
>
>L’étape Importation de données n’est pas utilisée par le tutoriel. Par conséquent, si cette étape échoue, ne vous inquiétez pas et continuez.

![Créer un environnement de test](./assets/images/dsnorg16.png)

Accédez à [https://experience.adobe.com/platform](https://experience.adobe.com/platform), à **Jeux de données**. Vous devriez maintenant voir une liste similaire de jeux de données, qui ont tous été créés par la configuration rapide du DSN.

![Créer un environnement de test](./assets/images/dsnorg17.png)

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](./overview.md)