---
title: "Foire aux questions sur le déploiement d’Azure Web Apps | Microsoft Docs"
description: "Obtenez des réponses aux questions fréquemment posées sur le déploiement de la fonctionnalité Azure Web Apps d’Azure App Service."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 69f8c50f7f5889b75544deca19c54268fbf5eca7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a><span data-ttu-id="2a9a7-103">Forum aux questions sur le déploiement de Web Apps dans Azure</span><span class="sxs-lookup"><span data-stu-id="2a9a7-103">Deployment FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="2a9a7-104">Cet article contient des réponses aux questions fréquemment posées sur les problèmes de déploiement de la [fonctionnalité Web Apps d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-104">This article has answers to frequently asked questions (FAQs) about deployment issues for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a><span data-ttu-id="2a9a7-105">Je découvre App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-105">I am just getting started with App Service web apps.</span></span> <span data-ttu-id="2a9a7-106">Comment publier mon code ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-106">How do I publish my code?</span></span>

<span data-ttu-id="2a9a7-107">Voici quelques options pour la publication de votre code d’application web :</span><span class="sxs-lookup"><span data-stu-id="2a9a7-107">Here are some options for publishing your web app code:</span></span>

*   <span data-ttu-id="2a9a7-108">Effectuer un déploiement à l’aide de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-108">Deploy by using Visual Studio.</span></span> <span data-ttu-id="2a9a7-109">Si vous disposez de la solution Visual Studio, cliquez avec le bouton droit sur le projet d’application web, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-109">If you have the Visual Studio solution, right-click the web application project, and then select **Publish**.</span></span>
*   <span data-ttu-id="2a9a7-110">Déployez à l’aide d’un client FTP.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-110">Deploy by using an FTP client.</span></span> <span data-ttu-id="2a9a7-111">Dans le portail Azure, téléchargez le profil de publication de l’application web vers laquelle vous souhaitez déployer votre code.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-111">In the Azure portal, download the publish profile for the web app that you want to deploy your code to.</span></span> <span data-ttu-id="2a9a7-112">Ensuite, chargez les fichiers dans \site\wwwroot en utilisant les informations d’identification FTP du profil de publication.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-112">Then, upload the files to \site\wwwroot by using the same publish profile FTP credentials.</span></span>

<span data-ttu-id="2a9a7-113">Pour plus d’informations, voir [Déploiement de votre application dans Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-113">For more information, see [Deploy your app to App Service](web-sites-deploy.md).</span></span>

## <a name="i-see-an-error-message-when-i-try-to-deploy-from-visual-studio-how-do-i-resolve-this"></a><span data-ttu-id="2a9a7-114">Un message d’erreur s’affiche quand je tente de déployer à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-114">I see an error message when I try to deploy from Visual Studio.</span></span> <span data-ttu-id="2a9a7-115">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-115">How do I resolve this?</span></span>

<span data-ttu-id="2a9a7-116">Un message peut indiquer que vous utilisez une ancienne version du Kit de développement logiciel (SDK).  Ce message est le suivant : « Erreur lors du déploiement pour la ressource ’NomDeVotreRessource’ du groupe de ressources ’NomDeVotreGroupeDeRessources’ : InscriptionManquantePourEmplacement : L’abonnement n’est pas inscrit pour le type de ressource « composants » à l’emplacement « Emplacement ».</span><span class="sxs-lookup"><span data-stu-id="2a9a7-116">If you see the following message, you might be using an older version of the SDK: “Error during deployment for resource 'YourResourceName' in resource group 'YourResourceGroup': MissingRegistrationForLocation: The subscription is not registered for the resource type 'components' in the location 'Central US'.</span></span> <span data-ttu-id="2a9a7-117">Renouvelez l’inscription pour ce fournisseur afin d’avoir accès à cet emplacement. »</span><span class="sxs-lookup"><span data-stu-id="2a9a7-117">Please re-register for this provider in order to have access to this location.”</span></span> 

<span data-ttu-id="2a9a7-118">Pour résoudre cette erreur, mettez à niveau vers la [dernière version du Kit de développement logiciel (SDK)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-118">To resolve this error, upgrade to the [latest SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2a9a7-119">Si vous voyez ce message et disposez de la dernière version du Kit de développement logiciel (SDK), envoyez une demande de support.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-119">If you see this message and you have the latest SDK, submit a support request.</span></span>

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-to-app-service"></a><span data-ttu-id="2a9a7-120">Comment déployer une application ASP.NET à partir de Visual Studio vers App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-120">How do I deploy an ASP.NET application from Visual Studio to App Service?</span></span>
<a id="deployasp"></a>

<span data-ttu-id="2a9a7-121">Le didacticiel [Création d’une application web ASP.NET dans Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) décrit comment déployer une application web ASP.NET vers une application web dans App Service à l’aide de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-121">The tutorial [Create your first ASP.NET web app in Azure in five minutes](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) shows you how to deploy an ASP.NET web application to a web app in App Service by using Visual Studio 2015.</span></span>

## <a name="what-are-the-different-types-of-deployment-credentials"></a><span data-ttu-id="2a9a7-122">Quelles sont les différents types d’informations d’identification de déploiement ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-122">What are the different types of deployment credentials?</span></span>

<span data-ttu-id="2a9a7-123">App Service prend en charge deux types d’informations d’identification pour le déploiement Git local et le déploiement FTP/S.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-123">App Service supports two types of credentials for local Git deployment and FTP/S deployment.</span></span> <span data-ttu-id="2a9a7-124">Pour plus d’informations sur la façon de configurer les informations d’identification de déploiement, voir [Configurer les informations d’identification de déploiement pour Azure App Service](app-service-deployment-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-124">For more information about how to configure deployment credentials, see [Configure deployment credentials for App Service](app-service-deployment-credentials.md).</span></span>

## <a name="what-is-the-file-or-directory-structure-of-my-app-service-web-app"></a><span data-ttu-id="2a9a7-125">Qu’est la structure de fichiers ou de répertoires de mon application web App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-125">What is the file or directory structure of my App Service web app?</span></span>

<span data-ttu-id="2a9a7-126">Pour plus d’informations sur la structure de fichiers de votre application App Service, voir [Structure de fichiers dans Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-126">For information about the file structure of your App Service app, see [File structure in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).</span></span>

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-the-disk-when-i-try-to-ftp-my-files"></a><span data-ttu-id="2a9a7-127">Comment résoudre l’« Erreur FTP 550 - Espace insuffisant sur le disque » lorsque j’essaie de transférer mes fichiers via FTP ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-127">How do I resolve "FTP Error 550 - There is not enough space on the disk" when I try to FTP my files?</span></span>

<span data-ttu-id="2a9a7-128">Si vous voyez ce message, il est probable que vous atteignez un quota de disque dans le plan de service pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-128">If you see this message, it's likely that you are running into a disk quota in the service plan for your web app.</span></span> <span data-ttu-id="2a9a7-129">Vous devez peut-être monter en puissance en passant à un niveau de service supérieur correspondant à vos besoins d’espace disque.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-129">You might need to scale up to a higher service tier based on your disk space needs.</span></span> <span data-ttu-id="2a9a7-130">Pour plus d’informations sur les plans de tarification et les limites de ressources, voir [Tarification de App Service](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-130">For more information about pricing plans and resource limits, see [App Service pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a><span data-ttu-id="2a9a7-131">Comment configurer un déploiement continu pour mon application web App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-131">How do I set up continuous deployment for my App Service web app?</span></span>

<span data-ttu-id="2a9a7-132">Vous pouvez configurer un déploiement continu à partir de plusieurs ressources, dont Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox et d’autres référentiels Git.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-132">You can set up continuous deployment from several resources, including Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox, and other Git repositories.</span></span> <span data-ttu-id="2a9a7-133">Ces options sont disponibles dans le portail.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-133">These options are available in the portal.</span></span> <span data-ttu-id="2a9a7-134">Le didacticiel [Déploiement continu vers App Service](app-service-continuous-deployment.md) explique comment configurer un déploiement continu.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-134">[Continuous deployment to App Service](app-service-continuous-deployment.md) is a helpful tutorial that explains how to set up continuous deployment.</span></span>

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a><span data-ttu-id="2a9a7-135">Comment résoudre les problèmes de déploiement continu à partir de GitHub et de Bitbucket ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-135">How do I troubleshoot issues with continuous deployment from GitHub and Bitbucket?</span></span>

<span data-ttu-id="2a9a7-136">Pour approfondir les problèmes liés à un déploiement continu à partir de GitHub ou de Bitbucket, voir [Analyse du déploiement continu](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-136">For help investigating issues with continuous deployment from GitHub or Bitbucket, see [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).</span></span>

## <a name="i-cant-ftp-to-my-site-and-publish-my-code-how-do-i-resolve-this"></a><span data-ttu-id="2a9a7-137">Je ne peux pas effectuer de transfert FTP vers mon site et publier mon code.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-137">I can't FTP to my site and publish my code.</span></span> <span data-ttu-id="2a9a7-138">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-138">How do I resolve this?</span></span>

<span data-ttu-id="2a9a7-139">Pour résoudre les problèmes de FTP :</span><span class="sxs-lookup"><span data-stu-id="2a9a7-139">To resolve FTP issues:</span></span>

1. <span data-ttu-id="2a9a7-140">Vérifiez que vous avez entré le nom d’hôte et les informations d’identification corrects.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-140">Verify that you are entering the correct host name and credentials.</span></span> <span data-ttu-id="2a9a7-141">Pour plus d’informations sur les différents types d’informations d’identification et leur utilisation, voir [Informations d’identification pour le déploiement](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-141">For detailed information about different types of credentials and how to use them, see [Deployment credentials](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).</span></span>
2. <span data-ttu-id="2a9a7-142">Vérifiez que les ports ne sont pas bloqués par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-142">Verify that the FTP ports are not blocked by a firewall.</span></span> <span data-ttu-id="2a9a7-143">Les ports doivent être paramétrés comme suit :</span><span class="sxs-lookup"><span data-stu-id="2a9a7-143">The ports should have these settings:</span></span>
    * <span data-ttu-id="2a9a7-144">Port de connexion de contrôle FTP : 21</span><span class="sxs-lookup"><span data-stu-id="2a9a7-144">FTP control connection port: 21</span></span>
    * <span data-ttu-id="2a9a7-145">Port de connexion de contrôle FTP : 989, 10001-10300</span><span class="sxs-lookup"><span data-stu-id="2a9a7-145">FTP data connection port: 989, 10001-10300</span></span>

## <a name="how-do-i-publish-my-code-to-app-service"></a><span data-ttu-id="2a9a7-146">Comment publier mon code sur App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-146">How do I publish my code to App Service?</span></span>

<span data-ttu-id="2a9a7-147">Le démarrage rapide Azure est conçu pour vous aider à déployer votre application à l’aide de la pile de déploiement et de la méthode de votre choix.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-147">The Azure Quickstart is designed to help you deploy your app by using the deployment stack and method of your choice.</span></span> <span data-ttu-id="2a9a7-148">Pour utiliser le démarrage rapide, dans le portail Azure, accédez à **Paramètres** > **Déploiement d’application**.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-148">To use the Quickstart, in the Azure portal, go to **Settings** > **App Deployment**.</span></span>

## <a name="why-does-my-app-sometimes-restart-after-deployment-to-app-service"></a><span data-ttu-id="2a9a7-149">Pourquoi mon application redémarre-t-elle parfois après un déploiement sur App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-149">Why does my app sometimes restart after deployment to App Service?</span></span>

<span data-ttu-id="2a9a7-150">Pour en savoir plus sur les circonstances dans lesquelles un déploiement d’application peut entraîner un redémarrage, voir [Problèmes de déploiement et d’exécution](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span><span class="sxs-lookup"><span data-stu-id="2a9a7-150">To learn about the circumstances under which an application deployment might result in a restart, see [Deployment vs. runtime issues](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts").</span></span> <span data-ttu-id="2a9a7-151">Comme décrit dans l’article, App Service déploie les fichiers dans le dossier wwwroot.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-151">As the article describes, App Service deploys files to the wwwroot folder.</span></span> <span data-ttu-id="2a9a7-152">Il ne redémarre jamais directement votre application.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-152">It never directly restarts your app.</span></span>

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a><span data-ttu-id="2a9a7-153">Comment intégrer le code de Visual Studio Team Services avec App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-153">How do I integrate Visual Studio Team Services code with App Service?</span></span>

<span data-ttu-id="2a9a7-154">Vous disposez de deux options pour l’utilisation d’un déploiement continu avec Visual Studio Team Services :</span><span class="sxs-lookup"><span data-stu-id="2a9a7-154">You have two options for using continuous deployment with Visual Studio Team Services:</span></span>

*   <span data-ttu-id="2a9a7-155">Utiliser un projet Git.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-155">Use a Git project.</span></span> <span data-ttu-id="2a9a7-156">Connectez-vous via App Service en utilisant les options de déploiement de ce référentiel.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-156">Connect via App Service by using the deployment options for that repo.</span></span>
*   <span data-ttu-id="2a9a7-157">Utiliser un projet Team Foundation Version Control (TFVC).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-157">Use a Team Foundation Version Control (TFVC) project.</span></span> <span data-ttu-id="2a9a7-158">Déployez à l’aide de l’agent de build pour App Service.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-158">Deploy by using the build agent for App Service.</span></span>

<span data-ttu-id="2a9a7-159">Le déploiement de code en continu pour ces deux options dépend des flux de travail de développeur et des procédures de vérification existants.</span><span class="sxs-lookup"><span data-stu-id="2a9a7-159">Continuous code deployment for both these options depends on existing developer workflows and check-in procedures.</span></span> <span data-ttu-id="2a9a7-160">Pour plus d’informations, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="2a9a7-160">For more information, see these articles:</span></span> 

*   [<span data-ttu-id="2a9a7-161">Implémenter un déploiement continu de votre application sur un site web Azure</span><span class="sxs-lookup"><span data-stu-id="2a9a7-161">Implement continuous deployment of your app to an Azure website</span></span>](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [<span data-ttu-id="2a9a7-162">Créer un compte Visual Studio Team Services pour pouvoir déployer vers une application web</span><span class="sxs-lookup"><span data-stu-id="2a9a7-162">Set up a Visual Studio Team Services account so it can deploy to a web app</span></span>](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-to-deploy-my-app-to-app-service"></a><span data-ttu-id="2a9a7-163">Comment utiliser FTP ou FTPS pour déployer mon application vers App Service ?</span><span class="sxs-lookup"><span data-stu-id="2a9a7-163">How do I use FTP or FTPS to deploy my app to App Service?</span></span>

<span data-ttu-id="2a9a7-164">Pour plus d’informations sur l’utilisation de FTP ou FTPS pour déployer votre application web vers App Service, voir [Déployer votre application dans Azure App Service avec FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="2a9a7-164">For information about using FTP or FTPS to deploy your web app to App Service, see [Deploy your app to App Service by using FTP/S](app-service-deploy-ftp.md).</span></span>