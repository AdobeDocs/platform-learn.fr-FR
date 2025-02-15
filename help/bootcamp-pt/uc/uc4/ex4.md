---
title: Bootcamp - Customer Journey Analytics - Préparation des données dans Analysis Workspace - Brésil
description: Bootcamp - Customer Journey Analytics - Préparation des données dans Analysis Workspace - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 1%

---

# 4.4 Preparation de dados em Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace sur CJA
- Entenda os concitos de preparation ação de dados no Analysis Workspace
- Aprenda a fazer cálculos de dados

## 4.4.1 L’interface utilisateur d’Analysis Workspace n’utilise pas CJA

O Analysis Workspace supprimer les jours fériés comme limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma É altamente recomendável assistir a este vídeo de visão geral de quatro minutos :

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on&enablevpops)

Se você nunca usou o Analysis Workspace antes, recomendamos este vídeo :

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on&enablevpops)

### Crie Seu Projeto

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique em **Créer**.

![demo](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Sélection **Projet vierge** então clique em **Créer**.

![demo](./images/prmenu1.png)

Você verá um projeto vazio.

![demo](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste exemplaire, a Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar :

| SE | Raccourci |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Commande + S |

Fenêtre contextuelle de Você verá este :

![demo](./images/prsave.png)

Utiliser le modèle de nomenclatura :

| Nom | Description |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **Enregistrer**.

![demo](./images/prsave2.png)

## 4.4.2 Calculades métriques

Embora tenhamos organizado todos os componentes na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar métricas calculadas para aprofundar a descoberta de insights.

Como exemplaire, criaremos uma Taxa de conversão calculada usando a métrica/evento Compras que definimos na Visualização de dados.

## Taxa de conversão

Vamos começar a abrir o constructeur de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada no Analysis Workspace.

![demo](./images/pradd.png)

O **créateur de mesures calculées** irá aparecer :

![demo](./images/prbuilder.png)

Encontre **Achats** na lista de métricas no menu do lado esquerdo. Em **Mesures** clique em **Tout afficher**

![demo](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Achats** na definição da métrica calculada.

![demo](./images/calcbuildercr2.png)

Normalmente, taxa de conversão significa **Conversions / Sessions**. Então, vamos fazer o mesmo cálculo na tela de definição de métrica calculada. Encontre a métrica **Sessions** e arraste e solte-a no criador de definição, no evento **Achats**.

![demo](./images/calcbuildercr3.png)

Observez que o operador de divisão é selecionado automaticamente.

![demo](./images/calcbuildercr4.png)

A taxa de conversão é commumente presentada em porcentagem. Então, vamos mudar o formato para porcentagem e selecionar 2 casas decimais.

![demo](./images/calcbuildercr5.png)

Enfin, modifiez le nom et la description de la mesure calculée :

| Titre | Description |
| ----------------- |-------------| 
| Taux de conversion | Taux de conversion |

Por fim, altere o nome a descripção da métrica calculada :

![demo](./images/calcbuildercr6.png)

Não se esqueça de **Salvar** a Métrica calculada.

![demo](./images/pr9.png)

## 4.4.3 Dimensões calculadas : Filtros (segmentação) e interval de datas

### Filtres : Dimensões calculadas

Os cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é interessante criar algumas **Dimensions calculées**. Isso significa, essencialmente, **segments** pas Adobe Analytics. Pas de Customer Journey Analytics, ess segmentos são chamados de **Filters**.

![demo](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas. Isso irá automatizar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão alguns exemploys :

1. Mídia Própria, Mídia Paga
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo exerício).

### Intervalles de données : Dimensões de tempo calculadas

As dimensões de tempo são outro tipo de dimensões calculadas. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas na fase de preparation ação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembrar datas importantes e usá-las para filtrar e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises :

- Quando foi a Black Friday do ano passado ? Entre os dias 21 e 29 ?
- Quando veiculamos aquela campanha de TV em dezembro ?
- De quando a quando fizemos as vendas de verão de 2018 ? Quero comparar com 2019. A propósito, você sabe os dias exatos em 2019 ?

![demo](./images/timedimensions.png)

Agora você concluiu o exerício de preparation ação de dados usando o Analysis Workspace do CJA.

Próxima etapa : [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
