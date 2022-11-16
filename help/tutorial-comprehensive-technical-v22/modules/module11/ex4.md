---
title: Customer Journey Analytics - Préparation des données dans Analysis Workspace
description: Customer Journey Analytics - Préparation des données dans Analysis Workspace
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c1d4037b-7656-4777-86ad-a1e3e9a8464b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 10%

---

# 11.4 Préparation des données dans Analysis Workspace

## Objectifs

- Présentation de l’interface utilisateur d’Analysis Workspace dans CJA
- Présentation des concepts de préparation des données dans Analysis Workspace
- Découvrez comment effectuer des calculs de données

## 11.4.1 Interface utilisateur d’Analysis Workspace dans CJA

Analysis Workspace élimine toutes les limites courantes d’un rapport Analytics unique. Il offre un canevas robuste et souple permettant de créer des projets d’analyses personnalisés. Faites glisser un nombre indéfini de tableaux de données, de visualisations et de composants (dimensions, mesures, segments et granularités temporelles) vers un projet. Créez instantanément des ventilations et des segments, des cohortes pour analyse, ainsi que des alertes, comparez des segments, analysez les flux et les abandons, et traitez et planifiez les rapports pour les partager avec n’importe qui dans votre entreprise.

Customer Journey Analytics ajoute cette solution aux données Platform. Nous vous recommandons vivement de regarder cette vidéo de présentation de quatre minutes :

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Si vous n’avez jamais utilisé Analysis Workspace auparavant, nous vous recommandons vivement de regarder cette vidéo :

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Créer un projet

Il est maintenant temps de créer votre premier projet CJA. Accédez à l’onglet Projets dans CJA.
Cliquez sur **Créer**.

![demo](./images/prmenu.png)

Vous verrez alors ceci. Sélectionner **Projet vierge** puis cliquez sur **Créer**.

![demo](./images/prmenu1.png)

Vous verrez alors un projet vide.

![demo](./images/premptyprojects.png)

Tout d’abord, veillez à sélectionner la bonne vue de données dans le coin supérieur droit de votre écran. Dans cet exemple, la Vue des données à sélectionner est `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Ensuite, vous allez enregistrer votre projet et lui donner un nom. Vous pouvez utiliser la commande suivante pour enregistrer :

| Système d’exploitation | Court |
| ----------------- |-------------| 
| Windows | Ctrl + S |
| Mac | Commande + S |

Vous verrez cette fenêtre contextuelle :

![demo](./images/prsave.png)

Utilisez cette convention d’affectation des noms :

| Nom | Description |
| ----------------- |-------------| 
| `--demoProfileLdap-- - Omnichannel Analysis` | `--demoProfileLdap-- - Omnichannel Analysis` |

Cliquez ensuite sur **Enregistrer**.

![demo](./images/prsave2.png)

## 11.4.2 Mesures calculées

Bien que nous ayons organisé tous les composants dans la vue de données, vous devez en adapter certains afin que les utilisateurs professionnels soient prêts à commencer leur analyse. En outre, durant toute analyse, vous pouvez créer une mesure calculée pour approfondir les résultats des insights.

Par exemple, nous allons créer un calcul **Taux de conversion** en utilisant la variable **Achats** mesure/événement que nous avons défini sur la vue de données.

### Taux de conversion

Commençons par ouvrir le créateur de mesures calculées. Cliquez sur le bouton **+** pour créer votre première mesure calculée dans Analysis Workspace.

![demo](./images/pradd.png)

Le **Créateur de mesures calculées** s’affiche :

![demo](./images/prbuilder.png)

Recherchez le **Achats** dans la liste des mesures du menu de gauche. Sous **Mesures** click **Tout afficher**

![demo](./images/calcbuildercr1.png)

Faites maintenant glisser un composant **Achats** dans la définition de mesure calculée.

![demo](./images/calcbuildercr2.png)

En règle générale, le taux de conversion signifie **Conversions / Sessions**. Alors faisons le même calcul dans le canevas de définition de mesure calculée. Recherchez le **Sessions** et faites-la glisser et déposez-la dans le créateur de définitions, sous **Achats** .

![demo](./images/calcbuildercr3.png)

Notez que l’opérateur de division est automatiquement sélectionné.

![demo](./images/calcbuildercr4.png)

Le taux de conversion est généralement représenté en pourcentage. Donc, changeons le format en pourcentage et sélectionnons aussi 2 décimales.

![demo](./images/calcbuildercr5.png)

Enfin, modifiez le nom et la description de la mesure calculée :

| Titre | Description |
| ----------------- |-------------| 
| Taux de conversion | Taux de conversion |

Vous verrez ce qui suit sur votre écran :

![demo](./images/calcbuildercr6.png)

N&#39;oublie pas de **Enregistrer** Mesure calculée.

![demo](./images/pr9.png)

## 11.4.3 Dimensions calculées : Filtres (segmentation) et plages de dates

### Filtres : Dimensions calculées

Les calculs ne sont pas destinés uniquement aux mesures. Avant de commencer une analyse, il est également intéressant de créer des analyses. **Dimensions calculées**. En gros, ça voulait dire **segments** de retour dans Adobe Analytics. En Customer Journey Analytics, ces segments sont appelés **Filtres**.

![demo](./images/prfilters.png)

La création de filtres permet aux utilisateurs professionnels de commencer l’analyse avec des dimensions calculées importantes. Cela permettra d’automatiser certaines tâches et d’aider à l’étape d’adoption. Voici quelques exemples :

1. Média, Média Payé,
2. Visites nouvelles ou renouvelées
3. Clients avec panier abandonné

Ces filtres peuvent être créés avant ou pendant la partie analyse (ce que vous allez faire lors de l’exercice suivant).

### Périodes : Dimensions de temps calculées

Les Dimensions de temps sont un autre type de dimensions calculées. Certains sont déjà créés, mais vous avez également la possibilité de créer vos propres Dimensions de temps personnalisées lors de la phase de préparation des données.

Ces Dimensions de temps calculé nous aideront les analystes et les utilisateurs professionnels à mémoriser des dates importantes et à les utiliser pour filtrer et modifier l’heure de création de rapports. Questions et doutes typiques qui nous viennent à l&#39;esprit lorsque nous faisons de l&#39;analyse :

- Quand était le Black Friday l&#39;année dernière ? 21e-29e ?
- Quand avons-nous dirigé cette campagne télévisée en décembre ?
- Quand avons-nous réalisé les ventes d&#39;été 2018 ? Je veux le comparer à 2019. Au fait, connaissez-vous les jours exacts de 2019 ?

![demo](./images/timedimensions.png)

Vous avez maintenant terminé l’exercice de préparation des données à l’aide de CJA Analysis Workspace.

Étape suivante : [11.5 Visualisation à l’aide de Customer Journey Analytics](./ex5.md)

[Revenir au module 11](./customer-journey-analytics-build-a-dashboard.md)

[Revenir à tous les modules](./../../overview.md)
