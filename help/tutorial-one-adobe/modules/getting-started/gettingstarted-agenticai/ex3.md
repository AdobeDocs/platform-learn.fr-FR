---
title: Prise en main - IA dédiée à l’agence - Utilisez votre site web AEM et votre sandbox AEP
description: Prise en main - IA dédiée à l’agence - Utilisez votre site web AEM et votre sandbox AEP
doc-type: multipage-overview
source-git-commit: bdade61b2f64a5138807a47f73d8006ce9c564fc
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# Utiliser votre site web AEM et votre sandbox AEP

En choisissant Agentic AI Tech Labs, vous utiliserez un programme AEM as a Cloud Service existant utilisant Edge Delivery Services. Ce programme AEM as a Cloud Service utilisant Edge Delivery Services a été créé pour vous et est déjà disponible au début des Tech Labs.

## Votre numéro

Lorsque vous avez eu accès à l’environnement d’activation, un numéro vous a été attribué. Ce nombre indique le programme AEM as a Cloud Service que vous devez utiliser et indique également le sandbox AEP que vous devez utiliser pour le laboratoire technique Brand Concierge.

>[!IMPORTANT]
>
>Si vous n’avez pas encore reçu cet e-mail, vous ne pourrez pas encore exécuter les étapes ci-dessous. Vous devez attendre de recevoir l’e-mail ci-dessous avant d’accéder aux applications Adobe ci-dessous.


![DSN ](./images/number.png)

## Votre programme AEM

>[!NOTE]
>
>Toutes les captures d’écran ci-dessous utilisent le chiffre 1 à titre d’illustration uniquement. Vous devez utiliser le numéro qui vous a été attribué dans le cadre de l’e-mail que vous avez reçu lors des étapes ci-dessous.

Votre programme AEM utilise le numéro qui vous a été attribué à son nom. Le nom de votre programme AEM doit être :

- **Insiders techniques - AEM + ACCS X** où X correspond au nombre qui vous a été attribué.

![DSN ](./images/aem1.png)

Vous pouvez accéder à votre programme AEM et le retrouver en accédant à [https://experience.adobe.com/cloud-manager/landing.html](https://experience.adobe.com/cloud-manager/landing.html). Vérifiez que l’environnement sélectionné est **`--aepImsOrgName--`**. Vous pouvez le vérifier dans le coin supérieur droit de l’écran.

![DSN ](./images/aem2.png)

### Réactivation de votre programme AEM

Le programme AEM utilisé est un programme « sandbox ». AEM sandboxes will hibernate automatically atfer not being used for a couple of hours, which means that you will need to de-hibernate those sandboxes prior to using them. To de-hibernate a program, go to [https://experience.adobe.com/cloud-manager/landing.html](https://experience.adobe.com/cloud-manager/landing.html). Click to open your program.

![DSN ](./images/aem3.png)

You should then see this. Click the 3 dots **...** and then select **De-hibernate**.

![DSN ](./images/aem4.png)

Cliquez sur **Envoyer**. De-hibernation takes 10-15 minutes.

![DSN ](./images/aem5.png)

### GitHub repository for your AEM program

Each AEM program is using Edge Delivery Services to deploy your website. This means that the code of your website is hosted in a GitHub repository. The GitHub repository has been created for you and can be accessed by going to:

**https://github.com/woutervangeluwe/techinsidersX-citisignal-aem-accs**, whereby you have to replace X by your number.

Your GitHub repository should look like this.

![DSN ](./images/aem6.png)

As part of the onboarding process before the start of your Tech Lab sessions, you will be asked to provide your GitHub username. By providing your GitHub username, you will be added as a collaborator to the GitHub repository that is attached to your website so that you can make changes to it.

### Access your website

To access your website, you can use these default URLs:

- **https://main--techinsidersX-citisignal-aem-accs--woutervangeluwe.aem.page/**
- **https://main--techinsidersX-citisignal-aem-accs--woutervangeluwe.aem.live/**

You need to replace the X in these URLs by the number that was assigned to you.

Additionally, a custom domain name has been created for each website, which you can access using this URL:

- **https://techinsidersX.adobedemosystem.com/**

Vous devez remplacer le X dans ces URL par le numéro qui vous a été attribué.

Vous devriez ensuite être en mesure de voir votre site web, qui ressemble à ceci :

![DSN ](./images/aem7.png)

## Votre sandbox AEP

>[!NOTE]
>
>Toutes les captures d’écran ci-dessous utilisent le chiffre 1 à titre d’illustration uniquement. Vous devez utiliser le numéro qui vous a été attribué dans le cadre de l’e-mail que vous avez reçu lors des étapes ci-dessous.

Pour le Brand Concierge Tech Lab, vous devez utiliser un sandbox AEP spécifique. Ce sandbox AEP s’appelle **techinsidersX** et vous devez remplacer le X par le numéro qui vous a été attribué.

Accédez à [https://platform.adobe.com](https://platform.adobe.com). Dans le coin supérieur droit de l’écran, ouvrez la liste déroulante pour sélectionner votre sandbox.

Il vous suffit d’utiliser ce sandbox pour le Brand Concierge Tech Lab.

![DSN ](./images/aep1.png)

## Étapes suivantes

Revenez à [Prise en main - Agentic AI](./getting-started-agentic-ai.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}./images
