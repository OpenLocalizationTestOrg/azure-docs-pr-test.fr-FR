---
title: "aaaAzure intégration du Kit de développement Web Mobile Engagement | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Kit de développement Web Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a>Intégration d’Azure Mobile Engagement dans une application web
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

les procédures de Hello dans cet article décrivent analytique de hello la plus simple façon tooactivate hello et de surveillance dans Azure Mobile Engagement dans votre application web.

Suivez hello étapes tooactivate hello journal des rapports qui sont nécessaire toocompute toutes les statistiques sur les utilisateurs, les sessions, les activités, blocages et technicals. Pour les statistiques dépend de l’application, telles que des événements, les erreurs et les tâches, vous devez activer manuellement les rapports du journal à l’aide de hello Azure Mobile Engagement API. Pour plus d’informations, Découvrez [comment toouse hello avancé Mobile Engagement marquage API dans une application web](mobile-engagement-web-use-engagement-api.md).

## <a name="introduction"></a>Introduction
[Télécharger hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).
Hello Web d’Engagement Mobile Kit de développement logiciel est fourni en tant qu’un seul fichier JavaScript, engagement.js azure, ce qui vous avez tooinclude dans chaque page de votre application ou un site web.

> [!IMPORTANT]
> Avant d’exécuter ce script, vous devez exécuter un script ou code extrait de code que vous écrivez tooconfigure Mobile Engagement pour votre application.
> 
> 

## <a name="browser-compatibility"></a>Compatibilité des navigateurs
Hello Kit de développement Web Mobile Engagement utilise JSON natif codage et décodage de plus les requêtes AJAX toocross-domaine (partie de confiance sur la spécification du W3C CORS hello). Il est compatible avec hello suivant navigateurs :

* Microsoft Edge 12+
* Internet Explorer 10+
* Firefox 3.5+
* Chrome 4+
* Safari 6+
* Opera 12+

## <a name="configure-mobile-engagement"></a>Configuration de Mobile Engagement
Écrire un script qui crée un global `azureEngagement` objet JavaScript, comme dans l’exemple suivant de hello. Étant donné que votre site peut comporter plusieurs pages, cet exemple suppose que ce script est inclus dans chaque page. Dans cet exemple, l’objet JavaScript de hello est nommé `azure-engagement-conf.js`.

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

Hello `connectionString` valeur de votre application s’affiche dans hello portail Azure.

> [!NOTE]
> Les valeurs `appVersionName` et `appVersionCode` sont facultatives. Toutefois, nous vous recommandons de les configurer pour que les analyses puissent traiter les informations de version.
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a>Inclure des scripts Mobile Engagement dans vos pages
Ajouter des pages de tooyour de scripts de Mobile Engagement dans un des hello suivant façons :

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

Ou cela :

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a>Alias
Une fois hello script du Kit de développement Web Mobile Engagement est chargé, il crée hello **engagement** alias tooaccess hello API du Kit de développement logiciel. Vous ne pouvez pas utiliser cette configuration de kit de développement logiciel alias toodefine hello. Cet alias est utilisé comme référence dans cette documentation.

Notez que si l’alias par défaut de hello est en conflit avec une autre variable globale à partir de votre page, vous pouvez redéfinir il dans la configuration de hello comme suit avant de les charger hello Kit de développement Web Mobile Engagement :

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a>Génération de rapports de base
La section Génération de rapports de base de Mobile Engagement présente les statistiques au niveau de la session, notamment les statistiques sur les utilisateurs, les sessions, les activités et les incidents.

### <a name="session-tracking"></a>Suivi de session
Une session Mobile Engagement est divisée en une séquence d’activités, chacune identifiée par un nom.

Dans un site web classique, nous vous recommandons de déclarer une autre activité sur chaque page de votre site. Pour une site Web ou une application web dans le hello page actuelle change jamais, vous pourriez tootrack des activités de hello sur une plus petite échelle, comme dans la page de hello.

Soit, toostart ou modification hello activité utilisateur en cours, appel hello `engagement.agent.startActivity` (fonction). Par exemple :

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

serveur de Mobile Engagement Hello termine automatiquement une session ouverte dans les trois minutes après la fermeture de la page de l’application hello.

Ou vous pouvez terminer une session manuellement en appelant `engagement.agent.endActivity`. Cela définit too'Idle activité utilisateur en cours de hello. »  Hello prendra fin 10 secondes plus tard, sauf si un nouvel appel`engagement.agent.startActivity` reprend la session de hello.

Vous pouvez configurer délai de 10 secondes hello dans l’objet d’engagement global hello, comme suit :

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> Vous ne pouvez pas utiliser `engagement.agent.endActivity` Bonjour `onunload` rappel étant donné que vous ne pouvez pas les appels AJAX à ce stade.
> 
> 

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, si vous souhaitez que les travaux, les erreurs et les événements d’application tooreport, vous devez toouse hello API d’Engagement Mobile. Vous accédez hello API d’Engagement Mobile via hello `engagement.agent` objet.

Vous pouvez accéder à tous les hello avancées dans Mobile Engagement Bonjour API d’Engagement Mobile. Hello API est détaillée dans l’article de hello [comment toouse hello avancé Mobile Engagement marquage API dans une application web](mobile-engagement-web-use-engagement-api.md).

## <a name="customize-hello-urls-used-for-ajax-calls"></a>Personnaliser des URL hello utilisés pour les appels AJAX
Vous pouvez personnaliser les URL que hello qu'utilise du Kit de développement Web Mobile Engagement. Par exemple, les URL de connexion de hello tooredefine (hello SDK point de terminaison pour la journalisation), vous pouvez remplacer la configuration de hello comme suit :

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

Si votre URL renvoient une chaîne qui commence par `/`, `//`, `http://`, ou `https://`, schéma par défaut de hello n’est pas utilisé. Par défaut, hello `https://` schéma est utilisé pour les URL. Si vous souhaitez que le schéma par défaut de hello toocustomize, remplacer la configuration de hello, comme suit :

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
