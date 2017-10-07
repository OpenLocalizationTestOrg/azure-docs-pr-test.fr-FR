---
title: annotations aaaRelease pour Application Insights | Documents Microsoft
description: "Ajouter un déploiement ou générer des marqueurs graphiques de l’Explorateur de métriques tooyour dans Application Insights."
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="8c0b5-103">Annotations sur les graphiques de métriques dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="8c0b5-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="8c0b5-104">Des annotations sur les graphiques [Metrics Explorer](app-insights-metrics-explorer.md) montrent les endroits où vous avez déployé une nouvelle build ou tout autre événement majeur.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="8c0b5-105">Elles rendent facile toosee si vos modifications avaient aucun effet sur les performances de votre application.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="8c0b5-106">Ils peuvent être créés automatiquement par hello [système de génération Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="8c0b5-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="8c0b5-107">Vous pouvez également créer annotations tooflag n’importe quel événement voulue en [leur création à partir de PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="8c0b5-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Exemples d’annotations avec corrélation visible avec le délai de réponse de serveur](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="8c0b5-109">Annotations de version avec Build VSTS</span><span class="sxs-lookup"><span data-stu-id="8c0b5-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="8c0b5-110">Les annotations de version sont une fonctionnalité de génération de nuage hello et version de service de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="8c0b5-111">Installation de l’extension d’Annotations hello (une fois)</span><span class="sxs-lookup"><span data-stu-id="8c0b5-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="8c0b5-112">annotations de toobe toocreate en mesure de mise en production, vous devez tooinstall une Hello plusieurs extensions de Service d’équipe disponibles dans hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="8c0b5-113">Connectez-vous à tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projet.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="8c0b5-114">Dans Visual Studio Marketplace, [obtenir hello version Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)et ajouter le compte de tooyour Team Services.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![En haut à droite de la page web de Team Services, ouvrez Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="8c0b5-117">Vous ne devez toodo ce qu’une seule fois pour votre compte Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="8c0b5-118">Des annotations de version peuvent désormais être configurées pour n’importe quel projet de votre compte.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="8c0b5-119">Configurer des annotations de version</span><span class="sxs-lookup"><span data-stu-id="8c0b5-119">Configure release annotations</span></span>

<span data-ttu-id="8c0b5-120">Vous devez tooget une API distincte clé pour chaque modèle de version VSTS.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="8c0b5-121">Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com) et ouvrir la ressource Application Insights hello surveille votre application.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="8c0b5-122">(Ou [créez-en une maintenant](app-insights-overview.md)si vous ne l’avez pas encore fait.)</span><span class="sxs-lookup"><span data-stu-id="8c0b5-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="8c0b5-123">Ouvrez **Accès d’API**, **ID Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Dans portal.azure.com, ouvrez votre ressource Application Insights, puis choisissez Paramètres.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="8c0b5-127">Dans une fenêtre de navigateur distincte, ouvrez (ou créez) modèle de version hello qui gère vos déploiements à partir de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="8c0b5-128">Ajouter une tâche, puis sélectionnez les tâches d’Application Insights version Annotation hello à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="8c0b5-129">Hello de coller **Id d’Application** que vous avez copié à partir de hello panneau d’accès de l’API.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![Dans Visual Studio Team Services, ouvrez Version, sélectionnez une définition de version, puis choisissez Modifier.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="8c0b5-133">Ensemble hello **APIKey** variable du champ de tooa `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="8c0b5-134">Dans hello fenêtre Azure, créez une nouvelle clé d’API et création d’une copie de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Bonjour panneau d’accès aux API Bonjour Azure fenêtre, cliquez sur Créer une clé API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="8c0b5-138">Ouvrez l’onglet de Configuration hello du modèle de mise en production hello.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="8c0b5-139">Créez une définition de variable pour `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="8c0b5-140">Collez votre définition de la variable ApiKey de toohello clé API.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Dans la fenêtre de hello Team Services, sélectionnez l’onglet de Configuration hello et cliquez sur Ajouter une Variable.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="8c0b5-143">Enfin, **enregistrer** hello de définition de la version.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="8c0b5-144">Afficher les annotations</span><span class="sxs-lookup"><span data-stu-id="8c0b5-144">View annotations</span></span>
<span data-ttu-id="8c0b5-145">Maintenant, chaque fois que vous utilisez hello version modèle toodeploy une nouvelle version, une annotation sera envoyée tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="8c0b5-146">les annotations Hello seront affiche sur les graphiques dans Metrics Explorer.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="8c0b5-147">Cliquez sur n’importe quel annotation marqueur tooopen plus d’informations sur version hello, y compris le demandeur, branche de contrôle de code source, la définition de mise en production, environnement et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Cliquez sur un marqueur d’annotation de version.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="8c0b5-149">Créer des annotations personnalisées à partir de PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c0b5-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="8c0b5-150">Vous pouvez également créer des annotations à partir du processus de votre choix (sans utiliser Visual Studio Team System).</span><span class="sxs-lookup"><span data-stu-id="8c0b5-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="8c0b5-151">Effectuer une copie locale de hello [script Powershell à partir de GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="8c0b5-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="8c0b5-152">Obtenir hello ID d’Application et créer une clé d’API à partir de hello panneau d’accès de l’API.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="8c0b5-153">Appeler le script de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8c0b5-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="8c0b5-154">Il s’agit de script de hello toomodify facile, par exemple toocreate annotations pour hello passée.</span><span class="sxs-lookup"><span data-stu-id="8c0b5-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c0b5-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c0b5-155">Next steps</span></span>

* [<span data-ttu-id="8c0b5-156">Créer des éléments de travail</span><span class="sxs-lookup"><span data-stu-id="8c0b5-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="8c0b5-157">Automation avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c0b5-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
