---
title: Bootcamp - Customer Journey Analytics - Créer une vue de données - Brésil
description: Customer Journey Analytics - Créer une vue de données - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: 8cfd4467-167d-4235-a305-4596e3a7d4fb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 2%

---

# 4.3 Crie uma Visualização de Dados

## Objetivos

- Envoi d&#39;une interface utilisateur de Visualização de Dados
- Comprendre en tant que configurações básicas de definitions ição de visita
- Comprendre une attribution : une personnalisation, une diffusion, une diffusion et une diffusion

## 4.3.1 Visualização de Dados

Agora, com sua conexão conclída, é possível progredir para influenciar a visualização. Uma diferença entre à Adobe Analytics e o CJA é que o CJA precisa de uma visualização de dados para limpar e preparar os dados da visualização .

Uma Visualização de Dados é semelhante ao disito de Virtual Report Suites no Adobe Analytics, onde você estabelece as define ições de visita com reconchaimento de contexto, filtragem e também comos components são chamados .

Será rendário, pas de mínimo, uma Visualização de Dados por conexão. No entanto, para alguns casos de uso, é ótimo ter múltiplas Visualizações de Dados para a mesma conexão, com o objetivo de fornecer insights diferentes para epes distinct. Se você deseja que sua empresa seja orientada por dados, deve adaptar a forma como os dados são vistos em cada équipe. Alguns s&#39;exclame :

- Métricas de UX apenas para a equipe de UX Design
- Utilisez os mesmos nomes para KPI e métricas para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma .
- Visualização de Dados filtrada para mostrar, por exemplaire, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

Na tela de **Connections** marque a caixa de seleção da conexão que você acabou de criar. Clique-Les **Créer Une Vue De Données**.

![demo](./images/exta.png)

Le workflow Você será redireciponado para o fluxo de trabalho **Créer une vue de données** .

![demo](./images/0-v2.png)

## 4.3.2 Définition de la &quot;Visualização de Dados&quot;

Agora você pode configurar en tant que definitions ições básicas para sua Visualização de dados.

![demo](./images/0-v2.png)

Une **Connexion** que você criou no muscio anterior já está selecionada. Sua conexão se chama `yourLastName – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Em seguida, dê um nome à sua Visualização de Dados seguindo este modelo de nomenclatura : `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a description: `yourLastName – Omnichannel Data View`.

| Nom | Description |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demo](./images/1-v2.png)

Para **Time Zone**, selecione o fuso horário **Berlim, Estock-olmo, Roma, Berna, Bruxelas, Viena, Amsterdã GMT+01:00**. Este é um cenário realmente interessante, pois algumas empresas opéram em diferentes países e geografias. Alocar o fuso horário certo para cada país evitará erros típicos de dados, como, por exemplaire, acreditar que a maioria das pessoas compa camisetas às 4h no Peru.

![demo](./images/ext7.png)

Você também pode modificar a nomenclatura das métricas principais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas alguns clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessão e Eventos (convenção de nomenclatura padrão do Customer Journey Analytics).

Agora você deve ter as seguintes configurações definitions :

![demo](./images/1-v2.png)

Cliquez sur **Enregistrer et continuer**.

![demo](./images/12-v2.png)

## 4.3.3 Composentes da Visualização de Dados

Neste exerício, você irá configurar os components ários para analisar os dados e visualizá-los usando o Analysis Workspace. Nesta UI, há três áreas principais :

- Lado esquerdo : Component dispatentes dos datasets selecionados
- Meio : Component adicionados à Visualização de Dados
- Lado direito : Configurações do components

![demo](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrar uma métrica ou dimensão específica, verifique se o campo `Contains data` foi removido de sua visualização de dados. Caso contrário, exclua esse campo.
>
>![demo](./images/2-v2a.png)

Agora você precisa arrastar e soltar os components rendários para a análise nos **Composants ajoutés**. Para isso, você deve selecionar os components no menu à esquerda e arrastá-los e soltá-los na tela no meio

Vamos começar com ou primeiro componente : **Nom (web.webPageDetails.name)**. Pesquise componente e arraste-o e solte-o na tela.

![demo](./images/3-v2.png)

Esse componente é é o nome da página, como você pode dérivar da leitura do campo do schema `(web.webPageDetails.name)`.

No entanto, usar **Name** como nome não é a melhor convenção de nomenclatura para um usuário corporativo rapente essa dimensuão

Vamos mudar ou nome para **Nom de page**. Clique no component e pour renomeie na área **Paramètres des composants**.

![demo](./images/3-0-v2.png)

Comme Configurações de persistence ência são **Paramètres de persistance**. Os discitos de eVars e prop não existe no CJA, mas as configurações de Persistência possibilitam comportement semelhante.

![demo](./images/3-0-v21.png)

Se você não alterar essas configurações, o CJA irá interpréter une dimension como um **Prop** (nível de ocorrência). Além disso, podemos alterar a Persistência para tornar a dimensião uma **eVar** (persistir o valor ao longo da jornada).

Se você não estiver familiarizado com eVars e Props, [leia mais sobre isso na documentação](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Vamos deixar sur Nome da Página como Prop. Dessa forma, você não precisa alterar nenhuma **Paramètres de persistance**.

| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| Nom (web.webPageDetails.name) | Nom de la page |          |

Em seguida, escolha a dimension **phoneNumber** e solte-a na tela. O novo nome user **Numéro de téléphone**.

![demo](./images/3-1-v2.png)

Por fim, vamos alterar comme Configurações de persistence ência, pois o Número do Celular deve persistir no nível do usuário.

Para alterar a Persistência, role para baixo no menu à direita e abra a aba **Persistence** :

![demo](./images/5-v2.png)

Marque a caixa de seleção para modificar en tant que configurações de persistence ência. Sélectionnez **Le plus récent** e o escopo **Personne (fenêtre de reporting)**, pois nos preocupamos apenas com o último número de celular da pessoa. Voir cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido.

![demo](./images/6-v2.png)

| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numéro de téléphone | Le plus récent, Personne (fenêtre de reporting) |

O próximo component `web.webPageDetails.pageViews.value`.

Aucun menu à esquerda, pesquise `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela.

Remplacez le paramètre nome par **Pages vues** sous les **paramètres de composant**.

| Nom du composant à rechercher | Nouveau nom | Paramètres d’attribution |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Pages vues |         |

![demo](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Observação : As configurações de persistence ência nas métricas também podem ser alteradas no Analysis Workspace. Em alguns casos, você pode opar por configurá-las aqui para evitar que os usuários de negócios tenham que pensar qual é melhor modelo de persistence ência.

Em seguida, você terá que configurar várias Dimensões e Métricas, conforme indicado na tabela abaixo.

### DIMENSIES

| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| brandName | Nom de la marque | Session la plus récente |
| callentiment | Raisonnement des appels |          |
| ID d’appel | Type d’interaction d’appel |          |
| callTopic | Rubrique d’appel | Session la plus récente |
| ecid | ECID | Le plus récent, Personne (fenêtre de reporting) |
| adresse e-mail | Email ID | Le plus récent, Personne (fenêtre de reporting) |
| Type de paiement | Type de paiement |          |
| Méthode d’ajout du produit | Méthode d’ajout du produit | Session la plus récente |
| Type d’événement | Type d’événement |         |
| Nom (productListItems.name) | Nom du produit |         |
| SKU | SKU (session) | Session la plus récente |
| Identifiant de transaction | Identifiant de transaction |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agent utilisateur | Agent utilisateur | Session la plus récente |

### MÉTRICA

| Nom du composant à rechercher | Nouveau nom | Paramètres d’attribution |
| ----------------- |-------------| --------------------| 
| Quantité | Quantité |          |
| commerce.order.priceTotal | Recettes |         |

Sua configuração deve ser semelhante ao seguinte :

![demo](./images/11-v2.png)

Não se esqueça de Salvar sua Visualização de Dados. Então groupe em **Save**.

![demo](./images/12-v2s.png)

## 4.3.4 Calculadas de médicaments

Embora tenhamos organisado todos os components na Visualização de dados, você ainda deve adaptar alguns para que os usuários de negócios estejam prontos para iniciar suas análises

Se você se lembra, não trouxemos specificamente Métricas como Adicionar ao Carrinho, Visualização do producto ou Compras para a Visualização de dados. No entanto, temos uma dimension chamada: **Type d’événement**. Então, vamos dérivar esses tipos de interação criando 3 métricas caladas.

Vamos começar com a primeira Métrica : **Consultations produits**.

Aucun événement lado esquerdo, pesquise **Type d’événement** e selecione a dimension. Em seguida, arraste-o e solte-o na tela **Composants inclus**.

![demo](./images/calcmetr1.png)

Clique para selecionar a nova métrica **Event Type**.

![demo](./images/calcmetr2.png)

Agora altere nome a description do componente para os seguinte valores :

| Nom du composant | Description du composant |
| ----------------- |-------------| 
| Consultations produits | Consultations produits |

![demo](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **Product Views**. Para fazer isso, role para baixo em **Component Settings** até Valores de **Include Exclude Values**. Certifique-se de réhabilitation a opção **Définir les valeurs d&#39;inclusion/exclusion**.

![demo](./images/calcmetr4.png)

La requête como contar apenas **Consultations produits**, en particulier **commerce.productViews** nos critères.

![demo](./images/calcmetr5.png)

Agora a sua métrica calculada está pronta !

Em seguida, repita o mesmo processo para os eventos **Ajouter au panier** e **Achat**.

### Ajouter au panier

Primeiro, araste e solte une dimension mesma **Type d’événement**.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável . Clique em **Add Anyway** :

![demo](./images/calcmetr6.png)

Agora, siga o mesmo processo que fizemos para a métrica Visualizações de producto :
- Primeiro altere nome e a description.
- Pour le fim, adicione **commerce.productListAdds** critères communs para contar apenas Ajouter au panier

| Nom | Description | Critères |
| ----------------- |-------------| -------------|
| Ajouter au panier | Ajouter au panier | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Achats

Primeiro, arraste e solte a mesma dimensão **Event Type** como fizemos para as duas métricas anteriores.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos usando a mesma variável . Clique em **Add Anyway** :

![demo](./images/calcmetr7.png)

Agora, siga o mesmo processo que fizemos para as métricas Consultations produits e Ajoutez au panier :
- Primeiro altere nome e a description.
- Por fim, adicione **commerce.purchase** critères de como para contabilizar apenas as as as Compras

| Nom | Description | Critères |
| ----------------- |-------------| -------------|
| Achats | Achats | commerce.purchases |

![demo](./images/calcmetr7a.png)

Sua configuração final deve ser semelhante ao seguinte. Cliquez sur em **Enregistrer et continuer**.

![demo](./images/calcmetr8.png)

## 4.3.5 Component da Configuração de Dados

Você, auteur de la redirection de l&#39;utilisateur para esta tela :

![demo](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações importantes para alterar a forma como os dados são processados . Définition de Vamos começar sur **Session Timeout** (30 min). Graças ao enregistrement de data e hora de cada evento de experiência, você pode estender o concito de uma sessão em todos canais . Por exemplaire, o que acontece se um cliente ligar para o call center depois de visitar o site ? Usando Tempos Limite de Sessão personalizados, você tem muita flexibilidade para decidir o que é uma sessa ão e como sessa sessa irá mesclar os dados

![demo](./images/ext8.png)

Nesta aba você pode modificar ouas coisas como filtrar os dados usando um segmento/filtro . Você não precisará fazer isso neste exercice.

![demo](./images/10-v2.png)

Terminaison Quando, claquez-moi **Enregistrer et terminer**.

![demo](./images/13-v2.png)

>[!NOTE]
>
>Você pode voltar a esta Visualização de dados posteriormente e alterar as configurações e os componentes a qualquer momento. Comme alterações afetarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise !

Próxima etapa : [4.4 Preparação de dados em Customer Journey Analytics](./ex4.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
