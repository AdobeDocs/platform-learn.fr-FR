---
title: Bootcamp - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - UI - Brésil
description: Bootcamp - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - UI - Brésil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# 1.2 Visualiser seu próprio perfil de cliente em tempo real - interface utilisateur

Neste exercio, você irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI

## História

No Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do evento, além das associações de segmentos existe. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções externes. Essa é a exibição mais poderosa da Adobe Experience Platform, o verdadeiro local do sistema de experiência.

## 1.2.1 Utilisation d’une visualisation du fichier client dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página official da Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Antes de continuar, você precisa selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte supérieur da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Ingestion des données](./images/sb1.png)

Aucun menu à esquerda, accédez à **Profils** et **Parcourir**.

![Profil client](./images/homemenu.png)

Pas de peinture Visualizador de perfil pas de site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace .

![Profil client](./images/identities.png)

Aucun peintre Visualizador de perfil, agora você pode over uma identidade semelhante a seguinte :

| Espace de noms | Identité |
|:-------------:| :---------------:|
| Identifiant Experience Cloud (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform, tous les identifiants são igualmente importantes. Anteriormente, o ECID ère o ID mais important pas contexto da Adobe e todos os outros IDs estavam vinculados ao ECID em uma relação hierárquica . Com a Adobe Experience Platform, isso mudou e cada pode ser penado um identificador primário.

Normalmente, o identificador primário depende do contexto. Se você perguntar ao seu Call Center : **Qual é o ID mais important ?** Eles prouavelmente responderão : **o número de telefone !** Mas se você perguntar à sua equipe de CRM, eles responderão : **o endereço de e-mail !** Un Adobe Experience Platform entende essa teinde e gerencia est so para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se comunicará com a Adobe Experience Platform referindo-se ao ID que attenam principal. C&#39;est une foncione simple.

Para o campo **Identity namespace**, select **ECID** e para o campo **Identity Value** insira o ECID que você pode ne contrarient pas le tableau Visualizador de perfil do site do Bootcamp. Cliquez Sur L’Écran **View**. Você verá seu perfil na lista. Cliquez sur **ID de profil** pour abrir seu perfil.

![Profil client](./images/popupecid.png)

Agora você tem uma visão geral de alguns **** importantes do seu perfil de cliente.

![Profil client](./images/profile.png)

Acesse **Events**, onde você se propage sous la forme d&#39;entradas de cada evento de experiência vinculado ao seu Perfil.

![Profil client](./images/profileee.png)

Pour faire vos besoins, accédez à une option de menu **Appartenance au segment**. Agora você verá todos os segmentos que qualificam para este perfil

![Profil client](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que você personnalise une experiência do cliente para um cliente anônimo ou conquête.

Próxima etapa : [1.3 Crie um segmento - UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
