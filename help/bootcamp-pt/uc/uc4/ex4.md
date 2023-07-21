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
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Préparation des dados em Customer Journey Analytics

## Objetivos

- Enrichissement d’une opération d’authentification unique pour Analysis Workspace sur CJA
- Entenda os vanitos de preparação de dados sur Analysis Workspace
- Aprenda a fazer cálculos de dados

## 4.4.1 Interface utilisateur d’Analysis Workspace sur CJA

O Analysis Workspace supprimez todas comme limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e components (dimensues, métricas, segmentos e granularidades de tempo) para project. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, compare ação de segmentos, análise de fluxo e falhas e relatórios de curadoria e agendamento para lhar com qualquer pessoa em eu negócio.

O Customer Journey Analytics traz essa Solution além dos dados da plataforma É altamente recomendável assistance a a este video de visão geral de quatro minutos :

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, recomendamos este vídeo

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Criez le projet

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique **Créer**.

![demo](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Select **Projet vierge** enão mafieux em **Créer**.

![demo](./images/prmenu1.png)

Você verá um projeto vazio.

![demo](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto supérieur direito da tela. exemplaire de Neste, une Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar :

| Système d’exploitation | Court |
| ----------------- |-------------| 
| Windows | Ctrl + S |
| Mac | Commande + S |

La pop-up Você verá este :

![demo](./images/prsave.png)

Utilisez le modèle de genre de nomenclatura :

| Nom | Description |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, groupe em **Enregistrer**.

![demo](./images/prsave2.png)

## 4.4.2 Calculadas de mesures

Embora tenhamos organisado todos os components na Visualização de dados, você ainda deve adaptar alguns para que os usuários de negócios estejam prontos para iniciar suas análises Além disso, durante qualquer processo de analytics, você pode criar métricas calculadas para aprofundar a descoberta de insights.

Como exemplaire, criaremos uma Taxa de conversada usando a métrica/evento Compras que definitions na Visualização de dados.

## Taxa de conversão

Vamos começar a abrir de construction de métricas calculadas. Clique **+** para criar sua primeira Métrica calculada sur Analysis Workspace.

![demo](./images/pradd.png)

O **Créateur de mesures calculées** Aparecer irá :

![demo](./images/prbuilder.png)

Encontre **Achats** une liste de métricas pas de menu pour lado esquerdo. Em **Mesures** groupe **Tout afficher**

![demo](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Achats** une définition ição da métrica calculada.

![demo](./images/calcbuildercr2.png)

Normalmente, taxa de conversão signião **Conversions / Sessions**. Então, vamos fazer o mesmo cálculo na tela de definition de métrica calculada. Encontre a métrica **Sessions** e arraste e solte-a no criador de define, pas même **Achats**.

![demo](./images/calcbuildercr3.png)

Observez que o operador de divisão é selecionado automatiquement.

![demo](./images/calcbuildercr4.png)

Un taxi de conversão é é comumente représentada em porcentagem. Então, vamos mudar o formato para porcentagem e selecionar 2 casas decimais.

![demo](./images/calcbuildercr5.png)

Enfin, modifiez le nom et la description de la mesure calculée :

| Titre | Description |
| ----------------- |-------------| 
| Taux de conversion | Taux de conversion |

Por fim, altere o nome a descripção da métrica calculada :

![demo](./images/calcbuildercr6.png)

Não se esqueça **Salvar** une calculette Métrica.

![demo](./images/pr9.png)

## 4.4.3 Dimensões calculadas : Filtros (segmentação) e intervalles de données

### Filtres : Dimensões calculadas

Os cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é interessante, algumas **Dimensions calculées**. Isso signifiait, essencialmente, **segments** Aucun Adobe Analytics. Aucun Customer Journey Analytics, ainsi segmentos são chamados de **Filtres**.

![demo](./images/prfilters.png)

Une criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas . &quot;Isso irá&quot;, alalém de ajudar na parte de adoção, algumas tarefas. Abaixo estão alguns s&#39;exclame :

1. Mídia Própria, Mídia Paga,
2. Visitas novas x recorrentes
3. Clientes com carrinho abandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo Exercício).

### Intervalos de datas : Dimensões de tempo calculadas

En tant que dimensions du tempo são outro tipo de dimensues calculadas. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas a fase de preparação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembar datas importantes e usá-las filtrar e alterar o tempo de relatório . Perguntas e dúvidas típicas quando fazemos análises

- Quando foi a Black Friday do ano passado ? Entre os dias 21 e 29 ?
- Quando veiculamos aquela campanha de TV em dezembro ?
- De quando a quando fizemos comme vendas de verão de 2018 ? Comparaison de Quero com 2019. Une propósito, você sabe os dias exatos em 2019 ?

![demo](./images/timedimensions.png)

L&#39;Agora você final o obligação de preparação de dados usando o Analysis Workspace do CJA.

Próxima etapa : [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
