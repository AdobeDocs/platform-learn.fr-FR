---
title: Qu’est-ce qu’une couche de données ?
description: Qu’est-ce qu’une couche de données ?
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Qu’est-ce qu’une couche de données ?

Lors de l’implémentation de technologies marketing sur votre site, il est probable que d’importantes données soient éparpillées dans l’interface utilisateur. Par exemple, le nom d’un produit peut se trouver dans un en-tête de la page et le prix peut être inférieur dans la page sous l’image du produit. Si vous souhaitez envoyer ces données à Adobe ou à un autre fournisseur, vous pouvez certainement trouver les éléments de HTML qui contiennent les données en recherchant des balises ou attributs de HTML spécifiques, extraire les données de ces éléments et les envoyer. Mais que se passe-t-il lorsque votre équipe d’ingénieurs décide de déplacer le nom du produit de l’en-tête vers une barre latérale ? Votre mise en oeuvre est interrompue. Votre implémentation ne peut plus trouver l’en-tête ou, pire, elle trouve l’en-tête et envoie des données non pertinentes au serveur.

L’un des principaux objectifs d’une couche de données est de résoudre ce problème. Dans sa plus simple expression, une couche de données est un objet JavaScript (ou, comme nous le verrons plus loin, un tableau) qui contient des données sur le produit sur la page ou toute autre donnée pertinente sur laquelle reposent vos technologies marketing pour atteindre vos objectifs. En ne comptant pas sur les éléments de l’interface utilisateur pour fournir ces données, notre mise en oeuvre devient plus robuste. La couche de données contient les données et doit être considérée comme un contrat. Ce contrat est généralement conclu entre l’équipe d’ingénieurs qui place des données dans la couche de données et l’équipe marketing qui récupère des données de la couche de données.

Si un ingénieur est sur le point de modifier la structure de la couche de données, il est plus probable qu’il envisage de travailler avec l’équipe marketing afin que des modifications appropriées puissent être apportées à l’implémentation marketing. Cette communication et cette coopération _must_ être mis en place au sein de votre entreprise pour garantir une mise en oeuvre robuste.

## Conteneur et contenu

Dans le secteur, le terme &quot;couche de données&quot; est lancé un peu plus ou moins librement et peut souvent conduire à la confusion et à la mauvaise communication. Prenons par exemple une boîte de billes. Il existe deux parties : le conteneur (la boîte) et le contenu (les billes). De même, une couche de données est souvent considérée comme comportant deux parties : le conteneur (l’objet ou le tableau JavaScript) et le contenu (les éléments de données comme `priceTotal`, `currencyCode`, et `purchaseOrderNumber` ).

Comme ce tutoriel fait référence à la couche de données client Adobe, il fait référence au conteneur et non au contenu. Lorsqu’il fait référence à XDM, il fait référence au contenu et non au conteneur. Dans le cas de la couche de données client Adobe, peu importe que le contenu soit XDM ou votre propre modèle de données. La couche de données client Adobe s’en fiche. Ce n&#39;est qu&#39;une boîte. Mais elle _is_ une boîte avec des pouvoirs spéciaux...

## Communication des modifications

Lors de l’utilisation d’une couche de données, vous pouvez modifier le contenu à tout moment. C&#39;est une fonctionnalité intéressante, parce que les données peuvent être disponibles à différents moments. Par exemple, certaines données sur l’utilisateur peuvent être disponibles immédiatement, mais vous devrez peut-être adresser une requête asynchrone à un tiers pour plus d’informations. Cela nécessite une attention particulière. Si vous devez envoyer ces données asynchrones à Adobe Experience Platform à un moment donné, comment vos technologies marketing savent-elles quand certaines données ont été ajoutées à la couche de données et sont prêtes à être envoyées ? Vous avez besoin d’une couche de données plus intelligente, c’est-à-dire une couche de données pilotée par les événements.

Une couche de données orientée événements peut signaler que son contenu a changé afin que les technologies marketing puissent réagir au changement. Utilisé correctement, cela peut aider à éviter les problèmes de minutage qui surviennent souvent avec les couches de données qui n’ont aucun moyen de communiquer lorsque des modifications se produisent.

La couche de données client Adobe est une couche de données pilotée par les événements.
