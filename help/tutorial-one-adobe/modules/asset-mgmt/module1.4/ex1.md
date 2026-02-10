---
title: Création de ressources et de modèles Dynamic Media
description: Création de ressources et de modèles Dynamic Media
kt: 5342
doc-type: tutorial
exl-id: 3867f23b-9b88-4971-a892-5821800e39ac
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '2241'
ht-degree: 1%

---

# 1.4.1 Création de vos ressources et de votre modèle Dynamic Media

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement de création AEM Assets CS fonctionnel dans lequel AEM Assets Dynamic Media est activé.
>
>Si vous ne disposez pas d’un tel environnement, accédez à [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.4.1.1 Créer votre société Dynamic Media

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`.

![AEM Assets Dynamic Media](./images/aaemassdmcomp1.png)

Faites défiler jusqu’à **Sociétés Dynamic Media**. Cliquez sur l’icône **+** pour créer une société Dynamic Media.

![AEM Assets Dynamic Media](./images/aaemassdmcomp2.png)

Renseignez les informations suivantes :

- **Nom de la société** : `--aepUserLdap---CitiSignal`.
- **Région de la société** : sélectionnez la région la plus proche de chez vous.
- **E-mails des administrateurs de la société** : saisissez le courrier électronique des administrateurs.

Cliquez sur **Créer**.

![AEM Assets Dynamic Media](./images/aaemassdmcomp3.png)

Vous devriez alors voir ceci.

![AEM Assets Dynamic Media](./images/aaemassdmcomp4.png)

Vous devriez maintenant recevoir un e-mail comme celui ci-dessous, qui contient votre mot de passe temporaire. Pour modifier votre mot de passe ou le récupérer si vous n’avez pas reçu d’e-mail, vous devez installer l’application de bureau **Adobe Dynamic Media Classic**. Vous trouverez les instructions d’installation ici : [https://experienceleague.adobe.com/fr/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app](https://experienceleague.adobe.com/fr/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app).

Suivez les instructions qui s&#39;y trouvent et revenez ici une fois l&#39;application installée sur votre système.

Ouvrez l’appli de bureau **Adobe Dynamic Media Classic**. Si vous connaissez votre mot de passe, veuillez le saisir ici et suivre les instructions pour le modifier lors de la première connexion.

Si vous ne connaissez pas votre mot de passe, cliquez sur le lien **Mot de passe oublié** et suivez les instructions pour réinitialiser votre mot de passe, puis revenez ici et connectez-vous.

![AEM Assets Dynamic Media](./images/aaemassdmcomp5.png)

Une fois la connexion établie, un écran similaire à celui-ci devrait s’afficher.

![AEM Assets Dynamic Media](./images/aaemassdmcomp6.png)

## 1.4.1.2 Configuration de Dynamic Media dans AEM

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`.

Cliquez pour ouvrir votre programme Cloud Manager, qui doit être appelé `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![AEM Assets Dynamic Media](./images/accsaemassets1.png)

Cliquez sur votre environnement.

![AEM Assets Dynamic Media](./images/accsaemassets3.png)

Cliquez sur l’URL de votre environnement.

![AEM Assets Dynamic Media](./images/accsaemassets2.png)

Accédez à **Outils**, à **Services cloud** puis à **Configuration Dynamic Media**.

![AEM Assets Dynamic Media](./images/accsaemassets4.png)

Sélectionnez **Global** (ne cochez pas la case), puis cliquez sur **Créer**.

![AEM Assets Dynamic Media](./images/accsaemassets5.png)

Renseignez les informations suivantes :

- **Titre** : utilisez ce titre : `--aepUserLdap-- - CitiSignal`.
- **Email** : saisissez votre adresse e-mail.
- **Mot de passe** : saisissez le mot de passe de votre compte Dynamic Media
- **Région** : sélectionnez la région choisie lors de la création de votre société Dynamic Media, dans cet exemple, **Europe**.

Cliquez sur **Connexion à Dynamic Media**.

![AEM Assets Dynamic Media](./images/accsaemassets6.png)

Vous devriez alors voir ceci. Configurez les éléments suivants :

- Sélectionnez la **Société** : `--aepUserLdap-- - CitiSignal`.
- Définissez **Publier Assets** sur **Immédiat**.
- Cochez la case pour **Synchroniser tout le contenu**.

Cliquez sur **Enregistrer**.

![AEM Assets Dynamic Media](./images/accsaemassets7.png)

Votre configuration Dynamic Media est maintenant terminée. Cliquez sur **OK**.

![AEM Assets Dynamic Media](./images/accsaemassets8.png)

## 1.4.1.3 Exporter des ressources

Téléchargez ce fichier [citisignal-fibre-max-is-coming.psd](./assets/citisignal-fiber-max-is-coming.psd){target="_blank"} et ouvrez-le avec Adobe Photoshop.

Vous devriez alors voir ceci. CitiSignal prévoit de déployer Fibre Max dans 3 villes : New York, Paris et Dubaï.

En affichant ou en masquant des calques spécifiques, vous pouvez afficher l’image créée par les concepteurs et conceptrices.

Vous trouverez ci-dessous les instructions pour exporter les fichiers image à partir du modèle Photoshop PSD. Si vous préférez, vous pouvez également télécharger les images terminées ici [citisignal-dm-email-assets.zip](./assets/citisignal-dm-email-assets.zip){target="_blank"} et décompresser le fichier sur votre bureau.

C&#39;est la version de New York.

![AEM Assets Dynamic Media](./images/aemdm1.png)

C&#39;est la version pour Dubaï.

![AEM Assets Dynamic Media](./images/aemdm2.png)

Voici la version pour Paris.

![AEM Assets Dynamic Media](./images/aemdm3.png)

Il y aura potentiellement beaucoup d&#39;autres villes dans lesquelles CitiSignal déploiera Fibre Max. Ainsi, à l&#39;avenir, de nouvelles couches pourraient être créées dans ce fichier. Pour l&#39;instant, l&#39;accent est mis sur les 3 villes déjà mentionnées.

Pour utiliser ces variations en combinaison avec AEM Assets Dynamic Media, les calques de chaque ville doivent être exportés séparément sous forme d’images, sans le fichier d’arrière-plan, et une autre exportation doit être effectuée pour le calque d’arrière-plan sans inclure de villes.

Vous devez maintenant masquer et afficher un seul des calques. Le premier calque à afficher est le calque **Paris**, et tous les autres calques doivent être masqués.

Pour exporter ce calque, accédez à **Fichier** > **Exporter** > **Exporter sous...**.

![AEM Assets Dynamic Media](./images/aemdm4.png)

Vous devriez alors voir ceci. Sélectionnez le type de fichier **PNG**, assurez-vous que **Transparence** est activé, puis cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm5.png)

Remplacez le nom du fichier par `citisignal-fiber-max-is-coming-paris.png`et cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm6.png)

Le calque suivant à afficher est le calque **Dubaï**, et tous les autres calques doivent être masqués.

Pour exporter ce calque, accédez à **Fichier** > **Exporter** > **Exporter sous...**.

![AEM Assets Dynamic Media](./images/aemdm4a.png)

Vous devriez alors voir ceci. Sélectionnez le type de fichier **PNG**, assurez-vous que **Transparence** est activé, puis cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm5a.png)

Remplacez le nom du fichier par `citisignal-fiber-max-is-coming-dubai.png`et cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm6a.png)

Le calque suivant à afficher est le calque **New York**, et tous les autres calques doivent être masqués.

Pour exporter ce calque, accédez à **Fichier** > **Exporter** > **Exporter sous...**.

![AEM Assets Dynamic Media](./images/aemdm4b.png)

Vous devriez alors voir ceci. Sélectionnez le type de fichier **PNG**, assurez-vous que **Transparence** est activé, puis cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm5b.png)

Remplacez le nom du fichier par `citisignal-fiber-max-is-coming-newyork.png`et cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm6b.png)

Le calque suivant à afficher est le calque **arrière-plan**, et tous les autres calques doivent être masqués.

Pour exporter ce calque, accédez à **Fichier** > **Exporter** > **Exporter sous...**.

![AEM Assets Dynamic Media](./images/aemdm4c.png)

Vous devriez alors voir ceci. Sélectionnez le type de fichier **PNG**, assurez-vous que **Transparence** est activé, puis cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm5c.png)

Remplacez le nom du fichier par `citisignal-fiber-max-is-coming-background`et cliquez sur **Exporter**.

![AEM Assets Dynamic Media](./images/aemdm6c.png)

Ces fichiers doivent alors être disponibles à l’emplacement d’exportation que vous avez sélectionné.

![AEM Assets Dynamic Media](./images/aemdm7.png)

## 1.4.1.4 Charger vos ressources dans AEM Assets CS

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Accédez à **Experience Manager Assets**.

![AEM Assets Dynamic Media](./images/aemdm8.png)

Sélectionnez votre référentiel, qui doit être nommé `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![AEM Assets Dynamic Media](./images/aemdm9.png)

Accédez à **Assets** puis cliquez sur **Créer un dossier**.

![AEM Assets Dynamic Media](./images/aemdm10.png)

Pour le dossier, utilisez le nom : `--aepUserLdap-- - CitiSignal Dynamic Media`. Cliquez sur **Créer**.

![AEM Assets Dynamic Media](./images/aemdm11.png)

Double-cliquez pour ouvrir le dossier que vous venez de créer.

![AEM Assets Dynamic Media](./images/aemdm12.png)

Cliquez sur **Ajouter Assets**.

![AEM Assets Dynamic Media](./images/aemdm13.png)

Cliquez sur **Parcourir** puis sélectionnez **Parcourir les fichiers**.

![AEM Assets Dynamic Media](./images/aemdm15.png)

Sélectionnez les 4 fichiers PNG que vous avez exportés à l’étape précédente.

![AEM Assets Dynamic Media](./images/aemdm16.png)

Cliquez sur **Télécharger**.

![AEM Assets Dynamic Media](./images/aemdm17.png)

Vos images sont désormais disponibles dans AEM Assets CS.

![AEM Assets Dynamic Media](./images/aemdm18.png)

Patientez quelques minutes, puis ouvrez l’application de bureau **Adobe Dynamic Media Classic**. Vous devriez maintenant également voir les images chargées devenir disponibles dans Dynamic Media.

![AEM Assets Dynamic Media](./images/aemdm19.png)

## 1.4.1.5 Configurer Le Modèle Dynamic Media

Dans le menu de gauche, accédez à **Dynamic Media Assets**. Cliquez pour ouvrir votre dossier `--aepUserLdap-- - CitiSignal Dynamic Media`. Cliquez ensuite sur **Créer un modèle**.

![AEM Assets Dynamic Media](./images/aemdm20.png)

Renseignez les informations suivantes :

- **Nom du modèle** : `--aepUserLdap-- - CitiSignal Fiber Max Launch Email Assets`
- **Largeur de la zone de travail** : `600px`
- **Hauteur de la zone de travail** : `600px`

Cliquez sur **Créer**.

![AEM Assets Dynamic Media](./images/aemdm21.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **Ajouter une image**.

![AEM Assets Dynamic Media](./images/aemdm22.png)

Faites glisser le fichier **citisignal-fibre-max-is-coming_citisignal-background.png** sur la zone de travail et faites-le tenir dans la zone de travail.

![AEM Assets Dynamic Media](./images/aemdm23.png)

Ensuite, faites glisser le fichier **citisignal-fibre-max-is-coming_citisignal-newyork.png** sur la zone de travail et faites-le tenir dans la zone de travail.

![AEM Assets Dynamic Media](./images/aemdm24.png)

Ensuite, faites glisser le fichier **citisignal-fibre-max-is-coming_citisignal-dubai.png** sur la zone de travail et faites-le tenir dans la zone de travail.

![AEM Assets Dynamic Media](./images/aemdm25.png)

Ensuite, faites glisser le fichier **citisignal-fibre-max-is-coming_citisignal-paris.png** sur la zone de travail et faites-le tenir dans la zone de travail.

![AEM Assets Dynamic Media](./images/aemdm26.png)

Vous disposez désormais des 3 variations du modèle en tant que calques distincts en même temps. Vous pouvez afficher/masquer des calques spécifiques en cliquant sur l’icône **calques**, qui affiche tous les calques actuellement visibles.

![AEM Assets Dynamic Media](./images/aemdm27.png)

En masquant quelques calques, vous pouvez contrôler l’aspect de l’image. Dans cet exemple, seul le calque **Paris** et le calque d’arrière-plan sont visibles.

![AEM Assets Dynamic Media](./images/aemdm28.png)

Vous devez ensuite ajouter un calque de texte. Cliquez sur l’icône **calque de texte**.

![AEM Assets Dynamic Media](./images/aemdm29.png)

Vous devriez alors voir ceci.

![AEM Assets Dynamic Media](./images/aemdm30.png)

N’hésitez pas à adapter le champ de texte comme vous le souhaitez. Voici un exemple. N’oubliez pas d’activer l’option **Redimensionnement intelligent du texte** afin que le texte réel inséré ultérieurement s’affiche correctement.

![AEM Assets Dynamic Media](./images/aemdm31.png)

Ajoutez un deuxième calque de texte et faites-le ressembler à ceci. N’oubliez pas d’activer l’option **Redimensionnement intelligent du texte** afin que le texte réel inséré ultérieurement s’affiche correctement.

![AEM Assets Dynamic Media](./images/aemdm32.png)

Sélectionnez le premier calque de texte. Cliquez sur le **de 3 points...**, puis sélectionnez **Modifier**.

![AEM Assets Dynamic Media](./images/aemdm33.png)

Vous devriez alors voir ceci. Faites défiler vers le bas.

![AEM Assets Dynamic Media](./images/aemdm34.png)

Cliquez sur l’icône **sélecteur** pour activer le champ **Texte**. Remplacez **Nom du paramètre** par `title`.

![AEM Assets Dynamic Media](./images/aemdm35.png)

Sélectionnez le deuxième calque de texte. Cliquez sur le **de 3 points...**, puis sélectionnez **Modifier**.

![AEM Assets Dynamic Media](./images/aemdm36.png)

Vous devriez alors voir ceci. Faites défiler vers le bas.

![AEM Assets Dynamic Media](./images/aemdm37.png)

Cliquez sur l’icône **sélecteur** pour activer le champ **Texte**. Remplacez **Nom du paramètre** par `body`.

![AEM Assets Dynamic Media](./images/aemdm38.png)

Sélectionnez le calque pour **Paris**. Cliquez sur le **de 3 points...**, puis sur **Modifier**.

![AEM Assets Dynamic Media](./images/aemdm39.png)

Accédez à **Paramètres**. Activez le champ **Masquer** et saisissez le **Nom du paramètre** : `city_paris`. Cliquez sur **Enregistrer**.

![AEM Assets Dynamic Media](./images/aemdm40.png)

Sélectionnez le calque pour **Dubaï**. Cliquez sur le **de 3 points...**, puis sur **Modifier**.

![AEM Assets Dynamic Media](./images/aemdm41.png)

Accédez à **Paramètres**. Activez le champ **Masquer** et saisissez le **Nom du paramètre** : `city_dubai`. Cliquez sur **Enregistrer**.

![AEM Assets Dynamic Media](./images/aemdm42.png)

Sélectionnez le calque pour **New York**. Cliquez sur le **de 3 points...**, puis sur **Modifier**.

![AEM Assets Dynamic Media](./images/aemdm43.png)

Accédez à **Paramètres**. Activez le champ **Masquer** et saisissez le **Nom du paramètre** : `city_ny`. Cliquez sur **Enregistrer**.

![AEM Assets Dynamic Media](./images/aemdm44.png)

Cliquez sur **Aperçu**.

![AEM Assets Dynamic Media](./images/aemdm45.png)

Activez le sélecteur pour **Inclure tous les paramètres** et modifiez certaines variables d’entrée comme indiqué dans la capture d’écran. Vous devriez voir votre image changer de manière dynamique en fonction de l’entrée fournie. Pour les champs **city_paris**, **city_dubai** et **city_ny**, une valeur de 0 signifie que cette image ne sera PAS masquée et une valeur de 1 signifie que cette image sera masquée.

![AEM Assets Dynamic Media](./images/aemdm46.png)

En modifiant certaines variables, une autre image s’affiche désormais.

![AEM Assets Dynamic Media](./images/aemdm47.png)

En modifiant d’autres variables, une autre image s’affiche désormais.

Pour utiliser ce modèle avec Adobe Journey Optimizer et répondre aux exigences de ce cas d’utilisation, vous devez ajouter un calque supplémentaire qui sera utilisé pour modifier dynamiquement le chemin d’accès au fichier qui doit être affiché, en fonction d’un champ qui fait partie du profil client en temps réel dans Adobe Experience Platform.

Lors de la préparation des données, un champ a été créé dans le du schéma Adobe Experience Platform pour stocker la **ville de déploiement la plus proche** pour un client. Le chemin d’accès du champ est `--aepTenantId--.individualCharacteristics.fiber_rollout.closest_rollout_city`.

>[!NOTE]
>
>La capture d’écran ci-dessous du schéma Adobe Experience Platform est fournie à titre d’information uniquement. Il n’est pas nécessaire d’accéder à AEP pour visualiser cela vous-même.

![AEM Assets Dynamic Media](./images/aemdm50.png)

Dans l’exercice suivant, vous utiliserez ce champ pour sélectionner de manière dynamique l’image à afficher à chaque client.

Pour ce faire, vous devez ajouter un nouveau calque d’image.

Tout d’abord, masquons les autres calques contenant des images pour les villes de déploiement.

![AEM Assets Dynamic Media](./images/aemdm51.png)

Ensuite, accédez à **Images** et sélectionnez une image aléatoire d’une ville, ajoutez-la à la zone de travail et assurez-vous qu’elle s’adapte à l’ensemble de la zone de travail. Peu importe l’image de la ville que vous choisissez, car le chemin sera modifié dynamiquement par AJO dans l’exercice suivant.

![AEM Assets Dynamic Media](./images/aemdm52.png)


![AEM Assets Dynamic Media](./images/aemdm53.png)

Accédez à **Paramètres**.

Cliquez sur l’icône **sélecteur** afin que le champ **Masquer** soit activé. Remplacez **Nom du paramètre** par `dynamic_city_hide`.

Cliquez sur l’icône **sélecteur** afin que le champ **Masquer** soit activé. Remplacez **Nom du paramètre** par `dynamic_city_image`.

Cliquez sur **Enregistrer**.

![AEM Assets Dynamic Media](./images/aemdm54.png)

Cliquez sur **Aperçu**.

![AEM Assets Dynamic Media](./images/aemdm55.png)

Vous devriez alors voir ceci. Activez l’icône du sélecteur pour **Inclure tous les paramètres**. Modifiez certaines variables d’entrée comme indiqué dans la capture d’écran. Vous devriez voir votre image changer de manière dynamique en fonction de l’entrée fournie. Les champs statiques **city_paris**, **city_dubai** et **city_ny** doivent être définis sur 1, ce qui signifie que ces images seront masquées.

Le champ **dynamic_city_hide** doit être défini sur 0, ce qui signifie qu’il sera affiché.

Le champ **dynamic_city_image** contient désormais l’URL de l’image de Paris, qui ressemble à ceci : `vangeluwCitiSignalDM/citisignal-fiber-max-is-coming_citisignal-paris-1`.

![AEM Assets Dynamic Media](./images/aemdm56.png)

Sélectionnez le mot **paris** dans l’URL.

![AEM Assets Dynamic Media](./images/aemdm57.png)

Remplacez **paris** par `newyork`, puis cliquez ailleurs dans l’interface utilisateur pour voir l’image remplacée par celle de la ville de New York.

![AEM Assets Dynamic Media](./images/aemdm58.png)

Sélectionnez le mot **newyork** et remplacez-le par `dubai`, puis cliquez ailleurs dans l’interface utilisateur pour afficher le changement d’image en image de Dubaï City.

Enfin, cliquez sur **Publier**.

![AEM Assets Dynamic Media](./images/aemdm60.png)

Vous devriez alors voir ceci. Cliquez sur **Oui**.

![AEM Assets Dynamic Media](./images/aemdm61.png)

Votre modèle Dynamic Media est maintenant configuré et publié. Dans l’exercice suivant, vous utiliserez ce modèle en combinaison avec une campagne par e-mail dans Adobe Journey Optimizer.

## Étapes suivantes

Étape suivante : [Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer](./ex2.md){target="_blank"}

Revenir à [Adobe Experience Manager Assets et Dynamic Media](./aemassetsdm.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
