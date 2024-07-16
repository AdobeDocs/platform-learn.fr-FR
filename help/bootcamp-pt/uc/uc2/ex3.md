---
title: Bootcamp - Journey Optimizer Créez votre parcours et votre email - Brésil
description: Bootcamp - Journey Optimizer Créez votre parcours et votre email - Brésil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: d486d1aa-7b8e-4301-91e6-4c84fba0c72a
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 3%

---

# 2.3 Crie sua jornada e mensuagem de e-mail

Neste exerício, você irá configurar a jornada que precisa ser acionada quando alguém criar uma conta no site de démonstração.

Connexion à Faça sur Adobe Journey Optimizer et accès à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Clique-Les **Journey Optimizer**.

![ACOP](./images/acophome.png)

Le Você será rediRecionado para a visualização da **Home** on Journey Optimizer. Primeiro, verifique se você está usando o sandbox correto. O nome do sandbox que deve ser usado `Bootcamp`. Para alternar de um sandbox para outro, groupe em **Prod** e selecione o sandbox na lista. exemplaire de Neste, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Prier a sua jornada

Aucun menu à esquerda, clic em **Parcours**. Em seguida, groupe em **Create Parcours** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia.

![ACOP](./images/journeyempty.png)

Aucun exercice antérieur, você criou um novo **Event**. Você nomeou même `seuSobrenomeAccountCreationEvent` e substitution `seuSobrenome` pelo seu sobrenome. Este foi o résultado da criação do Evento :

![ACOP](./images/eventdone.png)

Agora você deve penar este evento como início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e proando pelo seu evento a lista de eventos .

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte ou encore na tela de Jornada. Sua Jornada agora deve ser semelhante ao seguinte :

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma etapa curta de **Wait**. Vá para o lado esquerdo da tela até a seção **Orchestration** para encontrar isso. Você ustributos de precisará á que sejam prejam dos no Perfil do Cliem tempo real.

![ACOP](./images/journeywait.png)

Sua jornada agora deve ser semelhante ao seguinte. Pas de lado direito da tela você précisa configurar o tempo de espera. Définit une como à 1 minute. Isso dará bastante tempo para que os atributos do perfil estejam disponíveis após o disparo do evento.

![ACOP](./images/journeywait1.png)

Clique em **Ok** para salvar suas alterações.

Como terceira etapa da jornada, você deve adicionar uma ação **Email**. Vá para o lado esquerdo da tela para **Actions**, selecione a ação **Email** e arraste e solte a ação no segundo nó da sua jornada. Agora o seguinte será exibido.

![ACOP](./images/journeyactions.png)

Définissez une **catégorie** como **Marketing** e selecione uma **e-mail surface** que permita o envio de e-mail. Nesse caso, une **surface de courriel** a ser selecionada é E-mail. Certifique-se de que as caixas de seleção **Clics sur email** e **Ouvertures sur email** estejam marcadas.

![ACOP](./images/journeyactions1.png)

Un próximo etapa é criar sua mensuagem. Para isso, suivez-moi **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Pénétrer un sua mensuagem

Para criar sua mensuagem, groupe em **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

O seguinte será exibido.

![ACOP](./images/journeyactions3.png)

Clique no campo de texto **Objet**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, commerce **Olá**

![Journey Optimizer](./images/msg6.png)

Une linha de assunto ainda não está pronta. Em seguida, você precisa trazer o token de personalização para o **First name** que está armazenado em `profile.person.name.firstName`. Aucun menu à esquerda, rôle para baixo para encontro elemento **Person** e clique na seta para visualizar mais campos

![Journey Optimizer](./images/msg7.png)

Agora contre elemento **Nom complet** e clique na seta para visualizar mais campos.

![Journey Optimizer](./images/msg8.png)

Por fim, localisez sur campo **Prénom** e clique no símbolo **+** ao lado dele. Appart du Você verá o token de personalização no campo texto.

![Journey Optimizer](./images/msg9.png)

Em seguida, adicione o texto, **agradecemos a sua inscrição !**. Clique-Les **Enregistrer**.

![Journey Optimizer](./images/msg10.png)

Então, você irá retornar para esta tela. Clique em **Email Designer** para criar o conteúdo do e-mail.

![Journey Optimizer](./images/msg11.png)

Na próxima tela, será solicitado que você forneça o conteúdo e-mail através de 3 métodos diferentes :

- **Conception à partir de zéro** : Comece com uma tela em branco e use to editor WYSIWYG para arrastar e soltar a estrutura e os componentes de conteúdo para criar visualmente o conteúdo e e-mail.
- **Code your own** : Crie seu próprio modelo de e-mail codificando usando HTML
- **Import HTML** : Importe um modelo HTML existente, que você poderá editar.

Cliquez Sur **Importer L’HTML**.

![Journey Optimizer](./images/msg12.png)

Arraste e solte o arquivo **mailtemplatebootcamp.html**, que você pode baixa [aqui](../../assets/html/mailtemplatebootcamp.html.zip). Clique em Importar.

![Journey Optimizer](./images/msg13.png)

Você verá este modelo de e-mail padrão :

![Journey Optimizer](./images/msg14.png)

Vamos personalizar ou email. Clique ao lado do texto **Olá** e, em seguida, clic no ícone **Ajouter Personalization**.

![Journey Optimizer](./images/msg35.png)

Em seguida, você precisa trazer o token de personalização **First name** que está armazenado em `profile.person.name.firstName`. Aucun menu, localisez ou elemento **Person**, faça uma busca detalhada no elemento **Full Name** e clique no ícone **+** para adicionar o **First Name** ao editor.

Clique-Les **Enregistrer**.

![Journey Optimizer](./images/msg36.png)

Agora você verá como campo de personalização foi adicionado ao seu texto.

![Journey Optimizer](./images/msg37.png)

Clique em **Save** para salvar sua mensuagem.

![Journey Optimizer](./images/msg55.png)

Retorne para o pinel de mensuagens clicando na seta ao lado do texto da linha de assunto no canto supérieur esquerdo.

![Journey Optimizer](./images/msg56.png)

Agora você qui conclut une &quot;criação do seu e-mail de cadastro&quot; Clique na seta no canto supérieur esquerdo para retornar à sua jornada.

![Journey Optimizer](./images/msg57.png)

Cliquez Sur L’Écran **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Publique a sua jornada

Você ainda precisa dar um Nome à sua jornada. Você pode fazer isso clicando no ícone **Properties** no canto supérieur direito da tela.

![ACOP](./images/journeyname.png)

Você pode fazer isso clicando no item pas clicar no item &quot;Name&quot; e inserindo o seguinte nome `yourLastName - Account Creation Journey`. Clique em **OK** para salvar as mudanças.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Publish**.

![ACOP](./images/publishjourney.png)

Clique em **Publish** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de confirmação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Você terminou este exercice.

Próxima etapa : [2.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
