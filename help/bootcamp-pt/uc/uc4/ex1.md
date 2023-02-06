---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brésil
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brésil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entenda o que é o CJA
- Entenda qual é o papa do CJA
- Entenda au workflow pour CJA : da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics ?

O Customer Journey Analytics (CJA) fornece uma interface em que os times de Analytics, Negócios e Tecnologia conservguem unir todos os dados da company e analisar a jornada cross-channel (en ligne et hors ligne) do cliente de ponta a ponta . O CJA é capaz de fornecer contexto e clareza para essa jornada, trazendo uma visão acionável em cima das dificuldades no processo de conversation e possibilitando planejamento de experiências relevant e personalizadas nos pontos mais relevant.

O CJA traz à Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos esses dados, para que équipes de negócios e insights possam aprender com eles, analisando toda a jornada on-line para-off-line do cliente.

Comme équipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demo](./images/cja-adv-analysis1.png)

## 4.1.2 Principaux vendeurs

Os três principais bénéfique para os clientes são :

- Une condensidade de disponibilité des connaissances para todos (ou seja, Democzar o acesso aos dados).
- Une condensidade de ver o cliente em uma jornada contextuelle (ou seja, os dados podem ser visualizados séquencialmente, abrangendo múltiplos canais on-line e off-line).
- Une capacidade de aproveitar o poder dos dados sem que haja a necessidade (ou seja, permite que indivíduos usem dados para desbloquear insights e análises profundas para ativação de marketing).

## 4.1.3 ## 4.1.3 Por que escolher ou Customer Journey Analytics ?

O CJA não se destinée a substituir um aplicativo de BI réel, como Power BI, Microstratégie, Locker ou Tableau. O objetivo desses aplicativos de BI é visualizar dados para criar peis capativos para que todos em uma organization apam par métricas importantes rapidement amente. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitir a verdadeira inteligência do cliente :

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI précisam saba pergunta com antecedência
- En tant que consultant interativas são limitadas pela estrutura do banco de dados
- Habilidades de SQL são rendárias .
- Os aplicativos de BI não permitem que você pergunte o motivo um acontecimento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA você pode ter uma visão completa da jornada do cliente, usando dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios para entender que algo aconteceu e como responder a isso .

![demo](./images/cja-use-case.png)

## 4.1.4 Comportement de fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exerícios, é essencial talender quais etapas são besoin árias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter donne un aperçu des profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos verificar :

![demo](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que é je comprends os dados que estão disponíveis na Adobe Experience Platform.

**Des ordures, des ordures.** Le Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas a Adobe Experience Platform são configurados Comprendre les dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexão de dados, mas também na hora de construcir visualizações e fazer análises.

## 4.1.5 Etapa 0 : Comprendre les schémas et les jeux de données dans Adobe Experience Platform

Faça se connecte à Adobe Experience Platform et accède à une URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](../uc1/images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nomo do sandbox a ser selecionado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** pas de canto supérieur direito da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu sandbox dedicado.

![Ingestion des données](../uc1/images/sb1.png)

Vérification : envoie des schémas et des jeux de données dans Adobe Experience Platform.

| Jeu de données | Schéma |
| ----------------- |-------------| 
| Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1) | Système de démonstration - Schéma d’événement pour le site web (Global v1.1) |
| Système de démonstration - Jeu de données d’événement pour le centre d’appels (Global v1.1) | Système de démonstration - Schéma d’événement pour le centre d’appels (Global v1.1) |
| Système de démonstration - Jeu de données d’événement pour les assistants vocaux (Global v1.1) | Système de démonstration - Schéma d’événement pour les assistants vocaux (Global v1.1) |

Certifique-se de ter verificado ao menos :

- Identités : CRMID, phoneNumber, ECID, email. Quelles identités sont les identifiants Principaux, lesquels sont les identifiants secondaires ?
Vous pouvez trouver les identifiants en ouvrant un schéma et en regardant l’objet `_experienceplatform.identification.core`. Consultez le schéma [Système de démonstration - Schéma d’événement pour le site web (Global v1.1)](https://experience.adobe.com/platform/schema).

- Identidades : CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, quais são os identificadores secundários ?
Você pode encontrar os identificadores abrindo um schema e observando objecto `_experienceplatform.identification.core`. Vérification du schéma o [Système de démonstration - Schéma d’événement pour le site web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Exploration du schéma objeto de comércio dentro do [Système de démonstration - Schéma d’événement pour le site web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Visualisation des outils [jeux de données](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está pronto para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa : [Concevoir des jeux de données avec Adobe Experience Platform sans Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
