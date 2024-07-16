---
title: Bootcamp - Customer Journey Analytics - De la perspective à l'action - Brésil
description: Bootcamp - Customer Journey Analytics - De la perspective à l'action - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 28b87e21-3168-447e-9a93-a6ae7e969657
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Objetivos

- Entenda comar um público com base em uma visão coletada no Customer Journey Analytics
- Utilisez esse público no CDP em tempo real e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Call Feeling** e conservguiu visualizar a quantidade de usuários que tiveram suas ligações ao call center classificadas como **positivas**. Agora, você poderá criar um segmento com esses usuários e ativação-los em jornadas ou em canais de comunicação.

O primeiro passo é : pas de peintures criado no último exercice cio, selecione a linha **1. Appelez le ressenti : positif**, clique com o botão direito de seu mouse e selecione a opção **Créer une audience d’après la sélection** :

![demo](./images/aud1.png)

Em seguida, dê um nome para a sua audiência seguindo o modelo **yourLastName - cia audience appel impression positive** :

![demo](./images/aud2.png)

Remarque que é possível ter um preview da audiência que está sendo criada :

![demo](./images/aud3.png)

Para finalizar, groupe-em **Publicar** :

![demo](./images/aud4.png)

## 4.6.2 Utilisation de sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segments > Browse** e você consultation guirá visualizar o seu segmento criado no CJA pronto e disponível para ser usado nas suas ativações e jornadas !

![demo](./images/aud5.png)

Vamos agora usar esse segmento em uma ativação no Facebook e em uma jornada do cliente!

## 4.6.3 Utiliser seu segmento a Real-Time CDP em tempo real

Na Adobe Experience Platform, vá em **Segments > Browse** e contre a audiência que você crou no CJA :

![demo](./images/aud6.png)

Clique sans seu segmento e, em seguida, clic em **Activer vers la destination** :

![demo](./images/aud7.png)

Choisissez une destination chamada bootcamp-facebook e, em seguida, clic em Next :

![demo](./images/aud8.png)

Em seguida, groupe em Next novamente :

![demo](./images/aud9.png)

Choisissez une option **Origine de votre audience** e define como **Directly from clients** e clic em Suivant :

![demo](./images/aud10.png)

Por fim, un página **Review** et clic em Finish !

![demo](./images/aud11.png)

Pronto ! Agora o seu segmento está vinculado aos públicos personalizados do Facebook.
Agora, vamos utiliszar esse segmento no AJO!

## 4.6.4 Utilisation de segments de menu à pas dans Adobe Journey Optimizer

Na interface da Adobe Experience Platform clique em Journey Optimizer e, em seguida, pas de menu latéral esquerdo, et moi **Parcours** e commerce un criar uma jornada clicando em **Créer un Parcours** :

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Em seguida, aucun menu latéral esquerdo, em Eventos, select **Qualification de segment** e arraste-o até a jornada

![demo](./images/aud23.png)

Em seguida, em **Segment** et em **Edit** para selecionar um segmento:

![demo](./images/aud24.png)

Sélectionner une audience, une audio que você criou non CJA e clique em **Sauvez** :

![demo](./images/aud25.png)

Pronto ! Une partir daí você pode criar uma jornada para clientes que se qualificam para esse segmento !

[Retour au flux utilisateur 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
