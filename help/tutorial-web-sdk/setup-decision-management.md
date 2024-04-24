---
title: Configuration de la gestion des décisions avec le SDK Web de Platform
description: Découvrez comment mettre en oeuvre la gestion de la décision à l’aide du SDK Web Platform. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Decision Management,Offers
exl-id: f7852ef4-44b0-49df-aec8-cb211726247d
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '2511'
ht-degree: 3%

---

# Configuration de la gestion des décisions avec le SDK Web de Platform

Découvrez comment mettre en oeuvre la gestion de la décision à l’aide du SDK Web Platform. Ce guide couvre les conditions préalables fondamentales de la gestion des décisions, les étapes détaillées pour la configuration et une présentation approfondie d’un cas d’utilisation centré sur l’état de fidélité.

En suivant ce tutoriel, les utilisateurs de Journey Optimizer sont équipés pour appliquer efficacement les fonctionnalités d’offer decisioning, ce qui améliore la personnalisation et la pertinence de leurs interactions avec les clients.


![Diagramme SDK Web et Adobe Analytics](assets/dc-websdk-ajo.png)

## Objectifs d’apprentissage

À la fin de cette leçon, vous pouvez :

* Maîtrisez les concepts de base de la gestion de la décision dans Adobe Journey Optimizer et son intégration au SDK Web de Adobe Experience Platform.

* Découvrez le processus détaillé de configuration du SDK Web pour Offer Decisioning, assurant une intégration transparente avec Journey Optimizer.

* Explorez un cas d’utilisation détaillé axé sur les offres d’état de fidélité, en obtenant des informations sur la création et la gestion efficaces des offres, des décisions et des emplacements.

* Familiarisez-vous avec les termes essentiels et leurs implications dans le cadre de la gestion de la décision.

* Comprenez l’importance des règles de décision, des qualificateurs de collecte et des offres de secours pour diffuser l’offre appropriée à l’utilisateur approprié.

* Découvrez des rubriques avancées telles que les simulations et la collecte de données d’événement personnalisé, ce qui vous permet de tester, valider et améliorer vos mécanismes de diffusion d’offres.

## Conditions préalables

Pour terminer les leçons de cette section, vous devez d’abord :

* Assurez-vous que votre entreprise a accès à Adobe Journey Optimizer Ultimate (Journey Optimizer et Offer Decisioning) ou à Adobe Experience Platform et au module complémentaire du service d’application Offer Decisioning.

* Suivez toutes les leçons pour la configuration initiale du SDK Web de Platform.

* Activez votre organisation pour Edge Decisioning.

* Découvrez comment configurer un emplacement et instancier les ID d’emplacement et d’activité dans votre JSON de portée de décision.

## Limites

Prenez note des restrictions suivantes :

* Les offres basées sur un événement ne sont actuellement pas prises en charge dans Adobe Journey Optimizer. Si vous créez une règle de décision basée sur un événement, vous ne pouvez pas l’appliquer dans une offre.

## Octroi de l’accès à la gestion des décisions

Pour accorder l’accès à la fonctionnalité de gestion des décisions, vous devez créer une **Profil de produit** et attribuez les autorisations correspondantes à vos utilisateurs. [En savoir plus sur la gestion des utilisateurs et des autorisations Journey Optimizer dans cette section](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions#decisions-permissions).

## Configuration du flux de données

Offer Decisioning doit être activé dans la variable **datastream** avant que toute activité de gestion de la décision ne puisse être diffusée par le SDK Web de Platform.

Pour configurer l’Offer decisioning dans le flux de données :

1. Accédez au [Collecte de données](https://experience.adobe.com/#/data-collection) .

1. Dans le volet de navigation de gauche, sélectionnez **Datastreams**.

1. Sélectionnez le flux de données SDK Web Luma créé précédemment.

   ![Sélectionner un flux de données](assets/decisioning-datastream-select.png)

1. Sélectionner **Modifier** dans la fonction **Adobe Experience Platform Service**.

   ![Service d’édition](assets/decisioning-edit-datastream.png)

1. Vérifiez les **Offer decisioning** de la boîte.

   ![AJOUTER UNE CAPTURE D’ÉCRAN](assets/decisioning-check-offer-box.png)

1. Sélectionnez **Enregistrer**.

Ainsi, les événements entrants pour Journey Optimizer sont correctement gérés par la variable **Adobe Experience Platform Edge**.

## Configuration du SDK pour la gestion de la décision

La gestion des décisions nécessite des étapes SDK supplémentaires, selon le type de mise en oeuvre du SDK Web. Deux options sont disponibles pour configurer le SDK pour la gestion de la décision.

* Installation autonome du SDK
   1. Configurez la variable `sendEvent` agissez avec votre `decisionScopes`.

      ```javascript
      alloy("sendEvent", {
         ...
         "decisionScopes": [
            "[DECISION SCOPE 1]",
            "[DECISION SCOPE 2]"
         ]
      })
      ```

* Installation des balises SDK
   1. Accédez à l’interface Collecte de données .

   1. Dans le volet de navigation de gauche, sélectionnez **Balises**.

      ![Sélectionner des balises](assets/decisioning-data-collection-tags.png)

   1. Sélectionnez la variable **Propriété de balise**.

   1. Créez votre **Règles**.
      * Ajout d’un SDK Web Platform **Action Envoyer l’événement** et ajoutez les `decisionScopes` à la configuration de cette action.

   1. Création et publication d’une **Bibliothèque** contenant tous les éléments pertinents **Règles**, **Éléments de données**, et **Extensions** vous avez configuré.

## Terminologie

Tout d’abord, vous devez comprendre la terminologie utilisée dans l’interface de gestion des décisions.

* **Limitation**: contrainte déterminant la fréquence d’affichage d’une offre. Deux types :
   * Limites totales : nombre maximal de fois où une offre peut être affichée dans l’audience cible.
   * Limite de profil : la fréquence à laquelle une offre peut être présentée à un utilisateur spécifique.
* **Collections**: sous-ensembles d’offres regroupés par conditions spécifiques définies par un marketeur, par exemple catégorie d’offres.
* **Décision**: logique qui détermine le choix d’une offre.
* **Règle de décision**: contraintes sur les offres pour déterminer l’éligibilité d’un utilisateur.
* **Offre éligible**: offre qui correspond aux contraintes prédéfinies et qui peut être présentée à un utilisateur.
* **Gestion des décisions**: système de conception et de distribution d’offres personnalisées à l’aide d’une logique commerciale et de règles de décision.
* **Offres de secours**: offre par défaut affichée lorsqu’un utilisateur ne remplit aucune condition pour recevoir une offre dans une collection.
* **Offre**: message marketing avec des règles d’éligibilité potentielles déterminant ses visionneuses.
* **Bibliothèque d’offres**: un référentiel central qui gère les offres, les décisions et les règles associées.
* **Offres personnalisées**: messages marketing personnalisés adaptés en fonction des contraintes d’éligibilité.
* **Emplacements**: paramètre ou scénario dans lequel une offre s’affiche pour un utilisateur.
* **Priorité**: mesure de classement pour les offres qui prennent en compte diverses contraintes telles que l’éligibilité et la limitation.
* **Représentations**: informations spécifiques au canal, par exemple, emplacement ou langue, qui guident l’affichage d’une offre.

## Présentation du cas d’utilisation - Loyalty Rewards

Dans cette leçon, vous implémentez un exemple de cas d’utilisation Loyalty Rewards pour comprendre la gestion des décisions à l’aide du SDK Web.

Ce cas pratique vous permet de mieux comprendre comment Journey Optimizer peut vous aider à proposer la meilleure offre à vos clients, en utilisant la bibliothèque d’offres centralisée et le moteur de décision d’offre.

>[!NOTE]
>
> Comme ce tutoriel est destiné aux implémentateurs, il est intéressant de noter que cette leçon implique un travail d’interface substantiel dans Journey Optimizer. Bien que ces tâches d’interface soient généralement gérées par les marketeurs, il peut s’avérer utile pour les implémenteurs d’obtenir des informations sur le processus, même s’ils ne sont pas responsables de la création de campagnes de gestion de décision à long terme.

## Composants

Avant de commencer à créer les offres, vous devez définir plusieurs composants prérequis.

### Création d’un emplacement pour les offres de fidélité

**Emplacements** sont des conteneurs utilisés pour présenter les offres. Dans cet exemple, vous créez un emplacement en haut du site Luma.

La liste des emplacements est accessible dans le menu **Composants**. Des filtres sont disponibles pour vous aider à récupérer des emplacements en fonction d&#39;un canal ou d&#39;un contenu spécifique.

![Affichage des emplacements](assets/decisioning-placements-list.png)

Pour créer l’emplacement, procédez comme suit :

1. Cliquez sur **Créer un emplacement**.

   ![Créer un emplacement](assets/decisioning-create-placement.png)

1. Définissez les propriétés de l&#39;emplacement :
   * **Nom** : nom de l&#39;emplacement. Appelons l’exemple d’emplacement *&quot;Bannière de page d’accueil&quot;*.
   * **Type de canal**: canal pour lequel l’emplacement est utilisé. Utilisons *&#39;Web&#39;* car les offres s’affichent sur le site web de Luma.
   * **Type de contenu**: type de contenu que l’emplacement peut afficher : texte, HTML, lien d’image ou JSON. Vous pouvez utiliser *&quot;HTML&quot;* pour l’offre.
   * **Description** : description de l’emplacement (facultatif).

   ![Ajouter des détails](assets/decisioning-placement-details.png)

1. Cliquez sur **Enregistrer**.
1. Une fois l’emplacement créé, il s’affiche dans la liste des emplacements.
1. Sélectionnez la ligne contenant votre nouvel emplacement et notez l’identifiant de référencement, car cela peut s’avérer nécessaire pour la configuration dans votre champ de décision.

   ![Voir Identifiant de référencement ](assets/decisioning-placement-id.png)

### Règles de décision relatives à l’état de fidélité

**Règles de décision** indiquez les conditions dans lesquelles les offres sont présentées. Dans cet exemple, vous créez des règles de décision pour proposer différentes offres en fonction de l’état de fidélité d’un utilisateur.

La liste des règles de décision est accessible dans la variable **Composants** .

Pour créer des règles de décision, procédez comme suit :

1. Accédez au **Règles** , puis cliquez sur **Créer une règle**.

   ![Création de la règle](assets/decisioning-create-rule.png)

1. Nommons la première règle &#39;*Règle d’état de fidélité Gold*&#39;. Vous pouvez utiliser des champs XDM pour définir la règle. Adobe Experience Platform **Créateur de segments** est une interface intuitive que vous pouvez utiliser pour créer les conditions de règle.

   ![Définir la règle](assets/decisioning-define-rule.png)

1. Cliquez sur **Enregistrer** pour confirmer la condition de la règle.
1. Le nouveau fichier enregistré&#x200B;*Règle d’état de fidélité Gold*&quot; s’affichera dans le **Liste des règles**. Sélectionnez-la pour afficher ses propriétés.

   ![Afficher la règle créée](assets/decisioning-view-rules.png)

1. Créez maintenant les conditions de règle d’offre de fidélité restantes pour le cas d’utilisation.


### Qualificateurs de collection

**Qualificateurs de collection** vous permettent d’organiser et de rechercher facilement des offres dans la bibliothèque d’offres. Dans cet exemple, vous ajoutez des qualificateurs de collection aux offres Loyalty Rewards afin d’améliorer l’organisation des offres.

La liste des qualificateurs de collection est accessible dans la variable **Composants** .

Pour créer le qualificateur de collection Loyalty Rewards, procédez comme suit :

1. Accédez au **Qualificateurs de collection** , puis cliquez sur **Création d’un qualificateur de collection**.

   ![Création d’un qualificateur de collection](assets/decisioning-create-collection-qualifier.png)

1. Nommons le qualificateur de collection &#39;*Loyalty Rewards*&#39;

   ![Nommer la collection](assets/decisioning-name-collection.png)

1. Le nouveau qualificateur de collection doit maintenant s’afficher dans la variable **Qualificateur de collection** tab

## Offres

Il est maintenant temps de créer les offres Loyalty Rewards.

La liste des offres est accessible dans le **Offres** .

![Afficher le menu des offres](assets/decisioning-offers-menu.png)


### Création d’offres pour différents niveaux de fidélité

Commencez par créer des offres personnalisées pour les différents niveaux de fidélité de Luma.

Pour créer la première **offre**, procédez comme suit :

1. Cliquez sur **Créer une offre**, puis sélectionnez **Offre personnalisée**.

1. Nommons la première offre &#39;*Niveau de fidélité Luma - Or*&#39;. Vous devez spécifier une date et une heure de début/fin pour cette offre. Vous devez également associer la variable **qualificateur de collection** &#39;*Loyalty Rewards*&quot; à l’offre, ce qui vous permet de mieux vous organiser dans la variable **Bibliothèque d’offres**. Ensuite, cliquez sur **Suivant**.

   ![Ajout des détails de l’offre](assets/decisioning-add-offer-details.png)

1. Maintenant, vous devez ajouter **représentations** pour définir où s’affiche l’offre. Choisissons le **canal web**. Sélectionnez également le &quot;&quot;.*Bannière de page d’accueil*&#39; **placement** vous avez précédemment configuré. La sélection **placement** est de type HTML. Vous pouvez ainsi ajouter du contenu HTML, JSON ou TEXTE directement à l’éditeur pour créer l’offre à l’aide de la fonction **Personnalisé** bouton radio.

   ![Ajout de détails de représentation](assets/decisioning-add-representation-details.png)

1. Modifiez le contenu de l&#39;offre directement à l&#39;aide de la fonction **Éditeur d’expression**. N’oubliez pas que vous pouvez ajouter du contenu HTML, JSON ou TEXTE à cet emplacement. Assurez-vous de sélectionner les **mode** en bas de l’éditeur, selon le type de contenu. Vous pouvez également accéder à **valider** pour s’assurer qu’il n’y a aucune erreur.

   ![Ajouter un HTML d&#39;offres](assets/decisioning-add-offer-html.png)

1. Vous pouvez également utiliser l’éditeur d’expression pour récupérer les attributs stockés dans Adobe Experience Platform. Ajoutons le prénom d’un profil au contenu de l’offre afin de mieux personnaliser les membres du programme de fidélité au niveau 1:1.

   ![Ajout de la personnalisation des offres](assets/decisioning-add-offer-personalization.png)

1. Ajoutez des contraintes pour n’afficher que l’offre aux profils qui remplissent les critères de &quot;&quot;*Règle d’état de fidélité Gold*&#39;.

   ![Ajouter une contrainte de règle](assets/decisioning-add-rule-constraint.png)

1. Une fois que vous avez terminé de revoir votre offre, cliquez sur **Terminer**. Sélectionnez **Enregistrer et approuver**.

Créez maintenant le reste des offres pour les différents niveaux de fidélité Luma.

### Offres de secours

Vous souhaitez toujours proposer une offre aux visiteurs non fidèles de Luma sur le site Luma. Pour ce faire, vous pouvez configurer une **offre de secours** pour la campagne.

Pour créer l’offre de secours, procédez comme suit :

1. Cliquez sur **Créer une offre**, puis sélectionnez **Offre de secours**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Nommons l’offre de secours &quot;*Fidélité des non-Luma*&#39;. Vous pouvez également associer les **qualificateur de collection**, &#39;*Loyalty Rewards*&quot; à l’offre de secours pour faciliter l’organisation des offres.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez le contenu de l’offre de secours au **Éditeur d’expression**. N’oubliez pas que vous pouvez ajouter du contenu HTML, JSON ou TEXTE à cet emplacement. Assurez-vous de sélectionner les **mode** en bas de l’éditeur, selon le type de contenu. Vous pouvez également accéder à **valider** pour s’assurer qu’il n’y a aucune erreur.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Si tout est configuré correctement, appuyez sur **Terminer** puis **Enregistrer et approuver**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Décisions

**Décisions** sont des conteneurs pour les offres qui sélectionnent la meilleure offre disponible pour un client, selon la cible.

La liste des décisions est disponible dans le **Décisions** de la **Offres** .
<!--
   ![ADD SCREENSHOT](#)
-->

### Création d’une décision pour les offres de fidélité

Créons une décision pour le cas d’utilisation Loyalty Rewards de Luma.

Pour créer la décision, procédez comme suit :

1. Cliquez sur **Créer une décision**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Appelons la décision, &#39;*Offres de fidélité Luma de décembre*&#39;. Les offres doivent durer un mois. Indiquez-les ici.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous devez maintenant définir la variable **portées de décision**. Sélectionnez tout d’abord un emplacement. Vous pouvez utiliser le &quot;&quot; créé précédemment.*Bannière de page d’accueil*&#39;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ensuite, vous devez ajouter **critères d’évaluation** pour la portée de la décision. Cliquez sur **Ajouter** et sélectionnez le &quot;&quot; créé précédemment.*Loyalty Rewards*&#39; **collection** qui contient toutes les offres de fidélité à prendre en compte.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dans le *Loyalty Rewards* Collection, vous pouvez utiliser le champ d’éligibilité pour restreindre la diffusion de l’offre à un sous-ensemble de visiteurs Luma. Cependant, dans ce cas pratique, vous souhaitez que chaque visiteur reçoive l’une des offres. Pour rappel, vous avez configuré une **offre de secours** pour tous les visiteurs qui ne sont pas fidèles. Définissez l’éligibilité sur &quot;Aucun&quot;.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous pouvez également utiliser la variable **méthode de classement** pour sélectionner la meilleure offre pour chaque visiteur Luma, si plusieurs offres sont éligibles pour la combinaison utilisateur/emplacement. Pour ce cas pratique, vous pouvez utiliser la variable **Priorité des offres** qui utilise les valeurs définies dans les offres pour proposer la meilleure offre.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez maintenant la variable **offre de secours** à la décision. N’oubliez pas que l’offre de secours est l’offre par défaut qui s’affiche pour les visiteurs Luma s’ils ne font partie d’aucune des audiences de fidélité Luma. Sélectionnez &quot;*Fidélité des non-Luma*&#39; dans la liste des offres de secours disponibles pour le &#39;*Bannière de page d’accueil* Emplacement.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Avant d’activer la décision, examinons la portée de la décision, l’offre de secours, prévisualisons les offres disponibles et évaluons les profils qualifiés. Une fois que tout a l’air correct, vous pouvez cliquer sur **Terminer** et **Enregistrer et activer**.
<!--
   ![ADD SCREENSHOT](#)
-->

## Simulation

En règle générale, vous devez valider la logique de prise de décision de fidélité de Luma pour vous assurer que les offres correctes sont diffusées aux audiences de fidélité appropriées. Pour ce faire, utilisez **profils de test**. Il est également conseillé de tester les modifications apportées aux offres via des profils de test avant de mettre en production de nouvelles versions d’offres.

Pour commencer le test, sélectionnez l’événement **Simulation** à partir de la **Offres** .

### Test des offres de fidélité

1. Sélectionnez un profil de test à utiliser pour la simulation. Cliquez sur **Gérer le profil**. [Pour créer ou désigner un nouveau profil de test pour le test d’offre, suivez ce guide.](https://experienceleague.adobe.com/en/docs/journeys/using/building-journeys/about-journey-building/creating-test-profiles#create-test-profiles-csv).
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Ajoutez un ou plusieurs profils de test à la simulation et enregistrez votre sélection. Pour les tests de cas d’utilisation, vous devez vous assurer que vous disposez de profils de test configurés pour chaque audience de récompenses de fidélité Luma.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez la portée de décision à tester. Sélectionnez **Ajouter une portée de décision**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez le &quot;&quot; créé précédemment.*Bannière de page d’accueil* Emplacement.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Les décisions disponibles s&#39;affichent, sélectionnez le &quot;&quot; créé précédemment *Offres de fidélité Luma de décembre*&quot;, puis cliquez sur **Ajouter**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Lorsque vous sélectionnez un profil de test, cliquez sur **Affichage des résultats**. La meilleure offre disponible s’affiche pour le profil de test sélectionné pour le *Offres de fidélité Luma de décembre*&quot; décision.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sélectionnez un autre profil de test, puis cliquez sur **Affichage des résultats**. Idéalement, vous devriez voir une offre simulée différente, correspondant au niveau de fidélité du profil de test.

## Validation de la gestion des décisions à l’aide d’Adobe Experience Platform Debugger

La variable **Adobe Experience Platform Debugger** , disponible pour Chrome et Firefox, analyse vos pages web afin d’identifier les problèmes liés à la mise en oeuvre des solutions Adobe Experience Cloud.

Vous pouvez utiliser le débogueur sur le site Luma pour valider la logique de prise de décision en production. Il s’agit d’une bonne pratique une fois que le cas d’utilisation Loyalty Rewards est opérationnel, afin de s’assurer que tout est correctement configuré.

[Découvrez comment configurer le débogueur dans votre navigateur en suivant le guide ici](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/debugger/overview).

Pour commencer la validation à l’aide du débogueur :

1. Accédez à la page web Luma avec l’emplacement de l’offre.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Lorsque vous vous trouvez sur la page web, ouvrez le **Débogueur Adobe Experience Platform**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Accédez à **Résumé**. Vérifiez que la variable **Identifiant du flux de données** correspond à la variable **datastream** in **Adobe de la collecte de données** pour laquelle vous avez activé Offer Decisioning.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Sous **Solutions** accédez à la **SDK Web Experience Platform**.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Dans le **Configuration** onglet, activer **Activation du débogage**. Cela permet la journalisation de la session dans une **Adobe Experience Platform Assurance** session.
   <!--
      ![ADD SCREENSHOT](#)
   -->
1. Vous pouvez ensuite vous connecter au site à l’aide de divers comptes de fidélité Luma et utiliser le débogueur pour valider les requêtes envoyées à l’ **Réseau Adobe Experience Platform Edge**. Toutes ces requêtes doivent être capturées dans **Assurance** pour le suivi des journaux.
<!--
   ![ADD SCREENSHOT](#)
-->

[Suivant : ](setup-consent.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
