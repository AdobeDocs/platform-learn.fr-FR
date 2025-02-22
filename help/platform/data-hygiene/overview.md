---
title: Hygiène de données sur Adobe Experience Platform
description: En savoir plus sur les options des outils de nettoyage de données dans Adobe Experience Platform
solution: Experience Platform, Real-Time Customer Data Platform, Journey Optimizer
feature: Data Hygiene
role: Developer
level: Intermediate
source-git-commit: 9c15708f7300672caa963c0635179dd2855e5fed
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 24%

---

# Tutoriels sur l’hygiène des données

Découvrez les fonctionnalités d’hygiène des données de Adobe Experience Platform, notamment :

* Activation des principes de minimisation des données lors de l’ingestion des données
* Ajustement des données déjà présentes dans le système
* Suppression de données du système

<!--
Data hygiene:

* Enables citizen data stewards working in Privacy or IT teams to manage customer data lifecycle.
* Provides foundational workflows for setting expiration of datasets based on corporate policies, partner
arrangements, customer commitments or regulatory needs.
* Provides foundational workflows for managing targeted treatment of identities and data belonging to consumers in a
holistic fashion.
* Provides monitoring, work order management and notifications of tasks.
* Provides the ability to log the lifecyle management tasks for auditing purposes.
-->

## Minimisation des données lors de l’ingestion

La fonctionnalité de préparation des données vous permet d’ingérer uniquement les champs dont vous avez besoin à partir d’une source de données.

<!-- CARDS
{cta=Watch}
* data-prep-for-data-hygiene.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Data prep for data hygiene">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="data-prep-for-data-hygiene.md" title="Préparation des données pour l’hygiène des données" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429485/?format=jpeg&nocache=1740251397387" alt="Préparation des données pour l’hygiène des données"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" title="Préparation des données pour l’hygiène des données">Préparation des données pour l’hygiène des données</a>
                    </p>
                    <p class="is-size-6">Découvrez comment prendre en charge les principes de minimisation des données avec la fonction de préparation des données d’Experience Platform. Découvrez comment ingérer uniquement les champs dont vous avez besoin et les données de hachage lors de l’ingestion.</p>
                </div>
                <a href="data-prep-for-data-hygiene.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->

## Suppression de données dans le système

Il existe de nombreuses fonctionnalités pour vous aider à supprimer les données du système. Vous pouvez supprimer des jeux de données entiers à la demande ou selon un planning, faire expirer des enregistrements et des profils avec des paramètres de durée de vie, supprimer des profils individuels et respecter les demandes d’accès à des informations personnelles.
<!-- CARDS
{cta=Watch}
* delete-datasets-and-batches.md
* ../data-lifecycle/expire-datasets.md
* pseudonymous-profile-and-event-expiration.md
* ../profiles/delete-profiles.md{description=Learn how to delete data from the Profile Store using the Real-Time Customer Profile API. By using the Profile API, you can remove data from the profile store without affecting the data lake or identity graph.}
* ../privacy/introduction-to-privacy-services.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete datasets and batches">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="delete-datasets-and-batches.md" title="Supprimer les jeux de données et les lots" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429790/?format=jpeg&nocache=1740251397681" alt="Supprimer les jeux de données et les lots"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" title="Supprimer les jeux de données et les lots">Supprimer les jeux de données et les lots</a>
                    </p>
                    <p class="is-size-6">Découvrez comment supprimer des jeux de données et des lots dans Adobe Experience Platform.</p>
                </div>
                <a href="delete-datasets-and-batches.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Schedule dataset deletes">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../data-lifecycle/expire-datasets.md" title="Planifier des suppressions de jeux de données" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/345065?format=jpeg&nocache=1740251397716" alt="Planifier des suppressions de jeux de données"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" title="Planifier des suppressions de jeux de données">Planifier des suppressions de jeux de données</a>
                    </p>
                    <p class="is-size-6">Découvrez comment supprimer des jeux de données à l’aide de la fonctionnalité d’hygiène des données de Adobe Experience Platform.</p>
                </div>
                <a href="../data-lifecycle/expire-datasets.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Pseudonymous profile and Experience Event expirations">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="pseudonymous-profile-and-event-expiration.md" title="Expirations de profils pseudonymes et d’événements d’expérience" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3428361?format=jpeg&nocache=1740251397705" alt="Expirations de profils pseudonymes et d’événements d’expérience"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" title="Expirations de profils pseudonymes et d’événements d’expérience">Expirations du profil pseudonyme et de l’événement d’expérience</a>
                    </p>
                    <p class="is-size-6">Découvrez comment configurer des paramètres d’expiration pour les profils pseudonymes et les événements dans Experience Platform et quels en sont les avantages.</p>
                </div>
                <a href="pseudonymous-profile-and-event-expiration.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Delete profiles">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/delete-profiles.md" title="Suppression de profils" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3429807/?format=jpeg&nocache=1740251397692" alt="Suppression de profils"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" title="Suppression de profils">Supprimer des profils</a>
                    </p>
                    <p class="is-size-6">Découvrez comment supprimer des données du magasin de profils à l’aide de l’API Real-Time Customer Profile. En utilisant l’API Profile, vous pouvez supprimer des données de la banque de profils sans affecter le lac de données ou le graphique d’identité.</p>
                </div>
                <a href="../profiles/delete-profiles.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Introduction to Privacy Service">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../privacy/introduction-to-privacy-services.md" title="Présentation de Privacy Service" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/336074?format=jpeg&nocache=1740251397727" alt="Présentation de Privacy Service"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" title="Présentation de Privacy Service">Présentation de Privacy Service</a>
                    </p>
                    <p class="is-size-6">Découvrez les réglementations de confidentialité et leurs effets sur les opérations de données. Découvrez également comment Privacy Service gère ces défis.</p>
                </div>
                <a href="../privacy/introduction-to-privacy-services.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->





## Ajustement des données dans le système

<!-- CARDS
{cta=Watch}
* ../profiles/update-a-specific-attribute-with-upsert.md
-->
<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="Update specific profile attributes using `upsert`">
        <div class="card" style="height: 100%; display: flex; flex-direction: column; height: 100%;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="../profiles/update-a-specific-attribute-with-upsert.md" title="Mettre à jour des attributs de profil spécifiques à l’aide de « upsert »" target="_blank" rel="referrer">
                        <img class="is-bordered-r-small" src="https://video.tv.adobe.com/v/3416133/?format=jpeg&nocache=1740251398874" alt="Mettre à jour des attributs de profil spécifiques à l’aide de « upsert »"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" title="Mettre à jour des attributs de profil spécifiques à l’aide de « upsert »">Mettre à jour des attributs de profil spécifiques à l’aide de « upsert »</a>
                    </p>
                    <p class="is-size-6">Découvrez comment mettre à jour un attribut spécifique d’un profil à l’aide de la fonctionnalité « upsert » de Adobe Experience Platform.</p>
                </div>
                <a href="../profiles/update-a-specific-attribute-with-upsert.md" target="_blank" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Watch</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->
