---
title: Configuration de Journey Optimizer Decision Management avec Platform Web SDK
description: Découvrez comment implémenter la gestion des décisions à l’aide de Platform Web SDK. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
jira: KT-15412
exl-id: f7852ef4-44b0-49df-aec8-cb211726247d
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 3%

---

# Configuration de la gestion des décisions avec Platform Web SDK

Découvrez comment mettre en œuvre la fonctionnalité de gestion des décisions de Adobe Journey Optimizer à l’aide de Platform Web SDK. Ce guide couvre les conditions préalables fondamentales de la gestion des décisions, les étapes détaillées de configuration et un examen approfondi d’un cas d’utilisation axé sur le statut de fidélité.

En suivant ce tutoriel, les utilisateurs de Journey Optimizer sont équipés pour utiliser les fonctionnalités de gestion des décisions, ce qui améliore la personnalisation et la pertinence de leurs interactions client.


![Diagramme SDK web et Adobe Analytics](assets/dc-websdk-ajo.png)

## Objectifs d’apprentissage

À la fin de cette leçon, vous êtes capable de :

* Maîtrisez les concepts de base de la gestion des décisions dans Adobe Journey Optimizer et son intégration à Adobe Experience Platform Web SDK.

* Découvrez le processus détaillé de configuration de Web SDK pour Offer Decisioning, afin d’assurer une intégration transparente à Journey Optimizer.

* Explorez un cas d’utilisation détaillé centré sur les offres de statut de fidélité, afin d’obtenir des informations sur la création et la gestion efficaces des offres, des décisions et des emplacements.

* Familiarisez-vous avec les termes essentiels et leurs implications dans le cadre de la gestion des décisions.

* Découvrez l’importance des règles de décision, des qualificateurs de collection et des offres de secours pour diffuser la bonne offre au bon utilisateur.

* Explorez des sujets avancés tels que les simulations et la collecte de données d’événements personnalisés, ce qui vous permet de tester, valider et améliorer vos mécanismes de diffusion d’offres.

## Conditions préalables

Pour suivre les leçons de cette section, vous devez d’abord :

* Assurez-vous que votre entreprise a accès à Adobe Journey Optimizer Ultimate (Journey Optimizer et Offer Decisioning) ou à Adobe Experience Platform et au module complémentaire Offer Decisioning.

* Suivez toutes les leçons pour la configuration initiale de Platform Web SDK.

* Activez votre organisation pour la prise de décision Edge.

* Découvrez comment configurer un emplacement et instancier les identifiants d&#39;emplacement et d&#39;activité dans votre JSON de portée de décision.

## Limites

Les offres basées sur un événement ne sont actuellement pas prises en charge dans Adobe Journey Optimizer. Si vous créez une règle de décision basée sur un événement, vous ne pouvez pas l&#39;appliquer à une offre.

## Octroi de l’accès à la gestion des décisions

Pour accorder l’accès à la fonctionnalité de gestion des décisions, vous devez créer un **profil de produit** et attribuer les autorisations correspondantes à vos utilisateurs. [En savoir plus sur la gestion des utilisateurs et des autorisations Journey Optimizer dans cette section](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions#decisions-permissions).

## Configurer le flux de données

Offer Decisioning doit être activé dans la configuration **flux de données** pour que les activités de gestion des décisions puissent être diffusées par Platform Web SDK.

Pour configurer Offer Decisioning dans le flux de données :

1. Accédez à l’interface [Collecte de données](https://experience.adobe.com/#/data-collection).

1. Dans le volet de navigation de gauche, sélectionnez **Flux de données**.

1. Sélectionnez le flux de données Luma Web SDK créé précédemment.

   ![Sélectionner le flux de données](assets/decisioning-datastream-select.png)

1. Sélectionnez **Modifier** dans le service Adobe Experience Platform ****.

   ![Modifier le service](assets/decisioning-edit-datastream.png)

1. Cochez la case **Offer Decisioning**.

   ![AJOUTER UNE CAPTURE D’ÉCRAN](assets/decisioning-check-offer-box.png)

1. Sélectionnez **Enregistrer**.

Cela permet de s’assurer que les événements entrants pour Journey Optimizer sont correctement gérés par l’**Edge Adobe Experience Platform**.

## Configuration de SDK pour la gestion des décisions

La gestion des décisions nécessite des étapes SDK supplémentaires, en fonction de votre type d’implémentation de Web SDK. Deux options sont disponibles pour configurer SDK pour la gestion des décisions.

* Installation autonome de SDK
   1. Configurez l’action `sendEvent` avec votre `decisionScopes`.

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* Installation de SDK Tags
   1. Accédez à l’interface de collecte de données.

   1. Dans le volet de navigation de gauche, sélectionnez **Balises**.

      ![Sélectionner les balises](assets/decisioning-data-collection-tags.png)

   1. Sélectionnez la **Propriété de balise**.

   1. Créez vos **Règles**.
      * Ajoutez une action Platform Web SDK **Envoyer l’événement** et ajoutez les `decisionScopes` appropriées à la configuration de cette action.

   1. Créez et publiez une **Bibliothèque** contenant toutes les **Règles**, **Éléments de données** et **Extensions** pertinentes que vous avez configurées.

## Terminologie

Tout d’abord, vous devez comprendre la terminologie utilisée dans l’interface de gestion des décisions.

* **Limitation** : contrainte déterminant la fréquence d’affichage d’une offre. Deux types :
   * Limites totales : nombre maximal d’affichages d’une offre dans l’audience cible.
   * Limite de profil : nombre de fois où une offre peut être présentée à un utilisateur particulier.
* **Collections** : sous-ensembles d’offres regroupées selon des conditions spécifiques définies par un marketeur, par exemple, la catégorie d’offres.
* **Décision** : logique qui dicte le choix d’une offre.
* **Règle de décision** : contraintes imposées aux offres pour déterminer l’éligibilité d’un utilisateur.
* **Offre éligible** : offre qui correspond aux contraintes prédéfinies et peut être présentée à un utilisateur ou une utilisatrice.
* **Gestion des décisions** : système de conception et de distribution d’offres personnalisées à l’aide de la logique commerciale et des règles de décision.
* **Offres de secours** : offre par défaut affichée lorsqu’un utilisateur ne répond aux critères d’aucune offre d’une collection.
* **Offre** : message marketing contenant des règles d’éligibilité potentielles qui déterminent ses visiteurs.
* **Bibliothèque des offres** : référentiel central gérant les offres, les décisions et les règles associées.
* **Offres personnalisées** : messages marketing personnalisés adaptés aux contraintes d’éligibilité.
* **Emplacements** : paramètre ou scénario dans lequel une offre est présentée à un utilisateur.
* **Priorité** : mesure de classement des offres tenant compte de diverses contraintes telles que l’éligibilité et la limitation.
* **Représentations** : informations spécifiques au canal, par exemple, la localisation ou la langue, guidant l&#39;affichage d&#39;une offre.

## Présentation du cas d’utilisation - Récompenses de fidélité

Dans cette leçon, vous allez mettre en œuvre un exemple de cas d’utilisation de Récompenses de fidélité pour comprendre la gestion des décisions à l’aide du SDK web.

Ce cas pratique vous permet de mieux comprendre comment Journey Optimizer peut vous aider à proposer la meilleure offre à vos clients, à l’aide de la bibliothèque d’offres centralisée et du moteur de décision Decision Management.

>[!NOTE]
>
> Comme ce tutoriel s’adresse aux personnes qui mettent en œuvre , il est intéressant de noter que cette leçon implique un travail d’interface substantiel dans Journey Optimizer. Bien que ces tâches d’interface soient généralement gérées par les spécialistes marketing, il peut être bénéfique pour les personnes chargées de la mise en œuvre d’intégrer insight au processus, même si elles ne sont pas responsables de la création des campagnes de gestion des décisions à long terme.

## Composants

Avant de commencer à créer les offres, vous devez définir plusieurs composants requis.

### Créer un emplacement pour les offres de fidélité

Les **emplacements** sont des conteneurs utilisés pour présenter les offres. Dans cet exemple, vous allez créer un emplacement en haut du site Luma.

La liste des emplacements est accessible dans le menu **Composants**. Des filtres sont disponibles pour vous aider à récupérer des emplacements en fonction d&#39;un canal ou d&#39;un contenu spécifique.

![Afficher les emplacements](assets/decisioning-placements-list.png)

Pour créer l&#39;emplacement, procédez comme suit :

1. Cliquez sur **Créer un emplacement**.

   ![Créer un emplacement](assets/decisioning-create-placement.png)

1. Définissez les propriétés de l&#39;emplacement :
   * **Nom** : nom de l&#39;emplacement. Appelons l’exemple d’emplacement *’* Bannière de page d’accueil’.
   * **Type de canal** : canal pour lequel l’emplacement est utilisé. Utilisons le Web de *, car* offres sont affichées sur le site Web de Luma.
   * **Type de contenu** : type de contenu que l&#39;emplacement peut afficher : texte, HTML, lien d&#39;image ou JSON. Vous pouvez utiliser *’HTML’* pour l’offre.
   * **Description** : description de l’emplacement (facultatif).

   ![Ajouter des détails](assets/decisioning-placement-details.png)

1. Cliquez sur **Enregistrer**.
1. Une fois l&#39;emplacement créé, il s&#39;affiche dans la liste des emplacements.
1. Sélectionnez la ligne contenant votre nouvel emplacement et notez l’ID d’emplacement, car cela peut être nécessaire pour la configuration dans votre portée de décision.

   ![Voir ID d’emplacement ](assets/decisioning-placement-id.png)

### Règles de décision pour le statut de fidélité

**Règles de décision** spécifiez les conditions dans lesquelles les offres sont présentées. Dans cet exemple, vous créez des règles de décision pour diffuser différentes offres en fonction du statut de fidélité d’un utilisateur.

La liste des règles de décision est accessible dans le menu **Composants**.

Pour créer les règles de décision, procédez comme suit :

1. Accédez à l’onglet **Règles**, puis cliquez sur **Créer une règle**.

   ![Créer la règle](assets/decisioning-create-rule.png)

1. Nommons la première règle « *Règle du statut de fidélité Gold* ». Vous pouvez utiliser des champs XDM pour définir la règle. Le Adobe Experience Platform **Créateur de segments** est une interface intuitive que vous pouvez utiliser pour créer les conditions des règles.

   ![Définir la règle](assets/decisioning-define-rule.png)

1. Cliquez sur **Enregistrer** pour confirmer la condition de la règle.
1. La « *Règle de statut de fidélité Gold* nouvellement enregistrée s’affiche dans la **liste des règles**. Sélectionnez-le pour afficher ses propriétés.

   ![Afficher la règle créée](assets/decisioning-view-rules.png)

1. Créez maintenant les conditions restantes des règles d’offre de fidélité pour le cas d’utilisation.


### Qualificateurs De Collection

**Qualificateurs de collection** permettent d’organiser et de rechercher facilement des offres dans la bibliothèque des offres. Dans cet exemple, vous ajoutez des qualificateurs de collection aux offres de récompenses de fidélité pour améliorer l’organisation de l’offre.

La liste des qualificateurs de collection est accessible dans le menu **Composants**.

Pour créer le qualificateur de collection de récompenses de fidélité, procédez comme suit :

1. Accédez à l’onglet **Qualificateurs de collection**, puis cliquez sur **Créer un qualificateur de collection**.

   ![Créer un qualificateur de collection](assets/decisioning-create-collection-qualifier.png)

1. Nommons le qualificateur de collection « *Récompenses de fidélité* »

   ![Nommez la collection](assets/decisioning-name-collection.png)

1. Le nouveau qualificateur de collection doit maintenant s’afficher dans l’onglet **Qualificateur de collection**

## Offres

Il est maintenant temps de créer les offres de récompenses de fidélité.

La liste des offres est accessible dans le menu **Offres**.

![Afficher le menu des offres](assets/decisioning-offers-menu.png)


### Création d’offres pour différents niveaux de fidélité

Commencez par créer des offres personnalisées pour les différents niveaux de fidélité de Luma.

Pour créer la première **offre**, procédez comme suit :

1. Cliquez sur **Créer une offre**, puis sélectionnez **Offre personnalisée**.

1. Nommons la première offre « Niveau de fidélité *Luma - Or* ». Vous devez indiquer une date et une heure de début/fin pour cette offre. Vous devez également associer le **qualificateur de collection** « *récompenses de fidélité* » à l’offre, ce qui vous permet de mieux vous organiser dans la **bibliothèque des offres**. Cliquez ensuite sur **Suivant**.

   ![Ajouter les détails de l’offre](assets/decisioning-add-offer-details.png)

1. Vous devez maintenant ajouter des **représentations** pour définir l&#39;emplacement d&#39;affichage de l&#39;offre. Choisissons le **canal web**. Choisissons également la « *bannière de page d’accueil* » **emplacement** que vous avez précédemment configurée. Le **emplacement** sélectionné est de type HTML. Vous pouvez donc ajouter du contenu HTML, JSON ou TEXTE directement à l’éditeur pour créer l’offre à l’aide du bouton radio **Personnalisé**.

   ![Ajouter des détails de représentation](assets/decisioning-add-representation-details.png)

1. Modifiez le contenu de l&#39;offre directement à l&#39;aide du **Éditeur d&#39;expression**. N’oubliez pas que vous pouvez ajouter du contenu HTML, JSON ou TEXT à cet emplacement. Veillez à sélectionner le **mode** correct en bas de l’éditeur, en fonction de votre type de contenu. Vous pouvez également cliquer sur **valider** pour vous assurer qu’il n’y a aucune erreur.

   ![Ajout d’une offre HTML](assets/decisioning-add-offer-html.png)

1. Vous pouvez également utiliser l’éditeur d’expression pour récupérer les attributs stockés dans Adobe Experience Platform. Ajoutons le prénom d’un profil au contenu de l’offre pour mieux le personnaliser pour les membres du programme de fidélité au niveau 1:1.

   ![Ajouter la personnalisation d&#39;une offre](assets/decisioning-add-offer-personalization.png)

1. Ajoutez des contraintes pour afficher uniquement l’offre aux profils qui remplissent les critères de la « Règle *Gold Loyalty Status Rule* ».

   ![Ajouter une contrainte de règle](assets/decisioning-add-rule-constraint.png)

1. Une fois la révision de votre offre terminée, cliquez sur **Terminer**. Sélectionnez **Enregistrer et approuver**.

Créez maintenant le reste des offres pour les différents niveaux de fidélité de Luma

### Offres de secours

Vous souhaitez toujours proposer une offre aux visiteurs et visiteuses du site Luma ne faisant pas partie du programme de fidélité Luma. Pour ce faire, vous pouvez configurer une **offre de secours** pour la campagne.

Pour créer l&#39;offre de secours, procédez comme suit :

1. Cliquez sur **Créer une offre**, puis sélectionnez **Offre de secours**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Nommons l’offre de secours « *Fidélité autre que Luma* ». Vous pouvez également associer le **qualificateur de collection** précédemment créé, « *Récompenses de fidélité* » à l’offre de secours pour faciliter l’organisation des offres.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez le contenu de l&#39;offre de secours à l&#39;**Éditeur d&#39;expression**. N’oubliez pas que vous pouvez ajouter du contenu HTML, JSON ou TEXTE à cet emplacement. Veillez à sélectionner le **mode** correct en bas de l’éditeur, en fonction de votre type de contenu. Vous pouvez également cliquer sur **valider** pour vous assurer qu’il n’y a aucune erreur.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Si tout est correctement configuré, appuyez sur **Terminer** puis sur **Enregistrer et approuver**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Décisions

Les **décisions** sont des conteneurs d’offres qui sélectionnent la meilleure offre disponible pour un client ou une cliente, en fonction de la cible.

La liste des décisions est disponible dans l&#39;onglet **Décisions** du menu **Offres**.
<!--
   ![ADD SCREENSHOT](#)
-->

### Création d’une décision pour les offres de fidélité

Créons une décision pour le cas d’utilisation des récompenses de fidélité Luma .

Pour créer la décision, procédez comme suit :

1. Cliquez sur **Créer une décision**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Appelons la décision « Offres de fidélité Luma *décembre* ». Les offres doivent s’exécuter pendant 1 mois. Spécifions-le ici.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous devez maintenant définir les **portées de décision**. Sélectionnez d’abord un emplacement. Vous pouvez utiliser la « *bannière de page d’accueil* » créée précédemment.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous devez ensuite ajouter des **critères d’évaluation** pour la portée de décision. Cliquez sur **Ajouter** et sélectionnez la collection « *Récompenses de fidélité* » précédemment créée **qui contient toutes les offres de fidélité à prendre en compte.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dans la collection « *Récompenses de fidélité* », vous pouvez utiliser le champ d’éligibilité pour restreindre la diffusion de l’offre à un sous-ensemble de visiteurs Luma. Cependant, pour ce cas d’utilisation, vous souhaitez que chaque visiteur reçoive l’une des offres. N’oubliez pas que vous avez configuré une **offre de secours** pour tous les visiteurs non fidèles. Définissez l’éligibilité sur « Aucune ».
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. En outre, vous pouvez utiliser le champ **méthode de classement** pour sélectionner la meilleure offre pour chaque visiteur Luma, si plusieurs offres sont éligibles pour la combinaison utilisateur/emplacement. Pour ce cas d’utilisation, vous pouvez utiliser la méthode **Priorité des offres** qui utilise les valeurs définies dans les offres pour diffuser la meilleure offre.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez maintenant l’**offre de secours** à la décision. Rappel : l’offre de secours est l’offre par défaut affichée pour les visiteurs de Luma s’ils ne font partie d’aucune des audiences de fidélité de Luma. Sélectionnez « *Fidélité autre que Luma* » dans la liste des offres de secours disponibles pour l’emplacement « *Bannière de page d’accueil* ».
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Avant d’activer la décision, examinons la portée de la décision, l’offre de secours, la prévisualisation des offres disponibles et l’estimation des profils qualifiés. Une fois que tout semble correct, vous pouvez cliquer sur **Terminer** et **Enregistrer et activer**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Simulations

Il est recommandé de valider la logique de prise de décision de fidélité Luma pour vous assurer que les offres correctes sont diffusées aux audiences de fidélité appropriées. Vous pouvez effectuer cette validation à l’aide de **profils de test**. Il est également recommandé de tester les modifications apportées aux offres par le biais de profils de test avant de publier de nouvelles versions d’offres en production.

Pour commencer les tests, sélectionnez l’onglet **Simulations** dans le menu **Offres**.

### Test des offres de fidélité

1. Sélectionnez un profil de test à utiliser pour la simulation. Cliquez sur **Gérer le profil**. [Pour créer ou désigner un profil de test pour les tests d’offre, suivez ce guide](https://experienceleague.adobe.com/en/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles#create-test-profiles-csv).
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez un ou plusieurs profils de test à la simulation et enregistrez votre sélection. Pour les tests de cas d’utilisation, vous devez vous assurer que des profils de test sont configurés pour chaque audience de récompenses de fidélité Luma.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez la portée de décision à tester. Sélectionnez **Ajouter une portée de décision**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez l’emplacement « *Bannière de page d’accueil* » créé précédemment.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Les décisions disponibles s’affichent, sélectionnez la décision « Offres de fidélité Luma *décembre* précédemment créée, puis cliquez sur **Ajouter**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Une fois le profil de test sélectionné, cliquez sur **Afficher les résultats**. La meilleure offre disponible s’affiche pour le profil de test sélectionné pour la décision « Offres de fidélité Luma *décembre* ».
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez un autre profil de test, puis cliquez sur **Afficher les résultats**. Idéalement, vous devriez voir une offre simulée différente, correspondant au niveau de fidélité du profil de test.

## Validation de la gestion des décisions à l’aide d’Adobe Experience Platform Debugger

L’extension **Adobe Experience Platform Debugger**, disponible pour Chrome et Firefox, analyse vos pages web pour identifier les problèmes d’implémentation des solutions Adobe Experience Cloud.

Vous pouvez utiliser le débogueur sur le site Luma pour valider la logique de prise de décision en production. Cette validation est une bonne pratique une fois que le cas d’utilisation des récompenses de fidélité est opérationnel, afin de s’assurer que tout est correctement configuré.

[Découvrez comment configurer le débogueur dans votre navigateur à l’aide du guide ici](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Pour commencer la validation à l’aide du débogueur :

1. Accédez à la page web Luma contenant l’emplacement de l’offre.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sur la page web, ouvrez le débogueur Adobe Experience Platform ****.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Accédez à **Résumé**. Vérifiez que l’ID **flux de données** correspond au **flux de données** dans la **Collecte de données Adobe** pour laquelle vous avez activé Offer Decisioning.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sous **Solutions** accédez à **Experience Platform Web SDK**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dans l’onglet **Configuration**, activez l’option **Activer le débogage**. Cela permet la journalisation de la session dans une session **Adobe Experience Platform Assurance**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous pouvez ensuite vous connecter au site avec divers comptes de fidélité Luma et utiliser le débogueur pour valider les requêtes envoyées au réseau Adobe Experience Platform Edge ****. Toutes ces requêtes doivent être capturées dans **Assurance** pour le suivi des journaux.
<!--
   ![ADD SCREENSHOT](#)
-->

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
