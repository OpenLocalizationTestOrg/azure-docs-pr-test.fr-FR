---
title: "déploiement aaaContinuous pour les fonctions de Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de déploiement continu d’Azure App Service toopublish vos fonctions de Azure."
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
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="61d47-103">Déploiement continu pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="61d47-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="61d47-104">Les fonctions Azure rend toodeploy facilement votre application de fonction à l’aide de l’intégration continue du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="61d47-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="61d47-105">Functions s’intègre à BitBucket, Dropbox, GitHub et Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="61d47-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="61d47-106">Ainsi, un flux de travail où le code de la fonction mises à jour apportée à l’aide d’un de ces tooAzure de déploiement de déclencheur de services intégrés.</span><span class="sxs-lookup"><span data-stu-id="61d47-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="61d47-107">Si vous êtes nouvelles fonctions tooAzure, commencer par [vue d’ensemble des fonctions Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61d47-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="61d47-108">Le déploiement continu est une option intéressante pour les projets auxquels plusieurs contributions fréquentes sont intégrées.</span><span class="sxs-lookup"><span data-stu-id="61d47-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="61d47-109">Il vous permet également de conserver le contrôle de code source sur le code de vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="61d47-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="61d47-110">Hello sources de déploiement suivantes est actuellement prises en charge :</span><span class="sxs-lookup"><span data-stu-id="61d47-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="61d47-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="61d47-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="61d47-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="61d47-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="61d47-113">Référentiel externe (Git ou Mercurial)</span><span class="sxs-lookup"><span data-stu-id="61d47-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="61d47-114">Référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="61d47-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="61d47-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="61d47-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="61d47-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="61d47-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="61d47-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="61d47-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="61d47-118">Les déploiements sont configurés au cas par cas, selon les Function Apps.</span><span class="sxs-lookup"><span data-stu-id="61d47-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="61d47-119">Après le déploiement continu est activé, code d’accès toofunction dans le portail de hello est défini trop*en lecture seule*.</span><span class="sxs-lookup"><span data-stu-id="61d47-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="61d47-120">Conditions requises pour le déploiement continu</span><span class="sxs-lookup"><span data-stu-id="61d47-120">Continuous deployment requirements</span></span>

<span data-ttu-id="61d47-121">Vous devez disposer de votre source de déploiement configurée et votre code de fonctions dans la source de déploiement hello avant de configurer le déploiement continu.</span><span class="sxs-lookup"><span data-stu-id="61d47-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="61d47-122">Dans un déploiement d’application de fonction donnée, chaque fonction réside dans un sous-répertoire nommé, où le nom du répertoire hello est nom hello de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="61d47-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="61d47-123">Configurer un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="61d47-123">Set up continuous deployment</span></span>
<span data-ttu-id="61d47-124">Utilisez ce déploiement continu de procédure tooconfigure pour une application existante de la fonction.</span><span class="sxs-lookup"><span data-stu-id="61d47-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="61d47-125">Les étapes suivantes présentent l’intégration avec un référentiel GitHub, mais des étapes similaires s’appliquent à Visual Studio Team Services ou à d’autres services de déploiement.</span><span class="sxs-lookup"><span data-stu-id="61d47-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="61d47-126">Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="61d47-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="61d47-128">Ensuite, dans hello **déploiements** cliquez sur le panneau **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="61d47-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="61d47-130">Bonjour **source du déploiement** panneau, cliquez sur **choisir les sources de**, puis renseignez les informations de hello pour votre source de déploiement choisie, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="61d47-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Choisir une source de déploiement](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="61d47-132">Après avoir configuré un déploiement continu, toutes les modifications de fichier dans votre source de déploiement sont copiés toohello fonction application et un déploiement de site complet est déclenché.</span><span class="sxs-lookup"><span data-stu-id="61d47-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="61d47-133">site de Hello est redéployé lors de la mise à jour des fichiers de source de hello.</span><span class="sxs-lookup"><span data-stu-id="61d47-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="61d47-134">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="61d47-134">Deployment options</span></span>

<span data-ttu-id="61d47-135">Hello Voici certains scénarios de déploiement classiques :</span><span class="sxs-lookup"><span data-stu-id="61d47-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="61d47-136">Créer un déploiement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="61d47-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="61d47-137">Déplacer le déploiement de toocontinuous fonctions existant</span><span class="sxs-lookup"><span data-stu-id="61d47-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="61d47-138">Créer un déploiement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="61d47-138">Create a staging deployment</span></span>

<span data-ttu-id="61d47-139">Function Apps ne prend pas encore en charge les emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="61d47-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="61d47-140">Toutefois, vous pouvez tout de même gérer des déploiements intermédiaires et de production distincts à l’aide de l’intégration continue.</span><span class="sxs-lookup"><span data-stu-id="61d47-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="61d47-141">Hello tooconfigure de processus et de travail avec un déploiement intermédiaire se présente généralement comme suit :</span><span class="sxs-lookup"><span data-stu-id="61d47-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="61d47-142">Créez deux applications de fonction dans votre abonnement, un pour le code de production hello et un pour la mise en lots.</span><span class="sxs-lookup"><span data-stu-id="61d47-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="61d47-143">Créez une source de déploiement, si vous n’en avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="61d47-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="61d47-144">Cet exemple utilise [GitHub].</span><span class="sxs-lookup"><span data-stu-id="61d47-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="61d47-145">Pour votre application de fonction de production, les étapes de hello complète précédente **configurer le déploiement continu** et ensemble hello déploiement branche toohello de branche de maître du référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="61d47-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Choisir une branche de déploiement](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="61d47-147">Répétez cette étape pour hello application de la fonction de mise en lots, mais choisissez hello intermédiaire à la place de branche dans votre référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="61d47-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="61d47-148">Si votre source de déploiement ne prend pas en charge la création de branches, utilisez un autre dossier.</span><span class="sxs-lookup"><span data-stu-id="61d47-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="61d47-149">Assurez-vous de mises à jour tooyour code Bonjour branche ou un dossier de mise en lots, puis vérifiez que ces modifications sont répercutées dans hello déploiement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="61d47-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="61d47-150">Après le test, fusionner des modifications à partir de hello branche de mise en lots dans la branche principale de hello.</span><span class="sxs-lookup"><span data-stu-id="61d47-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="61d47-151">Cette application de fonction fusion déclencheurs déploiement toohello production.</span><span class="sxs-lookup"><span data-stu-id="61d47-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="61d47-152">Si votre source de déploiement ne prend pas en charge les branches, remplacer les fichiers hello dans le dossier de production hello fichiers hello hello dossier intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="61d47-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="61d47-153">Déplacer le déploiement de toocontinuous fonctions existant</span><span class="sxs-lookup"><span data-stu-id="61d47-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="61d47-154">Lorsque vous disposez de fonctions existantes que vous avez créé et mis à jour dans le portail de hello, vous devez toodownload votre fonction des fichiers de code à l’aide de FTP ou hello référentiel Git local avant de pouvoir définir le déploiement continu comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="61d47-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="61d47-155">Faire cela Bonjour les paramètres du Service d’applications pour votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="61d47-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="61d47-156">Une fois que vos fichiers sont téléchargés, vous pouvez les télécharger source du déploiement continu tooyour choisi.</span><span class="sxs-lookup"><span data-stu-id="61d47-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="61d47-157">Après avoir configuré l’intégration continue, vous ne seront plus en mesure de tooedit votre source de fichiers dans le portail de fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="61d47-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="61d47-158">Comment configurer les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="61d47-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="61d47-159">Comment télécharger des fichiers via FTP</span><span class="sxs-lookup"><span data-stu-id="61d47-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="61d47-160">Comment : télécharger des fichiers à l’aide du référentiel Git hello</span><span class="sxs-lookup"><span data-stu-id="61d47-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="61d47-161">Comment configurer les informations d’identification de déploiement</span><span class="sxs-lookup"><span data-stu-id="61d47-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="61d47-162">Avant de pouvoir télécharger des fichiers à partir de votre application de fonction avec FTP ou le référentiel Git, vous devez configurer votre site de hello tooaccess informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="61d47-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="61d47-163">Informations d’identification sont définies au niveau application à la fonction hello.</span><span class="sxs-lookup"><span data-stu-id="61d47-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="61d47-164">Utilisez hello suit les informations d’identification du déploiement tooset étapes Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="61d47-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="61d47-165">Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="61d47-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Définir les informations d’identification de déploiement local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="61d47-167">Entrez un nom d’utilisateur et un mot de passe, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="61d47-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="61d47-168">Vous pouvez désormais utiliser ces informations d’identification tooaccess votre application de la fonction à partir de FTP ou hello dépôt Git intégré.</span><span class="sxs-lookup"><span data-stu-id="61d47-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="61d47-169">Comment télécharger des fichiers via le FTP</span><span class="sxs-lookup"><span data-stu-id="61d47-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="61d47-170">Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **propriétés**, puis copiez les valeurs hello pour **FTP/déploiement utilisateur**, **Nom de l’hôte FTP**, et **nom d’hôte FTPS**.</span><span class="sxs-lookup"><span data-stu-id="61d47-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="61d47-171">**Déploiement/FTP utilisateur** doit être entrée comme indiqué dans le portail hello, y compris le nom de l’application hello, tooprovide le contexte approprié pour le serveur de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="61d47-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Obtenir vos informations de déploiement](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="61d47-173">À partir de votre client FTP, utilisez les informations de connexion hello collectées tooconnect tooyour application et télécharger des fichiers de source de hello pour vos fonctions.</span><span class="sxs-lookup"><span data-stu-id="61d47-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="61d47-174">Comment télécharger des fichiers via le référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="61d47-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="61d47-175">Dans votre application de la fonction Bonjour [portail Azure](https://portal.azure.com), cliquez sur **fonctionnalités de plateforme** et **options de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="61d47-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="61d47-177">Ensuite, dans hello **déploiements** cliquez sur le panneau **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="61d47-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="61d47-179">Bonjour **source du déploiement** panneau, cliquez sur **référentiel Git Local** puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="61d47-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="61d47-180">Dans **fonctionnalités de plateforme**, cliquez sur **propriétés** et notez la valeur hello URL Git.</span><span class="sxs-lookup"><span data-stu-id="61d47-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Configurer un déploiement continu](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="61d47-182">Cloner le référentiel hello sur votre ordinateur local à l’aide d’une invite de commandes prenant en charge Git ou votre outil préféré de Git.</span><span class="sxs-lookup"><span data-stu-id="61d47-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="61d47-183">commande de clone Git de Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="61d47-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="61d47-184">Récupérer les fichiers de votre clone de toohello fonction application sur votre ordinateur local, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="61d47-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="61d47-185">Si nécessaire, fournissez vos [informations d’identification de déploiement configurées](#credentials).</span><span class="sxs-lookup"><span data-stu-id="61d47-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
