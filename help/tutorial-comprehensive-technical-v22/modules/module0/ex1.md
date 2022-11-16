---
title: Prise en main - Installation de l’extension Chrome pour la documentation Experience League
description: Prise en main - Installation de l’extension Chrome pour la documentation Experience League
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6e0a88e7-65e3-4251-8ab1-e030a397a56b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# 0.1 Installation de l’extension Chrome pour la documentation Experience League

## 0.1.1 Pourquoi avons-nous créé une extension Chrome ?

La documentation a été rendue générique afin d’être facilement réutilisée par n’importe qui, à l’aide de n’importe quelle instance Adobe Experience Platform.
En rendant la documentation réutilisable, **Variables d’environnement** ont été introduites dans la documentation, ce qui signifie que vous trouverez les **keys** dans la documentation. Chaque clé est une variable spécifique pour un environnement spécifique. L’extension Chrome la modifie pour vous et vous permet ainsi de copier facilement du code et du texte à partir des pages du tutoriel et de le coller dans les différentes interfaces utilisateur que vous utiliserez dans le cadre du tutoriel.

Vous trouverez ci-dessous un exemple de ces valeurs. Actuellement, ces valeurs ne peuvent pas encore être utilisées, mais dès que vous installez et activez l’extension Chrome, ces variables se transforment en texte &quot;normal&quot; que vous pouvez copier et réutiliser.

| Nom | Clé |
|:-------------:| :---------------:|
| Identifiant de l’organisation IMS AEP | `--aepImsOrgId--` |
| Identifiant du client AEP | `--aepTenantId--` |
| Identifiant d’insertion DCS | `--dcsInletId--` |
| Demo Profile LDAP | `--demoProfileLdap--` |

Par exemple, dans la capture d’écran ci-dessous, vous pouvez voir une référence à `--aepTenantId--`.

![DSN](./images/mod7before.png)

Une fois l’extension installée, ce même texte sera automatiquement modifié pour refléter les valeurs spécifiques à votre instance.

![DSN](./images/mod7.png)

L’extension vous permettra également de :

- S’inscrire au tutoriel
- Effectuez le suivi de votre progression en envoyant la fin de chaque module comme indiqué dans la section [Comment la fin est-elle mesurée ?](../../completion.md)

## 0.1.2 Installation de l’extension Chrome

Pour installer cette extension Chrome, ouvrez votre navigateur Chrome et accédez à : [https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0](https://chrome.google.com/webstore/detail/platform-learn-configurat/hhnbkfgioecmhimdhooigajdajplinfi/related?hl=en&amp;authuser=0). Vous verrez alors ceci.

Cliquez sur **Ajouter à Chrome**.

![DSN](./images/c2.png)

Vous verrez alors ceci. Cliquez sur **Ajouter une extension**.

![DSN](./images/c3.png)

L’extension sera alors installée et une notification similaire s’affichera.

![DSN](./images/c4.png)

Dans le **extensions** , cliquez sur **pièce de puzzle** et épinglez le **Formation Platform - Configuration** extension au menu d’extension.

![DSN](./images/c6.png)

## 0.1.2 Configuration de l’extension Chrome

Accédez à [https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/overview.html?lang=en) puis cliquez sur l’icône d’extension pour l’ouvrir.

![DSN](./images/tuthome.png)

Vous verrez alors cette fenêtre contextuelle. Cliquez sur le bouton **+** icône .

![DSN](./images/c7.png)

Saisissez votre nom et l’ID de configuration qui a été créé pour votre environnement Adobe Experience Platform. Cliquez sur **Créer**.

>[!IMPORTANT]
>
>Si vous êtes un employé d’Adobe : vous trouverez l’identifiant de configuration à utiliser sur le référentiel Github interne (https://git.corp.adobe.com/vangeluw/platformenablement).
>
>Si vous êtes un partenaire en solutions Adobe, veuillez contacter votre contact en solutions ou par e-mail. **spphelp@adobe.com**.

![DSN](./images/c8.png)

Dans le menu de gauche de l’extension, une icône s’affiche avec vos initiales. Cliquez dessus. Vous verrez alors le mappage entre les **Variables d’environnement** et vos valeurs d’instance Adobe Experience Platform spécifiques. Cliquez sur **Activation de la configuration**.

![DSN](./images/c9.png)

Une fois la configuration activée, un point vert s’affiche en regard de vos initiales. Cela signifie que votre ID de configuration est désormais principal. Plusieurs options de menu supplémentaires s’affichent également.

![DSN](./images/c10.png)

Vous disposez désormais de 2 options :

- Si vous êtes un utilisateur existant de l’activation avec une configuration existante, accédez à **0.1.3 Utilisateur existant - Connexion**
- Si vous êtes un nouvel utilisateur qui lance ce tutoriel pour la première fois, accédez à **0.1.4 S’inscrire** et saut **0.1.3 Utilisateur existant - Connexion**

## 0.1.3 Utilisateur existant - Connexion

>[!IMPORTANT]
>
>Exercice **0.1.3 Utilisateur existant - Connexion** ne fonctionnera que si vous êtes un utilisateur existant qui s’est déjà abonné à ce tutoriel.

Si vous êtes un utilisateur existant qui configure cette extension Chrome pour la première fois, cliquez sur l’icône violette dans le menu de gauche. Vous verrez alors ceci.

![DSN](./images/chromeret1.png)

Remplissez les valeurs suivant vos besoins.

>[!IMPORTANT]
>
>Le **LDAP** est le champ le plus important : vous devez utiliser le même LDAP que celui utilisé lors de la première inscription au tutoriel. Cela permet de vous assurer que votre progression est bien chargée. Si vous n&#39;êtes pas sûr de ce qu&#39;est votre ldap, regardez votre adresse email. Utilisez le texte situé avant le @-symbol dans votre adresse email comme LDAP. Si votre adresse électronique est **vangeluw@adobe.com**, le LDAP que vous saisissez ici doit être : **vangeluw**).

![DSN](./images/chromeret2.png)

Cliquez sur **OK**.

![DSN](./images/chromeret3.png)

Après 30 secondes à 1 minute, votre écran change et vous revenez à **Accueil**, où vous verrez ceci :

![DSN](./images/chromeret4.png)

Votre extension Chrome est maintenant configurée et vous pouvez désormais vérifier si tout fonctionne correctement.

## 0.1.4 Nouvel utilisateur - S’inscrire

>[!IMPORTANT]
>
>Exercice **0.1.4 Nouvel utilisateur - S’inscrire** est destiné aux nouveaux utilisateurs qui démarrent ce tutoriel pour la première fois.

Si vous êtes un nouvel utilisateur qui s’inscrit pour la première fois à ce tutoriel, cliquez sur l’icône jaune dans le menu. Vous verrez alors ceci.

![DSN](./images/c11.png)

Renseignez les champs suivant vos besoins. Cliquez sur **Enregistrer**.

>[!IMPORTANT]
>
>Le **LDAP** est le champ le plus important. Si vous n&#39;êtes pas sûr de ce qu&#39;est votre ldap, regardez votre adresse email. Utilisez le texte situé avant le @-symbol dans votre adresse email comme LDAP. Si votre adresse électronique est **vangeluw@adobe.com**, le LDAP que vous saisissez ici doit être : **vangeluw**).

![DSN](./images/chrome1.png)

Après 30 secondes à 1 minute, votre écran change et vous revenez à **Accueil**, où vous verrez ceci :

![DSN](./images/chrome2.png)

Votre extension Chrome est maintenant configurée et vous pouvez désormais vérifier si tout fonctionne correctement.

## 0.1.5 Vérification du contenu du tutoriel

Pour un test, accédez à [cette page](https://experienceleague.adobe.com/docs/platform-learn/comprehensive-technical-tutorial-v22/module4/ex3.html?lang=fr).

Vous devriez maintenant voir que tous les **Variables d’environnement** ont été remplacés par leurs valeurs true, en fonction de l’ID de configuration dans l’extension chrome.

Vous devez maintenant disposer d’une vue similaire à celle ci-dessous, où les variables d’environnement `--aepTenantId--` a été remplacé par votre identifiant de client réel, qui, dans ce cas, est **_experienceplatform**.

![DSN](./images/c12.png)

Étape suivante : [0.2 Utilisation du système de démonstration en regard de la configuration de la propriété client de la collecte de données Adobe Experience Platform](./ex2.md)

[Revenir au module 0](./getting-started.md)

[Revenir à tous les modules](./../../overview.md)
