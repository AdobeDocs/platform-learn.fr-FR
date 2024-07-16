---
title: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360 - Brésil
description: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360 - Brésil
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação : J&#39;ai envie de segmento para o Facebook

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte supérieur da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingestion des données](./images/sb1.png)

Aucun menu à esquerda, vá para **Destinations** e, em seguida, vá para **Catalog**. Você verá o **Catalogue de destinations**. Em **Destinations**, groupe em **Activer les segments** sur **Audience personnalisée Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Sélectionnez **bootcamp-facebook** et suivez-moi **Suivant**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou no exerício anterior. Cliquez Sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mapping**, verifique se a caixa de seleção **Apply Transformation** está marcada. Cliquez Sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Planning de segment**, sélectionnez une **Origine de votre audience** e define como **Directly from clients**. Cliquez Sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, un página **Review**, groupe em **Finish**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se qualificar para segmento, um sinal será enviado do servdor (côté serveur) do Facebook para incluir client no Público Personalizado no lado do Facebook.

No Facebook, você encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados :

![RTCDP](./images/rtcdpcreatedest5b.png)

L&#39;apartheid Agora você pode ver seu público personalizado sur Facebook :

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
