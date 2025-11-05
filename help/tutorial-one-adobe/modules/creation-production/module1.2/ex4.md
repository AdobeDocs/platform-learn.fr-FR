---
title: Frame I/O vers Workfront Fusion vers AEM Assets
description: Frame I/O vers Workfront Fusion vers AEM Assets
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: f02ecbe4-f1d7-4907-9bbc-04e037546091
source-git-commit: 5af7b64e88dc0f260be030bca73d9fe9219ba255
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 1%

---

# 1.2.4 Frame I/O vers Workfront Fusion vers AEM Assets

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement de création AEM Assets CS fonctionnel. Si vous suivez l’exercice [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"} vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM Assets CS avec un environnement de création, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de commencer le processus de réactivation maintenant afin de ne pas se retrouver bloqué ultérieurement.

Dans l’exercice précédent, vous avez configuré un scénario qui génère automatiquement des variantes d’un fichier PSD Adobe Photoshop à l’aide d’Adobe Firefly, des API Photoshop et de Workfront Fusion. La sortie de ce scénario était un nouveau fichier PSD Photoshop.

Toutefois, les équipes commerciales n’ont pas besoin d’un fichier PSD, mais d’un fichier PNG ou d’un fichier JPG. Dans cet exercice, vous allez configurer une nouvelle automatisation qui entraînera la génération d’un fichier PNG une fois que la ressource dans Frame I/O sera approuvée, et ce fichier sera automatiquement stocké dans AEM Assets.

## 1.2.4.1 Créer un nouveau scénario

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Dans le menu de gauche, accédez à **Scénarios** et sélectionnez votre dossier `--aepUserLdap--`. Cliquez sur **Créer un nouveau scénario**.

![E/S de trame](./images/aemf1.png)

Utilisez le nom `--aepUserLdap-- - Asset Approved PNG AEM Assets`. Cliquez ensuite sur le **?** le module , saisissez le `webhook` du terme de recherche, puis cliquez sur **Webhooks**.

![E/S de trame](./images/aemf2.png)

Cliquez sur **Webhook personnalisé**.

![E/S de trame](./images/aemf3.png)

Cliquez sur **Ajouter** pour créer un webhook.

![E/S de trame](./images/aemf4.png)

Utilisez le nom `--aepUserLdap-- - Frame.io Webhook`. Cliquez sur **Enregistrer**.

![E/S de trame](./images/aemf5.png)

Vous devriez alors voir ceci. Cliquez sur **Copier l’adresse dans le presse-papiers**.

![E/S de trame](./images/aemf6.png)

## 1.2.4.2 Configurer le Webhook dans Frame.io

Accédez à Postman et ouvrez la requête **POST - Get Access Token** dans la collection **Adobe IO - OAuth**. Cliquez ensuite sur **Envoyer** pour demander un nouveau **access_token**.

![E/S de trame](./images/frameV4api2.png)

Dans le menu de gauche, revenez à **Collections**. Ouvrez la requête **POST - Créer un Webhook** dans la collection **Frame.io V4 - Tech Insiders**, dans le dossier **Webhooks**.

Accédez au **Corps** de la requête. Remplacez le champ **nom** par `--aepUserLdap--  - Fusion to AEM Assets`, puis remplacez le champ **url** par la valeur de l’URL Webhook que vous avez copiée à partir de Workfront Fusion.

Cliquez sur **Envoyer**.

![E/S de trame](./images/framewh1.png)

Votre action personnalisée Frame.io V4 a maintenant été créée.

![E/S de trame](./images/framewh2.png)

Accédez à [https://next.frame.io/project](https://next.frame.io/project){target="_blank"} puis au projet que vous avez créé précédemment, qui doit être nommé `--aepUserLdap--` et ouvrez le dossier **CitiSignal Fiber Campaign**. Vous devriez maintenant voir les ressources qui ont été créées dans l’exercice précédent.

![E/S de trame](./images/aemf11a.png)

Cliquez sur le champ **Statut** et modifiez le statut en **En cours**.

![E/S de trame](./images/aemf12.png)

Revenez à Workfront Fusion. Vous devriez maintenant voir que la connexion a été **déterminée avec succès**.

![E/S de trame](./images/aemf13.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour effectuer un test rapide.

![E/S de trame](./images/aemf14.png)

Revenez à Frame.io et cliquez sur le champ **En cours** et modifiez le statut en **Révision requise**.

![E/S de trame](./images/aemf15.png)

Revenez à Workfront Fusion et cliquez sur la bulle dans le module **Custom webhook**.

La vue détaillée de la bulle vous montre les données reçues de Frame.io. Vous devriez voir différents ID. Par exemple, le champ **resource.id** affiche l’ID unique dans Frame.io de la ressource **citisignal-fibre.psd**.

![E/S de trame](./images/aemf16.png)

## 1.2.4.3 Obtenir les détails de la ressource à partir de Frame.io

Maintenant que la communication entre Frame.io et Workfront Fusion a été établie via un webhook personnalisé, vous devriez obtenir plus de détails sur la ressource pour laquelle le libellé de statut a été mis à jour. Pour ce faire, vous utiliserez à nouveau le connecteur Frame.io dans Workfront Fusion, comme dans l’exercice précédent.

Pointez sur l’objet **Custom webhook** et cliquez sur l’icône **+** pour ajouter un autre module.

![E/S de trame](./images/aemf18a.png)

Saisissez le `frame` du terme de recherche. Cliquez sur **Frame.io**.

![E/S de trame](./images/aemf18.png)

Cliquez sur **Frame.io**.

![E/S de trame](./images/aemf19.png)

Cliquez sur **Effectuer un appel API personnalisé**.

![E/S de trame](./images/aemf20.png)

Vérifiez que la connexion est définie sur la même connexion que celle que vous avez créée dans l’exercice précédent, qui doit être nommée `--aepUserLdap-- - Adobe I/O - Frame.io S2S`.

![E/S de trame](./images/aemf21.png)

Pour configurer le module **Frame.io - Effectuer un appel API personnalisé**, utilisez l’URL : `/v4/accounts/{{1.account.id}}/files/{{1.resource.id}}`.

>[!NOTE]
>
>Les variables dans Workfront Fusion peuvent être spécifiées manuellement à l’aide de la syntaxe suivante : `{{1.account.id}}` et `{{1.resource.id}}`. Le nombre dans la variable fait référence au module dans le scénario. Dans cet exemple, vous pouvez constater que le premier module du scénario est appelé **Webhooks** et qu’il possède un numéro de séquence de **1**. Cela signifie que les variables `{{1.account.id}}` et `{{1.resource.id}}` accéderont à ce champ à partir du module portant le numéro de séquence 1. Les numéros de séquence peuvent parfois être différents. Faites donc attention lorsque vous copiez/collez de telles variables et vérifiez toujours que le numéro de séquence utilisé est correct.

Cliquez ensuite sur **+ Ajouter un élément** sous **Chaîne de requête**.

![E/S de trame](./images/aemf21a.png)

Saisissez ces valeurs et cliquez sur **Ajouter**.

| Clé | Valeur |
|:-------------:| :---------------:| 
| `include` | `media_links.original` |

![E/S de trame](./images/aemf21b.png)

Vous devriez maintenant avoir ceci. Cliquez sur **OK**.

![E/S de trame](./images/aemf22.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour tester votre configuration.

![E/S de trame](./images/aemf23.png)

Revenez à Frame.io et modifiez le statut en **En cours**.

![E/S de trame](./images/aemf24.png)

Revenez à Workfront Fusion et cliquez sur la bulle sur le module **Frame.io - Effectuer un appel API personnalisé**. Vous devriez alors voir une vue d’ensemble similaire.

![E/S de trame](./images/aemf25.png)

Ensuite, vous devez configurer un filtre pour vous assurer qu’un fichier PNG est rendu uniquement pour les ressources dont le statut est **Approuvé**. Pour ce faire, cliquez sur l’icône **Clé à molette** entre les modules **Webhook personnalisé** et **Frame.io - Effectuer un appel API personnalisé** puis sélectionnez **Configurer un filtre**.

![E/S de trame](./images/aemf25a.png)

Configurez les champs suivants :

- **Libellé** : utilisez `Status = Approved`.
- **Condition** : `{{1.metadata.value[]}}`.
- **Opérateurs de base** : sélectionnez **Égal à**.
- **Valeur** : `Approved`.

Cliquez sur **OK**.

![E/S de trame](./images/aemf35.png)

Tu devrais avoir ça. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/aemf35a.png)

## 1.2.4.4 Convertir au format PNG

Pointez sur le module **Frame.io - Effectuez un appel API personnalisé** puis cliquez sur l’icône **+**.

![E/S de trame](./images/aemf27.png)

Saisissez le terme de recherche `photoshop`, puis cliquez sur **Adobe Photoshop**.

![E/S de trame](./images/aemf28.png)

Cliquez sur **Convertir le format d’image**.

![E/S de trame](./images/aemf29.png)

Vérifiez que le champ **Connexion** utilise la connexion que vous avez créée précédemment et qui est nommée `--aepUserLdap-- - Adobe IO`.

Sous **Entrée**, définissez le champ **Stockage** sur **Externe** et définissez **Emplacement du fichier** pour utiliser la variable **Original** renvoyée par le module **Frame.io - Effectuez un appel API personnalisé**.

Cliquez ensuite sur **Ajouter un élément** sous **Sorties**.

![E/S de trame](./images/aemf30.png)

Pour la configuration **Sorties**, définissez le champ **Stockage** sur **Stockage interne Fusion** et le **Type** sur **image/png**. Cliquez sur **Ajouter**.

![E/S de trame](./images/aemf31.png)

Cliquez sur **OK**.

![E/S de trame](./images/aemf33.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour tester votre configuration.

![E/S de trame](./images/aemf32.png)

Revenez à Frame.io et cliquez sur le champ **En cours** et modifiez le statut en **Approuvé**.

![E/S de trame](./images/aemf37.png)

Revenez à Workfront Fusion. Vous devriez maintenant voir que tous les modules de votre scénario ont été exécutés avec succès. Cliquez sur la bulle dans le module **Adobe Photoshop - Convertir le format d’image**.

![E/S de trame](./images/aemf38.png)

Dans les détails de l’exécution du module **Adobe Photoshop - Convertir le format d’image**, vous pouvez constater qu’un fichier PNG a été généré. L’étape suivante consiste à stocker ensuite ce fichier dans AEM Assets CS.

![E/S de trame](./images/aemf39.png)

## 1.2.4.5 Store PNG in AEM Assets CS

Pointez sur le module **Adobe Photoshop - Convertir le format d’image** et cliquez sur l’icône **+**.

![E/S de trame](./images/aemf40.png)

Saisissez le terme de recherche `aem` et sélectionnez **AEM Assets**.

![E/S de trame](./images/aemf41.png)

Cliquez sur **Charger une ressource**.

![E/S de trame](./images/aemf42.png)

Vous devez maintenant configurer votre connexion à AEM Assets CS. Cliquez sur **Ajouter**.

![E/S de trame](./images/aemf43.png)

Utilisez les paramètres suivants :

- **Type de connexion** : **AEM Assets as a Cloud Service**.
- **Nom de la connexion** : `--aepUserLdap-- AEM Assets CS`.
- **URL de l’instance** : copiez l’URL de l’instance de votre environnement de création AEM Assets CS, qui doit se présenter comme suit : `https://author-pXXXXX-eXXXXXXX.adobeaemcloud.com`.
- **Options de remplissage des détails d’accès** : sélectionnez **Fournir un fichier JSON**.

Vous devez maintenant fournir les informations d’identification du compte technique **au format JSON**. Pour ce faire, il existe plusieurs étapes à suivre à l’aide d’AEM Cloud Manager. Pendant ce temps, gardez cet écran ouvert.

![E/S de trame](./images/aemf44.png)

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`. Vous verrez alors quelque chose comme ceci. Cliquez pour ouvrir votre programme, qui doit être nommé `--aepUserLdap-- - Citi Signal`.

![E/S de trame](./images/aemf45.png)

Cliquez sur le **de 3 points...** et sélectionnez **Developer Console**.

![E/S de trame](./images/aemf46.png)

Cliquez sur **Se connecter avec Adobe**.

![E/S de trame](./images/aemf47.png)

Accédez à **Outils** > **Intégrations**.

![E/S de trame](./images/aemf47a.png)

Cliquez sur **Créer un compte technique**.

![E/S de trame](./images/aemf48.png)

Vous devriez alors voir quelque chose comme ça. Ouvrez le compte technique que vous venez de créer. Cliquez sur le **de 3 points...**, puis sélectionnez **Afficher**.

![E/S de trame](./images/aemf48a.png)

Vous devriez alors voir une payload de jeton de compte technique similaire. Copiez la payload JSON complète dans le presse-papiers.

![E/S de trame](./images/aemf50.png)

Revenez à Workfront Fusion et collez la payload JSON complète dans le champ **Informations d’identification du compte technique au format JSON**. Cliquez sur **Continuer**.

![E/S de trame](./images/aemf49.png)

Votre connexion sera ensuite validée et, en cas de réussite, elle sera automatiquement sélectionnée dans le module AEM Assets. La procédure suivante consiste à configurer un dossier. Dans le cadre de l’exercice, vous devez créer un dossier dédié.

![E/S de trame](./images/aemf51.png)

Pour créer un dossier dédié, accédez à [https://experience.adobe.com](https://experience.adobe.com/){target="_blank"}. Assurez-vous que la bonne instance Experience Cloud est sélectionnée, ce qui doit être `--aepImsOrgName--`. Cliquez ensuite sur **Experience Manager Assets**.

![E/S de trame](./images/aemf52.png)

Cliquez sur **Sélectionner** dans votre environnement AEM Assets CS, qui doit être nommé `--aepUserLdap-- - Citi Signal dev`.

![E/S de trame](./images/aemf53.png)

Accédez à **Ressources** et cliquez sur **Créer un dossier**.

![E/S de trame](./images/aemf54.png)

Saisissez le nom `--aepUserLdap-- - CitiSignal Fiber Campaign` et cliquez sur **Créer**.

![E/S de trame](./images/aemf55.png)

Votre dossier est alors créé.

![E/S de trame](./images/aemf56.png)

Revenez à Workfront Fusion, sélectionnez **Cliquez ici pour choisir le dossier** puis choisissez le dossier `--aepUserLdap-- - CitiSignal Fiber Campaign`.

![E/S de trame](./images/aemf57.png)

Vérifiez que la destination est définie sur `--aepUserLdap-- - CitiSignal Fiber Campaign`. Ensuite, sous **Fichier Source**, sélectionnez **Map**.

Sous **Nom du fichier**, choisissez la variable `{{3.filenames[1]}}`.

Sous **Données**, choisissez la variable `{{3.files[1]}}`.

>[!NOTE]
>
>Les variables dans Workfront Fusion peuvent être spécifiées manuellement à l’aide de la syntaxe suivante : `{{3.filenames[1]}}`. Le nombre dans la variable fait référence au module dans le scénario. Dans cet exemple, vous pouvez constater que le troisième module du scénario s’appelle **Adobe Photoshop - Convertir le format d’image** et possède un numéro de séquence de **3**. Cela signifie que la variable `{{3.filenames[1]}}` accédera au champ **noms de fichier[]** à partir du module portant le numéro de séquence 3. Les numéros de séquence peuvent parfois être différents. Faites donc attention lorsque vous copiez/collez de telles variables et vérifiez toujours que le numéro de séquence utilisé est correct.

Cliquez sur **OK**.

![E/S de trame](./images/aemf58.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/aemf59.png)

Vous devez ensuite définir des autorisations spécifiques pour le compte technique que vous venez de créer. Lors de la création du compte dans **Developer Console** dans **Cloud Manager**, des droits d’accès **Lecture** lui ont été accordés, mais pour ce cas d’utilisation, des droits d’accès **Écriture** sont requis. Pour ce faire, accédez à l’environnement de création AEM CS.

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`. Cliquez pour ouvrir votre programme, qui doit être nommé `--aepUserLdap-- - Citi Signal`. Vous verrez alors quelque chose comme ceci. Cliquez sur l’URL de création.

![E/S de trame](./images/aemf60.png)

Cliquez sur **Se connecter avec Adobe**.

![E/S de trame](./images/aemf61.png)

Accédez à **Paramètres** > **Sécurité** > **Utilisateurs**.

![E/S de trame](./images/aemf62.png)

Cliquez pour ouvrir le compte d’utilisateur du compte technique.

![E/S de trame](./images/aemf63.png)

Accédez à **Groupes** et ajoutez cet utilisateur de compte technique au groupe **DAM-Users**.

![E/S de trame](./images/aemf64.png)

Cliquez sur **Enregistrer et fermer**.

![E/S de trame](./images/aemf65.png)

Revenez à Workfront Fusion. Cliquez sur **Exécuter une fois** pour tester votre scénario.

![E/S de trame](./images/aemf66.png)

Revenez à Frame.io et assurez-vous que le statut de votre ressource est de nouveau modifié en **Approuvé**.

>[!NOTE]
>
>Vous devrez peut-être d’abord la modifier en **En cours** ou **Doit être examiné**, puis la modifier en **Approuvé**.

![E/S de trame](./images/aemf15.png)

Votre scénario Workfront Fusion sera alors activé et devrait s’achever correctement. En affichant les informations dans la bulle sur le module **AEM Assets**, vous pouvez déjà voir que le fichier PNG a été correctement stocké dans AEM Assets CS.

![E/S de trame](./images/aemf67.png)

Revenez à AEM Assets CS et ouvrez le dossier `--aepUserLdap-- - Frame.io PNG`. Vous devriez maintenant voir le fichier PNG qui a été généré dans le cadre du scénario Workfront Fusion. Double-cliquez sur le fichier pour l’ouvrir.

![E/S de trame](./images/aemf68.png)

Vous pouvez maintenant voir plus de détails sur les métadonnées du fichier PNG qui a été généré.

![E/S de trame](./images/aemf69.png)

Vous avez maintenant terminé cet exercice avec succès.

## Étapes suivantes

Accédez à [&#x200B; Résumé et avantages de l’automatisation des workflows Creative avec Workfront Fusion &#x200B;](./summary.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
1,2,4