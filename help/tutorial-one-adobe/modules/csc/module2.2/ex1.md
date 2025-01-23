---
title: Prise en main de Workfront
description: Prise en main de Workfront
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 2%

---

# 2.2.1 Prise en main de Workfront

Connectez-vous à Adobe Workfront en allant sur [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Vous voyez alors ceci.

![WF](./images/wfb1.png)

## 2.2.1.1 Configurer votre intégration AEM Assets

Cliquez sur l’icône des 9 points **hamburger**, puis sélectionnez **Configuration**.

![WF](./images/wfb2.png)

Dans le menu de gauche, faites défiler l’écran jusqu’à **Documents** puis cliquez sur **Experience Manager Assets**.

![WF](./images/wfb3.png)

Cliquez sur **+ Ajouter une intégration Experience Manager**.

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

Votre intégration entre Workfront et AEM Assets CS est maintenant configurée.

![WF](./images/wfb7.png)

## 2.2.1.2 Configurer votre intégration AEM Sites

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

- **Libellé** : **URL Publish**
- **Nom** : **`aem_workfront_integration_publish_url`**

Cliquez sur **Appliquer**.

![WF](./images/wfb19.png)

Vous devriez alors disposer de 2 formulaires personnalisés.

![WF](./images/wfb20.png)

[Retour au module 2.2](./workfront.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
