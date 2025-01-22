---
title: Prise en main - Installez l’extension Chrome pour la documentation de l’Experience League.
description: Prise en main - Installez l’extension Chrome pour la documentation de l’Experience League.
kt: 5342
doc-type: tutorial
exl-id: 3618dacb-2203-4d19-ae51-f78415a693fd
source-git-commit: e505b8401509f6171d9c98f85a93af27c38a8303
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Installation de l’extension Chrome pour la documentation de l’Experience League

## À propos de l’extension Chrome

La documentation a été rendue générique afin qu’elle puisse être facilement réutilisée par n’importe qui, à l’aide de n’importe quelle instance Adobe Experience Platform.
Pour rendre la documentation réutilisable, les **variables d’environnement** ont été introduites dans la documentation, ce qui signifie que vous trouverez les **espaces réservés** ci-dessous dans la documentation. Chaque espace réservé est une variable spécifique pour un environnement spécifique, et l’extension Chrome modifiera cette variable pour vous afin de vous permettre de copier facilement le code et le texte des pages du tutoriel et de les coller dans les différentes interfaces utilisateur que vous utiliserez dans le cadre du tutoriel.

Vous trouverez ci-dessous un exemple de ces valeurs. Actuellement, ces valeurs ne peuvent pas encore être utilisées, mais dès que vous installez et activez l’extension Chrome, ces variables sont transformées en texte normal que vous pouvez copier et réutiliser.

| Nom | Clé | Exemple |
|:-------------:| :---------------:| :---------------:|
| ID d’organisation IMS AEP | `--aepImsOrgId--` | `907075E95BF479EC0A495C73@AdobeOrg` |
| Nom de l’organisation IMS AEP | `--aepImsOrgName--` | `Experience Platform International` |
| ID de client AEP | `--aepTenantId--` | `_experienceplatform` |
| Nom du sandbox AEP | `--aepSandboxName--` | `one-adobe` |
| Learner Profile LDAP | `--aepUserLdap--` | `vangeluw` |

Par exemple, dans la capture d’écran ci-dessous, vous pouvez voir une référence à `aepSandboxName`.

![DSN ](./images/mod7before.png)

Une fois l’extension installée, le même texte est automatiquement modifié pour refléter les valeurs spécifiques à votre instance.

![DSN ](./images/mod7.png)

## Installation de l’extension Chrome

Pour installer cette extension Chrome, ouvrez votre navigateur Chrome et accédez à : [https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi](https://chromewebstore.google.com/detail/tech-insiders-learning-fo/hhnbkfgioecmhimdhooigajdajplinfi). Tu verras ça.

Cliquez sur **Ajouter à Chrome**.

![DSN ](./images/c2.png)

Tu verras ça. Cliquez sur **Ajouter une extension**.

![DSN ](./images/c3.png)

L’extension sera ensuite installée et une notification similaire s’affichera.

![DSN ](./images/c4.png)

Dans le menu **extensions**, cliquez sur l’icône **puzzle** et épinglez l’extension **Platform Learn - Configuration** dans le menu d’extension.

![DSN ](./images/c6.png)

## Configuration de l’extension Chrome

Accédez à [https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-comprehensive-technical/overview) puis cliquez sur l’icône de l’extension pour l’ouvrir.

![DSN ](./images/tuthome.png)

Vous verrez alors cette fenêtre contextuelle. Cliquez sur l’icône **+** .

![DSN ](./images/c7.png)

Saisissez les valeurs comme indiqué ci-dessous, qui sont toutes liées à votre instance Adobe Experience Platform.

![DSN ](./images/c8.png)

Si vous ne savez pas exactement quelles valeurs saisir pour ces champs, suivez les conseils ci-dessous.

**Nom de l’organisation IMS AEP**

Lorsque vous vous connectez à votre instance Adobe Experience Platform sur [https://platform.adobe.com/](https://platform.adobe.com/), le nom de votre instance s’affiche dans le coin supérieur droit de l’écran.

![DSN ](./images/aepname.png)

**ID d’organisation IMS AEP**

L’ID d’organisation IMS est l’identifiant unique de votre instance Adobe Experience Cloud et est référencé à plusieurs endroits tout au long de ce tutoriel.

La recherche de votre identifiant de l’organisation IMS peut être effectuée de plusieurs façons. Si vous n’êtes pas sûr, contactez l’un des administrateurs système de votre instance pour trouver l’identifiant.

Vous pouvez le retrouver en accédant à [Admin Console ](https://https://adminconsole.adobe.com/), où vous pouvez le retrouver dans l&#39;URL.

![DSN ](./images/aepid1.png)

Vous pouvez également le trouver en accédant à **Gestion des données > Requêtes** dans votre menu AEP, où vous pouvez le trouver sous **Nom d’utilisateur**.

![DSN ](./images/aepid2.png)

Veillez à copier et coller la partie **@AdobeOrg** avec l&#39;ID.

**ID de client AEP**

Votre identifiant client est l’identifiant unique de l’instance AEP de votre organisation. Lorsque vous vous connectez à votre instance Adobe Experience Platform sur [https://platform.adobe.com/](https://platform.adobe.com/), l’identifiant du client s’affiche dans l’URL.

![DSN ](./images/aeptenantid.png)

Lorsque vous la saisissez dans l’extension Chrome, vous devez vous assurer qu’un trait de soulignement est ajouté sous forme de préfixe, de sorte que dans cet exemple **experienceplatform** devienne **_experienceplatform**.

**Nom du sandbox AEP**

Le nom de votre sandbox est le nom de l’environnement que vous utiliserez dans votre instance AEP. Lorsque vous vous connectez à votre instance Adobe Experience Platform sur [https://platform.adobe.com/](https://platform.adobe.com/), l’identifiant du client s’affiche dans l’URL.

Avant de prendre le nom du sandbox à partir de l’URL, vous devez vous assurer que vous vous trouvez dans le sandbox que vous devez utiliser pour ce tutoriel. Vous pouvez passer au sandbox de droite en cliquant sur le menu de sélection des sandbox dans le coin supérieur droit de l’écran.

![DSN ](./images/aepsandboxsw.png)

Dans cet exemple, le nom du sandbox AEP est **one-adobe**.

![DSN ](./images/aepsname.png)

**Votre LDAP**

Il s’agit du nom d’utilisateur qui sera utilisé dans le cadre du tutoriel. Dans cet exemple, le LDAP est basé sur l’adresse e-mail de cet utilisateur. L’adresse e-mail est **vangeluw@adobe.com** le protocole LDAP devient donc **vangeluw**.

Le LDAP est utilisé pour vous assurer que la configuration que vous effectuerez sera liée à vous et n’entrera pas en conflit avec d’autres utilisateurs susceptibles d’utiliser la même instance et le même sandbox que vous utilisez.

Vos valeurs doivent ressembler à celles-ci.
Enfin, cliquez sur **Créer**.

![DSN ](./images/c8a.png)

Dans le menu de gauche de l’extension, une nouvelle icône contenant les initiales de votre environnement s’affiche. Cliquez dessus. Le mappage entre les **variables d’environnement** et les valeurs de votre instance Adobe Experience Platform s’affiche alors. Cliquez sur **Activer la configuration**.

![DSN ](./images/c9.png)

Une fois la configuration activée, un point vert s’affiche en regard des initiales de votre environnement. Cela signifie que votre environnement est désormais actif.

![DSN ](./images/c10.png)

## Vérifier le contenu du tutoriel

Pour tester, accédez à [cette page](https://experienceleague.adobe.com/en/docs/platform-learn/tutorial-one-adobe/uce/module31/ex2).

Vous devriez maintenant voir que toutes les **variables d’environnement** de cette page ont été remplacées par leurs valeurs vraies, en fonction de l’environnement activé dans l’extension Chrome.

Vous devriez maintenant disposer d’une vue similaire à celle ci-dessous, où la variable d’environnement `aepSandboxName` a été remplacée par votre vrai nom de sandbox AEP, qui est dans ce cas **one-adobe**.

![DSN ](./images/mod7.png)

Étape suivante : [Utiliser le système de démonstration Suivant pour configurer la propriété de votre client de collecte de données Adobe Experience Platform](./ex2.md)

[Revenir à la prise en main](./getting-started.md)

[Revenir à tous les modules](./../../../overview.md)
