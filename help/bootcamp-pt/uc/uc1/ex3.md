---
title: Bootcamp - Real-time Customer Profile - Création d’un segment - IU - Brésil
description: Bootcamp - Real-time Customer Profile - Création d’un segment - IU - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 2%

---

# 1.3 Segmentation de base - IU

Neste exercio, você irá criar um segmento usando Contrutor de Segmentos da Adobe Experience Platform.

## História

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É possível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte supérieur da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingestion des données](./images/sb1.png)

Aucun menu à esquerda, accédez à **Segments**. Nesta página, você tem uma visão geral de todos os segmentos existe. Clique no botão + Criar segmento para começar a criar um novo segmento .

![Segmentation](./images/menuseg.png)

Quando estiver no novo contrutor de segmentos, você irá percepber imediatamente a opção de menu **Attributes** e a referência do **XDM Individual Profile**.

![Segmentation](./images/segmentationui.png)

Como XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o construction de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, dependentemente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a partir dessa interface do usuário do construction de segmento, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação .

Agora você précisa criar um segmento de todos os clientes que visualizaram o producto **Real-Time CDP**.

Para strucir este segmento, você precisa adicionar um Evento de experiência. Você pode encontrar todos os Eventos de experiência clicando no ícone **Events** na barra de menu **Fields**.

![Segmentation](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** do nível supérieur. Clique em **XDM ExperienceEvent**.

![Segmentation](./images/see.png)

Accédez aux **éléments de liste de produits**.

![Segmentation](./images/plitems.png)

Sélectionnez **Nom** e arraste e solte o objeto **Nom** do menu à esquerda na tela do construction de segmentos na seção **Événements**. Em seguida, o seguinte será exibido :

![Segmentation](./images/eewebpdtlname.png)

O parâmetro de comparativement&#39;ação deve ser **est égal à** e, pas de campo de entrada, insira **CDP en temps réel**.

![Segmentation](./images/pv.png)

Sempre que adicionar um elemento ao construction de segmentos, você pode clicar no botão **Actualiser l’estimation** para obter uma nova estimativa da população em seu segmento.

![Segmentation](./images/refreshest.png)

Para **Méthode d’évaluation**, sélectionnez **Edge**.

![Segmentation](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Le modèle como de nomenclatura utilise :

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clic no botão **Save and Close** para salvar seu segmento.

![Segmentation](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualização de amostra dos perfectionnis de clientes que qualificam para o seu segmento.

![Segmentation](./images/savedsegment.png)

Agora você pode continuar no próximo exercice cio e usar seu segmento com o Adobe Target

Próxima etapa : [1.4 Ação : J&#39;ai envie segmento para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
