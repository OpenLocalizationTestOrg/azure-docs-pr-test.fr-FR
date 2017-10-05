---
title: "Déployer des tâches web à l’aide de Visual Studio"
description: "Découvrez comment déployer des tâches web Azure dans Azure App Service Web Apps à l’aide de Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="f34ff-103">Déployer des tâches web à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f34ff-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="f34ff-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f34ff-104">Overview</span></span>
<span data-ttu-id="f34ff-105">Cette rubrique explique comme utiliser Visual Studio pour déployer un projet d’application console sur une application web dans [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en tant que [tâche web Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="f34ff-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="f34ff-106">Pour plus d’informations sur le déploiement de tâches web à l’aide du [portail Azure](https://portal.azure.com), consultez la section [Exécuter des tâches en arrière-plan avec les tâches web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="f34ff-107">Lorsque Visual Studio déploie un projet d'application console compatible avec des tâches web, il exécute deux tâches :</span><span class="sxs-lookup"><span data-stu-id="f34ff-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="f34ff-108">Il copie des fichiers exécutables dans le dossier approprié de l’application web (*App_Data/jobs/continuous* pour les tâches web continues, *App_Data/jobs/triggered* pour les tâches web planifiées et à la demande).</span><span class="sxs-lookup"><span data-stu-id="f34ff-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="f34ff-109">Il configure des [tâches Azure Scheduler](#scheduler) pour les tâches web dont l’exécution est prévue à des horaires précis.</span><span class="sxs-lookup"><span data-stu-id="f34ff-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="f34ff-110">(inutile pour les tâches web continues).</span><span class="sxs-lookup"><span data-stu-id="f34ff-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="f34ff-111">Un projet compatible avec les tâches web se voit ajouter les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f34ff-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="f34ff-112">Le package NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .</span><span class="sxs-lookup"><span data-stu-id="f34ff-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="f34ff-113">Un fichier [webjob-publish-settings.json](#publishsettings) qui contient des paramètres de déploiement et de planification.</span><span class="sxs-lookup"><span data-stu-id="f34ff-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagram showing what is added to a Console App to enable deployment as a WebJob](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="f34ff-115">Vous pouvez ajouter ces éléments à un projet d'application console existant ou utiliser un modèle pour créer un projet d'application console compatible avec les tâches web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="f34ff-116">Vous pouvez déployer un projet sous forme de tâche web ou le lier à un projet web afin qu'il soit déployé automatiquement lorsque vous déployez le projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="f34ff-117">Pour lier les projets, Visual Studio inclut le nom du projet compatible avec les tâches web dans un fichier [webjobs-list.json](#webjobslist) dans le projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Diagram showing WebJob project linking to web project](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="f34ff-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f34ff-119">Prerequisites</span></span>
<span data-ttu-id="f34ff-120">Les fonctionnalités de déploiement de WebJobs sont disponibles dans Visual Studio lorsque vous installez le Kit de développement logiciel (SDK) Azure pour .NET :</span><span class="sxs-lookup"><span data-stu-id="f34ff-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="f34ff-121">[Kit de développement logiciel (SDK) Azure pour .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f34ff-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="f34ff-122"><a id="convert"></a>Activer le déploiement de tâches web pour un projet d’application de console</span><span class="sxs-lookup"><span data-stu-id="f34ff-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="f34ff-123">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="f34ff-123">You have two options:</span></span>

* <span data-ttu-id="f34ff-124">[Activation d'un déploiement automatique avec un projet web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="f34ff-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="f34ff-125">Configurez un projet d'application console existant afin qu'il soit déployé automatiquement sous forme de tâche web lorsque vous déployez un projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="f34ff-126">Utilisez cette option lorsque vous voulez exécuter votre tâche web dans la même application web que celle dans laquelle vous exécutez l’application web liée.</span><span class="sxs-lookup"><span data-stu-id="f34ff-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="f34ff-127">[Activation d'un déploiement sans projet web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="f34ff-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="f34ff-128">Configurez un projet d'application console existant pour déployer une tâche web seule, sans lien avec un projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="f34ff-129">Utilisez cette option lorsque vous voulez exécuter une tâche web dans une application web seule, sans application web s’exécutant dans cette dernière.</span><span class="sxs-lookup"><span data-stu-id="f34ff-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="f34ff-130">Vous pouvez utiliser cette méthode afin de faire évoluer vos ressources de tâches web indépendamment de vos ressources d'application web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="f34ff-131"><a id="convertlink"></a> Activer un déploiement automatique de tâches web avec un projet web</span><span class="sxs-lookup"><span data-stu-id="f34ff-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="f34ff-132">Cliquez avec le bouton droit sur le projet web dans l’**Explorateur de solutions**, puis cliquez sur **Ajouter** > **Projet existant en tant que tâche web Azure**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Projet existant sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="f34ff-134">La boîte de dialogue [Ajouter une tâche web Azure](#configure) s'affiche.</span><span class="sxs-lookup"><span data-stu-id="f34ff-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="f34ff-135">Dans la liste déroulante **Nom du projet** , sélectionnez le projet d'application console à ajouter sous forme de tâche web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="f34ff-137">Remplissez la boîte de dialogue [Ajouter une tâche web Azure](#configure) , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="f34ff-138"><a id="convertnolink"></a> Activer un déploiement de tâches web sans projet web</span><span class="sxs-lookup"><span data-stu-id="f34ff-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="f34ff-139">Cliquez avec le bouton droit sur le projet d’application de console dans l’**Explorateur de solutions**, puis cliquez sur **Publier en tant que tâche web Azure**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="f34ff-141">La boîte de dialogue [Ajouter une tâche web Azure](#configure) s'affiche avec le projet sélectionné dans la zone **Nom du projet** .</span><span class="sxs-lookup"><span data-stu-id="f34ff-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="f34ff-142">Remplissez la boîte de dialogue [Ajouter une tâche web Azure](#configure) , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="f34ff-143">L'Assistant **Publier le site Web** s'ouvre.</span><span class="sxs-lookup"><span data-stu-id="f34ff-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="f34ff-144">Si vous ne voulez pas publier immédiatement, fermez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="f34ff-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="f34ff-145">Les paramètres que vous avez saisis sont enregistrés au cas où vous souhaiteriez [déployer le projet](#deploy).</span><span class="sxs-lookup"><span data-stu-id="f34ff-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="f34ff-146"><a id="create"></a>Créer un projet compatible avec les tâches web</span><span class="sxs-lookup"><span data-stu-id="f34ff-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="f34ff-147">Pour créer un projet compatible avec les tâches web, vous pouvez utiliser le modèle de projet d'application console et activer le déploiement des tâches web comme expliqué dans [la section précédente](#convert).</span><span class="sxs-lookup"><span data-stu-id="f34ff-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="f34ff-148">Vous pouvez également utiliser le modèle de nouveau projet de tâche web :</span><span class="sxs-lookup"><span data-stu-id="f34ff-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="f34ff-149">Utiliser le modèle de nouveau projet WebJobs pour une tâche web indépendante</span><span class="sxs-lookup"><span data-stu-id="f34ff-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="f34ff-150">Créez un projet et configurez-le pour qu'il se déploie seul sous forme de tâche web, sans lien avec un projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="f34ff-151">Utilisez cette option lorsque vous voulez exécuter une tâche web dans une application web seule, sans application web s’exécutant dans cette dernière.</span><span class="sxs-lookup"><span data-stu-id="f34ff-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="f34ff-152">Vous pouvez utiliser cette méthode afin de faire évoluer vos ressources de tâches web indépendamment de vos ressources d'application web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="f34ff-153">Utiliser le modèle de nouveau projet WebJobs pour une tâche web liée à un projet web</span><span class="sxs-lookup"><span data-stu-id="f34ff-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="f34ff-154">Créez un projet configuré pour être déployé automatiquement sous forme de tâche web lorsqu'un projet web dans la même solution est déployé.</span><span class="sxs-lookup"><span data-stu-id="f34ff-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="f34ff-155">Utilisez cette option lorsque vous voulez exécuter votre tâche web dans la même application web que celle dans laquelle vous exécutez l’application web liée.</span><span class="sxs-lookup"><span data-stu-id="f34ff-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="f34ff-156">Le modèle de nouveau projet WebJobs installe automatiquement les packages NuGet et inclut le code dans *Program.cs* pour le [Kit de développement logiciel (SDK) WebJobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="f34ff-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="f34ff-157">Si vous ne souhaitez pas utiliser le Kit de développement logiciel (SDK) WebJobs, supprimez ou modifiez l’instruction `host.RunAndBlock` dans *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="f34ff-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="f34ff-158"><a id="createnolink"></a> Utiliser le modèle de nouveau projet WebJobs pour une tâche web indépendante</span><span class="sxs-lookup"><span data-stu-id="f34ff-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="f34ff-159">Cliquez sur **Fichier** > **Nouveau projet**, puis dans la boîte de dialogue **Nouveau projet**, cliquez sur **Cloud** > **Azure WebJob (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="f34ff-161">Suivez les instructions affichées précédemment pour [faire du projet de l'application console un projet de tâche web indépendant](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="f34ff-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="f34ff-162"><a id="createlink"></a> Utiliser le modèle de nouveau projet WebJobs pour une tâche web liée à un projet web</span><span class="sxs-lookup"><span data-stu-id="f34ff-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="f34ff-163">Cliquez avec le bouton droit sur le projet web dans l’**Explorateur de solutions**, puis cliquez sur **Ajouter** > **Nouveau projet de tâche web Azure**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="f34ff-165">La boîte de dialogue [Ajouter une tâche web Azure](#configure) s'affiche.</span><span class="sxs-lookup"><span data-stu-id="f34ff-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="f34ff-166">Remplissez la boîte de dialogue [Ajouter une tâche web Azure](#configure) , puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="f34ff-167"><a id="configure"></a>Boîte de dialogue Ajouter une tâche web Azure</span><span class="sxs-lookup"><span data-stu-id="f34ff-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="f34ff-168">La boîte de dialogue **Ajouter un WebJob Azure** vous permet d’entrer le nom du WebJob et d’exécuter le paramètre de mode de votre WebJob.</span><span class="sxs-lookup"><span data-stu-id="f34ff-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="f34ff-170">Les champs de cette boîte de dialogue correspondent à ceux de la boîte de dialogue **Nouvelle tâche** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f34ff-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="f34ff-171">Pour plus d’informations, consultez [Exécuter des tâches en arrière-plan avec les tâches web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="f34ff-172">Pour plus d’informations sur le déploiement en ligne de commande, consultez la page [Activation de la ligne de commande ou de la livraison continue de tâches web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="f34ff-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="f34ff-173">Si vous déployez une tâche web et que vous décidez ensuite d’en modifier le type et de la redéployer, vous devez supprimer le fichier webjobs-publish-settings.json.</span><span class="sxs-lookup"><span data-stu-id="f34ff-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="f34ff-174">Ainsi Visual Studio affiche à nouveau les options de publication qui vous permettent de modifier le type de la tâche web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="f34ff-175">Si vous déployez une tâche web et que vous modifiez ultérieurement le mode d'exécution continue en non continue ou vice-versa, Visual Studio crée une tâche web dans Azure lorsque vous procédez à un nouveau déploiement.</span><span class="sxs-lookup"><span data-stu-id="f34ff-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="f34ff-176">Si vous modifiez d'autres paramètres de planification, mais que vous conservez le même mode d'exécution ou passez à une tâche planifiée ou à la demande, Visual Studio met à jour la tâche existante plutôt que d'en créer une.</span><span class="sxs-lookup"><span data-stu-id="f34ff-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="f34ff-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="f34ff-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="f34ff-178">Lorsque vous configurez une application console pour un déploiement de tâches web, Visual Studio installe le package NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) et stocke les informations de planification dans un fichier *webjob-publish-settings.json* du dossier *Propriétés* du projet WebJobs.</span><span class="sxs-lookup"><span data-stu-id="f34ff-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="f34ff-179">Voici un exemple de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="f34ff-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="f34ff-180">Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="f34ff-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="f34ff-181">Le schéma du fichier est stocké et consultable à l’adresse [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json).</span><span class="sxs-lookup"><span data-stu-id="f34ff-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="f34ff-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="f34ff-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="f34ff-183">Lorsque vous liez un projet compatible avec des tâches web à un projet web, Visual Studio stocke le nom du projet de tâches web sous le nom de fichier *webjobs-list.json* dans le dossier *Propriétés* du projet web.</span><span class="sxs-lookup"><span data-stu-id="f34ff-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="f34ff-184">La liste peut contenir plusieurs projets WebJobs, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f34ff-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="f34ff-185">Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="f34ff-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="f34ff-186">Le schéma du fichier est stocké et consultable à l’adresse [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json).</span><span class="sxs-lookup"><span data-stu-id="f34ff-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="f34ff-187"><a id="deploy"></a>Déployer un projet WebJobs</span><span class="sxs-lookup"><span data-stu-id="f34ff-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="f34ff-188">Lorsqu'il est lié à un projet web, un projet de tâches web est déployé automatiquement avec ce dernier.</span><span class="sxs-lookup"><span data-stu-id="f34ff-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="f34ff-189">Pour plus d’informations sur le déploiement du projet Web, consultez la page [Déployer une application web dans Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f34ff-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="f34ff-190">Pour déployer un projet WebJobs seul, cliquez avec le bouton droit sur le projet dans l’**Explorateur de solutions**, puis sur **Publier en tant que tâche web Azure**.</span><span class="sxs-lookup"><span data-stu-id="f34ff-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="f34ff-192">Pour une tâche web indépendante, l'Assistant **Publier le site Web** utilisé pour les projets web s'affiche, mais avec moins de paramètres modifiables.</span><span class="sxs-lookup"><span data-stu-id="f34ff-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="f34ff-193"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f34ff-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="f34ff-194">Cet article vous a expliqué comment déployer des WebJobs à l'aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f34ff-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="f34ff-195">Pour plus d’informations sur le déploiement d’Azure WebJobs, consultez la rubrique [Azure WebJobs - Ressources recommandées - Déploiement](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="f34ff-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

