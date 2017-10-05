---
title: "Créer une ressource Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="82e25-103">Création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="82e25-103">Create an Application Insights resource</span></span>
<span data-ttu-id="82e25-104">Azure Application Insights affiche les données relatives à votre application dans une *ressource* Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82e25-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="82e25-105">La création d’une nouvelle ressource fait, par conséquent, partie de la [configuration d’Application Insights pour surveiller une nouvelle application][start].</span><span class="sxs-lookup"><span data-stu-id="82e25-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="82e25-106">Dans de nombreux cas, il est possible de créer une ressource automatiquement à l’aide de l’IDE.</span><span class="sxs-lookup"><span data-stu-id="82e25-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="82e25-107">Mais dans certains cas, vous créez manuellement une ressource : par exemple, pour avoir des ressources distinctes pour le développement et la production des builds de votre application.</span><span class="sxs-lookup"><span data-stu-id="82e25-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="82e25-108">Après avoir créé la ressource, vous obtenez sa clé d’instrumentation et l’utilisez pour configurer le Kit SDK dans l’application.</span><span class="sxs-lookup"><span data-stu-id="82e25-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="82e25-109">La clé de ressource établit un lien entre la télémétrie et la ressource.</span><span class="sxs-lookup"><span data-stu-id="82e25-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="82e25-110">S’inscrire à Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="82e25-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="82e25-111">Si vous n’avez pas de [compte Microsoft, procurez-vous en un dès maintenant](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="82e25-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="82e25-112">(Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="82e25-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="82e25-113">Vous devez également vous abonner à [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="82e25-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="82e25-114">Si votre équipe ou votre organisation dispose d’un abonnement Azure, le propriétaire peut vous y ajouter à l’aide de votre Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="82e25-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="82e25-115">Vous êtes facturé uniquement pour ce que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="82e25-115">You're only charged for what you use.</span></span> <span data-ttu-id="82e25-116">Le plan de base (par défaut) vous permet d’utiliser gratuitement une partie des fonctionnalités, à titre d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="82e25-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="82e25-117">Dès que vous êtes abonné, connectez-vous à Application Insights à l’adresse [http://portal.azure.com](https://portal.azure.com), puis utilisez votre Live ID pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="82e25-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="82e25-118">Création d’une ressource Application Insights dans Azure</span><span class="sxs-lookup"><span data-stu-id="82e25-118">Create an Application Insights resource</span></span>
<span data-ttu-id="82e25-119">Dans le portail [portal.azure.com](https://portal.azure.com), ajoutez une ressource Application Insights :</span><span class="sxs-lookup"><span data-stu-id="82e25-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Cliquez sur Nouveau > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="82e25-121">**type d’application** définit le contenu du panneau de présentation et les propriétés disponibles dans [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="82e25-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="82e25-122">Si vous ne voyez pas votre type d’application, choisissez Général.</span><span class="sxs-lookup"><span data-stu-id="82e25-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="82e25-123">**Abonnement** est votre compte de paiement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82e25-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="82e25-124">**Groupe de ressources** facilite la gestion des propriétés telles que le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="82e25-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="82e25-125">Si vous avez déjà créé d’autres ressources Azure, vous pouvez choisir de placer cette nouvelle ressource dans le même groupe.</span><span class="sxs-lookup"><span data-stu-id="82e25-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="82e25-126">**Emplacement** correspond à l’endroit où nous conservons vos données.</span><span class="sxs-lookup"><span data-stu-id="82e25-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="82e25-127">**Épingler au tableau de bord** place une vignette d’accès rapide à votre ressource sur votre page d’accueil Azure.</span><span class="sxs-lookup"><span data-stu-id="82e25-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="82e25-128">Recommandé.</span><span class="sxs-lookup"><span data-stu-id="82e25-128">Recommended.</span></span>

<span data-ttu-id="82e25-129">Une fois votre application créée, un nouveau panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="82e25-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="82e25-130">Dans ce panneau, vous trouverez des données relatives à l’utilisation et aux performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="82e25-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="82e25-131">Pour y revenir lors de votre prochaine connexion à Azure, recherchez la vignette d’accès rapide à votre application située dans le panneau de démarrage (écran d’accueil).</span><span class="sxs-lookup"><span data-stu-id="82e25-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="82e25-132">Sinon, cliquez sur Parcourir.</span><span class="sxs-lookup"><span data-stu-id="82e25-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="82e25-133">Copie de la clé d’instrumentation</span><span class="sxs-lookup"><span data-stu-id="82e25-133">Copy the instrumentation key</span></span>
<span data-ttu-id="82e25-134">La clé d'instrumentation identifie la ressource que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="82e25-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="82e25-135">Vous devez la fournir au SDK.</span><span class="sxs-lookup"><span data-stu-id="82e25-135">You need it to give to the SDK.</span></span>

![Cliquez sur Essentials, sur la clé d'instrumentation, puis appuyez sur CTRL+C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="82e25-137">Installation du Kit SDK dans votre application</span><span class="sxs-lookup"><span data-stu-id="82e25-137">Install the SDK in your app</span></span>
<span data-ttu-id="82e25-138">Installez le Kit SDK Application Insights dans votre application.</span><span class="sxs-lookup"><span data-stu-id="82e25-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="82e25-139">Cette étape repose en grande partie sur votre type d’application.</span><span class="sxs-lookup"><span data-stu-id="82e25-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="82e25-140">La clé d’instrumentation permet de configurer le [kit de développement logiciel (SDK) que vous avez installé dans votre application][start].</span><span class="sxs-lookup"><span data-stu-id="82e25-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="82e25-141">Le SDK inclut des modules standard qui envoient des données de télémétrie sans avoir à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="82e25-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="82e25-142">Pour suivre les actions des utilisateurs ou diagnostiquer des problèmes plus en détail, [utilisez l'API][api] pour envoyer votre propre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="82e25-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="82e25-143"><a name="monitor"></a>Reportez-vous aux données de télémétrie</span><span class="sxs-lookup"><span data-stu-id="82e25-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="82e25-144">Fermez le panneau de démarrage rapide pour revenir au panneau de votre application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="82e25-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="82e25-145">Cliquez sur la vignette de recherche pour afficher [Recherche de diagnostic][diagnostic], où s’affichent les premiers événements.</span><span class="sxs-lookup"><span data-stu-id="82e25-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="82e25-146">Après quelques secondes, cliquez sur **Actualiser** pour obtenir des données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="82e25-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="82e25-147">Création automatique d’une ressource</span><span class="sxs-lookup"><span data-stu-id="82e25-147">Creating a resource automatically</span></span>
<span data-ttu-id="82e25-148">Vous pouvez écrire un [script PowerShell](app-insights-powershell.md) pour créer automatiquement une ressource.</span><span class="sxs-lookup"><span data-stu-id="82e25-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e25-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82e25-149">Next steps</span></span>
* [<span data-ttu-id="82e25-150">Création d’un tableau de bord</span><span class="sxs-lookup"><span data-stu-id="82e25-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="82e25-151">Recherche de diagnostic</span><span class="sxs-lookup"><span data-stu-id="82e25-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="82e25-152">Exploration des mesures</span><span class="sxs-lookup"><span data-stu-id="82e25-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="82e25-153">Écriture de requêtes Analytics</span><span class="sxs-lookup"><span data-stu-id="82e25-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

