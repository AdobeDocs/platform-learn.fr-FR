---
title: Offer decisioning - Configuration de vos offres et de votre ID de décision
description: Offer decisioning - Configuration de vos offres et de votre ID de décision
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 3%

---

# 3.3.2 Configuration de vos offres et de votre décision

## 3.3.2.1 Création de vos offres personnalisées

Dans cet exercice, vous allez créer quatre **offres personnalisées**. Voici les détails à prendre en compte lors de la création de ces offres :

| Nom | Période | Lien d’image pour le courrier électronique | Lien d’image pour le web | Texte | Priorité | Admissibilité | Langue |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--aepUserLdap-- - Nadia Elements Shell` | aujourd’hui - 1 mois plus tard | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | all - Clients féminins | Anglais (États-Unis) |
| `--aepUserLdap-- - Radiant Tee` | aujourd’hui - 1 mois plus tard | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | all - Clients féminins | Anglais (États-Unis) |
| `--aepUserLdap-- - Zeppelin Yoga Pant` | aujourd’hui - 1 mois plus tard | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | all - Clients masculins | Anglais (États-Unis) |
| `--aepUserLdap-- - Proteus Fitness Jackshirt` | aujourd’hui - 1 mois plus tard | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | all - Clients masculins | Anglais (États-Unis) |

{style="table-layout:auto"}

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `--aepSandboxName--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production Prod (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **AEP Enablement FY22**. Vous serez alors dans la vue **Home** de votre environnement de test `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Dans le menu de gauche, cliquez sur **Offres** , puis accédez à **Offres**. Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/offers1.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionnez **Offre personnalisée** et cliquez sur **Suivant**.

![Règle de décision](./images/offers2.png)

Vous êtes maintenant sur la vue **Détails**.

![Règle de décision](./images/offers3.png)

Dans ce cas, vous devez configurer l’offre `--aepUserLdap-- - Nadia Elements Shell`. Renseignez les informations du tableau ci-dessus pour remplir les champs. Dans cet exemple, le nom de l’offre personnalisée est **vangeluw - Nadia Elements Shell**. En outre, définissez la **date et l’heure de début** sur hier, et définissez la **date et l’heure de fin** sur une date dans un mois à partir de maintenant.

Une fois terminé, vous devriez avoir ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/offers4.png)

Vous devez maintenant créer des **représentations**. Les représentations sont une combinaison d’un **emplacement** et d’une ressource réelle.

Pour **Représentation 1**, sélectionnez :

- Canal : Web
- Placement : Web - Image
- Contenu : URL
- Emplacement public : copiez l’URL de la colonne **Lien d’image pour le Web** dans le tableau ci-dessus.

![Règle de décision](./images/addcontent1.png)

Vous pouvez également sélectionner la **bibliothèque de ressources** pour le contenu, puis cliquer sur **Parcourir**.

![Règle de décision](./images/addcontent2.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque Assets, accédez au dossier **enablement-assets** et sélectionnez le fichier image **nadia-web.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20.png)

Cliquez sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 2**, sélectionnez :

- Canal : e-mail
- Placement : Email - Image
- Contenu : URL
- Emplacement public : copiez l’URL de la colonne **Lien d’image pour le courrier électronique** dans le tableau ci-dessus.

![Règle de décision](./images/addcontentrep21.png)

Vous pouvez également sélectionner la **bibliothèque de ressources** pour le contenu, puis cliquer sur **Parcourir**.

![Règle de décision](./images/addcontent2b.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque Assets, accédez au dossier **enablement-assets** et sélectionnez le fichier image **nadia-email.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3b.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20b.png)

Cliquez ensuite sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 3**, sélectionnez :

- Canal : Non numérique
- Placement : non numérique - Texte

Vous devez ensuite ajouter du contenu. Dans ce cas, cela signifie ajouter le texte à utiliser comme appel à l’action.

Cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep31.png)

Vous verrez alors cette fenêtre contextuelle.

![Règle de décision](./images/addcontent3text.png)

Sélectionnez **Texte personnalisé** et remplissez les champs suivants :

Examinez le champ **Texte** du tableau ci-dessus et saisissez ce texte ici, dans ce cas : `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`.

Vous remarquerez également que vous pouvez sélectionner n’importe quel attribut de profil et l’inclure comme champ dynamique dans le texte de l’offre. Dans cet exemple, le champ `{{ profile.person.name.firstName }}` s’assure que le prénom du client qui recevra cette offre sera inclus dans le texte de l’offre.

Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![Règle de décision](./images/addcontentrep3text.png)

Vous avez maintenant ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/addcontentrep3textdone.png)

Vous verrez alors :

![Règle de décision](./images/constraints.png)

Sélectionnez **Par règle de décision définie** et cliquez sur l’icône **+** pour ajouter la règle **all - Female Customers**.

![Règle de décision](./images/constraints1.png)

Vous verrez alors ceci. Remplissez la **Priorité** comme indiqué dans le tableau ci-dessus. Cliquez sur **Suivant**.

![Règle de décision](./images/constraints2.png)

Vous verrez ensuite un aperçu de votre nouvelle **offre personnalisée**.

![Règle de décision](./images/offeroverview.png)

Enfin, cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprove.png)

Vous verrez ensuite votre nouvelle offre personnalisée devenir disponible dans la Présentation des offres :

![Règle de décision](./images/offeroverview1.png)

Vous devez maintenant répéter les étapes ci-dessus pour créer les trois autres offres personnalisées pour les produits Tee Radiant, Zeppelin Yoga Pant et Proteus Fitness Jackshirt.

Lorsque vous avez terminé, votre écran **Offer Overviews** pour **Offres personnalisées** devrait afficher toutes vos offres.

![Offres finales](./images/finaloffers.png)

## 3.3.2.2 Création de votre offre de secours

Après avoir créé quatre offres personnalisées, vous devez maintenant configurer une **offre de secours**.

Vérifiez que vous vous trouvez dans la vue **Offres** :

![Offres finales](./images/finaloffers.png)

Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/createoffer.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionnez **Offre de secours** et cliquez sur **Suivant**.

![Règle de décision](./images/foffers2.png)

Vous verrez alors :

![Règle de décision](./images/foffers3.png)

Saisissez ce nom pour votre offre de secours : `--aepUserLdap-- - Luma Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/foffers4.png)

Vous devez maintenant créer des **représentations**. Les représentations sont une combinaison d’un **emplacement** et d’une ressource réelle.

Pour **Représentation 1**, sélectionnez :

- Canal : Web
- Placement : Web - Image
- Contenu : URL
- Emplacement public : `https://bit.ly/3nBOt9h`

![Règle de décision](./images/addcontent1fb.png)

Vous pouvez également sélectionner la **bibliothèque de ressources** pour le contenu, puis cliquer sur **Parcourir**.

![Règle de décision](./images/addcontent2fb.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque Assets, accédez au dossier **enablement-assets** et sélectionnez le fichier image **spriteyogastraps-web.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3fb.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20fb.png)

Pour **Représentation 2**, sélectionnez :

- Canal : e-mail
- Placement : Email - Image
- Contenu : URL
- Emplacement public : `https://bit.ly/3nF4qvE`

![Règle de décision](./images/addcontentrep21fb.png)

Vous pouvez également sélectionner la **bibliothèque de ressources** pour le contenu, puis cliquer sur **Parcourir**.

![Règle de décision](./images/addcontent2bfb.png)

Vous verrez ensuite une fenêtre contextuelle de la bibliothèque Assets, accédez au dossier **enablement-assets** et sélectionnez le fichier image **spriteyogastraps-email.png**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3bfb.png)

Vous verrez alors :

![Règle de décision](./images/addcontentrep20bfb.png)

Cliquez ensuite sur **+ Ajouter une représentation**.

![Règle de décision](./images/addrep.png)

Pour **Représentation 3**, sélectionnez :

- Canal : Non numérique
- Placement : non numérique - Texte

Vous devez ensuite ajouter du contenu. Dans ce cas, cela signifie ajouter le lien de l’image.

Cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep21text.png)

Vous verrez alors cette fenêtre contextuelle.

![Règle de décision](./images/addcontent2text.png)

Sélectionnez **Texte personnalisé** et remplissez les champs suivants :

Saisissez le texte `{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!` et cliquez sur **Enregistrer**.

![Règle de décision](./images/faddcontent3text.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/faddcontentrep3.png)

Vous verrez ensuite un aperçu de votre nouvelle **offre de secours**. Cliquez sur **Terminer**.

![Règle de décision](./images/fofferoverview.png)

Enfin, cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprovefb.png)

Dans l’écran **Offer Overviews** , vous verrez maintenant ceci :

![Offres finales](./images/ffinaloffers.png)

## 3.3.2.3 Création de votre collection

Une collection est utilisée pour **filtrer** un sous-ensemble d’offres de la liste d’offres personnalisée et les utiliser dans le cadre d’une décision afin d’accélérer le processus de décision.

Accédez à **Collections**. Cliquez sur **+ Créer une collection**.

![Règle de décision](./images/collections.png)

Vous verrez alors cette fenêtre contextuelle. Configurez votre collection comme suit. Cliquez sur **Suivant**.

- Nom de la collection : utilisez `--aepUserLdap-- - Luma Collection`
- Sélectionnez **Créer une collection statique**.

![Règle de décision](./images/createcollectionpopup1.png)

Dans l’écran suivant, sélectionnez les quatre **Offres personnalisées** que vous avez créées dans l’exercice précédent. Cliquez sur **Enregistrer**.

![Règle de décision](./images/createcollectionpopup2.png)

Vous verrez maintenant ceci :

![Règle de décision](./images/colldone.png)

## 3.3.2.4 Créer votre décision

Une décision associe des emplacements, un ensemble d’offres personnalisées et une offre de secours qui, ultimement, seront utilisés par le moteur d’Offer decisioning pour trouver la meilleure offre pour un profil spécifique, en fonction de chacune des caractéristiques d’offre personnalisées individuelles telles que la priorité, la contrainte d’éligibilité et la limitation totale/utilisateur.

Pour configurer votre **décision**, accédez à **Décisions**. Cliquez sur **+ Créer l’activité**.

![Règle de décision](./images/activitydd.png)

Vous verrez alors :

![Règle de décision](./images/activity1.png)

Renseignez les champs comme celui-ci. Cliquez sur **Suivant**.

- Nom : `--aepUserLdap-- - Luma Decision`
- Date et heure de début : hier
- Date et heure de fin : aujourd’hui + 1 mois

![Règle de décision](./images/activity2.png)

Dans l’écran suivant, vous devez ajouter des emplacements aux portées de décision. Vous devrez créer des portées de décision pour les emplacements **Web - Image**, **Email - Image** et **Non-digital - Text**.

![Règle de décision](./images/addplacements.png)

Tout d’abord, créez la portée de décision pour **Non-digital - Text** en sélectionnant cet emplacement dans la liste déroulante. Cliquez ensuite sur le bouton **Ajouter** pour ajouter des critères d’évaluation.

![Règle de décision](./images/activity3.png)

Sélectionnez votre collection `--aepUserLdap-- - Luma Collection` et cliquez sur **Ajouter**.

![Règle de décision](./images/activity4text.png)

Vous verrez alors ceci. Cliquez sur le bouton **-** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity5text.png)

Sélectionnez l&#39;emplacement **Web - Image** et ajoutez votre collection `--aepUserLdap-- - Luma Collection` sous les critères d&#39;évaluation. Cliquez ensuite de nouveau sur le bouton **+** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity6text.png)

Sélectionnez l’emplacement **Email - Image** et ajoutez votre collection `--aepUserLdap-- - Luma Collection` sous les critères d’évaluation. Cliquez ensuite sur **Suivant**.

![Règle de décision](./images/activity4.png)

Vous devez maintenant sélectionner votre **offre de secours**, qui s’appelle `--aepUserLdap-- - Luma Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/activity10.png)

Vérifiez votre décision. Cliquez sur **Terminer**.

![Règle de décision](./images/activity11.png)

Dans la fenêtre contextuelle, cliquez sur **Enregistrer et activer**.

![Règle de décision](./images/activity12.png)

Enfin, vous verrez votre décision dans la présentation :

![Règle de décision](./images/activity13.png)

Vous avez maintenant correctement configuré votre décision. Votre décision est maintenant en ligne et peut être utilisée pour offrir des offres optimisées et personnalisées à vos clients, en temps réel.

Étape suivante : [3.3.3 Préparation de la configuration de la propriété du client de collecte de données et du SDK web pour Offer Decisioning](./ex3.md)

[Revenir au module 3.3](./offer-decisioning.md)

[Revenir à tous les modules](./../../../overview.md)
