---
title: "aaaDeploy tâches Web à l’aide de Visual Studio"
description: "Découvrez comment toodeploy tooAzure de tâches Web Azure App Service Web Apps à l’aide de Visual Studio."
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="95442-103">Déployer des tâches web à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95442-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="95442-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="95442-104">Overview</span></span>
<span data-ttu-id="95442-105">Cette rubrique explique comment toouse Visual Studio toodeploy une Application Console de projet application web tooa [du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) comme un [la tâche Web Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="95442-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="95442-106">Pour plus d’informations sur comment toodeploy tâches Web à l’aide de hello [Azure Portal](https://portal.azure.com), consultez [les tâches en arrière-plan de s’exécuter avec les tâches Web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="95442-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="95442-107">Lorsque Visual Studio déploie un projet d'application console compatible avec des tâches web, il exécute deux tâches :</span><span class="sxs-lookup"><span data-stu-id="95442-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="95442-108">Exécution de copies des fichiers toohello le dossier approprié dans l’application web hello (*App_Data/tâches/continue* pour les tâches Web continues, *App_Data/tâches/déclenchée* pour les tâches planifiées et à la demande Web).</span><span class="sxs-lookup"><span data-stu-id="95442-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="95442-109">Configure [les travaux Azure Scheduler](#scheduler) pour les tâches Web sont toorun planifiée à des moments particuliers.</span><span class="sxs-lookup"><span data-stu-id="95442-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="95442-110">(inutile pour les tâches web continues).</span><span class="sxs-lookup"><span data-stu-id="95442-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="95442-111">Un projet de tâche Web a hello suivant tooit Ajout d’éléments :</span><span class="sxs-lookup"><span data-stu-id="95442-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="95442-112">Hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) package NuGet.</span><span class="sxs-lookup"><span data-stu-id="95442-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="95442-113">Un fichier [webjob-publish-settings.json](#publishsettings) qui contient des paramètres de déploiement et de planification.</span><span class="sxs-lookup"><span data-stu-id="95442-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Diagramme montrant ce qui est ajouté le déploiement de tooenable tooa application Console comme une tâche Web](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="95442-115">Vous pouvez ajouter ces tooan éléments existants du projet d’Application Console ou utiliser un modèle de toocreate un nouveau projet d’Application de Console avec les tâches Web.</span><span class="sxs-lookup"><span data-stu-id="95442-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="95442-116">Vous pouvez déployer un projet en tant qu’une tâche Web en lui-même, ou lier le projet web de tooa afin qu’il déploie automatiquement chaque fois que vous déployez le projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="95442-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="95442-117">toolink projets, Visual Studio inclut le nom hello du projet de tâches Web compatible hello dans un [webjobs-list.json](#webjobslist) fichier projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="95442-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Diagramme montrant le projet de tâche Web liaison tooweb projet](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="95442-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95442-119">Prerequisites</span></span>
<span data-ttu-id="95442-120">Fonctionnalités de déploiement des tâches Web sont disponibles dans Visual Studio lorsque vous installez hello Azure SDK pour .NET :</span><span class="sxs-lookup"><span data-stu-id="95442-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="95442-121">[Kit de développement logiciel (SDK) Azure pour .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="95442-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="95442-122"><a id="convert"></a>Activer le déploiement de tâches web pour un projet d’application de console</span><span class="sxs-lookup"><span data-stu-id="95442-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="95442-123">Deux options s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="95442-123">You have two options:</span></span>

* <span data-ttu-id="95442-124">[Activation d'un déploiement automatique avec un projet web](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="95442-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="95442-125">Configurez un projet d'application console existant afin qu'il soit déployé automatiquement sous forme de tâche web lorsque vous déployez un projet web.</span><span class="sxs-lookup"><span data-stu-id="95442-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="95442-126">Utilisez cette option lorsque vous souhaitez toorun votre tâche Web Bonjour même application web dans lequel vous exécutez hello liées d’application web.</span><span class="sxs-lookup"><span data-stu-id="95442-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="95442-127">[Activation d'un déploiement sans projet web](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="95442-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="95442-128">Configurer un toodeploy de projet Application Console existante comme une tâche Web lui-même, avec aucun projet web ne tooa lien.</span><span class="sxs-lookup"><span data-stu-id="95442-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="95442-129">Utilisez cette option lorsque vous souhaitez toorun une tâche Web dans une application web par lui-même, à aucune application web en cours d’exécution dans l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="95442-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="95442-130">Vous souhaiterez peut-être toodo cela dans commande tooscale en mesure de toobe vos ressources de la tâche Web indépendamment de vos ressources d’application web.</span><span class="sxs-lookup"><span data-stu-id="95442-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="95442-131"><a id="convertlink"></a> Activer un déploiement automatique de tâches web avec un projet web</span><span class="sxs-lookup"><span data-stu-id="95442-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="95442-132">Projet de web avec le bouton hello dans **l’Explorateur de solutions**, puis cliquez sur **ajouter** > **projet existant en tant que tâche Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="95442-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Projet existant sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="95442-134">Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95442-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="95442-135">Bonjour **nom du projet** liste déroulante, sélectionnez hello tooadd de projet Application Console comme une tâche Web.</span><span class="sxs-lookup"><span data-stu-id="95442-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Selecting project in Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="95442-137">Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95442-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="95442-138"><a id="convertnolink"></a> Activer un déploiement de tâches web sans projet web</span><span class="sxs-lookup"><span data-stu-id="95442-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="95442-139">Projet d’Application Console hello avec le bouton droit dans **l’Explorateur de solutions**, puis cliquez sur **publier en tant que tâche Web Azure...** .</span><span class="sxs-lookup"><span data-stu-id="95442-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="95442-141">Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche, projet hello dans hello **nom du projet** boîte.</span><span class="sxs-lookup"><span data-stu-id="95442-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="95442-142">Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95442-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="95442-143">Hello **publier le site Web** Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95442-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="95442-144">Si vous ne souhaitez pas immédiatement toopublish, fermez l’Assistant de hello.</span><span class="sxs-lookup"><span data-stu-id="95442-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="95442-145">paramètres de Hello que vous avez entrées sont enregistrés pour lorsque vous ne souhaitez pas trop[déployer hello projet](#deploy).</span><span class="sxs-lookup"><span data-stu-id="95442-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="95442-146"><a id="create"></a>Créer un projet compatible avec les tâches web</span><span class="sxs-lookup"><span data-stu-id="95442-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="95442-147">toocreate un nouveau projet compatibles sur les tâches Web, vous pouvez utiliser hello Console projet modèle et activer les tâches Web déploiement d’Application comme expliqué dans [hello la section précédente](#convert).</span><span class="sxs-lookup"><span data-stu-id="95442-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="95442-148">En guise d’alternative, vous pouvez utiliser le modèle de nouveau projet hello WebJobs :</span><span class="sxs-lookup"><span data-stu-id="95442-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="95442-149">Utilisez le modèle de nouveau projet de tâches Web de hello pour une tâche Web indépendante</span><span class="sxs-lookup"><span data-stu-id="95442-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="95442-150">Créer un projet et configurez-le toodeploy par lui-même en tant qu’une tâche Web, avec aucun projet web ne tooa lien.</span><span class="sxs-lookup"><span data-stu-id="95442-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="95442-151">Utilisez cette option lorsque vous souhaitez toorun une tâche Web dans une application web par lui-même, à aucune application web en cours d’exécution dans l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="95442-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="95442-152">Vous souhaiterez peut-être toodo cela dans commande tooscale en mesure de toobe vos ressources de la tâche Web indépendamment de vos ressources d’application web.</span><span class="sxs-lookup"><span data-stu-id="95442-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="95442-153">Utiliser le modèle de nouveau projet hello tâches Web pour un projet de web de tooa lié de la tâche Web</span><span class="sxs-lookup"><span data-stu-id="95442-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="95442-154">Créez un projet qui est configuré toodeploy automatiquement comme une tâche Web lorsqu’un projet web Bonjour même solution est déployée.</span><span class="sxs-lookup"><span data-stu-id="95442-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="95442-155">Utilisez cette option lorsque vous souhaitez toorun votre tâche Web Bonjour même application web dans lequel vous exécutez hello liées d’application web.</span><span class="sxs-lookup"><span data-stu-id="95442-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="95442-156">modèle de nouveau projet de tâches Web Hello automatiquement installe les packages NuGet et inclut le code dans *Program.cs* pour hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="95442-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="95442-157">Si vous ne souhaitez pas toouse hello WebJobs SDK, supprimer ou modifier des hello `host.RunAndBlock` instruction *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="95442-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="95442-158"><a id="createnolink"></a>Utilisez le modèle de nouveau projet de tâches Web de hello pour une tâche Web indépendante</span><span class="sxs-lookup"><span data-stu-id="95442-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="95442-159">Cliquez sur **fichier** > **nouveau projet**, puis dans hello **nouveau projet** boîte dialogue, cliquez sur **Cloud**  >   **La tâche Web Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="95442-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![New Project dialog showing WebJob template](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="95442-161">Suivez les instructions de hello présentées précédemment trop[rendre hello projet d’Application Console à un projet de tâches Web indépendant](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="95442-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="95442-162"><a id="createlink"></a>Utiliser le modèle de nouveau projet hello tâches Web pour un projet de web de tooa lié de la tâche Web</span><span class="sxs-lookup"><span data-stu-id="95442-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="95442-163">Projet de web avec le bouton hello dans **l’Explorateur de solutions**, puis cliquez sur **ajouter** > **nouveau projet de la tâche Web Azure**.</span><span class="sxs-lookup"><span data-stu-id="95442-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![New Azure WebJob Project menu entry](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="95442-165">Hello [ajouter de la tâche Web Azure](#configure) boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95442-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="95442-166">Hello complète [ajouter de la tâche Web Azure](#configure) boîte de dialogue, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95442-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="95442-167"><a id="configure"></a>boîte de dialogue Ajouter de la tâche Web Azure Hello</span><span class="sxs-lookup"><span data-stu-id="95442-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="95442-168">Hello **ajouter de la tâche Web Azure** boîte de dialogue vous permet d’entrer le nom de la tâche Web hello et exécutez le paramètre de mode de votre tâche Web.</span><span class="sxs-lookup"><span data-stu-id="95442-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Add Azure WebJob dialog](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="95442-170">champs Hello dans cette boîte de dialogue correspondent toofields sur hello **nouveau travail** boîte de dialogue de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="95442-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="95442-171">Pour plus d’informations, consultez [Exécuter des tâches en arrière-plan avec les tâches web](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="95442-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="95442-172">Pour plus d’informations sur le déploiement en ligne de commande, consultez la page [Activation de la ligne de commande ou de la livraison continue de tâches web Azure](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="95442-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="95442-173">Si vous déployez une tâche Web et que vous décidez ensuite de que créer de type hello de toochange de la tâche Web et de redéploiement, vous devez le fichier de toodelete hello settings.json publier des tâches Web.</span><span class="sxs-lookup"><span data-stu-id="95442-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="95442-174">Cela facilitera afficher hello options de publication, vous pouvez modifier le type hello de tâche Web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95442-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="95442-175">Si vous déployez une tâche Web et que vous changez ultérieurement hello exécution en mode continu toonon continue, ou vice versa, Visual Studio crée une nouvelle tâche de Web dans Azure lorsque vous redéployez.</span><span class="sxs-lookup"><span data-stu-id="95442-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="95442-176">Si vous modifiez d’autres paramètres de planification, mais le mode de laisser s’exécuter même hello ou basculer entre planifiée et à la demande, mises à jour de Visual Studio hello travail existant plutôt que de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="95442-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="95442-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="95442-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="95442-178">Lorsque vous configurez une Application Console pour le déploiement des tâches Web, Visual Studio installe hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package et stocke les informations de planification un *settings.json publier la tâche Web*  fichier hello projet *propriétés* dossier du projet de tâches Web hello.</span><span class="sxs-lookup"><span data-stu-id="95442-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="95442-179">Voici un exemple de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="95442-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="95442-180">Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="95442-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="95442-181">schéma de fichier Hello est stockée au niveau [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) et vous pouvez les consulter.</span><span class="sxs-lookup"><span data-stu-id="95442-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="95442-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="95442-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="95442-183">Lorsque vous liez un projet web de tooa compatibles sur les tâches Web de projet, Visual Studio stocke le nom hello du projet de tâches Web hello dans un *webjobs-list.json* fichier de projet hello web *propriétés* dossier.</span><span class="sxs-lookup"><span data-stu-id="95442-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="95442-184">liste de Hello peut contenir plusieurs projets de tâches Web, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="95442-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="95442-185">Vous pouvez modifier ce fichier directement. Visual Studio est doté d'IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="95442-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="95442-186">schéma de fichier Hello est stockée au niveau [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) et vous pouvez les consulter.</span><span class="sxs-lookup"><span data-stu-id="95442-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="95442-187"><a id="deploy"></a>Déployer un projet WebJobs</span><span class="sxs-lookup"><span data-stu-id="95442-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="95442-188">Un projet de tâches Web que vous avez lié des projets web de tooa déploie automatiquement avec le projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="95442-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="95442-189">Pour plus d’informations sur le déploiement du projet web, consultez [comment toodeploy tooWeb applications](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="95442-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="95442-190">toodeploy un projet de tâches Web par lui-même, avec le bouton droit de projet hello dans **l’Explorateur de solutions** et cliquez sur **publier en tant que tâche Web Azure...** .</span><span class="sxs-lookup"><span data-stu-id="95442-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Publier sous forme de tâche web Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="95442-192">Pour une tâche Web indépendante, hello même **publier le site Web** Assistant qui est utilisé pour les projets web s’affiche, mais avec moins toochange de paramètres disponibles.</span><span class="sxs-lookup"><span data-stu-id="95442-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="95442-193"><a id="nextsteps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95442-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="95442-194">Cet article a expliqué comment toodeploy tâches Web à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="95442-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="95442-195">Pour plus d’informations sur comment toodeploy les tâches Web Azure, consultez [tâches Web Azure - déploiement des ressources - recommandées](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="95442-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

