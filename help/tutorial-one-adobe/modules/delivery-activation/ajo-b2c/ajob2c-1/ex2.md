---
title: Journey Optimizer - Création de fragments
description: Journey Optimizer - Création de fragments
kt: 5342
doc-type: tutorial
exl-id: 4e71164d-9e25-46aa-a4b8-a2f6535c491e
source-git-commit: d19bd2e39c7ff5eb5c99fc7c747671fb80e125ee
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 9%

---

# 3.1.2 Création de fragments à utiliser dans votre message

Dans cet exercice, vous allez configurer 2 fragments, 1 pour un en-tête réutilisable et 1 pour un pied de page réutilisable.

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`.

![ACOP ](./images/acoptriglp.png)

## 3.1.2.1 Créer un fragment d’en-tête

Dans le menu de gauche, cliquez sur **Fragments**. Un fragment est un composant réutilisable dans Journey Optimizer, ce qui évite la duplication et facilite les modifications futures qui devraient avoir un impact sur tous les messages, telles que les modifications apportées à un en-tête ou à un pied de page dans un e-mail.

Cliquez sur **Créer un fragment**.

![ACOP ](./images/fragm1.png)

Saisissez le `--aepUserLdap-- - CitiSignal - Header` de nom et sélectionnez le **Type : fragment visuel**. Cliquez sur **Créer**.

![ACOP ](./images/fragm2.png)

Tu verras ça. Dans le menu de gauche, vous trouverez les composants de structure que vous pouvez utiliser pour définir la structure de l’e-mail (lignes et colonnes).

Faites glisser et déposez une colonne **1:1** du menu vers la zone de travail. Il s’agira de l’espace réservé pour l’image du logo.

![Journey Optimizer](./images/fragm3.png)

Vous pouvez ensuite utiliser les composants de contenu pour ajouter du contenu à l’intérieur de ces blocs. Faites glisser et déposez un composant **Image** dans la première cellule de la première ligne. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/fragm4.png)

Une fenêtre contextuelle s’affiche alors pour vous montrer votre bibliothèque de médias AEM Assets. Accédez au dossier **citi-signal-images**, cliquez pour sélectionner l’image **CitiSignal-Logo-White.png**, puis cliquez sur **Sélectionner**.

>[!NOTE]
>
>Si vous ne voyez pas les images CitiSignal dans votre bibliothèque AEM Assets, vous pouvez les trouver [ici](./../../../../assets/ajo/CitiSignal-images.zip). Téléchargez-les sur votre bureau, créez le dossier **citi-signal-images** et chargez toutes les images de ce dossier.

![Journey Optimizer](./images/fragm5.png)

Tu verras ça. Votre image est blanche et ne s’affiche pas encore. Vous devez maintenant définir une couleur d’arrière-plan pour que l’image s’affiche correctement. Cliquez sur **Styles**, puis sur la zone **Couleur d’arrière-plan**.

![Journey Optimizer](./images/fragm6.png)

Dans la fenêtre contextuelle, modifiez le code couleur **Hex** en **#8821F4** puis changez la sélection en cliquant dans le champ **100 %**. La nouvelle couleur appliquée à l’image s’affiche.

![Journey Optimizer](./images/fragm7.png)

L&#39;image est aussi un peu trop grande en ce moment. Changeons la largeur en faisant glisser le sélecteur **Largeur** à **40 %**.

![Journey Optimizer](./images/fragm8.png)

Votre fragment d’en-tête est maintenant prêt. Cliquez sur **Enregistrer** puis sur la flèche pour revenir à l’écran précédent.

![Journey Optimizer](./images/fragm9.png)

Votre fragment doit être publié avant de pouvoir être utilisé. Cliquez sur **Publier**.

![Journey Optimizer](./images/fragm10.png)

Au bout de quelques minutes, vous verrez que le statut de votre fragment est passé à **Actif**.
Vous devez ensuite créer un fragment pour le pied de page de vos e-mails. Cliquez sur **Créer un fragment**.

![Journey Optimizer](./images/fragm11.png)

## 3.1.2.2 Créer le fragment de pied de page

Cliquez sur **Créer un fragment**.

![Journey Optimizer](./images/fragm11.png)

Saisissez le `--aepUserLdap-- - CitiSignal - Footer` de nom et sélectionnez le **Type : fragment visuel**. Cliquez sur **Créer**.

![Journey Optimizer](./images/fragm12.png)

Tu verras ça. Dans le menu de gauche, vous trouverez les composants de structure que vous pouvez utiliser pour définir la structure de l’e-mail (lignes et colonnes).

Faites glisser et déposez une colonne **1:1** du menu vers la zone de travail. Il s’agira de l’espace réservé pour le contenu du pied de page.

![Journey Optimizer](./images/fragm13.png)

Vous pouvez ensuite utiliser les composants de contenu pour ajouter du contenu à l’intérieur de ces blocs. Effectuez un glisser-déposer d’un composant **HTML** dans la première cellule de la première ligne. Cliquez sur le composant pour le sélectionner, puis sur l’icône **&lt;/>** pour modifier le code source HTML.

![Journey Optimizer](./images/fragm14.png)

Tu verras ça.

![Journey Optimizer](./images/fragm15.png)

Copiez le fragment de code HTML ci-dessous et collez-le dans la fenêtre **Modifier HTML** de Journey Optimizer.

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

Tu auras alors ceci. Aux lignes 7, 12 et 17, vous devez maintenant insérer un fichier image à l’aide des ressources de votre bibliothèque AEM Assets.

![Journey Optimizer](./images/fragm16.png)

Assurez-vous que votre curseur se trouve à la ligne 7, puis cliquez sur **Assets** dans le menu de gauche. Cliquez sur **Ouvrir le sélecteur de ressources** pour sélectionner votre image.

![Journey Optimizer](./images/fragm17.png)

Ouvrez le dossier **citi-signal-images** et cliquez pour sélectionner l’image **Icon_Facebook.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/fragm18.png)

Assurez-vous que le curseur se trouve à la ligne 12, puis cliquez sur **Ouvrir le sélecteur de ressources** pour sélectionner votre image.

![Journey Optimizer](./images/fragm19.png)

Ouvrez le dossier **citi-signal-images** et cliquez pour sélectionner l’image **Icon_X.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/fragm20.png)

Assurez-vous que le curseur se trouve à la ligne 17, puis cliquez sur **Ouvrir le sélecteur de ressources** pour sélectionner votre image.

![Journey Optimizer](./images/fragm21.png)

Ouvrez le dossier **citi-signal-images** et cliquez pour sélectionner l’image **Icon_Instagram.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/fragm22.png)

Tu verras ça. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/fragm23.png)

Vous serez alors de retour dans l&#39;éditeur. Vos icônes ne sont pas encore visibles car l’arrière-plan et les fichiers image sont tous en blanc. Pour modifier la couleur d’arrière-plan, accédez à **Styles**, puis cochez la case **Couleur d’arrière-plan**.

![Journey Optimizer](./images/fragm24.png)

Remplacez le code couleur **Hex** par **#000000**.

![Journey Optimizer](./images/fragm25.png)

Modifiez l&#39;alignement pour qu&#39;il soit centré.

![Journey Optimizer](./images/fragm26.png)

Ajoutons d’autres parties au pied de page. Faites glisser et déposez un composant **Image** au-dessus du composant HTML que vous venez de créer. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/fragm27.png)

Cliquez pour sélectionner le fichier image **`CitiSignal_Footer_Logo.png`** et cliquez sur **Sélectionner**.

![Journey Optimizer](./images/fragm28.png)

Accédez à **Styles** et cochez la case **Couleur d’arrière-plan**, nous allons à nouveau la modifier en noir. Remplacez le code couleur **Hex** par **#000000**.

![Journey Optimizer](./images/fragm29.png)

Remplacez la largeur par **20 %** et vérifiez que l&#39;alignement est centré.

![Journey Optimizer](./images/fragm30.png)

Ensuite, faites glisser et déposez un composant **Texte** sous le composant HTML que vous avez créé. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/fragm31.png)

Copiez et collez le texte ci-dessous en remplaçant le texte d’espace réservé.

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

Définissez l’**Alignement du texte** à centrer.

![Journey Optimizer](./images/fragm32.png)

Remplacez la **Couleur de police** par le blanc, **#FFFFFF**.

![Journey Optimizer](./images/fragm33.png)

Remplacez **Couleur d’arrière-plan** par le noir, **#000000**.

![Journey Optimizer](./images/fragm34.png)

Sélectionnez le texte **Se désabonner** dans le pied de page, puis cliquez sur l’icône **Lien** dans la barre de menus. Définissez le **Type** sur **Désinscription/opt-out externe** et définissez l’URL sur **https://aepdemo.net/unsubscribe.html** (le lien de désinscription ne peut pas contenir d’URL vide).

![Journey Optimizer](./images/fragm35.png)

Tu auras alors ceci. Votre pied de page est maintenant prêt. Cliquez sur **Enregistrer** puis sur la flèche pour revenir à la page précédente.

![Journey Optimizer](./images/fragm36.png)

Cliquez sur **Publier** pour publier votre pied de page afin de l’utiliser dans un e-mail.

![Journey Optimizer](./images/fragm37.png)

Au bout de quelques minutes, vous verrez que le statut de votre pied de page est passé à **Actif**.

![Journey Optimizer](./images/fragm38.png)

## Étapes suivantes

Accédez à [3.1.3 Création de votre parcours et de votre e-mail](./ex3.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : Orchestration](./journey-orchestration-create-account.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
