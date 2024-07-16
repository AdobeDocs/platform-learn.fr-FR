---
title: Bootcamp - Personalization dans le centre d'appel - Brésil
description: Bootcamp - Personalization dans le centre d'appel - Brésil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.6 Personalização no call center

Conforme discutido várias vezes durante o bootcamp, personalizar a experiência do cliente é algo que deve acontecer de maneira omnichannel. Oum call center geralmente é bastante desconectado do restante da jornada do cliente e isso pode, com fréquência, levar a experiências frustrantes do cliente, mas não precisa ser assim. Vamos mostrar um exemplaire de como pode du centre d&#39;appel ser facile conectado à Adobe Experience Platform, em tempo real.

## Fluxo da jornada do cliente

Pas d&#39;exercice antérieur, d&#39;usando o aplicativo móvel, de você compou producto clicando no botão **Buy**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu pedido, o que você faria ? Normalmente, você ligaria para o call center.

Antes de ligar para o call center, você precisa saber seu **Loyalty ID**. Você pode encontrar seu ID de fidelidade sur le site Visualizador de Perfil do .

![DSN](./images/cc1.png)

Nesse caso, o **Loyalty ID** é **5863105**. Como parte de nossa implementação personalizada do recurso de call center no ambiente de démonstração, você deve adicionar um prefixo seu **Loyalty ID**. O prefixo é **11373**, portanto, o ID de fidelidade a ser usado neste exemplaire é **11373 5863105**.

Vamos fazer est agora. Utilisez seu telefone e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será solicitado que você insira seu ID de fidelidade, seguido de **#**. Identifiant de fidelidade numérique.

![DSN](./images/cc3.png)

Você ouvirá **Bonjour, seu nome**. Esse nome é retirado do Perfil do Cliente em tempo real an Adobe Experience Platform. Você tem 3 escolhas. Pressione o número **1**, **État de la commande**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de pressionar **1** para voltar menu principal ou pressionar 2. Appuyez sur **2**.

![DSN](./images/cc5.png)

Em seguida, será solicitado que você avalie sua experiência de call center, selecionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça a sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o appel centre será encerrada.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte supérieur da tela. Depois de selecionar o [!UICONTROL sandbox] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingestion des données](./images/sb1.png)

Aucun menu à esquerda, accédez à **Profils** et **Parcourir**.

![Profil client](./images/homemenu.png)

Sélectionnez **Identity namespace** **Email** e insira o endereço de e-mail do seu perfil de cliente. Cliquez Sur L’Écran **View**. Clique para abrir seu perfil.

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. Accédez à **Events**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro evento é o result da sua resposta à pergunta **Évaluez votre satisfaction d’appel** (avalie seu chamada).

![DSN](./images/cc9.png)

Rôle um pouco para baixo e você verá o evento que foi enregistrement quando você selecionou a opção de verificar sur **État de la commande**.

![DSN](./images/cc10.png)

Accédez à **abonnement au segment**. Agora você verá que 2 segments se qualificam em seu perfil, em tempo real, com base nas interações que você teve por meio do call center. Essas associações de segmento podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este exercice.

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
