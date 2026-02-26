---
title: Création de votre campagne orchestrée
description: Création de votre campagne orchestrée
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 0328260e8699107bc82103af98caae684319a60d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# 3.8.2 Création de votre campagne orchestrée

## 3.8.2.1 Créer une campagne orchestrée

Accédez à **Campagnes**. Cliquez sur **Créer une campagne**.

![AJO OC](./images/ajooc1.png)

Sélectionnez **Orchestration - Marketing**, puis cliquez sur **Confirmer**.

![AJO OC](./images/ajooc2.png)

Saisissez le nom de la campagne : `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign` et cliquez sur **Enregistrer**.

![AJO OC](./images/ajooc3.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **+** .

![AJO OC](./images/ajooc4.png)

Sélectionnez **Branchement**.

![AJO OC](./images/ajooc5.png)

### Créer l’audience 1

Cliquez sur l’icône **+**, puis sélectionnez **Créer une audience**.

![AJO OC](./images/ajooc6.png)

Cliquez pour ouvrir le dossier pour **Dimension de ciblage**.

![AJO OC](./images/ajooc7.png)

Sélectionnez **`--aepUserLdap--_citisignal_recipients`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc8.png)

Cliquez sur **Créer une audience**.

![AJO OC](./images/ajooc9.png)

Cliquez sur **Ajouter une condition**.

![AJO OC](./images/ajooc10.png)

Sélectionnez **recipient_type** puis cliquez sur **Confirmer**.

![AJO OC](./images/ajooc11.png)

Saisissez **`account_holder`** dans le champ **Valeur** et cliquez sur **Calculer**.

![AJO OC](./images/ajooc12.png)

Vous devriez alors voir un nombre pour **profils ciblés**. Cliquez quelque part dans la zone grise comme indiqué.

![AJO OC](./images/ajooc13.png)

Cliquez sur **Ajouter une condition**.

![AJO OC](./images/ajooc14.png)

Analyser en profondeur jusqu’à **`citisignal_accounts`**.

![AJO OC](./images/ajooc15.png)

Sélectionnez **`account_status`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc16.png)

Saisissez **`active`** dans le champ **Valeur**. Cliquez ensuite quelque part dans la zone grise comme indiqué.

![AJO OC](./images/ajooc17.png)

Cliquez sur **Ajouter une condition**.

![AJO OC](./images/ajooc18.png)

Analyser en profondeur jusqu’à **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc19.png)

Sélectionnez **`subscription_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc20.png)

Activez le sélecteur pour **Données agrégées**. Sélectionnez ensuite les options suivantes :

- **Fonction d&#39;agrégat** : **Count**
- **Opérateur** : **supérieur ou égal à**
- **Valeur** : **1**

Cliquez sur **Confirmer**.

![AJO OC](./images/ajooc21.png)

Vous devriez alors voir ceci. Cliquez sur **Confirmer**.

![AJO OC](./images/ajooc22.png)

### Créer l’audience 2

Cliquez sur l’icône **+** sur le nœud suivant de l’autre chemin d’accès.

![AJO OC](./images/ajooc23.png)

Sélectionnez **Créer une audience**.

![AJO OC](./images/ajooc24.png)

Cliquez pour ouvrir le dossier pour **Dimension de ciblage**.

![AJO OC](./images/ajooc25.png)

Sélectionnez **`--aepUserLdap--_mobile_subscriptions`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc26.png)

Cliquez sur **Créer une audience**.

![AJO OC](./images/ajooc27.png)

Cliquez sur **Ajouter une condition**.

![AJO OC](./images/ajooc28.png)

Sélectionnez **subscription_status** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc29.png)

Saisissez **`active`** dans le champ **Valeur**. Cliquez ensuite sur **Ajouter une condition**.

![AJO OC](./images/ajooc30.png)

Sélectionnez **`is_upgrade_eligible`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc31.png)

Définissez **Value** sur **true**

![AJO OC](./images/ajooc32.png)

Cliquez sur **Calculer** pour afficher une estimation des profils qui remplissent les critères de cette audience. Cliquez ensuite sur **Confirmer**

![AJO OC](./images/ajooc33.png)

### Partage

Cliquez sur l’icône **+**, puis sélectionnez **Fractionner**.

![AJO OC](./images/ajooc34.png)

Remplacez le champ **Libellé** par Traitement **90/10 contre contrôle**. Cliquez pour ouvrir l’objet **Sous-ensemble**.

![AJO OC](./images/ajooc35.png)

Activez le sélecteur pour **Activer la limite** et définissez la **Taille limite** sur **10 %**.

![AJO OC](./images/ajooc36.png)

Cliquez sur **Ajouter un segment** et vous devriez voir l’objet **Result** ajouté.

Cliquez sur **Enregistrer**.

![AJO OC](./images/ajooc37.png)

### Enregistrer l’audience

Cliquez sur l’icône **+** , puis sélectionnez **Enregistrer l’audience**.

![AJO OC](./images/ajooc38.png)

Définissez le champ **libellé de l’audience** sur **`--aepUserLdap-- - Control Group`**. Cliquez sur **Ajouter un mappage d’audience**.

![AJO OC](./images/ajooc39.png)

Accédez à **dimension de ciblage**.

![AJO OC](./images/ajooc40.png)

Sélectionnez **`account_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc41.png)

Définissez le **champ de mappage de profil** sur **`--aepUserLdap--_citisignal_recipients - account_id`**.

![AJO OC](./images/ajooc41a.png)

### Enrichissement : Abonnement Internet

Cliquez sur l’icône **+** .

![AJO OC](./images/ajooc42.png)

Sélectionnez **Enrichissement**.

![AJO OC](./images/ajooc43.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter des données d’enrichissement**.

![AJO OC](./images/ajooc44.png)

Analyser en profondeur jusqu’à **`Targeting dimension`**.

![AJO OC](./images/ajooc44a.png)

Analyser en profondeur jusqu’à **`citisignal_accounts`**.

![AJO OC](./images/ajooc45.png)

Analyser en profondeur jusqu’à **`citisignal_internet_subscriptions`**.

![AJO OC](./images/ajooc45a.png)

Sélectionnez **`account_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc46.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc47.png)

Sélectionnez **`subscription_status`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc48.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc49.png)

Sélectionnez **`connection_type`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc50.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc51.png)

Sélectionnez **`service_city`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc52.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc53.png)

Sélectionnez **`avg_bandwidth_usage_gb`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc54.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc55.png)

Sélectionnez **`data_cap_gb`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc56.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc57.png)

Sélectionnez **`advertised_speed_mbps`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc58.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc59.png)

Sélectionnez **`monthly_recurring_charge`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc60.png)

Cliquez sur **Enregistrer**.

![AJO OC](./images/ajooc61.png)

Faites défiler vers le haut et remplacez le champ **Libellé** par `Enrichment: Internet Subscription`.

![AJO OC](./images/ajooc61a.png)

### Enrichissement : Abonnement pour appareils mobiles

Cliquez sur l’icône **+** sur le nœud suivant et sélectionnez **Enrichissement**.

![AJO OC](./images/ajooc62.png)

Remplacez le champ **Libellé** par `Enrichment: Mobile Devices Subscription`, puis cliquez sur **Ajouter des données d’enrichissement**.

![AJO OC](./images/ajooc63.png)

Accédez à **Dimension de ciblage**.

![AJO OC](./images/ajooc64.png)

Analyser en profondeur jusqu’à **`citisignal_accounts`**.

![AJO OC](./images/ajooc65.png)

Analyser en profondeur jusqu’à **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc65a.png)

Sélectionnez **`phone_number`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc66.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc67.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc68.png)

Sélectionnez **`model`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc68a.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc69.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc69a.png)

Sélectionnez **`recommended_device_model`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc70.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc71.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc71a.png)

Sélectionnez **`is_upgrade_eligible`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc72.png)

Vous pouvez maintenant tester votre progression en effectuant une exécution de test et en vérifiant les données disponibles dans votre campagne.

Enregistrez vos modifications, puis cliquez sur **Démarrer**.

![AJO OC](./images/ajooctest1.png)

Au bout d’un certain temps, vous devriez voir ceci. Cliquez sur **Aperçu des résultats**.

![AJO OC](./images/ajooctest2.png)

Vous devriez alors voir quelque chose de similaire à ceci. Cliquez sur **Fermer**.

![AJO OC](./images/ajooctest3.png)

Revenez au nœud **Enrichissement : Abonnement pour appareils mobiles**.

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc73.png)

Sélectionnez **`account_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc74.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc75.png)

Sélectionnez **`subscription_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc76.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc77.png)

Sélectionnez **`renewal_eligibility_date`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc78.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc79.png)

Sélectionnez **`line_user_recipient_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc80.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc81.png)

Sélectionnez **`current_device_id`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc82.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc86.png)

Sélectionnez **`contract_start_date`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc87.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc89.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc90.png)

Sélectionnez **`manufacturer`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc91.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc92.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc93.png)

Sélectionnez **`device_age_months`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc94.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc95.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc96.png)

Sélectionnez **`trade_in_value`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc97.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc98.png)

Analyser en profondeur jusqu’à **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc99.png)

Sélectionnez **`monthly_payment`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc100.png)

### Enrichissement : Abonnement pour appareils mobiles

Tu devrais avoir ça. Cliquez sur **Enregistrer**. Cliquez ensuite sur l’icône **+** pour ajouter un nouveau nœud et sélectionnez **Enrichissement**.

![AJO OC](./images/ajooc101.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter des données d’enrichissement**.

![AJO OC](./images/ajooc102.png)

Accédez à **Dimension de ciblage**.

![AJO OC](./images/ajooc103.png)

Analyser en profondeur jusqu’à **`citisignal_offer_eligibility`**.

![AJO OC](./images/ajooc104.png)

Analyser en profondeur jusqu’à **`citisignal_offers`**.

![AJO OC](./images/ajooc105.png)

Sélectionnez **`offer_name`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc106.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc107.png)

Analyser en profondeur jusqu’à **`citisignal_offers`**.

![AJO OC](./images/ajooc108.png)

Sélectionnez **`offer_code`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc109.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc110.png)

Analyser en profondeur jusqu’à **`citisignal_offers`**.

![AJO OC](./images/ajooc111.png)

Sélectionnez **`offer_description`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc112.png)

Cliquez sur **Ajouter un attribut**.

![AJO OC](./images/ajooc110.png)

Analyser en profondeur jusqu’à **`citisignal_offers`**.

![AJO OC](./images/ajooc113.png)

Sélectionnez **`offer_description`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc114.png)

Activez **Activer le tri**.

![AJO OC](./images/ajooc115.png)

Analyser en profondeur jusqu’à **`citisignal_offers`**.

![AJO OC](./images/ajooc116.png)

Sélectionnez **`offer_priority`** et cliquez sur **Confirmer**.

![AJO OC](./images/ajooc117.png)

Vous pouvez maintenant tester votre campagne. Cliquez sur **Démarrer**.

![AJO OC](./images/ajooc118.png)

Au bout d&#39;un certain temps, vous devriez voir ceci. Cliquez sur le **Résultat** puis sélectionnez **Prévisualiser les résultats**.

![AJO OC](./images/ajooc120.png)

Vous devriez alors voir quelque chose de similaire à ceci.

![AJO OC](./images/ajooc121.png)

### Activité e-mail

Cliquez sur l’icône **+**, puis sélectionnez **E-mail**.

![AJO OC](./images/ajooc122.png)

Cliquez sur **Modifier l’e-mail**.

![AJO OC](./images/ajooc123.png)

Accédez à **Actions**.

![AJO OC](./images/ajooc124.png)

Sélectionnez la **configuration du canal e-mail** que vous avez créée précédemment, puis cliquez sur **Modifier le contenu**.

![AJO OC](./images/ajooc125.png)

Pour la **ligne d’objet**, collez ce qui suit :

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

Cliquez sur **Modifier le corps de l’e-mail**.

![AJO OC](./images/ajooc126.png)

## Étapes suivantes

Revenez à [Adobe Journey Optimizer : Campagnes orchestrées](./ajocampaigns.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
