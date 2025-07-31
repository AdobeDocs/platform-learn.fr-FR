---
title: Prise en main de Workfront
description: Prise en main de Workfront
kt: 5342
doc-type: tutorial
source-git-commit: d583df79bff499b7605f77146d52e66bc02810b9
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# 1.2.1 Prise en main de Workfront

Connectez-vous à Adobe Workfront en allant sur [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Vous voyez alors ceci.

![WF](./images/wfb1.png)

## 1.2.1.1 Configurer votre intégration AEM Assets

Cliquez sur l’icône des 9 points **hamburger**, puis sélectionnez **Configuration**.

![WF](./images/wfb2.png)

Dans le menu de gauche, faites défiler l’écran jusqu’à **Documents** puis cliquez sur **Experience Manager Assets**.

![WF](./images/wfb3.png)

Cliquez sur **+ Ajouter l’intégration Experience Manager**.

![WF](./images/wfb4.png)

Pour le nom de votre intégration, utilisez `--aepUserLdap-- - Citi Signal AEM`.

Ouvrez la liste déroulante **Référentiel Experience Manager** et sélectionnez votre instance AEM CS, qui doit être nommée `--aepUserLdap-- - Citi Signal`.

![WF](./images/wfb5.png)

Sous **Métadonnées**, configurez le mappage suivant :

| Champ Workfront | Champ Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Document** > **Nom** | **wm:documentName** |
| **Projet** > **Description** | **wm:projectDescription** |
| **Tâche** > **Nom** | **wm:taskName** |
| **Tâche** > **Description** | **wm:taskDescription** |

Activez le commutateur pour **Synchroniser les métadonnées d’objet**.

Cliquez sur **Enregistrer**.

![WF](./images/wfb6.png)

Votre intégration de Workfront à AEM Assets CS est maintenant configurée.

![WF](./images/wfb7.png)

## 1.2.1.2 Configurer l’intégration des métadonnées avec AEM Assets

Ensuite, vous devez configurer AEM Assets pour que les champs de métadonnées de la ressource dans Workfront soient partagés avec AEM.

Pour ce faire, accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez sur **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Cliquez pour sélectionner votre environnement AEM Assets, qui doit être nommé `--aepUserLdap-- - Citi Signal dev`.

![WF](./images/wfbaem2.png)

Vous devriez alors voir ceci. Dans le menu de gauche, accédez à **Assets** puis cliquez sur **Créer un dossier**.

![WF](./images/wfbaem3.png)

Nommez votre `--aepUserLdap-- - Workfront Assets` de dossier et cliquez sur **Créer**.

![WF](./images/wfbaem4.png)

Ensuite, accédez à **Forms de métadonnées** dans le menu de gauche, puis cliquez sur **Créer**.

![WF](./images/wfbaem5.png)

Utilisez le `--aepUserLdap-- - Metadata Form` de nom et cliquez sur **Créer**.

![WF](./images/wfbaem6.png)

Ajoutez 3 nouveaux champs **texte monoligne** au formulaire et sélectionnez le premier champ. Cliquez ensuite sur l’icône **Schéma** en regard du champ **Propriété de métadonnées**.

![WF](./images/wfbaem7.png)

Dans le champ de recherche, saisissez `wm:project` puis sélectionnez le champ **Description du projet**. Cliquez sur **Sélectionner**.

![WF](./images/wfbaem8.png)

Remplacez le libellé du champ par **Description du projet**.

![WF](./images/wfbaem9.png)

Sélectionnez ensuite le deuxième champ **Texte d’une seule ligne** et cliquez de nouveau sur l’icône **Schéma** en regard du champ **Propriété de métadonnées**.

![WF](./images/wfbaem10b.png)

Vous verrez alors à nouveau cette fenêtre contextuelle. Dans le champ de recherche, saisissez `wm:project` puis sélectionnez le champ **ID du projet**. Cliquez sur **Sélectionner**.

![WF](./images/wfbaem10.png)

Remplacez le libellé du champ par **ID du projet**.

![WF](./images/wfbaem10a.png)

Sélectionnez le troisième champ **Texte monoligne** et cliquez de nouveau sur l’icône **Schéma** en regard du champ **Propriété de métadonnées**.

![WF](./images/wfbaem11a.png)

Vous verrez alors à nouveau cette fenêtre contextuelle. Dans le champ de recherche, saisissez `wm:project` puis sélectionnez le champ **Nom du projet**. Cliquez sur **Sélectionner**.

![WF](./images/wfbaem11.png)

Remplacez le libellé du champ par **Nom du projet**. Cliquez sur **Enregistrer**.

![WF](./images/wfbaem12.png)

Remplacez le **Nom de l’onglet** du formulaire par `--aepUserLdap-- - Workfront Metadata`. Cliquez sur **Enregistrer** et **Fermer**.

![WF](./images/wfbaem13.png)

Votre **Formulaire de métadonnées** est maintenant configuré.

![WF](./images/wfbaem14.png)

Ensuite, vous devez affecter le formulaire de métadonnées au dossier que vous avez créé précédemment. Cochez la case correspondant à votre formulaire de métadonnées et cliquez sur **Affecter au(x) dossier(s)**.

![WF](./images/wfbaem15.png)

Sélectionnez votre dossier, qui doit être nommé `--aepUserLdap-- - Workfront Assets`. Cliquez sur **Attribuer**.

![WF](./images/wfbaem16.png)

Le formulaire de métadonnées est maintenant correctement affecté à votre dossier.

![WF](./images/wfbaem17.png)

## 1.2.1.2 Configurer votre intégration AEM Sites

>[!NOTE]
>
>Ce plug-in est actuellement en mode **Accès anticipé** et n’est pas encore disponible pour la plupart des utilisateurs.
>
>Ce plug-in est peut-être déjà installé dans l’instance Workfront que vous utilisez. S’il est déjà installé, vous pouvez consulter les instructions ci-dessous, mais il n’est pas nécessaire de modifier quoi que ce soit dans votre configuration.

Accédez à [https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}.

Assurez-vous que la **bascule** de ce plug-in est définie sur **Activé**. Cliquez ensuite sur l’icône **engrenage**.

![WF](./images/wfb8.png)

Une fenêtre contextuelle **Configuration de l’extension** s’affiche. Configurez les champs suivants pour utiliser ce plug-in.

| Clé | Valeur |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{« previewUrl »: true, « publishUrl »: true}&#39;** |

Cliquez sur **Enregistrer**.

![WF](./images/wfb8.png)

Revenez à l’interface utilisateur de Workfront et cliquez sur l’icône des 9 points **hamburger**. Sélectionnez **Configuration**.

![WF](./images/wfb9.png)

Dans le menu de gauche, accédez à **Custom Forms** et sélectionnez **Form**. Cliquez sur **+ Nouveau formulaire personnalisé**.

![WF](./images/wfb10.png)

Sélectionnez **Tâche** et cliquez sur **Continuer**.

![WF](./images/wfb11.png)

Un formulaire personnalisé vide s’affiche alors. Saisissez le nom du formulaire `Content Fragment & Integration ID`.

![WF](./images/wfb12.png)

Effectuez un glisser-déposer d’un nouveau champ **Texte monoligne** sur la zone de travail.

![WF](./images/wfb13.png)

Configurez le nouveau champ comme suit :

- **Libellé** : **Fragment de contenu**
- **Nom** : **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

Ajoutez un nouveau champ **Texte monoligne** sur la zone de travail et configurez le nouveau champ comme suit :

- **Libellé** : **ID d’intégration**
- **Nom** : **`aem_workfront_integration_id`**

Cliquez sur **Appliquer**.

![WF](./images/wfb15.png)

Vous devez maintenant configurer un second formulaire personnalisé. Cliquez sur **+ Nouveau formulaire personnalisé**.

![WF](./images/wfb10.png)

Sélectionnez **Tâche** et cliquez sur **Continuer**.

![WF](./images/wfb11.png)

Un formulaire personnalisé vide s’affiche alors. Saisissez le nom du formulaire `Preview & Publish URL`.

![WF](./images/wfb16.png)

Effectuez un glisser-déposer d’un nouveau champ **Texte monoligne** sur la zone de travail.

![WF](./images/wfb17.png)

Configurez le nouveau champ comme suit :

- **Libellé** : **URL de prévisualisation**
- **Nom** : **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

Ajoutez un nouveau champ **Texte monoligne** sur la zone de travail et configurez le nouveau champ comme suit :

- **Libellé** : **URL de publication**
- **Nom** : **`aem_workfront_integration_publish_url`**

Cliquez sur **Appliquer**.

![WF](./images/wfb19.png)

Vous devriez alors disposer de 2 formulaires personnalisés.

![WF](./images/wfb20.png)

Étape suivante : [1.2.2 Vérification avec Workfront](./ex2.md){target="_blank"}

Revenir à [Gestion des workflows avec Adobe Workfront](./workfront.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
