---
title: aaaCreate une ressource Azure Application Insights | Documents Microsoft
description: "Configurez manuellement la surveillance d’Application Insights pour une nouvelle application en direct."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="90f5d-103">Création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="90f5d-103">Create an Application Insights resource</span></span>
<span data-ttu-id="90f5d-104">Azure Application Insights affiche les données relatives à votre application dans une *ressource* Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90f5d-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="90f5d-105">Création d’une ressource est par conséquent partie de [configurer Application Insights toomonitor une nouvelle application][start].</span><span class="sxs-lookup"><span data-stu-id="90f5d-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="90f5d-106">Dans de nombreux cas, la création d’une ressource peut faire automatiquement hello IDE.</span><span class="sxs-lookup"><span data-stu-id="90f5d-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="90f5d-107">Mais dans certains cas, vous créez manuellement une ressource, par exemple, les builds toohave des ressources distinctes pour le développement et de production de votre application.</span><span class="sxs-lookup"><span data-stu-id="90f5d-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="90f5d-108">Une fois que vous avez créé la ressource de hello, vous obtenez sa clé d’instrumentation et utilisez ce Kit de développement logiciel de hello tooconfigure dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="90f5d-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="90f5d-109">liens vers les ressources clés Hello hello ressource toohello de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="90f5d-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="90f5d-110">S’inscrire tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="90f5d-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="90f5d-111">Si vous n’avez pas de [compte Microsoft, procurez-vous en un dès maintenant](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="90f5d-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="90f5d-112">(Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="90f5d-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="90f5d-113">Vous devez également un abonnement trop[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="90f5d-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="90f5d-114">Si votre équipe ou organisation dispose d’un abonnement Azure, hello propriétaire peut ajouter vous tooit, à l’aide de votre identifiant Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="90f5d-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="90f5d-115">Vous êtes facturé uniquement pour ce que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="90f5d-115">You're only charged for what you use.</span></span> <span data-ttu-id="90f5d-116">plan de base par défaut Hello autorise une certaine quantité d’utilisation expérimentale gratuitement.</span><span class="sxs-lookup"><span data-stu-id="90f5d-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="90f5d-117">Lorsque vous avez accès tooa abonnement, connectez-vous à Insights tooApplication à [http://portal.azure.com](https://portal.azure.com)et utiliser votre toologin Live ID.</span><span class="sxs-lookup"><span data-stu-id="90f5d-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="90f5d-118">Création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="90f5d-118">Create an Application Insights resource</span></span>
<span data-ttu-id="90f5d-119">Bonjour [portal.azure.com](https://portal.azure.com), ajouter une ressource Application Insights :</span><span class="sxs-lookup"><span data-stu-id="90f5d-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Cliquez sur Nouveau > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="90f5d-121">**Type d’application** affecte ce que vous voyez sur le panneau de vue d’ensemble de hello et propriétés hello disponibles dans [explorer métrique][metrics].</span><span class="sxs-lookup"><span data-stu-id="90f5d-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="90f5d-122">Si vous ne voyez pas votre type d’application, choisissez Général.</span><span class="sxs-lookup"><span data-stu-id="90f5d-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="90f5d-123">**Abonnement** est votre compte de paiement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="90f5d-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="90f5d-124">**Groupe de ressources** facilite la gestion des propriétés telles que le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="90f5d-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="90f5d-125">Si vous avez déjà créé des autres ressources Windows Azure, vous pouvez choisir tooput cette nouvelle ressource Bonjour même groupe.</span><span class="sxs-lookup"><span data-stu-id="90f5d-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="90f5d-126">**Emplacement** correspond à l’endroit où nous conservons vos données.</span><span class="sxs-lookup"><span data-stu-id="90f5d-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="90f5d-127">**Code confidentiel toodashboard** place une vignette d’accès rapide pour vos ressources sur votre page d’accueil Azure.</span><span class="sxs-lookup"><span data-stu-id="90f5d-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="90f5d-128">Recommandé.</span><span class="sxs-lookup"><span data-stu-id="90f5d-128">Recommended.</span></span>

<span data-ttu-id="90f5d-129">Une fois votre application créée, un nouveau panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="90f5d-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="90f5d-130">Dans ce panneau, vous trouverez des données relatives à l’utilisation et aux performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="90f5d-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="90f5d-131">tooit de retour tooget prochaine ouverture de session dans tooAzure, recherchez la vignette de démarrage rapide de votre application sur hello démarrer carte (écran d’accueil).</span><span class="sxs-lookup"><span data-stu-id="90f5d-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="90f5d-132">Ou cliquez sur Parcourir toofind il.</span><span class="sxs-lookup"><span data-stu-id="90f5d-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="90f5d-133">Copiez la clé d’instrumentation hello</span><span class="sxs-lookup"><span data-stu-id="90f5d-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="90f5d-134">clé d’instrumentation Hello identifie la ressource hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="90f5d-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="90f5d-135">Vous en avez besoin toogive toohello Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="90f5d-135">You need it toogive toohello SDK.</span></span>

![Cliquez sur Essentials, hello clé d’Instrumentation, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="90f5d-137">Installer hello SDK dans votre application</span><span class="sxs-lookup"><span data-stu-id="90f5d-137">Install hello SDK in your app</span></span>
<span data-ttu-id="90f5d-138">Installer hello Application Insights SDK dans votre application.</span><span class="sxs-lookup"><span data-stu-id="90f5d-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="90f5d-139">Cette étape dépend fortement de type hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="90f5d-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="90f5d-140">Utilisez tooconfigure de clé hello instrumentation [hello du Kit de développement logiciel que vous installez dans votre application][start].</span><span class="sxs-lookup"><span data-stu-id="90f5d-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="90f5d-141">Hello SDK inclut des modules standards qui envoient des données de télémétrie sans que vous ayez toowrite n’importe quel code.</span><span class="sxs-lookup"><span data-stu-id="90f5d-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="90f5d-142">actions de l’utilisateur tootrack ou diagnostiquer les problèmes plus en détail, [utilisent les API hello] [ api] toosend vos propres données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="90f5d-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="90f5d-143"><a name="monitor"></a>Reportez-vous aux données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="90f5d-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="90f5d-144">Fermer hello rapide Démarrer Panneau des applications panneau tooreturn tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="90f5d-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="90f5d-145">Cliquez sur hello recherche vignette toosee [recherche Diagnostic][diagnostic], où les événements de première hello apparaissent.</span><span class="sxs-lookup"><span data-stu-id="90f5d-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="90f5d-146">Après quelques secondes, cliquez sur **Actualiser** pour obtenir des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="90f5d-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="90f5d-147">Création automatique d’une ressource</span><span class="sxs-lookup"><span data-stu-id="90f5d-147">Creating a resource automatically</span></span>
<span data-ttu-id="90f5d-148">Vous pouvez écrire un [script PowerShell](app-insights-powershell.md) toocreate une ressource automatiquement.</span><span class="sxs-lookup"><span data-stu-id="90f5d-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90f5d-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90f5d-149">Next steps</span></span>
* [<span data-ttu-id="90f5d-150">Création d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="90f5d-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="90f5d-151">Recherche de diagnostic</span><span class="sxs-lookup"><span data-stu-id="90f5d-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="90f5d-152">Exploration des mesures</span><span class="sxs-lookup"><span data-stu-id="90f5d-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="90f5d-153">Écriture de requêtes Analytics</span><span class="sxs-lookup"><span data-stu-id="90f5d-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

