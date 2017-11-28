---
title: "aaaContinuous tooAzure de déploiement du Service d’applications | Documents Microsoft"
description: "Découvrez comment tooenable déploiement continu tooAzure du Service d’applications."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="99bdb-103">TooAzure de déploiement continue du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="99bdb-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="99bdb-104">Ce didacticiel vous montre comment tooconfigure un flux de travail de déploiement continu pour votre [Azure App Service] application.</span><span class="sxs-lookup"><span data-stu-id="99bdb-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="99bdb-105">Intégration du Service d’applications avec BitBucket, GitHub, et [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) permet un continue où Azure extrait dans hello plus récentes des mises à jour à partir de votre projet de workflow de déploiement publié tooone de ces services.</span><span class="sxs-lookup"><span data-stu-id="99bdb-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="99bdb-106">Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées.</span><span class="sxs-lookup"><span data-stu-id="99bdb-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="99bdb-107">toofind out comment un déploiement continu tooconfigure manuellement à partir d’un référentiel de cloud ne pas répertorié par hello portail Azure (tels que [GitLab](https://gitlab.com/)), consultez [vous configurez le déploiement continu à l’aide des étapes manuelles](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="99bdb-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="99bdb-108"><a name="overview"></a>Activer le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="99bdb-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="99bdb-109">déploiement continu tooenable,</span><span class="sxs-lookup"><span data-stu-id="99bdb-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="99bdb-110">Publier votre référentiel de contenu toohello d’application qui sera utilisé pour le déploiement continu.</span><span class="sxs-lookup"><span data-stu-id="99bdb-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="99bdb-111">Pour plus d’informations sur la publication de vos services de toothese de projet, consultez [créer un référentiel (GitHub)], [créer un référentiel (BitBucket)], et [prise en main VSTS].</span><span class="sxs-lookup"><span data-stu-id="99bdb-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="99bdb-112">Dans le panneau de menu de votre application Bonjour [portail Azure], cliquez sur **déploiement d’applications > options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="99bdb-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="99bdb-113">Cliquez sur **choisir la Source de**, puis sélectionnez source du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="99bdb-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="99bdb-114">tooconfigure un compte VSTS pour le déploiement du Service d’applications, consultez ce [didacticiel](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="99bdb-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="99bdb-115">Flux de travail d’autorisation hello terminée.</span><span class="sxs-lookup"><span data-stu-id="99bdb-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="99bdb-116">Bonjour **source du déploiement** panneau, choisissez le projet de hello et créer une branche toodeploy à partir de.</span><span class="sxs-lookup"><span data-stu-id="99bdb-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="99bdb-117">Quand vous avez terminé, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="99bdb-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="99bdb-118">Lors de l’activation du déploiement continu avec GitHub ou BitBucket, les projets publics et privés sont tous deux affichés.</span><span class="sxs-lookup"><span data-stu-id="99bdb-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="99bdb-119">Service d’applications crée une association avec le référentiel sélectionné de hello, extrait les fichiers hello à partir de la branche spécifiée de hello et conserve un clone de votre référentiel pour votre application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="99bdb-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="99bdb-120">Lorsque vous configurez le déploiement continu VSTS hello portail Azure, l’intégration hello utilise hello du Service d’applications [moteur de déploiement Kudu](https://github.com/projectkudu/kudu/wiki), qui automatise les tâches de génération et de déploiement avec déjà chaque `git push`.</span><span class="sxs-lookup"><span data-stu-id="99bdb-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="99bdb-121">Vous n’avez pas besoin de tooseparately définir un déploiement continu dans VSTS.</span><span class="sxs-lookup"><span data-stu-id="99bdb-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="99bdb-122">Une fois ce processus terminé, hello **options de déploiement** Panneau de l’application affiche un déploiement actif qui indique le déploiement a réussi.</span><span class="sxs-lookup"><span data-stu-id="99bdb-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="99bdb-123">tooverify hello application est déployée avec succès, cliquez sur hello **URL** haut hello du Panneau de l’application hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="99bdb-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="99bdb-124">tooverify déploiement continu se produit à partir du référentiel hello de votre choix, transmettre un référentiel de toohello de modification.</span><span class="sxs-lookup"><span data-stu-id="99bdb-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="99bdb-125">Votre application doit mettre à jour les modifications de hello tooreflect peu de temps après que le référentiel de toohello hello par émission de données se termine.</span><span class="sxs-lookup"><span data-stu-id="99bdb-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="99bdb-126">Vous pouvez vérifier qu’il a tiré mise à jour hello Bonjour **options de déploiement** Panneau de votre application.</span><span class="sxs-lookup"><span data-stu-id="99bdb-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="99bdb-127"><a name="VSsolution"></a>Déploiement continu avec une solution Visual Studio</span><span class="sxs-lookup"><span data-stu-id="99bdb-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="99bdb-128">En exécutant un push d’un tooAzure de solution Visual Studio du Service d’applications est aussi simple que d’envoyer un fichier index.html simple.</span><span class="sxs-lookup"><span data-stu-id="99bdb-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="99bdb-129">Hello, processus de déploiement du Service d’applications rationalise tous les détails de hello, y compris la restauration des dépendances de NuGet et la création de fichiers binaires d’application hello.</span><span class="sxs-lookup"><span data-stu-id="99bdb-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="99bdb-130">Vous pouvez suivre les meilleures pratiques de contrôle de code source d’hello de gestion du code uniquement dans votre référentiel Git et permettent de déploiement du Service de l’application reste de hello prennent en charge.</span><span class="sxs-lookup"><span data-stu-id="99bdb-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="99bdb-131">Hello étapes pour pousser votre tooApp de solution Visual Studio Service sont hello même comme hello [section précédente](#overview), à condition que vous configurez votre solution et l’espace de stockage comme suit :</span><span class="sxs-lookup"><span data-stu-id="99bdb-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="99bdb-132">Utilisez hello Visual Studio source contrôle option toogenerate un `.gitignore` fichier telles que l’image hello ci-dessous ou ajoutez manuellement un `.gitignore` fichier racine du référentiel avec contenu toothis similaire [.gitignore exemple](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="99bdb-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="99bdb-133">Ajouter le référentiel de la solution entière hello répertoire arborescence tooyour, avec le fichier .sln de hello dans la racine du référentiel hello.</span><span class="sxs-lookup"><span data-stu-id="99bdb-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="99bdb-134">Après avoir configuré votre référentiel comme décrit et configuré votre application dans Azure pour la publication continue à partir d’un des référentiels de Git hello en ligne, vous pouvez développer votre application ASP.NET localement dans Visual Studio et en continu de simplement à déployer votre code en exécutant un push de votre référentiel Git en ligne de modifications tooyour.</span><span class="sxs-lookup"><span data-stu-id="99bdb-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="99bdb-135"><a name="disableCD"></a>Désactiver le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="99bdb-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="99bdb-136">déploiement continu toodisable,</span><span class="sxs-lookup"><span data-stu-id="99bdb-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="99bdb-137">Dans le panneau de menu de votre application Bonjour [portail Azure], cliquez sur **déploiement d’applications > options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="99bdb-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="99bdb-138">Puis cliquez sur **déconnexion** Bonjour **options de déploiement** panneau.</span><span class="sxs-lookup"><span data-stu-id="99bdb-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="99bdb-139">Après avoir répondu **Oui** toohello message de confirmation, vous pouvez retourner le panneau de l’application tooyour et cliquez sur **déploiement d’applications > options de déploiement** si vous souhaitez que tooset configuration d’une publication à partir d’une autre source.</span><span class="sxs-lookup"><span data-stu-id="99bdb-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="99bdb-140">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="99bdb-140">Additional Resources</span></span>
* [<span data-ttu-id="99bdb-141">Comment tooinvestigate commun émet avec un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="99bdb-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="99bdb-142">[Comment toouse PowerShell pour Azure]</span><span class="sxs-lookup"><span data-stu-id="99bdb-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="99bdb-143">[Comment toouse hello des outils de ligne de commande Azure pour Mac et Linux]</span><span class="sxs-lookup"><span data-stu-id="99bdb-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="99bdb-144">[Documentation Git]</span><span class="sxs-lookup"><span data-stu-id="99bdb-144">[Git documentation]</span></span>
* [<span data-ttu-id="99bdb-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="99bdb-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="99bdb-146">Utiliser Azure tooautomatically générer une application toodeploy une ASP.NET 4 du pipeline CI/CD</span><span class="sxs-lookup"><span data-stu-id="99bdb-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="99bdb-147">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="99bdb-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="99bdb-148">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="99bdb-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[portail Azure]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Comment toouse PowerShell pour Azure]: /powershell/azureps-cmdlets-docs
[Comment toouse hello des outils de ligne de commande Azure pour Mac et Linux]:../cli-install-nodejs.md
[Documentation Git]: http://git-scm.com/documentation

[créer un référentiel (GitHub)]: https://help.github.com/articles/create-a-repo
[créer un référentiel (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[prise en main VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
