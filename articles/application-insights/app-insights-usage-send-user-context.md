---
title: "utilisation de tooenable aaaSending utilisateur contexte expériences dans Azure Application Insights | Documents Microsoft"
description: "Suivez les déplacements des utilisateurs dans votre service après avoir assigné à chacun d’eux une chaîne d’ID unique et permanente dans Application Insights."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Utilisation de tooenable de contexte utilisateur envoi expériences dans Azure Application Insights

## <a name="tracking-users"></a>Suivi des utilisateurs

Application Insights permet de vous toomonitor et effectuer le suivi de vos utilisateurs via un ensemble d’outils de l’utilisation de produit : 
* [Utilisateurs, sessions, événements](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Entonnoirs](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Rétention](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Cohortes
* [Classeurs](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

Dans tootrack commande quelles un utilisateur effectue au fil du temps, Application Insights nécessite un ID pour chaque utilisateur ou de la session. Incluez ces ID dans chaque vue personnalisée de page ou d’événement personnalisé.
- Utilisateurs, Entonnoirs, Rétention et Cohortes : incluez l’ID d’utilisateur.
- Sessions : incluez l’ID de session.

Si votre application est intégrée à hello [SDK JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), utilisateur, ID de suivi est effectué automatiquement.

## <a name="choosing-user-ids"></a>Choix d’ID d’utilisateur

ID d’utilisateur doivent être persistantes sur tootrack de sessions utilisateur comment les utilisateurs se comporteront au fil du temps. Il existe différentes approches pour la persistance hello ID.
- Définition d’un utilisateur dont vous disposez déjà dans votre service.
- Si le service de hello a accès tooa navigateur, il peut passer navigateur de hello un cookie avec un ID qu’il contient. ID de Hello est conservées pour tant que cookie de hello demeure dans le navigateur de l’utilisateur hello.
- Si nécessaire, vous pouvez utiliser un nouvel ID de chaque session, mais les résultats hello sur les utilisateurs seront limitées. Par exemple, vous ne serez en mesure de toosee comment le comportement de l’utilisateur change au fil du temps.

Hello ID doit être un Guid ou une autre chaîne de chaque utilisateur assez complexe tooidentify identifie de façon unique. Par exemple, il peut s’agir d’un nombre aléatoire long.

Si l’ID de hello contienne des informations personnelles sur l’utilisateur de hello, il n’est pas une tooApplication de toosend Insights valeur appropriée en tant qu’un ID utilisateur. Vous pouvez envoyer un ID un [ID de l’utilisateur authentifié](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), mais il ne remplit pas la nécessité d’ID d’utilisateur hello pour les scénarios d’utilisation.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>Applications ASP.NET : définissez le contexte utilisateur dans ITelemetryInitializer

Créez un initialiseur de télémétrie, comme décrit en détail [ici](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)et ensemble hello Context.User.Id et hello Context.Session.Id.

Cet exemple définit l’identificateur hello utilisateur ID tooan qui expire après une session de hello. Si possible, utilisez un ID d’utilisateur qui se conserve d’une session à l’autre.

*C#*

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a>Étapes suivantes
- l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.
    * [Vue d’ensemble de l’utilisation](app-insights-usage-overview.md)
    * [Utilisateurs, Sessions et Événements](app-insights-usage-segmentation.md)
    * [Entonnoirs](usage-funnels.md)
    * [Rétention](app-insights-usage-retention.md)
    * [Classeurs](app-insights-usage-workbooks.md)
