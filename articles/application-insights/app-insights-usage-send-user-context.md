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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="76a73-103">Utilisation de tooenable de contexte utilisateur envoi expériences dans Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="76a73-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="76a73-104">Suivi des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="76a73-104">Tracking users</span></span>

<span data-ttu-id="76a73-105">Application Insights permet de vous toomonitor et effectuer le suivi de vos utilisateurs via un ensemble d’outils de l’utilisation de produit :</span><span class="sxs-lookup"><span data-stu-id="76a73-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="76a73-106">Utilisateurs, sessions, événements</span><span class="sxs-lookup"><span data-stu-id="76a73-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="76a73-107">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="76a73-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="76a73-108">Rétention</span><span class="sxs-lookup"><span data-stu-id="76a73-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="76a73-109">Cohortes</span><span class="sxs-lookup"><span data-stu-id="76a73-109">Cohorts</span></span>
* [<span data-ttu-id="76a73-110">Classeurs</span><span class="sxs-lookup"><span data-stu-id="76a73-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="76a73-111">Dans tootrack commande quelles un utilisateur effectue au fil du temps, Application Insights nécessite un ID pour chaque utilisateur ou de la session.</span><span class="sxs-lookup"><span data-stu-id="76a73-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="76a73-112">Incluez ces ID dans chaque vue personnalisée de page ou d’événement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="76a73-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="76a73-113">Utilisateurs, Entonnoirs, Rétention et Cohortes : incluez l’ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="76a73-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="76a73-114">Sessions : incluez l’ID de session.</span><span class="sxs-lookup"><span data-stu-id="76a73-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="76a73-115">Si votre application est intégrée à hello [SDK JavaScript](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), utilisateur, ID de suivi est effectué automatiquement.</span><span class="sxs-lookup"><span data-stu-id="76a73-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="76a73-116">Choix d’ID d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="76a73-116">Choosing user IDs</span></span>

<span data-ttu-id="76a73-117">ID d’utilisateur doivent être persistantes sur tootrack de sessions utilisateur comment les utilisateurs se comporteront au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="76a73-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="76a73-118">Il existe différentes approches pour la persistance hello ID.</span><span class="sxs-lookup"><span data-stu-id="76a73-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="76a73-119">Définition d’un utilisateur dont vous disposez déjà dans votre service.</span><span class="sxs-lookup"><span data-stu-id="76a73-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="76a73-120">Si le service de hello a accès tooa navigateur, il peut passer navigateur de hello un cookie avec un ID qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="76a73-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="76a73-121">ID de Hello est conservées pour tant que cookie de hello demeure dans le navigateur de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="76a73-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="76a73-122">Si nécessaire, vous pouvez utiliser un nouvel ID de chaque session, mais les résultats hello sur les utilisateurs seront limitées.</span><span class="sxs-lookup"><span data-stu-id="76a73-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="76a73-123">Par exemple, vous ne serez en mesure de toosee comment le comportement de l’utilisateur change au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="76a73-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="76a73-124">Hello ID doit être un Guid ou une autre chaîne de chaque utilisateur assez complexe tooidentify identifie de façon unique.</span><span class="sxs-lookup"><span data-stu-id="76a73-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="76a73-125">Par exemple, il peut s’agir d’un nombre aléatoire long.</span><span class="sxs-lookup"><span data-stu-id="76a73-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="76a73-126">Si l’ID de hello contienne des informations personnelles sur l’utilisateur de hello, il n’est pas une tooApplication de toosend Insights valeur appropriée en tant qu’un ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="76a73-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="76a73-127">Vous pouvez envoyer un ID un [ID de l’utilisateur authentifié](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), mais il ne remplit pas la nécessité d’ID d’utilisateur hello pour les scénarios d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="76a73-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="76a73-128">Applications ASP.NET : définissez le contexte utilisateur dans ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="76a73-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="76a73-129">Créez un initialiseur de télémétrie, comme décrit en détail [ici](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer)et ensemble hello Context.User.Id et hello Context.Session.Id.</span><span class="sxs-lookup"><span data-stu-id="76a73-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="76a73-130">Cet exemple définit l’identificateur hello utilisateur ID tooan qui expire après une session de hello.</span><span class="sxs-lookup"><span data-stu-id="76a73-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="76a73-131">Si possible, utilisez un ID d’utilisateur qui se conserve d’une session à l’autre.</span><span class="sxs-lookup"><span data-stu-id="76a73-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="76a73-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="76a73-132">*C#*</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="76a73-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76a73-133">Next steps</span></span>
- <span data-ttu-id="76a73-134">l’utilisation de tooenable rencontre, démarrer l’envoi de [événements personnalisés](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [des consultations de page](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="76a73-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="76a73-135">Si vous envoyez déjà hello l’utilisation des outils toolearn Explorer les événements personnalisés ou des vues de la page, comment les utilisateurs utiliser votre service.</span><span class="sxs-lookup"><span data-stu-id="76a73-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="76a73-136">Vue d’ensemble de l’utilisation</span><span class="sxs-lookup"><span data-stu-id="76a73-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="76a73-137">Utilisateurs, Sessions et Événements</span><span class="sxs-lookup"><span data-stu-id="76a73-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="76a73-138">Entonnoirs</span><span class="sxs-lookup"><span data-stu-id="76a73-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="76a73-139">Rétention</span><span class="sxs-lookup"><span data-stu-id="76a73-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="76a73-140">Classeurs</span><span class="sxs-lookup"><span data-stu-id="76a73-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
