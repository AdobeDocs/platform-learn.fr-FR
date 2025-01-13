---
title: Collecte de données - AEC - Configurer votre compte de Snowflake
description: Foundation - AEC - Configuration de votre compte de Snowflake
kt: 5342
doc-type: tutorial
exl-id: e72cdbfc-5b42-411f-9c63-e886776deabe
source-git-commit: d26d4735c92498d56beb7859ec67a0c3e174fc25
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# 3.1.1 Configuration de l’environnement de votre Snowflake

## 3.1.1.1 Créer votre compte

Accédez à [https://snowflake.com](https://snowflake.com). Cliquez sur **DÉMARRER GRATUITEMENT**.

![AAAA](./images/sf1.png)

Saisissez vos informations et cliquez sur **Continuer**.

![AAAA](./images/sf2.png)

Saisissez vos informations, choisissez votre fournisseur de cloud et cliquez sur **Commencer**.

![AAAA](./images/sf3.png)

Saisissez vos informations ou cliquez sur **Ignorer** (x2).

![AAAA](./images/sf4.png)

Tu verras ça. Vérifiez votre e-mail et cliquez sur l’e-mail de confirmation qui vous a été envoyé.

![AAAA](./images/sf5.png)

Cliquez sur le lien contenu dans l’e-mail de confirmation pour activer votre compte, définir votre nom d’utilisateur et votre mot de passe. Cliquez sur **Commencer**. Vous devrez utiliser ce nom d’utilisateur et ce mot de passe dans l’exercice suivant.

![AAAA](./images/sf6.png)

Vous serez alors connecté à Snowflake. Cliquez sur **Ignorer pour l’instant**.

![AAAA](./images/sf7.png)

## 3.1.1.2 Créer votre base de données

Accédez à **Données > Bases de données**. Cliquez sur **+ Base de données**.

![AAAA](./images/db1.png)

Utilisez le nom **CITISIGNAL** pour votre base de données. Cliquez sur **CRÉER**.

![AAAA](./images/db2.png)

## 3.1.1.3 Créer des tableaux

Vous pouvez maintenant commencer à créer vos tableaux dans Snowflake. Vous trouverez ci-dessous des scripts à exécuter pour créer vos tableaux.

### Table CK_PERSON

Cliquez sur **+ Créer**, puis sur **Tableau** et enfin sur **Standard**.

![AAAA](./images/tb1.png)

Tu verras ça. Copiez la requête ci-dessous et collez-la dans Snowflake. Veillez à sélectionner la base de données **CITISIGNAL** dans le coin supérieur gauche de votre écran avant de créer votre tableau.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_PERSONS (
	PERSON_ID NUMBER(38,0) NOT NULL,
	NAME VARCHAR(255),
	AGE NUMBER(38,0),
	EMAIL VARCHAR(255),
	PHONE_NUMBER VARCHAR(20),
	GENDER VARCHAR(10),
	OCCUPATION VARCHAR(100),
	ISATTMOBILESUB BOOLEAN,
	primary key (PERSON_ID)
);
```

Cliquez sur **Créer une table**.

![AAAA](./images/tb2.png)

Une fois le script exécuté, vous pouvez trouver votre table sous **Bases de données > CITISIGNAL > PUBLIC**.

![AAAA](./images/tb3.png)

### Table CK_HOUSEHOLDS

Cliquez sur **+ Créer**, puis sur **Tableau** et enfin sur **Standard**.

![AAAA](./images/tb1.png)

Tu verras ça. Copiez la requête ci-dessous et collez-la dans Snowflake. Veillez à sélectionner la base de données **CITISIGNAL** dans le coin supérieur gauche de votre écran avant de créer votre tableau.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_HOUSEHOLDS (
	HOUSEHOLD_ID NUMBER(38,0) NOT NULL,
	ADDRESS VARCHAR(255),
	CITY VARCHAR(100),
	STATE VARCHAR(50),
	POSTAL_CODE VARCHAR(20),
	COUNTRY VARCHAR(100),
	ISELIGIBLEFORFIBER BOOLEAN,
	PRIMARY_PERSON_ID NUMBER(38,0),
	ISFIBREENABLED BOOLEAN,
	primary key (HOUSEHOLD_ID)
);
```

Cliquez sur **Créer une table**.

![AAAA](./images/tb4.png)

Une fois le script exécuté, vous pouvez trouver votre table sous **Bases de données > CITISIGNAL > PUBLIC**.

![AAAA](./images/tb5.png)

### Table CK_USERS

Cliquez sur **+ Créer**, puis sur **Tableau** et enfin sur **Standard**.

![AAAA](./images/tb1.png)

Tu verras ça. Copiez la requête ci-dessous et collez-la dans Snowflake. Veillez à sélectionner la base de données **CITISIGNAL** dans le coin supérieur gauche de votre écran avant de créer votre tableau.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_USERS (
	USER_ID NUMBER(38,0) NOT NULL,
	PERSON_ID NUMBER(38,0),
	HOUSEHOLD_ID NUMBER(38,0),
	primary key (USER_ID),
	foreign key (PERSON_ID) references CITISIGNAL.PUBLIC.CK_PERSONS(PERSON_ID),
	foreign key (HOUSEHOLD_ID) references CITISIGNAL.PUBLIC.CK_HOUSEHOLDS(HOUSEHOLD_ID)
);
```

Cliquez sur **Créer une table**.

![AAAA](./images/tb6.png)

Une fois le script exécuté, vous pouvez trouver votre table sous **Bases de données > CITISIGNAL > PUBLIC**.

![AAAA](./images/tb7.png)

### Table CK_MONTHLY_DATA_USAGE

Cliquez sur **+ Créer**, puis sur **Tableau** et enfin sur **Standard**.

![AAAA](./images/tb1.png)

Tu verras ça. Copiez la requête ci-dessous et collez-la dans Snowflake. Veillez à sélectionner la base de données **CITISIGNAL** dans le coin supérieur gauche de votre écran avant de créer votre tableau.

```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MONTHLY_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	MONTH DATE,
	DATA_USAGE_GB NUMBER(10,2),
	primary key (USAGE_ID)
);
```

Cliquez sur **Créer une table**.

![AAAA](./images/tb8.png)

Une fois le script exécuté, vous pouvez trouver votre table sous **Bases de données > CITISIGNAL > PUBLIC**.

![AAAA](./images/tb9.png)

### Table CK_MOBILE_DATA_USAGE

Cliquez sur **+ Créer**, puis sur **Tableau** et enfin sur **Standard**.

![AAAA](./images/tb1.png)

Tu verras ça. Copiez la requête ci-dessous et collez-la dans Snowflake. Veillez à sélectionner la base de données **CITISIGNAL** dans le coin supérieur gauche de votre écran avant de créer votre tableau.


```sql
create or replace TABLE CITISIGNAL.PUBLIC.CK_MOBILE_DATA_USAGE (
	USAGE_ID NUMBER(38,0) NOT NULL autoincrement start 1 increment 1 noorder,
	USER_ID NUMBER(38,0),
	DATE DATE,
	TIME TIME(9),
	APP_NAME VARCHAR(255),
	DATA_USAGE_MB NUMBER(10,2),
	NETWORK_TYPE VARCHAR(50),
	DEVICE_TYPE VARCHAR(50),
	COUNTRY_CODE VARCHAR(10),
	primary key (USAGE_ID)
);
```

Cliquez sur **Créer une table**.

![AAAA](./images/tb10.png)

Une fois le script exécuté, vous pouvez trouver votre table sous **Bases de données > CITISIGNAL > PUBLIC**.

![AAAA](./images/tb11.png)

Toutes vos tables sont maintenant créées.


## 3.1.1.4 Ingérer des données d’exemple

Vous pouvez maintenant commencer à charger des données d’exemple dans votre base de données.

…

Vous avez maintenant terminé la configuration dans Snowflake.


Étape suivante : [3.1.2 Création de schémas, de modèles de données et de liens](./ex2.md)

[Retour au module 3.1](./fac.md)

[Revenir à tous les modules](../../../overview.md)
