---
title: offer decisioning - Configuration de vos offres et de votre ID de décision
description: offer decisioning - Configuration de vos offres et de votre ID de décision
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 4b2c2753-8b7e-496e-9fb5-3ccb9f6a10ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 3%

---

# 9.2 Configuration de vos offres et de votre décision

## 9.2.1 Création de vos offres personnalisées

Dans cet exercice, vous allez créer quatre **Offres personnalisées**. Voici les détails à prendre en compte lors de la création de ces offres :

| Nom | Période | Lien d’image pour le courrier électronique | Lien d’image pour le web | Texte | Priorité | Admissibilité | Langue |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--demoProfileLdap-- - Nadia Elements Shell` | aujourd’hui - 1 mois plus tard | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | all - Clients féminins | Anglais (États-Unis) |
| `--demoProfileLdap-- - Radiant Tee` | aujourd’hui - 1 mois plus tard | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | all - Clients féminins | Anglais (États-Unis) |
| `--demoProfileLdap-- - Zeppelin Yoga Pant` | aujourd’hui - 1 mois plus tard | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | all - Clients masculins | Anglais (États-Unis) |
| `--demoProfileLdap-- - Proteus Fitness Jackshirt` | aujourd’hui - 1 mois plus tard | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | all - Clients masculins | Anglais (États-Unis) |

{style=&quot;table-layout:auto&quot;}

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Activation AEP FY22**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Dans le menu de gauche, cliquez sur **Offres** puis accédez à **Offres**. Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/offers1.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionner **Offre personnalisée** et cliquez sur **Suivant**.

![Règle de décision](./images/offers2.png)

Vous êtes maintenant sur le **Détails** vue.

![Règle de décision](./images/offers3.png)

Dans ce cas, vous devez configurer l’offre. `--demoProfileLdap-- - Nadia Elements Shell`. Renseignez les informations du tableau ci-dessus pour remplir les champs. Dans cet exemple, le nom de l’offre personnalisée est **vangeluw - Shell Nadia Elements**. Définissez également la variable **Date et heure de début** sur hier, puis définissez la variable **Date et heure de fin** à une date dans un mois.

Une fois terminé, vous devriez avoir ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/offers4.png)

Vous devez maintenant créer **Représentations**. Les représentations sont une combinaison d’une **Emplacement** et un actif réel.

Pour **Représentation 1**, sélectionnez :

- Canal : Web
- Placement : Web - Image
- Contenu : URL
- Emplacement public : Copiez l’URL de la colonne **Lien d’image pour le web** dans le tableau ci-dessus

![Règle de décision](./images/addcontent1.png)

Vous pouvez également sélectionner **Bibliothèque de ressources** pour le contenu, puis cliquez sur **Parcourir**.

![Règle de décision](./images/addcontent2.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque de ressources, puis accédez au dossier . **enablement-assets** et sélectionnez le fichier image. **nadia-web.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20.png)

Cliquez sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 2**, sélectionnez :

- Canal : Email
- Placement : Email - Image
- Contenu : URL
- Emplacement public : Copiez l’URL de la colonne **Lien d’image pour le courrier électronique** dans le tableau ci-dessus

![Règle de décision](./images/addcontentrep21.png)

Vous pouvez également sélectionner **Bibliothèque de ressources** pour le contenu, puis cliquez sur **Parcourir**.

![Règle de décision](./images/addcontent2b.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque de ressources, puis accédez au dossier . **enablement-assets** et sélectionnez le fichier image. **nadia-email.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3b.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20b.png)

Cliquez ensuite sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 3**, sélectionnez :

- Canal : Non numérique
- Placement : Non numérique - Texte

Vous devez ensuite ajouter du contenu. Dans ce cas, cela signifie ajouter le texte à utiliser comme appel à l’action.

Cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep31.png)

Vous verrez alors cette fenêtre contextuelle.

![Règle de décision](./images/addcontent3text.png)

Sélectionner **Texte personnalisé** et renseignez les champs suivants :

Consultez la **Texte** dans le tableau ci-dessus et saisissez ce texte ici, ici, dans ce cas : `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`.

Vous remarquerez également que vous pouvez sélectionner n’importe quel attribut de profil et l’inclure comme champ dynamique dans le texte de l’offre. Dans cet exemple, le champ `{{ profile.person.name.firstName }}` s’assure que le prénom du client qui recevra cette offre sera inclus dans le texte de l’offre.

Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![Règle de décision](./images/addcontentrep3text.png)

Vous avez maintenant ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/addcontentrep3textdone.png)

Vous verrez alors :

![Règle de décision](./images/constraints.png)

Sélectionner **Par règle de décision définie** et cliquez sur le bouton **+** pour ajouter la règle **all - Clients féminins**.

![Règle de décision](./images/constraints1.png)

Vous verrez alors ceci. Remplissez la variable **Priorité** comme indiqué dans le tableau ci-dessus. Cliquez sur **Suivant**.

![Règle de décision](./images/constraints2.png)

Vous verrez ensuite un aperçu de votre nouvelle **Offre personnalisée**.

![Règle de décision](./images/offeroverview.png)

Enfin, cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprove.png)

Vous verrez ensuite votre nouvelle offre personnalisée devenir disponible dans la Présentation des offres :

![Règle de décision](./images/offeroverview1.png)

Vous devez maintenant répéter les étapes ci-dessus pour créer les trois autres offres personnalisées pour les produits Tee Radiant, Zeppelin Yoga Pant et Proteus Fitness Jackshirt.

Lorsque vous avez terminé, votre **Présentation des offres** écran pour **Offres personnalisées** devrait afficher toutes vos offres.

![Offres finales](./images/finaloffers.png)

## 9.2.2 Création de votre offre de secours

Après avoir créé quatre offres personnalisées, vous devez maintenant configurer une **Offre de secours**.

Assurez-vous que vous êtes dans le **Offres** view :

![Offres finales](./images/finaloffers.png)

Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/createoffer.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionner **Offre de secours** et cliquez sur **Suivant**.

![Règle de décision](./images/foffers2.png)

Vous verrez alors :

![Règle de décision](./images/foffers3.png)

Saisissez ce nom pour votre offre de secours : `--demoProfileLdap-- - Luma Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/foffers4.png)

Vous devez maintenant créer **Représentations**. Les représentations sont une combinaison d’une **Emplacement** et un actif réel.

Pour **Représentation 1**, sélectionnez :

- Canal : Web
- Placement : Web - Image
- Contenu : URL
- Emplacement public : `https://bit.ly/3nBOt9h`

![Règle de décision](./images/addcontent1fb.png)

Vous pouvez également sélectionner **Bibliothèque de ressources** pour le contenu, puis cliquez sur **Parcourir**.

![Règle de décision](./images/addcontent2fb.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque de ressources, puis accédez au dossier . **enablement-assets** et sélectionnez le fichier image. **spriteyogastraps-web.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3fb.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20fb.png)

Pour **Représentation 2**, sélectionnez :

- Canal : Email
- Placement : Email - Image
- Contenu : URL
- Emplacement public : `https://bit.ly/3nF4qvE`

![Règle de décision](./images/addcontentrep21fb.png)

Vous pouvez également sélectionner **Bibliothèque de ressources** pour le contenu, puis cliquez sur **Parcourir**.

![Règle de décision](./images/addcontent2bfb.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque de ressources, puis accédez au dossier . **enablement-assets** et sélectionnez le fichier image. **spriteyogastraps-email.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3bfb.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20bfb.png)

Cliquez ensuite sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 3**, sélectionnez :

- Canal : Non numérique
- Placement : Non numérique - Texte

Vous devez ensuite ajouter du contenu. Dans ce cas, cela signifie ajouter le lien de l’image.

Cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep21text.png)

Vous verrez alors cette fenêtre contextuelle.

![Règle de décision](./images/addcontent2text.png)

Sélectionner **Texte personnalisé** et renseignez les champs suivants :

Saisissez le texte `{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!` et cliquez sur **Enregistrer**.

![Règle de décision](./images/faddcontent3text.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/faddcontentrep3.png)

Vous verrez ensuite un aperçu de votre nouvelle **Offre de secours**. Cliquez sur **Terminer**.

![Règle de décision](./images/fofferoverview.png)

Enfin, cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprovefb.png)

Dans votre **Présentation des offres** s’affiche alors :

![Offres finales](./images/ffinaloffers.png)

## 9.2.3 Création de votre collection

Une collection est utilisée pour **filter** Déterminez un sous-ensemble d’offres de la liste d’offres personnalisée et utilisez-les dans le cadre d’une décision afin d’accélérer le processus de décision.

Accédez à **Collections**. Cliquez sur **+ Créer une collection**.

![Règle de décision](./images/collections.png)

Vous verrez alors cette fenêtre contextuelle. Configurez votre collection comme suit. Cliquez sur **Suivant**.

- Nom de la collection : use `--demoProfileLdap-- - Luma Collection`
- Sélectionner **Créer une collection statique**.

![Règle de décision](./images/createcollectionpopup1.png)

Dans l’écran suivant, sélectionnez les quatre **Offres personnalisées** vous avez créé dans l’exercice précédent. Cliquez sur **Enregistrer**.

![Règle de décision](./images/createcollectionpopup2.png)

Vous verrez maintenant ceci :

![Règle de décision](./images/colldone.png)

## 9.2.4 Créer votre décision

Une décision associe des emplacements, un ensemble d’offres personnalisées et une offre de secours qui, ultimement, seront utilisés par le moteur d’Offer decisioning pour trouver la meilleure offre pour un profil spécifique, en fonction de chacune des caractéristiques d’offre personnalisées individuelles telles que la priorité, la contrainte d’éligibilité et la limitation totale/utilisateur.

Pour configurer votre **Décision**, accédez à **Décisions**. Cliquez sur **+ Créer une activité**.

![Règle de décision](./images/activitydd.png)

Vous verrez alors :

![Règle de décision](./images/activity1.png)

Renseignez les champs comme celui-ci. Cliquez sur **Suivant**.

- Nom: `--demoProfileLdap-- - Luma Decision`
- Date et heure de début : hier
- Date et heure de fin : aujourd’hui + 1 mois

![Règle de décision](./images/activity2.png)

Dans l’écran suivant, vous devez ajouter des emplacements aux portées de décision. Vous devrez créer des portées de décision pour les emplacements. **Web - Image**, **Email - Image** et **Non numérique - Texte**.

![Règle de décision](./images/addplacements.png)

Tout d’abord, créez la portée de décision pour **Non numérique - Texte** en sélectionnant cet emplacement dans la liste déroulante. Cliquez ensuite sur le bouton **Ajouter** pour ajouter des critères d’évaluation.

![Règle de décision](./images/activity3.png)

Sélectionner votre collection `--demoProfileLdap-- - Luma Collection` et cliquez sur **Ajouter**.

![Règle de décision](./images/activity4text.png)

Vous verrez alors ceci. Cliquez sur le bouton **-** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity5text.png)

Sélectionner l’emplacement **Web - Image** et ajoutez votre collection `--demoProfileLdap-- - Luma Collection` sous les critères d’évaluation. Cliquez ensuite sur le bouton **+** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity6text.png)

Sélectionner l’emplacement **Email - Image** et ajoutez votre collection `--demoProfileLdap-- - Luma Collection` sous les critères d’évaluation. Cliquez ensuite sur **Suivant**.

![Règle de décision](./images/activity4.png)

Vous devez maintenant sélectionner votre **Offre de secours**, qui est nommé `--demoProfileLdap-- - Luma Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/activity10.png)

Vérifiez votre décision. Cliquez sur **Terminer**.

![Règle de décision](./images/activity11.png)

Dans la fenêtre contextuelle, cliquez sur **Enregistrer et activer**.

![Règle de décision](./images/activity12.png)

Enfin, votre décision s’affiche dans la présentation :

![Règle de décision](./images/activity13.png)

Vous avez maintenant correctement configuré votre décision. Votre décision est maintenant en ligne et peut être utilisée pour offrir des offres optimisées et personnalisées à vos clients, en temps réel.

Étape suivante : [9.3 Préparation de la configuration de la propriété du client de collecte de données et du SDK Web pour Offer Decisioning](./ex3.md)

[Revenir au module 9](./offer-decisioning.md)

[Revenir à tous les modules](./../../overview.md)
