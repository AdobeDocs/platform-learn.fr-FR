---
title: Collecte de données - AEC - Créer une composition fédérée
description: Foundation - AEC - Créer une composition fédérée
kt: 5342
doc-type: tutorial
exl-id: 6c1773d1-ca2e-43e5-bfa7-6e5e0fbcf859
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---

# 1.3.3 Créer une composition fédérée

Vous pouvez désormais configurer la composition de votre audience fédérée dans AEP.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../dc1.2/images/sb1.png)

## 1.3.3.1 Créer votre audience

Dans le menu de gauche, accédez à **Audiences** puis à **Compositions fédérées**. Cliquez sur **Créer une composition**.

![AAAA](./images/fedcomp1.png)

Pour l’étiquette, utilisez la commande suivante : `--aepUserLdap-- - CitiSignal Fiber`. Sélectionnez le modèle de données que vous avez créé dans l’exercice précédent, qui est nommé `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Cliquez sur **Créer**.

![AAAA](./images/fedcomp2.png)

Tu verras ça.

![AAAA](./images/fedcomp3.png)

Cliquez sur l’icône **+**, puis sur **Créer une audience**.

![AAAA](./images/fedcomp4.png)

Tu verras ça. Sélectionnez **Créer une audience**. Cliquez sur l’icône **rechercher** pour sélectionner un schéma.

![AAAA](./images/fedcomp5.png)

Sélectionnez le schéma **—aepUserLdap—_HOUSEHOLDS**. Cliquez sur **Confirmer**.

![AAAA](./images/fedcomp6.png)

Cliquez ensuite sur **Continuer**.

![AAAA](./images/fedcomp7.png)

Vous pouvez maintenant commencer à créer la requête qui sera envoyée à Snowflake. Cliquez sur l’icône **+**, puis sur **Condition personnalisée**.

![AAAA](./images/fedcomp8.png)

Sélectionnez l’attribut **ISELIGIBLEFORFIBER** puis cliquez sur **Confirmer**.

![AAAA](./images/fedcomp9.png)

Tu verras ça. Définissez le champ **Valeur** sur **Vrai**. Cliquez sur **Calculer** pour pousser la requête vers Snowflake et obtenir une estimation des profils qui remplissent désormais les critères.

![AAAA](./images/fedcomp10.png)

Ensuite, cliquez de nouveau sur l’icône **+** et cliquez de nouveau sur **Condition personnalisée** pour ajouter une autre condition.

![AAAA](./images/fedcomp11.png)

La deuxième condition à ajouter est : `Is the user an existing CitiSignal Mobile subscriber?`. La réponse à cette question consiste à utiliser la relation entre le ménage et le client principal du ménage, qui est définie dans une autre table, **—aepUserLdap—_PERSON**. Vous pouvez effectuer une analyse plus approfondie dans le menu d’attributs à l’aide du lien **household2person**.

![AAAA](./images/fedcomp12.png)

Sélectionnez l’attribut **ISMOBILESUB** et cliquez sur **Confirmer**.

![AAAA](./images/fedcomp13.png)

Définissez le champ **Valeur** sur **Vrai** Cliquez de nouveau sur **Calculer** pour mettre à jour le nombre de profils qui seront ciblés. Cliquez sur **Confirmer**.

![AAAA](./images/fedcomp14.png)

Cliquez sur l’icône **+**, puis sur **Enregistrer l’audience**.

![AAAA](./images/fedcomp15.png)

Définissez le **libellé Audience** sur `--aepUserLdap-- - CitiSignal Eligible for Fiber`.

Cliquez sur **+ Ajouter un mappage d’audience**.

![AAAA](./images/fedcomp16.png)

Sélectionnez **HOUSEHOLD_ID** et cliquez sur **Confirmer**.

![AAAA](./images/fedcomp17.png)

Cliquez sur **+ Ajouter un mappage d’audience**.

![AAAA](./images/fedcomp18.png)

Analyser en cliquant sur **Dimension de ciblage**.

![AAAA](./images/fedcomp18a.png)

Explorez en cliquant sur le lien **household2person**.

![AAAA](./images/fedcomp18b.png)

Sélectionnez le champ **NOM**. Cliquez sur **Confirmer**.

![AAAA](./images/fedcomp18c.png)

Cliquez sur **+ Ajouter un mappage d’audience**.

![AAAA](./images/fedcomp20.png)

Analyser en cliquant sur **Dimension de ciblage**.

![AAAA](./images/fedcomp20a.png)

Explorez en cliquant sur le lien **household2person**.

![AAAA](./images/fedcomp20b.png)

Sélectionnez le champ **E-MAIL**. Cliquez sur **Confirmer**.

![AAAA](./images/fedcomp20c.png)

Tu verras ça. Vous devez maintenant définir le champ d’identité du Principal ****, définissez-le sur **Household2person_EMAIL**. Définissez **Espace de noms d’identité** sur **E-mail**.

Cliquez sur **Enregistrer**.

![AAAA](./images/fedcomp21.png)

Votre composition est maintenant terminée. Cliquez sur **Démarrer** pour l’exécuter.

![AAAA](./images/fedcomp21a.png)

La requête sera désormais transmise à Snowflake, qui y interrogera les données sources. Les résultats seront redirigés vers AEP, mais les données sources restent dans Snowflake.

L’audience est maintenant renseignée et peut être ciblée à partir de l’écosystème AEP.

![AAAA](./images/fedcomp22.png)

## Étapes suivantes

Accédez à [ Résumé et avantages ](./summary.md){target="_blank"}

Revenez à [ Composition d’audience fédérée ](./fac.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
