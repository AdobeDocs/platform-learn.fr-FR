---
title: Foundation - Ingestion de données - Configuration des schémas et définition d’identifiants
description: Foundation - Ingestion de données - Configuration des schémas et définition d’identifiants
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 40a50618-ecbb-4ada-b1ca-90bcb2257ed6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3632'
ht-degree: 5%

---

# 2.2 Configuration de schémas et définition d’identifiants

Dans cet exercice, vous allez configurer les schémas XDM requis pour classer les informations de profil et le comportement des clients. Dans chaque schéma XDM, vous devrez également configurer un identifiant Principal pour lier toutes les informations.

## Histoire

Avant de commencer à configurer des schémas XDM et de définir des identifiants Principal, nous devons réfléchir au contexte d’entreprise de ce que nous essayons de faire :

- Vous voulez des données
- Vous souhaitez lier les données à un client
- Vous souhaitez créer un profil client en temps réel progressif

Il existe deux types de données que nous voulons capturer :

- Qui est ce client ?
- Que fait ce client ?

Cependant, la question **Qui est ce client ?** est une question très ouverte qui a de nombreuses réponses. Lorsque votre entreprise souhaite obtenir une réponse à cette question, vous recherchez des informations démographiques telles que le prénom, le nom et l’adresse. Mais également pour les coordonnées telles qu’une adresse électronique ou un numéro de téléphone mobile. Et aussi pour les informations liées à Langue, OptIn/OptOut et peut-être même les photos de profil. Et enfin, ce que vous avez vraiment besoin de savoir, c&#39;est comment nous allons identifier ce client dans les différents systèmes que votre entreprise utilise.

La même chose vaut pour la question. **Que fait ce client ?**. C&#39;est une question très ouverte avec de nombreuses réponses. Lorsque votre entreprise souhaite obtenir une réponse à cette question, vous recherchez toute interaction qu’un client a eue avec l’une de vos propriétés en ligne et hors ligne. Quelles pages ou quels produits ont été consultés ? Ce client a-t-il ajouté un produit à son panier ou a-t-il même acheté un article ? Quel périphérique et navigateur a été utilisé pour parcourir le site web ? Quel type d’informations ce client recherche-t-il et comment pouvons-nous l’utiliser pour configurer et offrir une expérience agréable à ce client ? Et enfin, ce que nous avons vraiment besoin de savoir, c&#39;est comment nous allons identifier ce client dans les différents systèmes que votre entreprise va utiliser.

## 2.1.1 - Qui est ce client

Capturer la réponse à **Qui est ce client ?** pour votre société, effectuez cette opération via la page Connexion/Enregistrement .

![Ingestion des données](./images/pv10.png)

Du point de vue des schémas, nous considérons ceci comme une **Classe**. La question : **Qui est ce client ?** est quelque chose que nous définissons dans la classe **[!UICONTROL XDM Individual Profile]**.

Ainsi, lorsque vous créez un schéma XDM pour capturer la réponse à **Qui est ce client ?**, tout d’abord, vous devez créer et définir 1 schéma qui référence la classe **[!UICONTROL XDM Individual Profile]**.

Pour spécifier le type de réponse à donner à cette question, vous devez définir [!UICONTROL Groupes de champs]. [!UICONTROL Groupes de champs] sont des extensions de la classe Profile et ont des configurations très spécifiques. Par exemple, les informations démographiques telles que Prénom, Nom, Genre et Anniversaire font partie des [!UICONTROL Groupe de champs]: **[!UICONTROL Détails démographiques]**.

Deuxièmement, votre entreprise doit décider comment identifier ce client. Dans le cas de votre société, l’identifiant principal d’un client connu peut être un identifiant de client spécifique, comme une adresse électronique. Mais techniquement, il existe d&#39;autres moyens d&#39;identifier un client dans votre entreprise, comme utiliser un numéro de téléphone portable.
Dans ce laboratoire, nous définirons l&#39;adresse email comme identifiant Principal et le numéro de téléphone comme identifiant secondaire.

Enfin, il est important de distinguer le canal sur lequel les données ont été capturées. Dans ce cas, nous parlerons des abonnements au site web et le schéma qui doit être défini doit refléter **where** les données d’enregistrement ont été capturées. Le canal aura également un rôle important à jouer pour influencer les données capturées. Il est donc recommandé de définir des schémas pour chaque combinaison de canal, d’identifiant Principal et de type de données collectées.

En fonction de ce qui précède, vous devez configurer un schéma dans Adobe Experience Platform.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--module2sandbox--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./images/sb1.png)

Dans Adobe Experience Platform, cliquez sur **[!UICONTROL Schémas]** dans le menu du côté gauche de l’écran. Vous verrez la liste des [!UICONTROL Schémas].

![Ingestion des données](./images/menuschemas.png)

Vous devez créer un nouveau schéma. Pour créer un nouveau schéma, cliquez sur le bouton **[!UICONTROL + Créer un schéma]** et sélectionnez **[!UICONTROL XDM Individual Profile]**.

![Ingestion des données](./images/createschema.png)

Après avoir cliqué sur le bouton **[!UICONTROL + Créer un schéma]** , un nouveau schéma est créé et vous serez invité à sélectionner ou à créer **groupes de champs**.

![Ingestion des données](./images/emptyschema.png)

Vous devez maintenant définir la réponse à la question. **Qui est ce client ?** devrait ressembler à ça.
Dans l’introduction de ce laboratoire, nous avons noté la nécessité d’utiliser les attributs suivants pour définir un client :

- Informations démographiques telles que le prénom, le nom et l’adresse
- Coordonnées telles qu’une adresse de domicile, une adresse électronique ou un numéro de téléphone mobile
- Autres informations liées à Langue, OptIn/OptOut et peut-être même les images de profil.
- Identifiant Principal d’un client

Pour que ces informations fassent partie de votre schéma, vous devez ajouter les éléments suivants : [!UICONTROL Groupes de champs] à votre schéma :

- Détails démographiques (informations démographiques)
- Coordonnées personnelles (coordonnées)
- Détails des préférences (autres informations)
- Groupe de champs d’identification de profil personnalisé de votre entreprise (identifiants Principal et Secondaires)

Dans le **[!UICONTROL Ajouter un groupe de champs]** sélectionnez l’écran [!UICONTROL Groupe de champs] **[!UICONTROL Détails démographiques]**, **[!UICONTROL Détails du contact personnel]** et **[!UICONTROL Détails des préférences]**.

![Ingestion des données](./images/ppfd.png)

Cliquez sur le bouton **[!UICONTROL Ajout de groupes de champs]** pour ajouter le bouton [!UICONTROL Groupe de champs] à votre schéma.

![Ingestion des données](./images/addmixin1.png)

Vous allez maintenant avoir ceci :

![Ingestion des données](./images/schemathis.png)

Ensuite, vous avez besoin d’une nouvelle [!UICONTROL Groupe de champs] pour capturer la variable **[!UICONTROL Identifiant]** utilisé pour la collecte de données. Comme vous l’avez vu dans l’exercice précédent, il y a un concept d’identifiants Principal et Secondaires. Un identifiant Principal est le plus important, car toutes les données collectées seront liées à cet identifiant.

Vous allez maintenant créer votre propre [!UICONTROL Groupe de champs] et par conséquent, vous allez étendre la variable [!UICONTROL Schéma XDM] pour répondre aux exigences de votre propre entreprise.

Cliquez sur le bouton **[!UICONTROL + Ajouter]** pour commencer à ajouter un [!UICONTROL Groupe de champs].

![Ingestion des données](./images/addmixin2.png)

Au lieu de réutiliser une [!UICONTROL Groupe de champs], vous allez maintenant créer les vôtres [!UICONTROL Groupe de champs]. Pour ce faire, sélectionnez **[!UICONTROL Créer un groupe de champs]**.

![Ingestion des données](./images/createmixin.png)

Vous devez maintenant fournir un **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour votre nouveau [!UICONTROL Groupe de champs].

Pour le nom de notre schéma, nous utiliserons ceci :
`--demoProfileLdap-- - Profile Identification Field Group`

Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Groupe de champs d’identification du profil]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/mixinname.png)

Cliquez sur le bouton **[!UICONTROL Ajout de groupes de champs]** pour ajouter le bouton nouvellement créé [!UICONTROL Groupe de champs] à votre schéma.

![Ingestion des données](./images/addmixin1.png)

Cette structure de schéma devrait maintenant être en place.

![Ingestion des données](./images/schemastructurem.png)

Votre nouveau [!UICONTROL Groupe de champs] est toujours vide. Vous devrez donc ajouter des champs à ce champ. [!UICONTROL Groupe de champs].
Dans le [!UICONTROL Groupe de champs]-list, cliquez sur votre [!UICONTROL Groupe de champs].

![Ingestion des données](./images/schemastructurem.png)

Plusieurs nouveaux boutons s’affichent désormais.

Au niveau supérieur de votre schéma, cliquez sur le **[!UICONTROL + Ajouter un champ]** bouton .

![Ingestion des données](./images/clickaddfield.png)

Après avoir cliqué sur le bouton **[!UICONTROL + Ajouter un champ]** , un nouveau bouton s’affiche. **[!UICONTROL objet]** dans votre schéma. Cet objet représente une **[!UICONTROL objet]** dans votre schéma et porte le nom de votre identifiant de tenant Adobe Experience Platform. Votre identifiant de client Adobe Experience Platform est `--aepTenantId--`.

![Ingestion des données](./images/tenant.png)

Vous allez maintenant ajouter un nouvel objet sous ce client. Pour cela, cliquez sur le champ **[!UICONTROL Nouveau champ]** sous l’objet client.

![Ingestion des données](./images/tenantfield.png)

Utilisez les définitions d’objet suivantes :

- Nom du champ : **[!UICONTROL identification]**
- Nom d’affichage :  **[!UICONTROL identification]**
- Type : **[!UICONTROL Objet]**

![Ingestion des données](./images/tenantfielddef.png)

Cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

![Ingestion des données](./images/apply.png)

Après avoir cliqué sur **[!UICONTROL Appliquer]**, vous voyez maintenant votre **[!UICONTROL identification]** dans le schéma.

![Ingestion des données](./images/schemaid.png)

Vous allez maintenant ajouter 3 nouveaux champs sous le  **[!UICONTROL identification]** objet :

- ecid :
   - Nom du champ : **[!UICONTROL ecid]**
   - Nom d’affichage :  **[!UICONTROL ecid]**
   - Type :**[!UICONTROL chaîne]**

- emailId
   - Nom du champ : **[!UICONTROL emailId]**
   - Nom d’affichage :  **[!UICONTROL emailId]**
   - Type :**[!UICONTROL chaîne]**

- mobilenr
   - Nom du champ : **[!UICONTROL mobilenr]**
   - Nom d’affichage :  **[!UICONTROL mobilenr]**
   - Type :**[!UICONTROL chaîne]**

Chaque champ est défini comme type **[!UICONTROL Chaîne]** et nous configurerons ces champs en tant que **[!UICONTROL Identités]**. Pour le schéma **[!UICONTROL Schéma d’enregistrement de site web]**, nous supposons qu’un client sera toujours identifié par son adresse électronique, ce qui signifie que vous devez configurer le champ . **[!UICONTROL emailId]** as a **[!UICONTROL Principal]** et les autres champs comme **[!UICONTROL Secondaire]** identifiants.

Pour ajouter les champs, cliquez sur le bouton **[!UICONTROL +]** en regard du bouton **[!UICONTROL identification]** .

![Ingestion des données](./images/schemaid2.png)

Vous avez maintenant un champ vide. Vous devez configurer les 3 champs ci-dessus comme indiqué.

![Ingestion des données](./images/emptyfield.png)

Voici comment chaque champ doit s’occuper de votre configuration initiale de champ.

Cliquez sur le bouton **[!UICONTROL +]** en regard du bouton **[!UICONTROL identification]** pour créer un champ et remplir les champs comme indiqué.

- ecid

![Ingestion des données](./images/ecidfield.png)

Pour enregistrer votre champ, faites défiler l’écran vers le bas de la **[!UICONTROL Propriétés du champ]** jusqu’à ce que le bouton s’affiche **[!UICONTROL Appliquer]**. Cliquez sur le bouton **[!UICONTROL Appliquer]** bouton .

![Ingestion des données](./images/apply.png)

Cliquez sur le bouton **[!UICONTROL +]** en regard du bouton **[!UICONTROL identification]** pour créer un champ et remplir les champs comme indiqué.

- emailId

![Ingestion des données](./images/emailidfield.png)

Pour enregistrer votre champ, faites défiler l’écran vers le bas de la **[!UICONTROL Propriétés du champ]** jusqu’à ce que le bouton s’affiche **[!UICONTROL Appliquer]**. Cliquez sur le bouton **[!UICONTROL Appliquer]** bouton .

![Ingestion des données](./images/apply.png)

Cliquez sur le bouton **[!UICONTROL +]** en regard du bouton **[!UICONTROL identification]** pour créer un champ et remplir les champs comme indiqué.

- mobilenr

![Ingestion des données](./images/mobilenrfield.png)

Pour enregistrer votre champ, faites défiler l’écran vers le bas de la **[!UICONTROL Propriétés du champ]** jusqu’à ce que le bouton s’affiche **[!UICONTROL Appliquer]**. Cliquez sur le bouton **[!UICONTROL Appliquer]** bouton .

![Ingestion des données](./images/apply.png)

Vous disposez désormais de 3 champs, mais ceux-ci n’ont pas été définis comme **[!UICONTROL Identité]**-fields encore.

![Ingestion des données](./images/3fields.png)

Pour commencer à définir ces champs comme **[!UICONTROL Identité]**-fields, procédez comme suit :

- Sélectionner le champ **[!UICONTROL emailId]**.
- Sur le côté droit, dans les propriétés du champ, faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **[!UICONTROL Identité]**. Cochez la case correspondant à **[!UICONTROL Identité]**.

   ![Ingestion des données](./images/emailidid.png)

- Cochez maintenant la case pour **[!UICONTROL Identité Principal]**.

   ![Ingestion des données](./images/emailidprimid.png)

- Enfin, sélectionnez l’espace de noms **[!UICONTROL Email]** de la liste de **[!UICONTROL Espaces de noms]**. Un espace de noms est utilisé par le graphique d’identités de Adobe Experience Platform pour classer les identifiants dans les espaces de noms et définir la relation entre ces espaces de noms.

   ![Ingestion des données](./images/emailidprimidns.png)

- Enfin, cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

   ![Ingestion des données](./images/apply.png)

Ensuite, vous devez définir les autres champs pour **[!UICONTROL ecid]** et **[!UICONTROL mobilenr]** comme identifiants secondaires.

- Sélectionner le champ **[!UICONTROL ecid]**.
- Sur le côté droit, dans les propriétés du champ, faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **[!UICONTROL Identité]**. Cochez la case correspondant à **[!UICONTROL Identité]**.

   ![Ingestion des données](./images/ecidid.png)

- Sélectionnez ensuite l’espace de noms **[!UICONTROL ECID]** de la liste de **[!UICONTROL Espaces de noms]**. A [!UICONTROL Espace de noms] est utilisé par le graphique d’identités dans Adobe Experience Platform pour classer les identifiants dans les espaces de noms et définir la relation entre ces espaces de noms.

   ![Ingestion des données](./images/ecidprimidns.png)

- Cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

   ![Ingestion des données](./images/apply.png)

- Sélectionner le champ **[!UICONTROL mobilenr]**.
- Sur le côté droit, dans les propriétés du champ, faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **[!UICONTROL Identité]**. Cochez la case correspondant à **[!UICONTROL Identité]**.

   ![Ingestion des données](./images/mobid.png)

- Veillez à sélectionner l’espace de noms **[!UICONTROL Téléphone]** de la liste de **[!UICONTROL Espaces de noms]**. Un espace de noms est utilisé par le graphique d’identités de Adobe Experience Platform pour classer les identifiants dans les espaces de noms et définir la relation entre ces espaces de noms.

   ![Ingestion des données](./images/mobprimidns.png)

- Cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

   ![Ingestion des données](./images/apply.png)

Le **[!UICONTROL identification]** doit maintenant ressembler à ceci, avec les 3 champs id qui affichent également un **[!UICONTROL empreinte digitale]** pour indiquer qu’elles ont été définies comme identifiants.

![Ingestion des données](./images/applyiden.png)

Attribuons maintenant un nom à votre schéma. Sélectionner le champ **Schéma sans titre**.

![Ingestion des données](./images/schemaname1.png)

Pour le nom de notre schéma, vous utiliserez ceci :

`--demoProfileLdap-- - Demo System - Profile Schema for Website`

Remplacer **[!UICONTROL ldap]** par votre ldap spécifique. Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Système de démonstration - Schéma de profil pour le site web]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/schemaname.png)

Vous avez maintenant défini un schéma, lié existant et nouvellement créé. [!UICONTROL Groupes de champs] et ont défini des identifiants.

Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer vos modifications.

![Ingestion des données](./images/save.png)

La dernière chose à faire ici est d’activer le schéma à lier à la variable **[!UICONTROL Profil]**.
En activant votre schéma pour Profile, vous vous assurez que toutes les données envoyées à Adobe Experience Platform par rapport à ce schéma feront partie de l’environnement Real-time Customer Profile, qui garantit que toutes ces données peuvent être utilisées en temps réel pour l’interrogation, la segmentation et l’activation.

Pour ce faire, sélectionnez le nom de votre schéma.

![Ingestion des données](./images/schemastructure.png)

Dans l’onglet droit de votre schéma, un **[!UICONTROL Bascule des profils]**, actuellement désactivé.

![Ingestion des données](./images/upswitcher.png)

Activez la variable [!UICONTROL Profil] - basculez en cliquant dessus.

Ce message s’affiche :

![Ingestion des données](./images/sure.png)

Cliquez sur **[!UICONTROL Activer]** pour activer ce schéma pour Profile.

Votre schéma est maintenant configuré pour faire partie de la [!UICONTROL Real-time Customer Profile].

![Ingestion des données](./images/surey.png)

Enfin, cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer votre schéma.

![Ingestion des données](./images/save.png)

### 2.1.2 - Que fait ce client

Capture de la réponse à la question **Que fait ce client ?** pour votre entreprise, par exemple, une consultation de produit est effectuée sur une page de produits.

![Ingestion des données](./images/pv7.png)

Du point de vue du schéma, nous considérons ceci comme une **[!UICONTROL Classe]**. La question : **Que fait ce client ?** est quelque chose que nous avons défini dans la classe **[!UICONTROL ExperienceEvent]**.

Ainsi, lorsque vous créez une [!UICONTROL Schéma XDM] pour capturer la réponse à **Que fait ce client ?**, tout d’abord, vous devez créer et définir 1 schéma qui référence la classe **[!UICONTROL ExperienceEvent]**.

Pour spécifier le type de réponse à donner à cette question, vous devez définir [!UICONTROL Groupe de champs]. [!UICONTROL Groupes de champs] sont des extensions de la variable [!UICONTROL ExperienceEvent]-class et possèdent des configurations très spécifiques. Par exemple, les informations sur le type de produits qu’un client a consulté ou ajouté à son panier font partie de la variable [!UICONTROL Groupe de champs] **Détails du commerce**.

Deuxièmement, votre entreprise doit décider comment vous identifierez le comportement de ce client. Puisque nous parlons d’interactions sur un site web, il est possible que votre entreprise connaisse le client, mais il est tout aussi possible qu’un visiteur anonyme inconnu soit principal sur le site web. Nous ne pouvons donc pas utiliser d&#39;identifiant comme adresse email. Dans ce cas, votre société décidera probablement d’utiliser la variable [!UICONTROL Identifiant Experience Cloud (ECID)] comme identifiant Principal.

Enfin, il est important de distinguer le canal sur lequel les données ont été capturées. Dans ce cas, nous parlerons des interactions avec les sites web et le schéma qui doit être défini doit être reflété. **where** les données d’interaction ont été capturées. Le canal aura également un rôle important à jouer pour influencer les données capturées. Il est donc recommandé de définir des schémas pour chaque combinaison de canal, d’identifiant Principal et de type de données collectées.

En fonction de ce qui précède, vous devez configurer un schéma dans Adobe Experience Platform.

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **[!UICONTROL sandbox]**. Le [!UICONTROL sandbox] pour sélectionner est nommé ``--module2sandbox--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./images/sb1.png)

Dans Adobe Experience Platform, cliquez sur **[!UICONTROL Schémas]** dans le menu du côté gauche de l’écran.

![Ingestion des données](./images/menuschemas.png)

Dans [!UICONTROL Schémas], vous verrez tous les schémas existants.

![Ingestion des données](./images/schemasee.png)

Vous devez créer un nouveau schéma. Pour créer un nouveau schéma, cliquez sur le bouton **[!UICONTROL + Créer un schéma]** et sélectionnez **[!UICONTROL XDM ExperienceEvent]**.

![Ingestion des données](./images/createschema1.png)

Après avoir cliqué sur le bouton **[!UICONTROL + Créer un schéma]** , un nouveau schéma est créé et vous serez invité à sélectionner ou à créer **groupes de champs**.

![Ingestion des données](./images/emptyschemaee.png)

Vous devez maintenant définir la réponse à la question. **Que fait ce client ?** devrait ressembler à ça.
Dans l’introduction de ce laboratoire, nous avons noté la nécessité d’utiliser les attributs suivants pour définir ce qu’un client fait :

- Quelles pages ou quels produits ont été consultés ?
- Ce client a-t-il ajouté un produit à son panier ou a-t-il même acheté un article ?
- Quel périphérique et navigateur a été utilisé pour parcourir le site web ?
- Quel type d’informations ce client recherche-t-il et comment pouvons-nous l’utiliser pour configurer et offrir une expérience agréable à ce client ?
- Identifiant Principal d’un client


Pour que ces informations fassent partie de votre schéma, vous devez ajouter les éléments suivants : [!UICONTROL Groupe de champs] à votre schéma :

- Informations web
- Informations commerciales
- Informations sur l’environnement
- identification personnalisée du profil de votre entreprise [!UICONTROL Groupe de champs] (Identifiants Principal et Secondaire)

Dans le **[!UICONTROL Ajouter un groupe de champs]** sélectionnez l’écran [!UICONTROL Groupes de champs] **[!UICONTROL Détails web]**, **[!UICONTROL Détails du commerce]** et **[!UICONTROL Détails de l’environnement]**.

![Ingestion des données](./images/eeed.png)

Cliquez sur le bouton **[!UICONTROL Ajout de groupes de champs]** pour ajouter le groupe de champs à votre schéma.

![Ingestion des données](./images/addmixin1.png)

Vous obtiendrez alors ce qui suit :

![Ingestion des données](./images/eethis.png)

Ensuite, vous devez créer une [!UICONTROL Groupe de champs] pour capturer la variable **[!UICONTROL Identifiant]** utilisé pour la collecte de données. Comme vous l’avez vu dans l’exercice précédent, il y a un concept d’identifiants Principal et Secondaires. Un identifiant Principal est le plus important, car toutes les données collectées seront liées à cet identifiant.

Vous allez maintenant créer votre propre [!UICONTROL Groupe de champs] et, en tant que tel, vous allez étendre la variable [!UICONTROL Schéma XDM] pour répondre aux exigences de votre propre entreprise.

A [!UICONTROL Groupe de champs] est lié à un [!UICONTROL Classe], ce qui signifie que vous ne pouvez pas simplement réutiliser les [!UICONTROL Groupe de champs].

Cliquez sur le bouton **[!UICONTROL + Ajouter]** pour commencer à ajouter un [!UICONTROL Groupe de champs].

![Ingestion des données](./images/addmixinee2.png)

Au lieu de réutiliser une [!UICONTROL Groupe de champs], vous allez maintenant créer les vôtres [!UICONTROL Groupe de champs]. Pour ce faire, sélectionnez **[!UICONTROL Créer un groupe de champs]**.

![Ingestion des données](./images/createmixin.png)

Vous devez maintenant fournir un **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour votre nouveau groupe de champs.

Pour le nom de votre groupe de champs, utilisez ceci :

`--demoProfileLdap-- - ExperienceEvent Identification Field Group`

Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Groupe de champs d’identification ExperienceEvent]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/mixinnameee.png)

Cliquez sur le bouton **[!UICONTROL Ajouter un groupe de champs]** pour ajouter le bouton nouvellement créé [!UICONTROL Groupe de champs] à votre schéma.

![Ingestion des données](./images/addmixin1.png)

Vous devriez maintenant disposer de [!UICONTROL Schéma] structure en place.

![Ingestion des données](./images/schemastructuremee.png)

Votre nouveau [!UICONTROL Groupe de champs] est toujours vide. Vous devrez donc ajouter des champs à ce groupe de champs.
Dans le [!UICONTROL Groupe de champs]-list, cliquez sur votre [!UICONTROL Groupe de champs].

![Ingestion des données](./images/schemastructuremee1.png)

Plusieurs nouveaux boutons s’affichent désormais.

Sur le niveau supérieur de votre schéma, en regard de votre schéma - nom, cliquez sur le bouton **[!UICONTROL +]** bouton .

![Ingestion des données](./images/clickaddfieldee.png)

Après avoir cliqué sur le bouton **[!UICONTROL +]** , un nouveau bouton s’affiche. **[!UICONTROL objet]** dans votre schéma. Cet objet représente une **[!UICONTROL objet]** dans votre [!UICONTROL Schéma] et porte le nom de votre ID de tenant Adobe Experience Platform. Votre identifiant de client Adobe Experience Platform est `--aepTenantId--`.

![Ingestion des données](./images/tenantee.png)

Vous allez maintenant ajouter un nouvel objet sous ce client. Pour cela, cliquez sur le champ **[!UICONTROL Nouveau champ]** sous l’objet client.

![Ingestion des données](./images/tenantfieldee.png)

Utilisez les définitions d’objet suivantes :

- Nom du champ : **[!UICONTROL identification]**
- Nom d’affichage :  **[!UICONTROL identification]**
- Type : **[!UICONTROL Objet]**

![Ingestion des données](./images/tenantfielddefee.png)

Faites défiler la page vers le bas et cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

![Ingestion des données](./images/apply.png)

Après avoir cliqué sur **[!UICONTROL Appliquer]**, vous voyez maintenant votre **[!UICONTROL identification]** dans le schéma.

![Ingestion des données](./images/schemaidee.png)

Vous allez maintenant ajouter 1 nouveau champ sous le  **[!UICONTROL identification]** .

Cliquez sur le bouton **[!UICONTROL +]** en regard du bouton **[!UICONTROL identification]** pour créer un champ.

![Ingestion des données](./images/schemaideeplus.png)

Le champ ECID sera défini comme type **[!UICONTROL Chaîne]** et vous allez configurer ce champ en tant que **[!UICONTROL Identité]**. Pour le schéma **[!UICONTROL Système de démonstration - Schéma d’événement pour le site web]**, nous supposons qu’un client sera toujours identifié par son [!UICONTROL ECID], ce qui signifie que vous devez configurer le champ . **[!UICONTROL ECID]** as a **Principal** identifier

Vous avez maintenant un champ vide. Vous devez configurer le champ ci-dessus comme indiqué.

- ecid :

   - Nom du champ : **[!UICONTROL ecid]**
   - Nom d’affichage :  **[!UICONTROL ecid]**
   - Type :**[!UICONTROL chaîne]**

Voici comment la variable [!UICONTROL ecid]-field doit s’occuper de la configuration initiale de votre champ :

![Ingestion des données](./images/ecidfieldee.png)

Faites défiler la page vers le bas et cliquez sur **[!UICONTROL Appliquer]**.

![Ingestion des données](./images/apply.png)

Vous disposez désormais d’un nouveau champ, mais celui-ci n’a pas été défini comme une **[!UICONTROL Identité]**-field encore.

![Ingestion des données](./images/3fieldsee.png)

Pour commencer à définir ces champs comme **[!UICONTROL Identité]**-fields, procédez comme suit :

- Sélectionner le champ **[!UICONTROL ecid]**.
- Sur le côté droit, dans les propriétés du champ, faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **[!UICONTROL Identité]**. Cochez la case correspondant à **[!UICONTROL Identité]**.

![Ingestion des données](./images/ecididee.png)

- Cochez maintenant la case pour **[!UICONTROL Identité Principal]**.

![Ingestion des données](./images/ecidprimidee.png)

- Enfin, sélectionnez l’espace de noms **[!UICONTROL ECID]** de la liste de **[!UICONTROL Espaces de noms]**. A [!UICONTROL Espace de noms] est utilisé par la variable [!UICONTROL Graphique d’identités] dans Adobe Experience Platform pour classer les identifiants dans les espaces de noms et définir la relation entre ces espaces de noms.

   ![Ingestion des données](./images/ecidprimidnsee.png)

- Enfin, cliquez sur **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

   ![Ingestion des données](./images/apply.png)

Le **[!UICONTROL identification]** doit maintenant ressembler à ceci, avec le champ ecid qui affiche désormais également une **empreinte digitale** pour indiquer qu’elles ont été définies comme identifiants.

![Ingestion des données](./images/applyidenee.png)

Attribuons maintenant un nom à votre schéma. Sélectionner le champ **Schéma sans titre**.

![Ingestion des données](./images/schemaname1ee.png)

Pour le nom de notre schéma, nous utiliserons ceci :
`--demoProfileLdap-- - Demo System - Event Schema for Website`

Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Système de démonstration - Schéma d’événement pour le site web]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/schemanameee.png)

Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer vos modifications.

![Ingestion des données](./images/save.png)

Il est important de noter que lors de l’ingestion finale de données par rapport à ce schéma, certains champs sont obligatoires.
Par exemple, les champs **[!UICONTROL _id]** et **[!UICONTROL timestamp]** sont des champs obligatoires.

- _id doit contenir un identifiant unique pour une ingestion de données spécifique.
- l’horodatage doit être l’horodatage de cet accès, au format **[!UICONTROL &quot;AAAA-MM-JJTHH:MM:SSSZ&quot;]**, par exemple : **[!UICONTROL &quot;2019-04-08T07:20:000Z&quot;]**

Vous avez maintenant défini un schéma, lié existant et nouvellement créé. [!UICONTROL Groupes de champs] et ont défini des identifiants.

La dernière chose à faire ici est d’activer le schéma à lier à la variable **[!UICONTROL Profil]**.
En activant votre schéma pour [!UICONTROL Profil], vous vous assurez que toutes les données envoyées à Adobe Experience Platform par rapport à ce schéma feront partie de Real-time Customer Profile, qui s’assure que toutes ces données peuvent être utilisées en temps réel pour l’interrogation, la segmentation et l’activation.

Pour ce faire, sélectionnez le nom de votre schéma.

![Ingestion des données](./images/schemastructureeee.png)

Dans l’onglet droit de votre schéma, un **[!UICONTROL Profil] basculer**, actuellement désactivé.

![Ingestion des données](./images/upswitcheree.png)

Activez la variable [!UICONTROL Profil] - basculez en cliquant dessus.

Ce message s’affiche :

![Ingestion des données](./images/sure.png)

Cliquez sur **[!UICONTROL Activer]** pour activer ce schéma pour Profile.

Votre schéma est maintenant configuré pour faire partie de Real-time Customer Profile.

![Ingestion des données](./images/surey.png)

Enfin, cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer votre schéma.

![Ingestion des données](./images/save.png)

Vous avez maintenant terminé de créer des schémas qui sont activés pour être utilisés dans Real-time Customer Profile.

Regardons les jeux de données dans le prochain exercice.

Étape suivante : [2.3 Configuration de jeux de données](./ex3.md)

[Revenir au module 2](./data-ingestion.md)

[Revenir à tous les modules](../../overview.md)
