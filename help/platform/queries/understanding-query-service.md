---
title: Présentation de Query Service et de Data Distiller
description: Adobe Experience Platform Query Service permet aux utilisateurs d’explorer, de valider et de transformer les données d’expérience client stockées dans le lac de données à l’aide de SQL. Des fonctionnalités améliorées telles que la sortie de données et la planification sont disponibles via le module complémentaire Data Distiller. Cette vidéo présente les principales fonctionnalités de pour aider les utilisateurs à comprendre comment exploiter Query Service dans diverses applications basées sur Platform.
feature: Queries
role: Data Engineer, Developer
level: Beginner
jira: KT-3139
last-substantial-update: 2025-06-23T00:00:00Z
exl-id: 988bc316-9eec-4dca-8049-95c2d613379d
source-git-commit: b0466e114d657c2584b23bfd76e4f6c185c83c06
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 17%

---

# Présentation de Query Service et de Data Distiller

Adobe Experience Platform Query Service permet aux utilisateurs d’explorer, de valider et de transformer les données d’expérience client stockées dans le lac de données à l’aide de SQL. Des fonctionnalités améliorées telles que la sortie de données et la planification sont disponibles via le module complémentaire Data Distiller. Cette vidéo présente les principales fonctionnalités de pour aider les utilisateurs à comprendre comment exploiter Query Service dans diverses applications basées sur Platform. Pour plus d’informations, consultez la [documentation de Query Service](https://experienceleague.adobe.com/fr/docs/experience-platform/query/home).

>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on&enablevpops)

## Utilisation de base

<!-- CARDS
* query-service-ui.md
* query-service-api.md
* adobe-defined-functions.md
* run-queries.md
* understanding-data-usage-patterns-with-query-service.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service UI">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-ui.md" title="Interface utilisateur de Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333403?format=jpeg&nocache=1740415310696" alt="Interface utilisateur de Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-ui.md" target="_blank" rel="referrer" title="Interface utilisateur de Query Service">UI Query Service</a>
                    </p>
                    <p class="is-size-6">Apprenez comment écrire et exécuter des requêtes, afficher des requêtes précédemment exécutées et accéder à des requêtes enregistrées par dʼautres utilisateurs au sein de votre organisation IMS dans Query Service dʼAdobe Experience Platform.</p>
                </div>
                <a href="query-service-ui.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Query Service API">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="query-service-api.md" title="API Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333700?format=jpeg&nocache=1740415310716" alt="API Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="query-service-api.md" target="_blank" rel="referrer" title="API Query Service">API Query Service</a>
                    </p>
                    <p class="is-size-6">Découvrez comment écrire et exécuter des requêtes, créer des requêtes de planning et créer un modèle de requête à l’aide de l’API Query Service de Adobe Experience Platform.</p>
                </div>
                <a href="query-service-api.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Adobe Defined Functions">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="adobe-defined-functions.md" title="Fonctions définies par Adobe" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333701?format=jpeg&nocache=1740415310668" alt="Fonctions définies par Adobe"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="adobe-defined-functions.md" target="_blank" rel="referrer" title="Fonctions définies par Adobe">Fonctions définies par Adobe</a>
                    </p>
                    <p class="is-size-6">Découvrez comment utiliser des fonctions définies par Adobe dans Adobe Experience Platform Query Service pour effectuer des tâches courantes liées à l’entreprise sur les données d’événement d’expérience.</p>
                </div>
                <a href="adobe-defined-functions.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Run Queries with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="run-queries.md" title="Exécuter des requêtes avec Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29796?format=jpeg&nocache=1740415310683" alt="Exécuter des requêtes avec Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="run-queries.md" target="_blank" rel="referrer" title="Exécuter des requêtes avec Query Service">Exécuter des requêtes avec Query Service</a>
                    </p>
                    <p class="is-size-6">Cette vidéo montre comment exécuter des requêtes dans l’interface de Adobe Experience Platform et dans un client PSQL. En outre, l’utilisation de propriétés individuelles dans un objet XDM, l’utilisation de fonctions définies par Adobe et l’utilisation de CREATE TABLE AS SELECT (CTAS) sont illustrées.</p>
                </div>
                <a href="run-queries.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Comprendre les modèles d’utilisation des données avec Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415310706" alt="Comprendre les modèles d’utilisation des données avec Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Comprendre les modèles d’utilisation des données avec Query Service">Présentation des modèles d’utilisation des données avec Query Service</a>
                    </p>
                    <p class="is-size-6">Cette vidéo partage des conseils et des bonnes pratiques pour l’exécution de requêtes dans l’interface du requêteur, les clients PSQL, les solutions de Business Intelligence (BI) et l’API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Validation et exploration des données

<!-- CARDS
* explore-data.md
* validate-data-in-the-datalake.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Explore data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="explore-data.md" title="Exploration des données" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333415?format=jpeg&nocache=1740415312087" alt="Exploration des données"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="explore-data.md" target="_blank" rel="referrer" title="Exploration des données">Explorer des données</a>
                    </p>
                    <p class="is-size-6">Apprenez comment valider les données ingérées, prévisualiser les données et explorer les propriétés statistiques et analytiques des données à lʼaide des fonctions SQL.</p>
                </div>
                <a href="explore-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Validate data in the datalake with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="validate-data-in-the-datalake.md" title="Valider des données dans le lac de données avec Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416130?format=jpeg&nocache=1740415312076" alt="Valider des données dans le lac de données avec Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" title="Valider des données dans le lac de données avec Query Service">Valider des données dans le lac de données avec Query Service</a>
                    </p>
                    <p class="is-size-6">Découvrez comment vérifier si les données ont bien été ingérées dans le lac de données à l’aide de Adobe Experience Platform Query Service.</p>
                </div>
                <a href="validate-data-in-the-datalake.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Transformation des données avec Data Distiller

<!-- CARDS
* 
* prepare-data.md
* 
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Prepare data">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="prepare-data.md" title="Préparer les données" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333699?format=jpeg&nocache=1740415313086" alt="Préparer les données"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="prepare-data.md" target="_blank" rel="referrer" title="Préparer les données">Préparation des données</a>
                    </p>
                    <p class="is-size-6">Découvrez comment nettoyer, préparer et combiner des données provenant de plusieurs jeux de données afin de créer un jeu de données à l’aide des fonctions CTAS (Create Table AS) et Spark SQL pour la création de rapports et de tableaux de bord.</p>
                </div>
                <a href="prepare-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Cas d’utilisation

<!-- CARDS
* understanding-data-usage-patterns-with-query-service.md
* psql-client-tableau.md
* analyze-and-visualize.md
* recharge-your-customer-data.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Understanding Data Usage Patterns with Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="understanding-data-usage-patterns-with-query-service.md" title="Comprendre les modèles d’utilisation des données avec Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/29811?format=jpeg&nocache=1740415313190" alt="Comprendre les modèles d’utilisation des données avec Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" title="Comprendre les modèles d’utilisation des données avec Query Service">Présentation des modèles d’utilisation des données avec Query Service</a>
                    </p>
                    <p class="is-size-6">Cette vidéo partage des conseils et des bonnes pratiques pour l’exécution de requêtes dans l’interface du requêteur, les clients PSQL, les solutions de Business Intelligence (BI) et l’API HTTP.</p>
                </div>
                <a href="understanding-data-usage-patterns-with-query-service.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Connect Tableau to Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="psql-client-tableau.md" title="Connexion de Tableau à Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/333702?format=jpeg&nocache=1740415313229" alt="Connexion de Tableau à Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="psql-client-tableau.md" target="_blank" rel="referrer" title="Connexion de Tableau à Query Service">Connexion de Tableau à Query Service</a>
                    </p>
                    <p class="is-size-6">Découvrez comment vous connecter à Query Service à partir de diverses applications de bureau clientes qui prennent en charge le protocole PostgreSQL et comment utiliser les outils et pilotes PostgreSQL pour connecter et écrire des requêtes.</p>
                </div>
                <a href="psql-client-tableau.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Analyze and visualize omni-channel insights in Tableau using Query Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="analyze-and-visualize.md" title="Analyse et visualisation des informations omnicanal dans Tableau à l’aide de Query Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342115?format=jpeg&nocache=1740415313204" alt="Analyse et visualisation des informations omnicanal dans Tableau à l’aide de Query Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="analyze-and-visualize.md" target="_blank" rel="referrer" title="Analyse et visualisation des informations omnicanal dans Tableau à l’aide de Query Service">Analyse et visualisation des informations omnicanal dans Tableau à l’aide de Query Service</a>
                    </p>
                    <p class="is-size-6">Découvrez comment utiliser le Query Service d’Adobe Experience Platform avec des outils de visualisation de données externes à l’aide d’un exemple d’analyse de perte de la clientèle.</p>
                </div>
                <a href="analyze-and-visualize.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Recharge your customer data to deliver electrifying experiences">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="recharge-your-customer-data.md" title="Rechargez vos données client pour offrir des expériences électrisantes" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/342533?format=jpeg&nocache=1740415313218" alt="Rechargez vos données client pour offrir des expériences électrisantes"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" title="Rechargez vos données client pour offrir des expériences électrisantes">Rechargez vos données client pour offrir des expériences électrisantes</a>
                    </p>
                    <p class="is-size-6">Découvrez comment atténuer l’impact des données de faible qualité, réduire le délai de rentabilisation et multiplier le retour sur investissement en utilisant les mêmes données pour une multitude de cas d’utilisation.</p>
                </div>
                <a href="recharge-your-customer-data.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold"> En savoir plus </span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
