---
title: "Déploiement continu pour Azure Functions | Microsoft Docs"
description: "Utilisez les fonctionnalités de déploiement continu d’Azure App Service pour publier vos fonctions Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="88e13-103">Déploiement continu pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="88e13-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="88e13-104">Azure Functions vous permet de déployer votre Function App facilement à l’aide de l’intégration continue App Service.</span><span class="sxs-lookup"><span data-stu-id="88e13-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="88e13-105">Functions s’intègre à BitBucket, Dropbox, GitHub et Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="88e13-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="88e13-106">Cela permet d’activer un workflow dans lequel les mises à jour du code de fonctions sont effectuées à l’aide d’un de ces services intégrés qui déclenchent le déploiement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="88e13-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="88e13-107">Si vous ne connaissez pas Azure Functions, commencez par consulter l’article [Vue d’ensemble d’Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88e13-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="88e13-108">Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées.</span><span class="sxs-lookup"><span data-stu-id="88e13-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="88e13-109">Il vous permet également de conserver le contrôle de code source sur le code de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="88e13-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="88e13-110">Les sources de déploiement actuellement prises en charge sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="88e13-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="88e13-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="88e13-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="88e13-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="88e13-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="88e13-113">Référentiel externe (Git ou Mercurial)</span><span class="sxs-lookup"><span data-stu-id="88e13-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="88e13-114">Référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="88e13-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="88e13-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="88e13-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="88e13-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="88e13-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="88e13-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="88e13-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="88e13-118">Les déploiements sont configurés au cas par cas, selon les Function Apps.</span><span class="sxs-lookup"><span data-stu-id="88e13-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="88e13-119">Une fois le déploiement continu activé, l’accès au code de fonction dans le portail est défini sur *lecture seule*.</span><span class="sxs-lookup"><span data-stu-id="88e13-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="88e13-120">Conditions requises pour le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="88e13-120">Continuous deployment requirements</span></span>

<span data-ttu-id="88e13-121">Avant que vous ne configuriez le déploiement continu, votre source de déploiement doit être configurée et contenir votre code de fonctions.</span><span class="sxs-lookup"><span data-stu-id="88e13-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="88e13-122">Dans un déploiement d’application de fonction donnée, chaque fonction se trouve dans un sous-répertoire nommé, où le nom du répertoire est le nom de la fonction.</span><span class="sxs-lookup"><span data-stu-id="88e13-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="88e13-123">Configurer un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="88e13-123">Set up continuous deployment</span></span>
<span data-ttu-id="88e13-124">Utilisez cette procédure pour configurer le déploiement continu d’une Function App existante.</span><span class="sxs-lookup"><span data-stu-id="88e13-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="88e13-125">Les étapes suivantes présentent l’intégration avec un référentiel GitHub, mais des étapes similaires s’appliquent à Visual Studio Team Services ou à d’autres services de déploiement.</span><span class="sxs-lookup"><span data-stu-id="88e13-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="88e13-126">Dans votre Function App, dans le [portail Azure](https://portal.azure.com), cliquez sur **Fonctionnalités de la plate-forme** et **Options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="88e13-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="88e13-128">Puis, dans le panneau **Déploiements**, cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="88e13-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="88e13-130">Dans le panneau **Source de déploiement**, cliquez sur **Choisir une source**, entrez les informations pour la source de déploiement que vous avez choisie, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="88e13-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Choisir une source de déploiement](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="88e13-132">Une fois le déploiement continu configuré, tous les fichiers de modifications dans votre source de déploiement sont copiés vers votre Function App et un déploiement complet de site est déclenché.</span><span class="sxs-lookup"><span data-stu-id="88e13-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="88e13-133">Le site est redéployé lorsque les fichiers de la source sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="88e13-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="88e13-134">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="88e13-134">Deployment options</span></span>

<span data-ttu-id="88e13-135">Voici quelques scénarios de déploiement classiques :</span><span class="sxs-lookup"><span data-stu-id="88e13-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="88e13-136">Créer un déploiement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="88e13-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="88e13-137">Déplacer des fonctions existantes vers un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="88e13-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="88e13-138">Créer un déploiement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="88e13-138">Create a staging deployment</span></span>

<span data-ttu-id="88e13-139">Function Apps ne prend pas encore en charge les emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="88e13-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="88e13-140">Toutefois, vous pouvez tout de même gérer des déploiements intermédiaires et de production distincts à l’aide de l’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="88e13-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="88e13-141">Voici à quoi ressemble généralement le processus pour configurer et travailler avec un déploiement intermédiaire :</span><span class="sxs-lookup"><span data-stu-id="88e13-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="88e13-142">Créez deux applications de fonction dans votre abonnement, une pour le code de production et une pour le code intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="88e13-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="88e13-143">Créez une source de déploiement, si vous n’en avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="88e13-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="88e13-144">Cet exemple utilise [GitHub].</span><span class="sxs-lookup"><span data-stu-id="88e13-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="88e13-145">Pour votre Function App de production, effectuez les étapes décrites ci-dessus dans la section **Configurer un déploiement continu**, puis définissez la branche de déploiement sur la branche principale de votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="88e13-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Choisir une branche de déploiement](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="88e13-147">Répétez cette étape pour la Function App intermédiaire, mais cette fois, sélectionnez la branche intermédiaire au lieu de votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="88e13-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="88e13-148">Si votre source de déploiement ne prend pas en charge la création de branches, utilisez un autre dossier.</span><span class="sxs-lookup"><span data-stu-id="88e13-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="88e13-149">Mettez à jour votre code dans le dossier ou la branche intermédiaire, puis vérifiez que ces modifications sont répercutées dans le déploiement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="88e13-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="88e13-150">Après vérification, fusionnez les modifications de la branche intermédiaire dans la branche principale.</span><span class="sxs-lookup"><span data-stu-id="88e13-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="88e13-151">Cette opération déclenche le déploiement de la Function App de production.</span><span class="sxs-lookup"><span data-stu-id="88e13-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="88e13-152">Si votre source de déploiement ne prend pas en charge les branches, remplacez les fichiers dans le dossier de production par les fichiers du dossier intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="88e13-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="88e13-153">Déplacer des fonctions existantes pour un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="88e13-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="88e13-154">Lorsque vous disposez de fonctions existantes que vous avez créées et conservées dans le portail, vous devez télécharger vos fichiers de code de fonction existante à l’aide du FTP ou du référentiel Git local avant de pouvoir configurer le déploiement continu comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="88e13-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="88e13-155">Vous pouvez le faire dans les paramètres App Service pour votre application de fonction.</span><span class="sxs-lookup"><span data-stu-id="88e13-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="88e13-156">Une fois que vos fichiers sont téléchargés, vous pouvez les télécharger vers la source de déploiement continu que vous avez choisie.</span><span class="sxs-lookup"><span data-stu-id="88e13-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="88e13-157">Après avoir configuré l’intégration continue, vous ne serez plus en mesure de modifier vos fichiers sources dans le portail Functions.</span><span class="sxs-lookup"><span data-stu-id="88e13-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="88e13-158">Comment configurer les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="88e13-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="88e13-159">Comment télécharger des fichiers via FTP</span><span class="sxs-lookup"><span data-stu-id="88e13-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="88e13-160">Comment télécharger des fichiers via le référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="88e13-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="88e13-161">Comment configurer les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="88e13-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="88e13-162">Avant de pouvoir télécharger des fichiers à partir de votre Function App via FTP ou un référentiel Git local, vous devez configurer vos informations d’identification afin d’accéder au site.</span><span class="sxs-lookup"><span data-stu-id="88e13-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="88e13-163">Les informations d’identification sont définies au niveau de l’application de fonction.</span><span class="sxs-lookup"><span data-stu-id="88e13-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="88e13-164">Utilisez la procédure suivante pour définir les informations d’identification de déploiement dans le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="88e13-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="88e13-165">Dans votre Function App, dans le [portail Azure](https://portal.azure.com), cliquez sur **Fonctionnalités de la plate-forme** et **Informations d’identification du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="88e13-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Définir les informations d’identification de déploiement local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="88e13-167">Entrez un nom d’utilisateur et un mot de passe, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="88e13-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="88e13-168">Vous pouvez désormais utiliser ces informations d’identification pour accéder à votre application de fonction à partir du FTP ou du référentiel Git intégré.</span><span class="sxs-lookup"><span data-stu-id="88e13-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="88e13-169">Comment télécharger des fichiers via le FTP</span><span class="sxs-lookup"><span data-stu-id="88e13-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="88e13-170">Dans votre Function App, dans le [portail Azure](https://portal.azure.com), cliquez sur **Fonctionnalités de la plate-forme** et **Propriétés**, puis copiez les valeurs de **Nom d’utilisateur FTP/déploiement**, **Nom d’hôte FTP** et **Nom d’hôte FTPS**.</span><span class="sxs-lookup"><span data-stu-id="88e13-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="88e13-171">La valeur **Utilisateur FTP/déploiement** doit être entrée telle qu’elle est affichée dans le portail et inclure le nom de l’application afin de fournir le contexte approprié pour le serveur FTP.</span><span class="sxs-lookup"><span data-stu-id="88e13-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Obtenir vos informations de déploiement](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="88e13-173">À partir de votre client FTP, utilisez les informations de connexion que vous avez recueillies pour vous connecter à votre application et télécharger les fichiers sources pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="88e13-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="88e13-174">Comment télécharger des fichiers via le référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="88e13-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="88e13-175">Dans votre Function App, dans le [portail Azure](https://portal.azure.com), cliquez sur **Fonctionnalités de la plate-forme** et **Options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="88e13-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="88e13-177">Puis, dans le panneau **Déploiements**, cliquez sur **Installation**.</span><span class="sxs-lookup"><span data-stu-id="88e13-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="88e13-179">Dans le panneau **Source de déploiement**, cliquez sur **Référentiel Git local**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="88e13-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="88e13-180">Dans **Fonctionnalités de la plate-forme**, cliquez sur **Propriétés** et notez la valeur de l’URL Git.</span><span class="sxs-lookup"><span data-stu-id="88e13-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="88e13-182">Clonez le référentiel sur votre machine locale à l’aide d’une invite de commande prenant en charge Git ou de votre outil Git favori.</span><span class="sxs-lookup"><span data-stu-id="88e13-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="88e13-183">La commande de clone Git se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="88e13-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="88e13-184">Récupérez les fichiers à partir de votre application de fonction sur le clone de votre ordinateur local, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="88e13-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="88e13-185">Si nécessaire, fournissez vos [informations d’identification de déploiement configurées](#credentials).</span><span class="sxs-lookup"><span data-stu-id="88e13-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="88e13-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="88e13-186">[GitHub]: https://github.com/</span></span>
