---
title: Offer Decisioning - Configuration de vos offres et de votre identifiant de décision
description: Offer Decisioning - Configuration de vos offres et de votre identifiant de décision
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 4%

---

# 3.3.2 Configuration de vos offres et de votre décision

## 3.3.2.1 Créer vos offres personnalisées

Dans cet exercice, vous allez créer quatre **Offres personnalisées**. Voici les détails à prendre en compte lors de la création de ces offres :

| Nom | Période | Lien d’image pour l’e-mail | Lien de l’image pour le Web | Texte | Priorité | Admissibilité | Langue | Fréquence de limitation | Nom de l’image |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | aujourd’hui - 1 mois plus tard | https://bit.ly/4a9RJ5d | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | all - Clientes | Anglais (États-Unis) | 3 | Apple AirPods Max- Femme.jpg |
| `--aepUserLdap-- - Galaxy S24` | aujourd’hui - 1 mois plus tard | https://bit.ly/3W8yuDv | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | all - Clientes | Anglais (États-Unis) | 3 | Galaxy S24 - Femme.jpg |
| `--aepUserLdap-- - Apple Watch` | aujourd’hui - 1 mois plus tard | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | all - Clients | Anglais (États-Unis) | 3 | Apple Watch - Masculin.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | aujourd’hui - 1 mois plus tard | https://bit.ly/4gTrkeo | Choisir parmi la bibliothèque Assets | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | all - Clients | Anglais (États-Unis) | 3 | Galaxy Watch7 - Homme.jpg |

{style="table-layout:auto"}

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Dans le menu de gauche, cliquez sur **Offres** puis accédez à **Offres**. Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/offers1.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionnez **Offre personnalisée** puis cliquez sur **Suivant**.

![Règle de décision](./images/offers2.png)

Vous êtes maintenant dans la vue **Détails**.

![Règle de décision](./images/offers3.png)

Dans ce cas, vous devez configurer le `--aepUserLdap-- - AirPods Max` de l&#39;offre. Utilisez les informations du tableau ci-dessus pour remplir les champs. Dans cet exemple, le nom de l’offre personnalisée est **vangeluw - AirPods Max**. En outre, définissez la **Date et heure de début** sur aujourd’hui, et la **Date et heure de fin** sur une date dans un mois à partir de maintenant.

Une fois cette opération terminée, vous devriez disposer de ceci. Cliquez sur **Suivant**.

![Règle de décision](./images/offers4.png)

Vous verrez alors ceci :

![Règle de décision](./images/constraints.png)

Sélectionnez **Par règle de décision définie** et cliquez sur l’icône **+** pour ajouter la règle **Tous - Clientes**.

Remplissez le champ **Priorité** comme indiqué dans le tableau ci-dessus. Cliquez ensuite sur **+ Créer une limitation** pour définir le nombre de fois où cette offre peut être présentée à un client.

![Règle de décision](./images/constraints1.png)

Pour la limitation, sélectionnez les options suivantes :

- **Choisir un événement de limitation** : **événement de décision**
- **Type de limitation** : **Par profil (appliquer une limitation pour chaque profil)**
- **Nombre d’événements de limitation** : **3**
- **Réinitialiser la fréquence de limitation** : **quotidiennement**
- **Tous les** : **1 jour**

Cela permet de s’assurer que cette offre ne sera pas présentée plus de 3 fois par jour par client.

Cliquez sur **Créer**.

![Règle de décision](./images/constraints2.png)

Tu seras de retour ici. Cliquez sur **Suivant**.

![Règle de décision](./images/constraints3.png)

Vous devez maintenant créer des **Représentations**. Les représentations sont une combinaison d&#39;un **Emplacement** et d&#39;une ressource réelle.

Pour **Représentation 1**, sélectionnez :

- Canal : Web
- Emplacement : Web - Image
- Contenu : URL
- Emplacement public : copiez l’URL à partir de la colonne **Lien d’image pour le Web** dans le tableau ci-dessus.

![Règle de décision](./images/addcontent1.png)

Vous pouvez également sélectionner **Bibliothèque de ressources** pour le contenu, puis cliquer sur **Parcourir**.

![Règle de décision](./images/addcontent2.png)

Une fenêtre contextuelle de la bibliothèque Assets s’affiche, accédez au dossier **enablement-assets** et sélectionnez le fichier image **Apple AirPods Max - Female.jpg**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3.png)

Tu verras ça. Cliquez sur **+ Ajouter une représentation**.

![Règle de décision](./images/addcontentrep20.png)

Pour **Représentation 2**, sélectionnez :

- Canal : e-mail
- Emplacement : E-mail - Image
- Contenu : URL
- Emplacement public : sélectionnez **Bibliothèque de ressources**. Cliquez sur **Parcourir**

![Règle de décision](./images/addcontentrep21.png)

Une fenêtre contextuelle de la bibliothèque Assets s’affiche, accédez au dossier **enablement-assets** et sélectionnez le fichier image **Apple AirPods Max - Female.jpg**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3b.png)

Tu verras ça. Cliquez ensuite sur **+ Ajouter une représentation**.

![Règle de décision](./images/addcontentrep20b.png)

Pour **Représentation 3**, sélectionnez :

- Canal : non numérique
- Emplacement : Non numérique - Texte

Vous devez ensuite ajouter du contenu. Dans ce cas, il s’agit d’ajouter le texte à utiliser comme appel à l’action.

Sélectionnez **Personnalisé** puis cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep31.png)

Vous verrez alors cette fenêtre contextuelle.

![Règle de décision](./images/addcontent3text.png)

Examinez le champ **Texte** du tableau ci-dessus et saisissez ce texte ici, dans ce cas : `{{ profile.person.name.firstName }}, 10% discount on AirPods Max`.

Vous remarquerez également que vous pouvez sélectionner n’importe quel attribut de profil et l’inclure en tant que champ dynamique dans le texte de l’offre. Dans cet exemple, le champ `{{ profile.person.name.firstName }}` garantit que le prénom du client qui recevra cette offre sera inclus dans le texte de l&#39;offre.

Tu verras ça. Cliquez sur **Enregistrer**.

![Règle de décision](./images/addcontentrep3text.png)

Vous l&#39;avez maintenant. Cliquez sur **Suivant**.

![Règle de décision](./images/addcontentrep3textdone.png)

Vous verrez ensuite un aperçu de votre nouvelle **Offre personnalisée**. Cliquez sur **Terminer**.

![Règle de décision](./images/offeroverview.png)

Cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprove.png)

Votre offre personnalisée nouvellement créée est alors disponible dans la Présentation des offres :

![Règle de décision](./images/offeroverview1.png)

Vous devez maintenant répéter les étapes ci-dessus pour créer les trois autres offres personnalisées pour les produits que vous trouverez dans le tableau ci-dessus.

Une fois cette opération terminée, votre écran **Vues d’ensemble des offres** pour **Offres personnalisées** doit afficher toutes vos offres.

![Offres finales](./images/finaloffers.png)

## 3.3.2.2 Créer votre offre de secours

Après avoir créé quatre offres personnalisées, vous devez maintenant configurer une **offre de secours**.

Vérifiez que vous êtes dans la vue **Offres**. Cliquez sur **+ Créer une offre**.

![Règle de décision](./images/createoffer.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionnez **Offre de secours** puis cliquez sur **Suivant**.

![Règle de décision](./images/foffers2.png)

Tu verras ça. Saisissez le nom suivant pour votre offre de secours : `--aepUserLdap-- - CitiSignal Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/foffers4.png)

Vous devez maintenant créer des **Représentations**. Les représentations sont une combinaison d&#39;un **Emplacement** et d&#39;une ressource réelle.

Pour **Représentation 1**, sélectionnez :

- **Canal** : **Web**
- **Emplacement** : **Web - Image**
- **Contenu** : **Bibliothèque de ressources**

Cliquez sur **Parcourir** pour sélectionner votre image.

![Règle de décision](./images/addcontent1fb.png)

Une fenêtre contextuelle de la bibliothèque Assets s’affiche alors, accédez au dossier **citi-signal-images** et sélectionnez le fichier image **App-Banner-Ad.jpg**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3fb.png)

Tu verras ça. Cliquez sur **+ Ajouter une représentation**.

![Règle de décision](./images/addcontentrep20fb.png)

Pour **Représentation 2**, sélectionnez :

- **Canal** : **E-mail**
- **Emplacement** : **E-mail - Image**
- **Contenu** : **Bibliothèque de ressources**

Cliquez sur **Parcourir** pour sélectionner votre image.

![Règle de décision](./images/addcontentrep21fb.png)

Une fenêtre contextuelle de la bibliothèque Assets s’affiche alors, accédez au dossier **citi-signal-images** et sélectionnez le fichier image **App-Banner-Ad.jpg**. Cliquez ensuite sur **Sélectionner**.

![Règle de décision](./images/addcontent3bfb.png)

Tu verras ça. Cliquez sur **+ Ajouter une représentation**.

![Règle de décision](./images/addcontentrep20bfb.png)

Pour **Représentation 3**, sélectionnez :

- **Canal** : **Non numérique**
- **Emplacement** : **Non numérique - Texte**
- **Contenu** : **Personnalisé**

Cliquez sur **Ajouter du contenu**.

![Règle de décision](./images/addcontentrep21text.png)

Vous verrez alors cette fenêtre contextuelle. Saisissez le `{{ profile.person.name.firstName }}, download the CitiSignal app now!` de texte et cliquez sur **Enregistrer**.

![Règle de décision](./images/faddcontent3text.png)

Tu verras ça. Cliquez sur **Suivant**.

![Règle de décision](./images/faddcontentrep3.png)

Vous verrez ensuite un aperçu de votre nouvelle **offre de secours**. Cliquez sur **Terminer**.

![Règle de décision](./images/fofferoverview.png)

Enfin, cliquez sur **Enregistrer et approuver**.

![Règle de décision](./images/saveapprovefb.png)

Dans l’écran **Présentation des offres**, vous verrez ceci :

![Offres finales](./images/ffinaloffers.png)

## 3.3.2.3 Créer votre collection

Une collection est utilisée pour **filtrer** un sous-ensemble d’offres de la liste d’offres personnalisée et l’utiliser dans le cadre d’une décision afin d’accélérer le processus de décision.

Accédez à **Collections**. Cliquez sur **+ Créer une collection**.

![Règle de décision](./images/collections.png)

Vous verrez alors cette fenêtre contextuelle. Configurez votre collection comme suit : Cliquez sur **Suivant**.

- Nom de la collection : utiliser `--aepUserLdap-- - CitiSignal Collection`
- Sélectionnez **Créer une collection statique**.

Cliquez sur **Suivant**.

![Règle de décision](./images/createcollectionpopup1.png)

Dans l’écran suivant, sélectionnez les quatre **Offres personnalisées** vous avez créées dans l’exercice précédent. Cliquez sur **Enregistrer**.

![Règle de décision](./images/createcollectionpopup2.png)

Vous verrez maintenant ceci :

![Règle de décision](./images/colldone.png)

## 3.3.2.4 Créer votre décision

Une décision combine des emplacements, une collection d’offres personnalisées et une offre de secours afin que le moteur Offer Decisioning puisse finalement l’utiliser pour trouver la meilleure offre pour un profil spécifique, en fonction de chacune des caractéristiques d’offre personnalisées individuelles telles que la priorité, la contrainte d’éligibilité et la limitation totale/utilisateur.

Pour configurer votre **Décision**, accédez à **Décisions**. Cliquez sur **+ Créer une décision**.

![Règle de décision](./images/activitydd.png)

Tu verras ça. Remplissez les champs comme ceci. Cliquez sur **Suivant**.

- Nom : `--aepUserLdap-- - CitiSignal Decision`
- Date et heure de début : aujourd&#39;hui
- Date et heure de fin : aujourd’hui + 1 mois

![Règle de décision](./images/activity2.png)

Dans l&#39;écran suivant, vous devez ajouter des emplacements dans les portées de décision. Vous devez créer des portées de décision pour les emplacements **Web - Image**, **E-mail - Image** et **Non numérique - Texte**.

![Règle de décision](./images/addplacements.png)

Créez tout d’abord la portée de décision pour **Non numérique - Texte** en sélectionnant cet emplacement dans la liste déroulante. Cliquez ensuite sur le bouton **Ajouter** pour ajouter des critères d’évaluation.

![Règle de décision](./images/activity3.png)

Sélectionnez votre `--aepUserLdap-- - CitiSignal Collection` de collection et cliquez sur **Ajouter**.

![Règle de décision](./images/activity4text.png)

Tu verras ça. Cliquez sur le bouton **+** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity5text.png)

Sélectionnez l’emplacement **Web - Image** et ajoutez votre `--aepUserLdap-- - CitiSignal Collection` de collection sous critères d’évaluation. Cliquez ensuite à nouveau sur le bouton **+** pour ajouter une nouvelle portée de décision.

![Règle de décision](./images/activity6text.png)

Sélectionnez l’emplacement **E-mail - Image** et ajoutez vos `--aepUserLdap-- - CitiSignal Collection` de collection sous critères d’évaluation. Cliquez ensuite sur **Suivant**.

![Règle de décision](./images/activity4.png)

Vous devez maintenant sélectionner votre **Offre de secours**, qui porte le nom `--aepUserLdap-- - CitiSignal Fallback Offer`. Cliquez sur **Suivant**.

![Règle de décision](./images/activity10.png)

Passez en revue votre décision. Cliquez sur **Terminer**.

![Règle de décision](./images/activity11.png)

Dans la fenêtre contextuelle, cliquez sur **Enregistrer et activer**.

![Règle de décision](./images/activity12.png)

Enfin, votre décision s’affiche désormais dans la vue d’ensemble :

![Règle de décision](./images/activity13.png)

Vous avez maintenant correctement configuré votre décision. Votre décision est maintenant en ligne et peut être utilisée pour diffuser des offres optimisées et personnalisées à vos clients et clientes, en temps réel.

## Étapes suivantes

Accédez à [3.3.3 Préparer la propriété du client de collecte de données et la configuration de Web SDK pour Offer Decisioning](./ex3.md){target="_blank"}

Revenir à [Offer Decisioning](offer-decisioning.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
