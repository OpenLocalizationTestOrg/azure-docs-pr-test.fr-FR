---
title: "procédures de mise à niveau de kit de développement Web Mobile Engagement aaaAzure | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Web SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a>Procédures de mise à niveau du SDK web Azure Mobile Engagement
Si vous avez déjà intégré une version antérieure de hello Kit de développement Web Azure Mobile Engagement dans votre application web, vous devez hello tooconsider points suivants lorsque vous mettez à niveau hello SDK.

Si vous avez ignoré plusieurs versions du Kit de développement Web Mobile Engagement de hello, vous devrez peut-être toocomplete plusieurs procédures au cours du processus de mise à niveau hello. Par exemple, si vous migrez à partir de 1.4.0 too1.6.0, première tooupgrade procédures hello de suivi à partir de 1.4.0 too1.5.0. Ensuite, suivez hello procédures tooupgrade de 1.5.0 too1.6.0.

Quelle que soit la version mise à niveau à partir, remplacez toute version antérieure du fichier de hello azure-engagement.js avec la version la plus récente du fichier de hello hello.

## <a name="upgrade-from-121-too200"></a>Mise à niveau à partir de 1.2.1 too2.0.0
Cette section décrit comment toomigrate une intégration du Kit de développement Web Mobile Engagement à partir du service de Capptain hello, prestation Capptain SAS, tooan Azure Mobile Engagement application. Si vous effectuez une migration à partir d’une version antérieure, veuillez consulter hello toofirst du site Web Capptain migrer too1.2.1 et puis hello procédures suivantes.

Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge les TV actives Samsung, Opera TV, webOS ou fonctionnalité de couverture hello.

> [!IMPORTANT]
> Capptain et Azure Mobile Engagement ne sont pas hello même service. Hello, suivant la procédure met en surbrillance uniquement comment toomigrate hello application cliente. Migration hello Kit de développement Web Mobile Engagement dans l’application hello ne migre pas vos données à partir d’un serveur Capptain server tooa Mobile Engagement.
> 
> 

### <a name="javascript-files"></a>Fichiers JavaScript
Remplacez hello fichier capptain-sdk.js par hello fichier azure-engagement.js, puis mettez à jour votre script importe en conséquence.

### <a name="remove-capptain-reach"></a>Supprimer Capptain Reach
Cette version du Kit de développement Web Mobile Engagement de hello ne prend pas en charge la fonctionnalité de couverture hello. Si vous intégré Capptain portée dans votre application, vous devez tooremove il.

Suppression hello atteindre le CSS importation à partir de votre page et fichier .css connexes de hello (capptain-reach.css, par défaut).

Supprimer hello suivant des ressources de portée : hello fermer image (capptain-close.png, par défaut) et l’icône de marque hello (capptain-notification-icône, par défaut).

Supprimez hello atteindre de l’interface utilisateur pour les notifications dans l’application. disposition par défaut de Hello ressemble à ceci :

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

Supprimez hello atteindre de l’interface utilisateur pour les annonces de web et de texte et les sondages. disposition par défaut de Hello ressemble à ceci :

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

Supprimer hello `reach` de l’objet à partir de votre configuration, si elle existe. Voici à quoi cela ressemble :

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

Supprimez toute autre personnalisation Reach, notamment les catégories.

### <a name="remove-deprecated-apis"></a>Supprimer les API déconseillées
Certaines API de Capptain est déconseillées dans hello Kit de développement Web Mobile Engagement.

Supprimer tout toohello appels suivant API : `agent.connect`, `agent.disconnect`, `agent.pause`, et `agent.sendMessageToDevice`.

Supprimez toutes les instances de hello suivant des rappels à partir de votre configuration Capptain : `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, et `onPushMessageReceived`.

### <a name="configuration"></a>Configuration
Mobile Engagement utilise une connexion chaîne tooconfigure Kit de développement logiciel des identificateurs, par exemple, identificateur d’application hello.

Remplacez l’ID de l’application hello avec votre chaîne de connexion. Notez qu’objet global hello de hello configuration du Kit de développement logiciel passe de `capptain` trop`azureEngagement`.

Avant la migration :

    window.capptain = {
      appId: ...,
      [...]
    };

Après la migration :

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

chaîne de connexion Hello pour votre application s’affiche dans hello portail Azure.

### <a name="javascript-apis"></a>API JavaScript
objet JavaScript global de Hello `window.capptain` a été renommé `window.azureEngagement` mais vous pouvez utiliser hello `window.engagement` alias pour les appels d’API. Vous ne pouvez pas utiliser configuration de kit de développement logiciel hello alias toodefine hello.

Par exemple : `capptain.deviceId` devient `engagement.deviceId`, `capptain.agent.startActivity` devient `engagement.agent.startActivity`, etc.

