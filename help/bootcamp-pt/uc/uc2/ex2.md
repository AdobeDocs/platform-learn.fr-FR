---
title: Bootcamp - Journey Optimizer Créer votre événement - Brésil
description: Bootcamp - Journey Optimizer Créer votre événement - Brésil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Événement de la seu de cri

Connexion à la Faça sur l’accès à Adobe Journey Optimizer a [Adobe Experience Cloud](https://experience.adobe.com). Clique **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será rediredireconado para a visualização da **Accueil** Aucun Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nomo do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, groupe em Prod e selecione o sandbox na lista. exemplaire de Neste, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Accueil** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Aucun menu à esquerda, rôle para baixo e clique em **Configurations**. Em seguida, clans pas botão **Gérer** abaixo de **Événements**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique **Créer un événement** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Appart de Uma nova janela de evento vazia irá .

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por exemplaires : `seuSobrenomeAccountCreationEvent` e adicione uma descripção como, por exemplaire o : `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Type** está définitivement ido como **Unitaire** e, para a seleção de **Type d’identifiant d’événement**, selecione **Généré par le système**.

![ACOP](./images/eventidtype.png)

Un schéma etapa seguinte é a seleção do . Um schema foi preparado para este exercice ício. Utilisation d’un schéma `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Champs**. Agora você deve passar o mouse sobre a seção **Champs** e três ícones pop-up serão exibidos. Clique no ícone **Modifier**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Champs**, onde você deve selecionar alguns dos campos que precisamos para personalizar o e-mail Escolheremos outros atributos de perfil posteriormente, utilitzando os dados já existe na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Aucun objet `_experienceplatform.demoEnvironment`, certifique-se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Aucun objet `_experienceplatform.identification.core`, certifique-se de selecionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique **Ok** à para salvar suas alterações.

![ACOP](./images/saveok.png)

Em seguida, un tela abaixo deve ser exibida. Clique **Enregistrer**  mais uma vez para salvar suas alterações..

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **Modifier l’événement**. Passe à la souris sobre **Champs** para ver os 3 ícones outra vez. Clique no ícone **Afficher la charge utile**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplaires a carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você construction irá em um dos próximos exercice Lembre-se deste eventID, você pode precisar dele posteriormente.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique **Ok** e, em seguida, clique em **Annuler**.

Agora você terminou este Exercício.

Próxima etapa : [ 2.3 Crie sua mensuagem de e-mail](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
