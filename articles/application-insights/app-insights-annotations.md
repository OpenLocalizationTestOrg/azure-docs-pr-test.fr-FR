---
title: Annotations de version pour Application Insights | Microsoft Docs
description: "Ajouter des marqueurs déploiement ou de build aux graphiques Metrics Explorer dans Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="874e7-103">Annotations sur les graphiques de métriques dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="874e7-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="874e7-104">Des annotations sur les graphiques [Metrics Explorer](app-insights-metrics-explorer.md) montrent les endroits où vous avez déployé une nouvelle build ou tout autre événement majeur.</span><span class="sxs-lookup"><span data-stu-id="874e7-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="874e7-105">Elles vous permettent de mieux voir l’effet de vos modifications sur les performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="874e7-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="874e7-106">Elles peuvent être créées automatiquement par le [système de génération Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="874e7-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="874e7-107">Vous pouvez également créer des annotations pour tout événement en [les créant à partir de PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="874e7-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Exemples d’annotations avec corrélation visible avec le délai de réponse de serveur](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="874e7-109">Annotations de version avec Build VSTS</span><span class="sxs-lookup"><span data-stu-id="874e7-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="874e7-110">Les annotations de version sont une fonctionnalité de la build sur le cloud et le service de version de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="874e7-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="874e7-111">Installer l’extension Annotations (une fois)</span><span class="sxs-lookup"><span data-stu-id="874e7-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="874e7-112">Pour être en mesure de créer des annotations de version, vous devez installer l’une des nombreuses extensions Team Service disponibles dans Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="874e7-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="874e7-113">Connectez-vous à votre projet [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="874e7-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="874e7-114">Dans Visual Studio Marketplace, [obtenez l’extension Release Annotations](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)et ajoutez-la à votre compte Team Services.</span><span class="sxs-lookup"><span data-stu-id="874e7-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![En haut à droite de la page web de Team Services, ouvrez Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="874e7-117">Vous devez procéder ainsi une seule fois pour votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="874e7-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="874e7-118">Des annotations de version peuvent désormais être configurées pour n’importe quel projet de votre compte.</span><span class="sxs-lookup"><span data-stu-id="874e7-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="874e7-119">Configurer des annotations de version</span><span class="sxs-lookup"><span data-stu-id="874e7-119">Configure release annotations</span></span>

<span data-ttu-id="874e7-120">Vous devez obtenir une clé API distincte pour chaque modèle de version VSTS.</span><span class="sxs-lookup"><span data-stu-id="874e7-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="874e7-121">Connectez-vous au [portail Microsoft Azure](https://portal.azure.com) et ouvrez la ressource Application Insights qui surveille votre application.</span><span class="sxs-lookup"><span data-stu-id="874e7-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="874e7-122">(Ou [créez-en une maintenant](app-insights-overview.md)si vous ne l’avez pas encore fait.)</span><span class="sxs-lookup"><span data-stu-id="874e7-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="874e7-123">Ouvrez **Accès d’API**, **ID Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="874e7-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Dans portal.azure.com, ouvrez votre ressource Application Insights, puis choisissez Paramètres.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="874e7-127">Dans une fenêtre de navigateur distincte, ouvrez (ou créez) le modèle de version qui gère vos déploiements à partir de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="874e7-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="874e7-128">Ajoutez une tâche, sélectionnez la tâche d’annotation de version d’Application Insights à partir du menu.</span><span class="sxs-lookup"><span data-stu-id="874e7-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="874e7-129">Collez **l’ID de l’application** que vous avez copié à partir du panneau Accès API.</span><span class="sxs-lookup"><span data-stu-id="874e7-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![Dans Visual Studio Team Services, ouvrez Version, sélectionnez une définition de version, puis choisissez Modifier.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="874e7-133">Affectez au champ **APIKey** une variable `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="874e7-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="874e7-134">De retour dans la fenêtre Azure, créez une clé API et copiez-la.</span><span class="sxs-lookup"><span data-stu-id="874e7-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Dans le panneau Accès API de la fenêtre Azure, cliquez sur Créer une clé API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="874e7-138">Ouvrez l’onglet Configuration du modèle de version.</span><span class="sxs-lookup"><span data-stu-id="874e7-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="874e7-139">Créez une définition de variable pour `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="874e7-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="874e7-140">Collez votre clé API pour la définition de la variable APIKey.</span><span class="sxs-lookup"><span data-stu-id="874e7-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![Dans la fenêtre Team Services, sélectionnez l’onglet Configuration, puis cliquez sur Ajouter une variable.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="874e7-143">Enfin, **enregistrez** la définition de version.</span><span class="sxs-lookup"><span data-stu-id="874e7-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="874e7-144">Afficher les annotations</span><span class="sxs-lookup"><span data-stu-id="874e7-144">View annotations</span></span>
<span data-ttu-id="874e7-145">Désormais, lorsque vous utilisez le modèle de version pour déployer une nouvelle version, une annotation est envoyée à Application Insights.</span><span class="sxs-lookup"><span data-stu-id="874e7-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="874e7-146">Les annotations figureront sur les graphiques Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="874e7-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="874e7-147">Cliquez sur un marqueur d’annotation pour ouvrir les détails sur la version, notamment le demandeur, la branche de contrôle de code source, la définition de la version, l’environnement et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="874e7-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Cliquez sur un marqueur d’annotation de version.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="874e7-149">Créer des annotations personnalisées à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="874e7-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="874e7-150">Vous pouvez également créer des annotations à partir du processus de votre choix (sans utiliser Visual Studio Team System).</span><span class="sxs-lookup"><span data-stu-id="874e7-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="874e7-151">Créez une copie locale du [script Powershell à partir de GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="874e7-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="874e7-152">Obtenez l’ID d’application et créez une clé API à partir du panneau Accès d’API.</span><span class="sxs-lookup"><span data-stu-id="874e7-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="874e7-153">Appelez le script comme suit :</span><span class="sxs-lookup"><span data-stu-id="874e7-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="874e7-154">Il est facile de modifier le script, par exemple pour créer des annotations pour les événements passés.</span><span class="sxs-lookup"><span data-stu-id="874e7-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="874e7-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="874e7-155">Next steps</span></span>

* [<span data-ttu-id="874e7-156">Créer des éléments de travail</span><span class="sxs-lookup"><span data-stu-id="874e7-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="874e7-157">Automation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="874e7-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
