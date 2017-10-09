---
title: aaaAdvanced Configuration pour Windows applications Engagement SDK Universal
description: "Options de configuration avancées pour Engagement avec des applications Windows Universal"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="e38e4-103">Configuration avancée du Kit de développement logiciel (SDK) des applications Windows Universal pour Engagement</span><span class="sxs-lookup"><span data-stu-id="e38e4-103">Advanced Configuration for Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e38e4-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="e38e4-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-configuration.md)
> * [<span data-ttu-id="e38e4-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="e38e4-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="e38e4-106">iOS</span><span class="sxs-lookup"><span data-stu-id="e38e4-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="e38e4-107">Android</span><span class="sxs-lookup"><span data-stu-id="e38e4-107">Android</span></span>](mobile-engagement-android-advanced-configuration.md)
> 
> 

<span data-ttu-id="e38e4-108">Cette procédure décrit comment tooconfigure différentes options de configuration pour les applications Azure Mobile Engagement Android.</span><span class="sxs-lookup"><span data-stu-id="e38e4-108">This procedure describes how tooconfigure various configuration options for Azure Mobile Engagement Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e38e4-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e38e4-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a><span data-ttu-id="e38e4-110">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="e38e4-110">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="e38e4-111">Désactiver le signalement automatique des incidents</span><span class="sxs-lookup"><span data-stu-id="e38e4-111">Disable automatic crash reporting</span></span>
<span data-ttu-id="e38e4-112">Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="e38e4-112">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="e38e4-113">Puis, lorsqu’une exception non gérée se produit, Engagement ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="e38e4-113">Then, when an unhandled exception occurs, Engagement does nothing.</span></span>

> [!WARNING]
> <span data-ttu-id="e38e4-114">Si vous désactivez cette fonctionnalité, puis lorsqu’un incident non gérée se produit dans votre application, Engagement n’envoie pas de blocage de hello **et** ne ferme pas la session de hello et les travaux.</span><span class="sxs-lookup"><span data-stu-id="e38e4-114">If you disable this feature, then when an unhandled crash occurs in your app, Engagement does not send hello crash **AND** does not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="e38e4-115">toodisable automatique sur incident reporting, personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :</span><span class="sxs-lookup"><span data-stu-id="e38e4-115">toodisable automatic crash reporting, customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="e38e4-116">Dans le fichier `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="e38e4-116">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="e38e4-117">Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.</span><span class="sxs-lookup"><span data-stu-id="e38e4-117">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="e38e4-118">Dans l'objet `EngagementConfiguration` au moment l'exécution</span><span class="sxs-lookup"><span data-stu-id="e38e4-118">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="e38e4-119">Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="e38e4-119">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a><span data-ttu-id="e38e4-120">Désactiver les rapports en temps réel</span><span class="sxs-lookup"><span data-stu-id="e38e4-120">Disable real time reporting</span></span>
<span data-ttu-id="e38e4-121">Par défaut, les rapports de service d’Engagement hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="e38e4-121">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="e38e4-122">Si votre application rapports journaux fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers.</span><span class="sxs-lookup"><span data-stu-id="e38e4-122">If your application reports logs frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time basis.</span></span> <span data-ttu-id="e38e4-123">On parle dans ce cas de « mode rafale ».</span><span class="sxs-lookup"><span data-stu-id="e38e4-123">This is called “burst mode”.</span></span>

<span data-ttu-id="e38e4-124">toodo appeler par conséquent, la méthode hello :</span><span class="sxs-lookup"><span data-stu-id="e38e4-124">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="e38e4-125">l’argument Hello est une valeur dans **millisecondes**.</span><span class="sxs-lookup"><span data-stu-id="e38e4-125">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="e38e4-126">Chaque fois que vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez la méthode hello sans paramètres ou avec la valeur de hello 0.</span><span class="sxs-lookup"><span data-stu-id="e38e4-126">Whenever you want tooreactivate hello real-time logging, call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="e38e4-127">Mode rafale augmente l’autonomie des batteries hello légèrement mais a un impact sur hello Engagement moniteur : durée des sessions et les travaux toute sont arrondis toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible).</span><span class="sxs-lookup"><span data-stu-id="e38e4-127">Burst mode slightly increases hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration are rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="e38e4-128">Nous vous recommandons d'utiliser un seuil de rafale inférieur à 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="e38e4-128">We recommend using a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="e38e4-129">Journaux enregistrés sont des éléments too300 limité.</span><span class="sxs-lookup"><span data-stu-id="e38e4-129">Saved logs are limited too300 items.</span></span> <span data-ttu-id="e38e4-130">Si l'envoi est trop long, vous risquez de perdre certains journaux.</span><span class="sxs-lookup"><span data-stu-id="e38e4-130">If sending is too long, you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="e38e4-131">seuil de croissance Hello ne peut pas être configuré tooa période de moins d’une seconde.</span><span class="sxs-lookup"><span data-stu-id="e38e4-131">hello burst threshold cannot be configured tooa period less than one second.</span></span> <span data-ttu-id="e38e4-132">Si vous le faites, hello SDK montre une trace avec l’erreur de hello et réinitialise automatiquement toohello par défaut, zéro seconde.</span><span class="sxs-lookup"><span data-stu-id="e38e4-132">If you do so, hello SDK shows a trace with hello error and automatically resets toohello default value, zero seconds.</span></span> <span data-ttu-id="e38e4-133">Cette hello tooreport de déclencheurs hello SDK se connecte en temps réel.</span><span class="sxs-lookup"><span data-stu-id="e38e4-133">This triggers hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
