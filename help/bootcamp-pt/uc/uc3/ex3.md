---
title: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push - Brazilnotification
description: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push - Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 1%

---

# 3.3 Presse sua jornada e notificação push

Neste exerício, você irá configurar a jornada e a mensuagem que precisa ser acionada quando alguém inserir uma sinalização (balise) usando o aplicativo móvel .

Connexion à Faça sur Adobe Journey Optimizer et accès à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Clique-Les **Journey Optimizer**.

![ACOP](./images/acophome.png)

Le Você será rediRecionado para a visualização da **Home** on Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, groupe em **Prod** e selecione o sandbox na lista. exemplaire de Neste, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Prier a sua jornada

Aucun menu à esquerda, clic em **Parcours**. Em seguida, groupe em **Create Parcours** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Aucun exercice antérieur, você criou um novo **Event**. Você nomeou même `yourLastNameBeaconEntryEvent` e substitution `yourLastName` pelo seu sobrenome. Este foi o résultado da criação do Evento :

![ACOP](./images/eventdone.png)

Agora você deve penar este evento como início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e proando pelo seu evento a lista de eventos .

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte ou encore na tela de jornada. Sua jornada agora deve ser semelhante ao seguinte. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

No lado direito da tela, agora você deve criar sua notificação push.

Définissez une **catégorie** como **Marketing** e selecione um push surface que permite enviar notificações push. Nesse caso, un superfície pousse une selecionada é **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Pénétrer un sua mensuagem

Clique-Les **Modifier Le Contenu**.

![ACOP](./images/emptymsg.png)

Em seguida, une tela abaixo será exibida :

![ACOP](./images/emailmsglist.png)

Vamos define o conteúdo da notificação push.

Clique no campo de texto **Title**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, commerce **Olá**. Clique no ícone de personalização.

![Journey Optimizer](./images/msg6.png)

Agora você précisa trazer o token de personalização para o campo **First name** que está armazenado em `profile.person.name.firstName`. Aucun menu à esquerda, selecione **Attributs de profil**, rôle para baixo/navegue para encontrar o elemento **Person** e clique na seta para avançar um nível chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela. Clique-Les **Enregistrer**.

![Journey Optimizer](./images/msg7.png)

Então, você irá retornar para esta tela. Clique no ícone de personalização ao lado do campo **Body**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, groupe em **Attributs Contextuels** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Cliquez Sur Les **Événements**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Cliquez Sur L’Icône **Placer Le Contexte**.

![ACOP](./images/jomsg6.png)

Cliquez Sur L’Icône **Interaction Du Point Ciblé**.

![ACOP](./images/jomsg7.png)

Cliquez Sur Les **Détails Du Point Ciblé**.

![ACOP](./images/jomsg8.png)

Appuyez sur l’icône **+** sur **Nom du point ciblé**.
Em seguida, o seguinte será exibido. Clique-Les **Enregistrer**.

![ACOP](./images/jomsg9.png)

Sua mensuagem agora está pronta. Clique na seta no canto supérieur esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Cliquez Sur L’Écran **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie : mensualité de la uma tela

Como terceira etapa da jornada, você deve adicionar uma ação **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Actions**, select a ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensuagem no **Endpoint** usado pela exibição na loja. Une ação **sendMessageToScreen** espera que múltiplas variáveis sejam definitions. Você pode visualizar essas variáveis rolando para baixo ver **Paramètres d&#39;action**.

![ACOP](./images/jomsg16.png)

Agora você precisa define os valores para cada parâmetro de ação Siga esta tabela para entender quais valores são rendários e onde.

| Paramètre | valeur |
|:-------------:| :---------------:|
| DIFFUSION | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| PREMIER NOM | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| ENVIRONNEMENT DE TEST | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para Definir dénombre des valeurs, clique no ícone **Edit**.

![ACOP](./images/jomsg17.png)

Em seguida, select **Mode avancé**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Cliquez Sur L’Écran **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de substitution `yourLastName` pelo seu sobrenome.

O result final user semelhante ao seguinte :

![ACOP](./images/jomsg20.png)

Rôle para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

Vous devez toujours donner un nom à votre parcours. Pour ce faire, cliquez sur l’icône **Propriétés** dans le coin supérieur droit de votre écran.

![ACOP](./images/journeyname.png)

Le pode Você Inserir ou nome da jornada aqui. Utilisez `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercice.

Próxima etapa : [3.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
