---
title: Bootcamp - Real-time Customer Profile - De inconnu à connu sur le site - Brésil
description: Bootcamp - Real-time Customer Profile - De inconnu à connu sur le site - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 1%

---

# 1.1 Procédez à desconchaido ao conhecido em nosso site

## Contexto

Un Adobe Experience Platform desempenha um papel important nessa jornada. Une Plataforma é o cébro da comunicação, o **système d’enregistrement d’expérience**.

Plataforma é um ambiente em que a palavra cliente globale, mais do que clientes conhecidos. Oum visitante desconchaido no site também é um cliente do ponto de vista da Plataforma e, como tal, todo o visitor amento um visitante desconhecido também é enviado à Plataforma. Graças a abordagem, quando esse visitante éventuellement almente se torna um cliente conquête, uma marca também pode visualizar o que aconteceu antes daquele momento. Isso ajuda a une partir de uma perspectiva de otimização de tribuição e experiência.

## Fluxo da jornada do cliente

Acesse [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique **Tout autoriser**.

![DSN](./images/web8.png)

Clique no ícone do loégocipo da Adobe no canto supérieur esquerdo da tela para abrir o Visualizador de perfil.

![Démonstration](./images/pv1.png)

Vérifique o peel do Visualizador de perfil e no Perfil do cliente em tempo real com o **ID Experience Cloud** como identificador primário para este cliente ainda é desconchaido.

![Démonstration](./images/pv2.png)

Você também pode ver todos os Eventos de Experiência coletados com base no comportamento do cliente. Une lista está vazia no momento, mas is mudará em breve.

![Démonstration](./images/pv3.png)

Acesse à l&#39;opção de menu **Services d’application** e clic no producto **Real-Time CDP**.

![Démonstration](./images/pv4.png)

Você verá a página de detalhes do producto. Oum Evento de experiência do tipo **Consultation produit** agora foi enviado para a Adobe Experience Platform usando a implementação do Web SDK que você version no Módulo 1. Abra o peel Visualizador de perfil e verifique **Événements d’expérience**.

![Démonstration](./images/pv5.png)

Acesse à l&#39;opção de menu **Services d’application** e clic no producto **Adobe Journey Optimizer**. Mais um Evento de experiência foi enviado para a Adobe Experience Platform.

![Démonstration](./images/pv7.png)

Abra o peel Visualizador de perfil. Agora você verá 2 Eventos de experiência do tipo **Consultation produit**. Embora o comportto seja anônimo, cada clique é rastreado e armazenado na Adobe Experience Platform. Depois que o cliente anônimo se tornar conchaido, poderemos mesclar todo o comportement amento anônimo automatisente perfil conchido.

![Démonstration](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportement amento para personalizar sua experiência do cliente no site.

Próxima etapa : [1.2 Visualiser seu próprio perfil de cliente em tempo real - interface utilisateur](./ex2.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
