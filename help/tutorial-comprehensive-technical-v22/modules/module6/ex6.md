---
title: CDP en temps réel - Audiences externes
description: CDP en temps réel - Audiences externes
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 38489c2b-69d4-4ddc-9a75-84bd54b4c823
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 2%

---

# 6.6 Audiences externes

Dans de nombreux cas, votre entreprise peut vouloir utiliser des segments existants provenant d’autres applications pour enrichir le profil client dans Adobe Experience Platform.
Ces audiences externes peuvent avoir été définies en fonction d’un modèle de science des données ou à l’aide de plateformes de données externes.

La fonctionnalité d&#39;audiences externes de Adobe Experience Platform vous permet de vous concentrer sur l&#39;ingestion des audiences externes et leur activation sans avoir à redéfinir en détail la définition de segment correspondante dans Adobe Experience Platform.

Le processus global se divise en trois grandes étapes :

- Importez les métadonnées d’audience externe : cette étape est destinée à ingérer dans Adobe Experience Platform les métadonnées d’audience externe, telles que le nom de l’audience.
- Attribuez l’appartenance d’audience externe au profil client : cette étape est destinée à enrichir le profil client avec l’attribut d’appartenance au segment externe.
- Créez les segments dans Adobe Experience Platform : cette étape est destinée à créer des segments exploitables en fonction de l’appartenance aux audiences externes.

## Métadonnées 6.6.1

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

>[!IMPORTANT]
>
>L’environnement de test à utiliser pour cet exercice est : ``--module2sandbox--``!

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--module2sandbox--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](./images/sb1.png)

Tandis que les données de segment définissent la condition pour qu’un profil fasse partie d’un segment, les métadonnées du segment sont des informations sur le segment telles que le nom, la description et l’état du segment. Les métadonnées d’audience externe étant stockées dans Adobe Experience Platform, vous devez utiliser un espace de noms d’identité pour ingérer les métadonnées dans Adobe Experience Platform.

## 6.6.1.1 Espace de noms d’identité pour les audiences externes

Un espace de noms d’identité a déjà été créé pour être utilisé avec **Audiences externes**.
Pour afficher l’identité qui a déjà été créée, accédez à **Identités** et recherchez **Externe**. Cliquez sur l’élément &quot;Audiences externes&quot;.

Remarque :

- Symbole de l’identité **externalaudiences** sera utilisé dans les étapes suivantes pour faire référence à l’identité des audiences externes.
- Le **Identifiant de non-personne** type est utilisé pour cet espace de noms d’identité, car cet espace de noms n’est pas destiné à identifier les profils clients mais les segments.

![Identité d’audiences externes](images/extAudIdNS.png)

## 6.6.1.2 Création du schéma de métadonnées Audiences externes

Les métadonnées des audiences externes sont basées sur la variable **Schéma de définition de segment**. Pour plus d’informations, reportez-vous à la section [Référentiel XDM Github](https://github.com/adobe/xdm/blob/master/docs/reference/classes/segmentdefinition.schema.md).

Dans le menu de gauche, accédez à Schémas. Cliquez sur **+ Créer un schéma** puis cliquez sur **Parcourir**.

![Schéma de métadonnées des audiences externes 1](images/extAudMDXDM1.png)

Pour attribuer une classe, recherchez **définition de segment**. Sélectionnez la **Définition de segment** et cliquez sur **Attribuer une classe**.

![Schéma de métadonnées Audiences externes 2](images/extAudMDXDM2.png)

Vous verrez alors ceci. Cliquez sur **Annuler**.

![Schéma de métadonnées Audiences externes 3](images/extAudMDXDM3.png)

Vous verrez alors ceci. Sélectionner le champ **_id**. Dans le menu de droite, faites défiler l’écran vers le bas et activez l’option **Identité** et le **Identité Principal** des cases à cocher. Sélectionnez la **Audiences externes** espace de noms d’identité. Cliquez sur **Appliquer**.

![Schéma de métadonnées d’audiences externes 4](images/extAudMDXDM4.png)

Sélectionnez ensuite le nom du schéma. **Schéma sans titre**. Remplacez le nom par `--demoProfileLdap-- - External Audiences Metadata`.

![Schéma de métadonnées d’audiences externes 5](images/extAudMDXDM5.png)

Activez la variable **Profil** basculez et confirmez. Enfin, cliquez sur **Enregistrer**.

![Schéma de métadonnées d’audiences externes 5](images/extAudMDXDM6.png)

## 6.6.1.3 Création du jeu de données de métadonnées Audiences externes

Dans **Schémas**, accédez à **Parcourir**. Recherchez et cliquez sur le bouton `--demoProfileLdap-- - External Audiences Metadata` schéma que vous avez créé à l’étape précédente. Cliquez ensuite sur **Création d’un jeu de données à partir d’un schéma**.

![Métadonnées d’audience externe DS 1](images/extAudMDDS1.png)

Pour le champ **Nom**, saisissez `--demoProfileLdap-- - External Audience Metadata`. Cliquez sur **Création d’un jeu de données**.

![Métadonnées d’audience externe DS 2](images/extAudMDDS2.png)

Vous verrez alors ceci. N’oubliez pas d’activer la variable **Profil** bascule !

![Métadonnées d’audience externe DS 3](images/extAudMDDS3.png)

## 6.6.1.4 Création d’une connexion à la source de l’API HTTP

Ensuite, vous devez configurer le connecteur source de l’API HTTP que vous utiliserez pour ingérer les métadonnées dans le jeu de données.

Accédez à **Sources**. Dans le champ de recherche, saisissez **HTTP**. Cliquez sur **Ajouter des données**.

![Métadonnées d’audience externe http 1](images/extAudMDhttp1.png)

Saisissez les informations suivantes :

- **Type de compte**: select **Nouveau compte**
- **Nom du compte**: enter `--demoProfileLdap-- - External Audience Metadata`
- Cochez la case . **Zone compatible XDM**

Cliquez ensuite sur **Connexion à la source**.

![Métadonnées d’audience externe http 2](images/extAudMDhttp2.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![Métadonnées d’audience externe http 2](images/extAudMDhttp2a.png)

Sélectionner **Jeu de données existant** et dans le menu déroulant, recherchez et sélectionnez le jeu de données. `--demoProfileLdap-- - External Audience Metadata`.

Vérifiez les **Détails du flux de données** puis cliquez sur **Suivant**.

![Métadonnées d’audience externe http 3](images/extAudMDhttp3.png)

Vous verrez alors ceci.

Le **Mappage** L’étape de l’assistant est vide car vous ingérez une payload compatible XDM dans le connecteur source de l’API HTTP. Aucun mappage n’est donc nécessaire. Cliquez sur **Suivant**.

![Métadonnées d’audience externe http 3](images/extAudMDhttp3a.png)

Dans le **Réviser** vous pouvez éventuellement consulter les détails de la connexion et du mappage. Cliquez sur **Terminer**.

![Métadonnées d’audience externe http 4](images/extAudMDhttp4.png)

Vous verrez alors ceci.

![Métadonnées d’audience externe http 4](images/extAudMDhttp4a.png)

## 6.6.1.5 Ingestion des métadonnées d’audience externe

Dans l’onglet Aperçu du connecteur source , cliquez sur **...** puis cliquez sur **Copie de la payload de schéma**.

![Métadonnées d’audiences externes str 1](images/extAudMDstr1a.png)

Ouvrez l’application de l’éditeur de texte sur votre ordinateur et collez la charge utile que vous venez de copier, qui ressemble à ceci. Ensuite, vous devez mettre à jour la variable **xdmEntity** dans cette payload.

![Métadonnées d’audiences externes str 1](images/extAudMDstr1b.png)

Objet **xdmEntity** doit être remplacé par le code ci-dessous. Copiez le code ci-dessous, puis collez-le dans votre fichier texte en remplaçant le **xdmEntity** dans l’éditeur de texte.

```
"xdmEntity": {
    "_id": "--demoProfileLdap---extaudience-01",
    "description": "--demoProfileLdap---extaudience-01 description",
    "segmentIdentity": {
      "_id": "--demoProfileLdap---extaudience-01",
      "namespace": {
        "code": "externalaudiences"
      }
    },
    "segmentName": "--demoProfileLdap---extaudience-01 name",
    "segmentStatus": "ACTIVE",
    "version": "1.0"
  }
```

Vous devriez alors voir ceci :

![Métadonnées d’audiences externes str 1](images/extAudMDstr1.png)

Ouvrez ensuite une nouvelle **Terminal** fenêtre. Copiez tout le texte de votre éditeur de texte et collez-le dans la fenêtre du terminal.

![Métadonnées d’audiences externes str 1](images/extAudMDstr1d.png)

Ensuite, appuyez sur **Entrée**.

Une confirmation de l’ingestion des données s’affiche alors dans la fenêtre Terminal :

![Métadonnées d’audiences externes str 1](images/extAudMDstr1e.png)

Actualisez l’écran du connecteur source de l’API HTTP, où vous verrez maintenant que les données sont en cours de traitement :

![Métadonnées d’audiences externes str 2](images/extAudMDstr2.png)

## 6.6.1.6 Validation de l’ingestion des métadonnées des audiences externes

Une fois le traitement terminé, vous pouvez vérifier la disponibilité des données dans le jeu de données à l’aide de Query Service.

Dans le menu de droite, accédez à **Jeux de données** et sélectionnez la variable `--demoProfileLdap-- - External Audience Metadata` jeu de données que vous avez créé précédemment.

![Métadonnées d’audiences externes str 3](images/extAudMDstr3.png)

Dans le menu de droite, accédez à Requêtes et cliquez sur **Créer une requête**.

![Métadonnées d’audiences externes str 4](images/extAudMDstr4.png)

Saisissez le code suivant, puis appuyez sur **MAJ + ENTRÉE**:

```
select * from --demoProfileLdap--_external_audience_metadata
```

Dans les résultats de la requête, vous verrez les métadonnées de l’audience externe que vous avez ingérées.

![Métadonnées d’audiences externes str 5](images/extAudMDstr5.png)

## 6.6.2 Adhésion au segment

Les métadonnées d’audience externe étant disponibles, vous pouvez désormais ingérer l’adhésion au segment pour un profil client spécifique.

Vous devez maintenant préparer un jeu de données de profil enrichi par rapport au schéma d’adhésion au segment. Pour plus d’informations, reportez-vous à la section [Référentiel XDM Github](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/segmentmembership.schema.md).

## 6.6.2.1 Création du schéma d’adhésion aux audiences externes

Dans le menu de droite, accédez à **Schémas**. Cliquez sur **Création d’un schéma** puis cliquez sur **XDM Individual Profile**.

![Schéma de profil d’audiences externes 1](images/extAudPrXDM1.png)

Dans le **Ajouter des groupes de champs** fenêtre contextuelle, rechercher **Core du profil**. Sélectionnez la **Profile Core v2** groupe de champs.

![Schéma de profil d’audiences externes 2](images/extAudPrXDM2.png)

Ensuite, dans le **Ajouter des groupes de champs** fenêtre contextuelle, rechercher **abonnement au segment**. Sélectionnez la **Détails de l’adhésion au segment** groupe de champs. Cliquez ensuite sur **Ajouter des groupes de champs**.

![Schéma de profil d’audiences externes 3](images/extAudPrXDM3.png)

Vous verrez alors ceci. Accédez au champ `--aepTenantId--.identification.core`. Cliquez sur le bouton **crmId** champ . Dans le menu de droite, faites défiler l’écran vers le bas et cochez la case **Identité** et le **Identité Principal** des cases à cocher. Pour le **Espace de noms d’identité** select **Système de démonstration - CRMID**.

Cliquez sur **Appliquer**.

![Schéma de profil d’audiences externes 4](images/extAudPrXDM4.png)

Sélectionnez ensuite le nom du schéma. **Schéma sans titre**. Dans le champ du nom d’affichage, saisissez `--demoProfileLdap-- - External Audiences Membership`.

![Schéma de profil d’audiences externes 5](images/extAudPrXDM5a.png)

Ensuite, activez la fonction **Profil** basculez et confirmez. Cliquez sur **Enregistrer**.

![Schéma de profil d’audiences externes 5](images/extAudPrXDM5.png)

## 6.6.2.2 Création du jeu de données d’adhésion aux audiences externes

Dans **Schémas**, accédez à **Parcourir**. Recherchez et cliquez sur le bouton `--demoProfileLdap-- - External Audiences Membership` schéma que vous avez créé à l’étape précédente. Cliquez ensuite sur **Création d’un jeu de données à partir d’un schéma**.

![Métadonnées d’audience externe DS 1](images/extAudPrDS1.png)

Pour le champ **Nom**, saisissez `--demoProfileLdap-- - External Audiences Membership`. Cliquez sur **Création d’un jeu de données**.

![Métadonnées d’audience externe DS 2](images/extAudPrDS2.png)

Vous verrez alors ceci. N’oubliez pas d’activer la variable **Profil** bascule !

![Métadonnées d’audience externe DS 3](images/extAudPrDS3.png)

## 6.6.2.3 Création d’une connexion source à l’API HTTP


Ensuite, vous devez configurer le connecteur source de l’API HTTP que vous utiliserez pour ingérer les métadonnées dans le jeu de données.

Accédez à **Sources**. Dans le champ de recherche, saisissez **HTTP**. Cliquez sur **Ajouter des données**.

![Métadonnées d’audience externe http 1](images/extAudMDhttp1.png)

Saisissez les informations suivantes :

- **Type de compte**: select **Nouveau compte**
- **Nom du compte**: enter `--demoProfileLdap-- - External Audience Membership`
- Cochez la case . **Zone compatible XDM**

Cliquez ensuite sur **Connexion à la source**.

![Métadonnées d’audience externe http 2](images/extAudPrhttp2.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![Métadonnées d’audience externe http 2](images/extAudPrhttp2a.png)

Sélectionner **Jeu de données existant** et dans le menu déroulant, recherchez et sélectionnez le jeu de données. `--demoProfileLdap-- - External Audiences Membership`.

Vérifiez les **Détails du flux de données** puis cliquez sur **Suivant**.

![Métadonnées d’audience externe http 3](images/extAudPrhttp3.png)

Vous verrez alors ceci.

Le **Mappage** L’étape de l’assistant est vide car vous ingérez une payload compatible XDM dans le connecteur source de l’API HTTP. Aucun mappage n’est donc nécessaire. Cliquez sur **Suivant**.

![Métadonnées d’audience externe http 3](images/extAudPrhttp3a.png)

Dans le **Réviser** vous pouvez éventuellement consulter les détails de la connexion et du mappage. Cliquez sur **Terminer**.

![Métadonnées d’audience externe http 4](images/extAudPrhttp4.png)

Vous verrez alors ceci.

![Métadonnées d’audience externe http 4](images/extAudPrhttp4a.png)

## 6.6.2.4 Ingestion des données d’adhésion d’audiences externes

Dans l’onglet Aperçu du connecteur source , cliquez sur **...** puis cliquez sur **Copie de la payload de schéma**.

![Métadonnées d’audiences externes str 1](./images/extAudPrstr1a.png)

Ouvrez l’application de l’éditeur de texte sur votre ordinateur et collez la charge utile que vous venez de copier, qui ressemble à ceci. Ensuite, vous devez mettre à jour la variable **xdmEntity** dans cette payload.

![Métadonnées d’audiences externes str 1](images/extAudPrstr1b.png)

Objet **xdmEntity** doit être remplacé par le code ci-dessous. Copiez le code ci-dessous, puis collez-le dans votre fichier texte en remplaçant le **xdmEntity** dans l’éditeur de texte.

```
  "xdmEntity": {
    "_id": "--demoProfileLdap---profile-test-01",
    "_experienceplatform": {
      "identification": {
        "core": {
          "crmId": "--demoProfileLdap---profile-test-01"
        }
      }
    },
    "personID": "--demoProfileLdap---profile-test-01",
    "segmentMembership": {
      "externalaudiences": {
        "--demoProfileLdap---extaudience-01": {
          "status": "realized",
          "lastQualificationTime": "2022-03-05T00:00:00Z"
        }
      }
    }
  }
```

Vous devriez alors voir ceci :

![Métadonnées d’audiences externes str 1](images/extAudPrstr1.png)

Ouvrez ensuite une nouvelle **Terminal** fenêtre. Copiez tout le texte de votre éditeur de texte et collez-le dans la fenêtre du terminal.

![Métadonnées d’audiences externes str 1](images/extAudPrstr1d.png)

Ensuite, appuyez sur **Entrée**.

Une confirmation de l’ingestion des données s’affiche alors dans la fenêtre Terminal :

![Métadonnées d’audiences externes str 1](images/extAudPrstr1e.png)

Actualisez l’écran du connecteur source de l’API HTTP, où, au bout de quelques minutes, vous verrez que les données sont en cours de traitement :

![Métadonnées d’audiences externes str 2](images/extAudPrstr2.png)

## 6.6.2.5 Validation de l’ingestion des membres d’audiences externes

Une fois le traitement terminé, vous pouvez vérifier la disponibilité des données dans le jeu de données à l’aide de Query Service.

Dans le menu de droite, accédez à **Jeux de données** et sélectionnez la variable `--demoProfileLdap-- - External Audiences Membership ` jeu de données que vous avez créé précédemment.

![Métadonnées d’audiences externes str 3](images/extAudPrstr3.png)

Dans le menu de droite, accédez à Requêtes et cliquez sur **Créer une requête**.

![Métadonnées d’audiences externes str 4](images/extAudPrstr4.png)

Saisissez le code suivant, puis appuyez sur **MAJ + ENTRÉE**:

```
select * from --demoProfileLdap--_external_audiences_membership
```

Dans les résultats de la requête, vous verrez les métadonnées de l’audience externe que vous avez ingérées.

![Métadonnées d’audiences externes str 5](images/extAudPrstr5.png)

## 6.6.3 Création d’un segment

Vous êtes maintenant prêt à agir sur les audiences externes.
Dans Adobe Experience Platform, l’action est réalisée en créant des segments, en renseignant les audiences respectives et en partageant ces audiences vers les destinations.
Vous allez maintenant créer un segment à l’aide de l’audience externe que vous venez de créer.

Dans le menu de gauche, accédez à **Segments** et cliquez sur **Créer un segment**.

![Audiences externes : SegBuilder 1](images/extAudSegUI2.png)

Accédez à **Audiences**. Vous verrez alors ceci. Cliquez sur **Audiences externes**.

![Audiences externes : SegBuilder 1](images/extAudSegUI2a.png)

Sélectionnez l’audience externe que vous avez créée précédemment, qui est nommée `--demoProfileLdap---extaudience-01`. Faites glisser l’audience sur la zone de travail.

![Audiences externes : SegBuilder 1](images/extAudSegUI2b.png)

Attribuez un nom à votre segment, utilisez `--demoProfileLdap-- - extaudience-01`. Cliquez sur **Enregistrer et fermer**.

![Audiences externes : SegBuilder 1](images/extAudSegUI1.png)

Vous verrez alors ceci. Vous remarquerez également que le profil pour lequel vous avez ingéré l’adhésion au segment s’affiche désormais dans la liste des **Exemples de profils**.

![Audiences externes : SegBuilder 1](images/extAudSegUI3.png)

Votre segment est maintenant prêt et peut être envoyé vers une destination pour activation.

## 6.6.4 Visualisation du profil client

Vous pouvez désormais également visualiser la qualification du segment sur votre profil client. Accédez à **Profils**, utilisez l’espace de noms d’identité **Système de démonstration - CRMID** et fournir l’identité `--demoProfileLdap---profile-test-01`, que vous avez utilisé dans le cadre de l’exercice 6.6.2.4, puis cliquez sur **Affichage**. Cliquez ensuite sur le **Identifiant de profil** pour ouvrir le profil.

![Audiences externes : SegBuilder 1](images/extAudProfileUI1.png)

Accédez à **abonnement au segment**, où s’affiche votre audience externe.

![Audiences externes : SegBuilder 1](images/extAudProfileUI2.png)

Étape suivante : [SDK de destinations 6.7](./ex7.md)

[Revenir au module 6](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
