---
title: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
description: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2 Concevoir les jeux de données da Adobe Experience Platform sans Customer Journey Analytics

## Objetivos

- Comprendre une interface utilisateur da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda un ID da pessoa e a compilão de dados
- Approbation de la diffusion en continu des données sur le Parcours client

## 4.2.1 Conexão

Accédez à [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página officiant do Customer Journey Analytics, accédez à **Connexions**.

![demo](./images/cja2.png)

Aqui você pode ver todas as as diferentes conexões feitas entre CJA e a Plataforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics. No entanto, a coleta dos dados é completamente diferente. Todos os dados m de datasets da Adobe Experience Platform.

Vamos criar sua primeira conexão. Clique em **Créer une connexion**.

![demo](./images/cja4.png)

Você verá a UI **Créer une connexion**.

![demo](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Utilisez le modèle de crime de nomenclatura : `yourLastName – Omnichannel Data Connection`.

Exemplo : `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox core para usar. Aucun environnement de test de menu, sélection d’un environnement de test, que d’affichage utilisateur `Bootcamp`. Neste exemplaire, o sandbox a ser usado é sur **Bootcamp**. E você também est défini sur **Nombre moyen d&#39;événements quotidiens** à **moins de 1 million**.

![demo](./images/cjasb.png)

Após selecionar seu sandbox, você pode começar a adicionar datasets a esta conexão . Cliquez Sur **Ajouter Des Jeux De Données**.

![demo](./images/cjasb1.png)

## 4.2.2 Sélection des jeux de données dans Adobe Experience Platform

Pesquise du jeu de données `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para adicionar du jeu de données a esta conexão.

![demo](./images/cja7.png)

Agora occupe la place de marque en tant que caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` et `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. Cliquez Sur **Suivant**.

![demo](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora é juntar délivre des jeux de données. Para cada dataset selecionado, você verá um campo chamado **Person ID**. Jeu de données du Cada tem seu próprio campo de ID de pessoa.

![demo](./images/cja11.png)

Le podium Como você, une maioria deles e o ID da pessoa selecionado Automcamente. Isso porte le porque um identificador principal é selecionado em cada esquema na Adobe Experience Platform. Como exemplaire, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador Primário está define como `phoneNumber`.

![demo](./images/cja13.png)

Non entanto, você ainda pode influenciar qual identificador será usado para compilar datasets para sua conexão . Le pode Você usar qualquer identificador configurado no esquema vinculado ao seu dataset. Ne cliquez pas sur les suspensions de menus pour que les identifiants du système d’exploitation explorateur distribuent le jeu de données em cada.

![demo](./images/cja14.png)

Conforme mencionado, você pode definitions diferentes IDs de pessoa para cada dataset. Isso permite reunir diferentes jeux de données de múltiplas sur les origines de CJA. Imaginez le traducteur NPS ou dados de pesquisa que seriam muito interessantes e úteis para relevant ou contexto e motivo um acontecimento.

O nome do campo ID da pessoa é important, desde que o valor nos campos ID da pessoa corresponda. Digamos que temos `email` em um dataset e `emailAddress` em outro dataset definition como ID da pessoa. Voir `delaigle@adobe.com` véto o mesmo valor para o campo ID da pessoa em ambos os datasets, ou CJA poderá compilar os dados.

Atualmente, existent algumas ouas limitações, como comar o comportamento anônimo para conchaido. Consulte en tant que perguntas fréquentes aqui : [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).


### Compilando os dados usando o ID da pessoa

Agora que você compréhensible o disito de compilar datasets usando o ID da pessoa, vamos escolher `email` como ID da pessoa para cada dataset.

![demo](./images/cja15.png)

Acesse cada dataset para atualizar o ID da pessoa.

![demo](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa.

![demo](./images/cja17.png)

Dépois de compilar os três, estamos prontos para continuar.

| Jeu de données | ID de personne |
| ----------------- |-------------| 
| Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour les assistants vocaux (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour le centre d’appels (Global v1.1) | adresse e-mail |

Você também precisa que, para cada dataset, essas opções estejam habilitadas as :

- Importants outils os novos dados
- Preencher todos os dados existentes
- Preencher tipo de fonte de dados com &quot;Autres&quot;
- Prévisualisez une description com o mesmo nome do Dataset

Cliquez Sur **Ajouter Des Jeux De Données**.

![demo](./images/cja16.png)

Clique em **Save** e vá para o próximo Exercício. Depois de criar sua **Connection**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demo](./images/cja20.png)

Próxima etapa : [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
