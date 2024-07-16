---
title: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à Adobe Target - Brésil
description: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à Adobe Target - Brésil
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Segments, Integrations
exl-id: 862afd4c-1b6c-48fe-bc1f-967c065642e0
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# 1.4 Ação : J&#39;ai envie seu segmento para o Adobe Target

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte supérieur da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingestion des données](./images/sb1.png)

## 1.4.1 Événement actif segmento para o destination do Adobe Target

O Adobe Target está disponível como um deso do CDP em tempo real. Para configurar sua integração com o Adobe Target, accédez à **Destinations** et **Catalogue**.

Cliquez sur **Personalization** dans le menu **Catégories**. Você verá o cartão de destination do **Adobe Target**. Clique-Les **Activer Les Segments**.

![AT](./images/atdest1.png)

Sélectionnez une destination ``Bootcamp Target`` e clique **Suivant**.

![AT](./images/atdest3.png)

Na lista de segmentos disponíveis, selecione o segmento que você criou em [1.3 Crie um segmento](./ex3.md), com o nome `yourLastName - Interest in Real-Time CDP`. Em seguida, groupe-moi **Suivant**.

![AT](./images/atdest8.png)

Na próxima página, groupe em **Next**.

![AT](./images/atdest9.png)

Cliquez Sur L’Écran **Finish**.

![AT](./images/atdest10.png)

Seu segmento agora está ativado para o Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Imediatamente após criar seu destination do Adobe Target on Real-Time CDP, pode levar uma hora para que o deso seja ativado. Este é um tempo de espera único devido à definition ição da configuração de back-end. Depois que o tempo de espera intual de 1 hora e a configuração do back-end forem conclu ídos, os segmentos de borda recém-adicionados que são enviados ao destinée o Adobe Target estarão disponíveis para segmentação em tempo real.

## 1.4.2 Configuration d’une diffusion sua sur Adobe Target

Agora que seu segmento Real-Time CDP está configurado para ser enviado ao Adobe Target, é possível configurar sua atividade de Segmentação por experiência no Adobe Target. Neste exerício, você irá configurar uma atividade baseada no Visual Experience Composer.

Accédez à un accès non officiel à Adobe Experience Cloud de página [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Clique em **Target** para abrir.

![RTCDP](./images/excl.png)

Na página officials do **Adobe Target**, você verá todas as as as atividades existent.
Clique em **+ Créer l’activité** para criar uma nova atividade.

![RTCDP](./images/exclatov.png)

Sélectionnez **Ciblage d’expérience**.

![RTCDP](./images/exclatcrxt.png)

Sélectionnez **Visuel** et définissez une **URL d’activité** como `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mas, antes disso, substitua XX por um número entre 01 et 60.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e contracte un accès à l&#39;URL : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as as as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Pour exemplaire, ou participant 1 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, ou participant 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Sélectionnez un espace de travail **AT Bootcamp**.

Cliquez Sur **Suivant**.

![RTCDP](./images/exclatcrxtdtlform.png)

Agora você está aucun compositeur d&#39;expérience visuelle. Pode levar de 20 a 30 segundos que o site esteja completamente carregado .

![RTCDP](./images/atform1.png)

Atualmente, o público padrão são **Tous les visiteurs**. Clique nos **3 points** ao lado de **Tous les visiteurs** e clique em **Changer d’audience**.

![RTCDP](./images/atform3.png)

Agora você está vendo a lista de públicos disponíveis, e o segmento da Adobe Experience Platform que você criou anteriormente e enviou ao Adobe Target agora faz parte dessa lista. Sélection de la segmento que você criou anteriormente na Adobe Experience Platform. Cliquez Sur **Attribuer Une Audience**.

![RTCDP](./images/exclatvecchaud.png)

Seu segmento da Adobe Experience Platform agora faz parte dessa Atividade de segmentação por experiência.

![RTCDP](./images/atform4.png)

Antes de alterar a imagem principal, você deve clicar em **Allow All** no banner de cookies.

Para isso, vá para **Browse**

![RTCDP](./images/cook1.png)

Em seguida, groupe-moi **Autoriser tout**.

![RTCDP](./images/cook2.png)

Em seguida, restauré para **Composer**.

![RTCDP](./images/cook3.png)

Agora vamos mudar a imagem principal na página incial do site. Clique un padrão principal de l&#39;image sur le site, clic em **Remplacer le contenu** e select **Image**.

![RTCDP](./images/atform5.png)

Pesquise o arquivo de imagem **rtcdp.png**. Sélectionnez l&#39;activité de groupe **Enregistrer**.

![RTCDP](./images/atform6.png)

Você verá a nova experiência com a nova imagem para o seu Público selecionado

![RTCDP](./images/atform7.png)

Clique no título da sua atividade no canto supérieur esquerdo para renomeá-la.

![RTCDP](./images/exclatvecname.png)

Para o nome, utilisez :

- `seuSobrenome - RTCDP - XT (VEC)`

Cliquez Sur **Suivant**.

![RTCDP](./images/atform8.png)

Cliquez Sur **Suivant**.

![RTCDP](./images/atform8a.png)

Na página **Objectifs et paramètres**, accédez à **Mesures d’objectif**.

![RTCDP](./images/atform9.png)

Définissez une métamodèle principale **Engagement** - **Temps passé sur le site**. Clique-Les **Enregistrer Et Fermer**.

![RTCDP](./images/vec3.png)

Agora você está na página **Aperçu de l&#39;activité**. Você ainda precisa ativar sua Atividade.

![RTCDP](./images/atform10.png)

Cliquez sur no campo **Inactive** et sélectionnez **Activer**.

![RTCDP](./images/atform11.png)

Você recberá uma confirmação visuel de que sua atividade agora está ativa.

![RTCDP](./images/atform12.png)

Agora sua atividade está ativa e pode ser testada no site do bootcamp.

Voir agora você voltar ao seu site de démonstração e visitar a página do producto para **Real-Time CDP**, você se qualificará instantané amente para o segmento que criou e verá a atividade do Adobe Target exibida na página inlegal em tempo real.

>[!IMPORTANT]
>
>Cada participante da capacitação deve usar uma página da Web separada para evitar a colisão de várias experiências do Adobe Target. É possível escolher uma página da Web e contracte un lien d&#39;accès à l&#39;URL : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Todas as as as páginas compartilham a mesma URL base e terminam com o número do participante.
>
>Por exemplaire, o participante 1 deve usar a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, ou participante 30 deve usar a URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Próxima etapa : [1.5 Ação : J&#39;ai envie segmento para o Facebook](./ex5.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
