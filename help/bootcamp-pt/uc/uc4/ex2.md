---
title: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
description: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 4.2 Concevoir les jeux de données da Adobe Experience Platform sans Customer Journey Analytics

## Objetivos

- Comprendre une interface utilisateur da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda un ID da pessoa e a compilão de dados
- Approbation de la diffusion en continu des données sur le Parcours client

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página officieuse do Customer Journey Analytics, acesse **Connexions**.

![demo](./images/cja2.png)

Aqui você pode ver todas as as diferentes conexões feitas entre CJA e a Plataforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics. No entanto, a coleta dos dados é completamente diferente. Todos os dados m de datasets da Adobe Experience Platform.

Vamos criar sua primeira conexão. Clique **Créer une connexion**.

![demo](./images/cja4.png)

Você verá a UI **Créer une connexion** Interface utilisateur.

![demo](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Utilisez le modèle de genre de nomenclatura : `yourLastName – Omnichannel Data Connection`.

Exemplo : `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox core para usar. Aucun environnement de test de menu, sélection d’un environnement de test de l’environnement de test de l’environnement de test `Bootcamp`. Neste exemplaire, o sandbox a ser usado é o **Bootcamp**. E você também deve definition o **Nombre moyen d’événements quotidiens** to **moins de 1 million**.

![demo](./images/cjasb.png)

Após selecionar seu sandbox, você pode começar a adicionar datasets a esta conexão . Clique **Ajout de jeux de données**.

![demo](./images/cjasb1.png)

## 4.2.2 Sélection des jeux de données dans Adobe Experience Platform

Pesquisse d’un jeu de données `Demo System - Event Dataset for Website (Global v1.1)`. Clique **+** para adicionar du jeu de données a esta conexão.

![demo](./images/cja7.png)

Agora occupe l&#39;e-marque en tant que caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` et `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. Clique **Suivant**.

![demo](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora é juntar délivre des jeux de données. Para cada dataset selecionado, você verá um campo chamado **ID de personne**. Jeu de données du Cada tem seu próprio campo de ID de pessoa.

![demo](./images/cja11.png)

Le podium Como você, une maioria deles e o ID da pessoa selecionado Automcamente. Isso porte le porque um identificador principal é selecionado em cada esquema na Adobe Experience Platform. Como exemplaire, qui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, pode onde você ver que o Identificador Primário está define comido `phoneNumber`.

![demo](./images/cja13.png)

Non entanto, você ainda pode influenciar qual identificador será usado para compilar datasets para sua conexão . Você pode usar qualquer identificador configurado no esquema vinculado ao seu dataset. Ne cliquez pas sur les suspensions de menus pour que les identifiants du système d’exploitation explorateur distribuent le jeu de données em cada.

![demo](./images/cja14.png)

Conforme mencionado, você pode definitions diferentes IDs de pessoa para cada dataset. Isso permite reunir diferentes jeux de données de múltiplas sur les origines de CJA. Imaginez le traducteur NPS ou dados de pesquisa que seriam muito interessantes e úteis para relevant ou contexto e motivo um acontecimento.

O nome do campo ID da pessoa é important, desde que o valor nos campos ID da pessoa corresponda. Digamos que temos `email` em um dataset e `emailAddress` définition du jeu de données externe como ID da pessoa. Se `delaigle@adobe.com` véto o mesmo valor para o campo ID da pessoa em ambos os datasets, ou CJA poderá compilar os dados.

Atualmente, existent algumas ouas limitações, como comar o comportamento anônimo para conchaido. Consulte en tant que perguntas fréquentes aqui : [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=fr).


### Compilando os dados usando o ID da pessoa

Agora que você compréhensible o disito de compilar datasets usando o ID da pessoa, vamos escolher `email` ensemble de données como ID da pessoa para cada .

![demo](./images/cja15.png)

Acesse cada dataset para atualizar o ID da pessoa.

![demo](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` une lista suspensa.

![demo](./images/cja17.png)

Dépois de compilar os três, estamos prontos para continuar.

| jeu de données | ID de personne |
| ----------------- |-------------| 
| Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour les assistants vocaux (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour le centre d’appels (Global v1.1) | adresse e-mail |

Você também precisa que, para cada dataset, essas opções estejam habilitadas as :

- Importants outils os novos dados
- Preencher todos os dados existentes
- Preencher tipo de fonte de dados com &quot;Autres&quot;
- Prévisualisez une description com o mesmo nome do Dataset

Clique **Ajout de jeux de données**.

![demo](./images/cja16.png)

Clique **Enregistrer** e vá para o próximo exercice. Depois de criar sua **Connexion**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demo](./images/cja20.png)

Próxima etapa : [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
