---
title: Applications web avec Python avec Bottle dans Azure
description: "Didacticiel expliquant comment exécuter une application web Python dans Azure App Service Web Apps."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 84f043b8-9d05-479f-a9d0-d0d9a32a0bb9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: de5831defc395cd8a4033be8c1fc5dc6cbc9d683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="df043-103">Création d’applications web avec Bottle dans Azure</span><span class="sxs-lookup"><span data-stu-id="df043-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="df043-104">Ce didacticiel décrit la prise en main de l’exécution de Python dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="df043-104">This tutorial describes how to get started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="df043-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="df043-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="df043-106">À mesure que votre application croît, vous pouvez passer à un hébergement payant, et vous pouvez également intégrer l’application à tous les autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="df043-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="df043-107">Vous allez créer une application web à l’aide de l’infrastructure web Bottle (consultez d’autres versions de ce tutoriel pour [Django](web-sites-python-create-deploy-django-app.md) et [Flask](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="df043-107">You will create a web app using the Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="df043-108">Vous allez créer l’application web dans Azure Marketplace, configurer le déploiement de Git et cloner le référentiel localement.</span><span class="sxs-lookup"><span data-stu-id="df043-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="df043-109">Vous exécuterez ensuite l’application web localement, vous apporterez des modifications que vous validerez et transmettrez à [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="df043-109">Then you will run the web app locally, make changes, commit and push them to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="df043-110">Ce didacticiel vous explique comment procéder depuis Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="df043-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="df043-111">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="df043-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="df043-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="df043-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="df043-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="df043-113">Prerequisites</span></span>
* <span data-ttu-id="df043-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="df043-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="df043-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="df043-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="df043-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="df043-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="df043-117">Git</span><span class="sxs-lookup"><span data-stu-id="df043-117">Git</span></span>
* <span data-ttu-id="df043-118">[Python Tools 2.2 pour Visual Studio][Python Tools 2.2 pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="df043-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="df043-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="df043-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="df043-120">Windows</span><span class="sxs-lookup"><span data-stu-id="df043-120">Windows</span></span>
<span data-ttu-id="df043-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="df043-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="df043-122">Cette opération installe la version 32 bits de Python, setuptools, pip, virtualenv, etc. (Python 32 bits est installé sur les machines hôtes Azure).</span><span class="sxs-lookup"><span data-stu-id="df043-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="df043-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="df043-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="df043-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="df043-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="df043-125">Si vous travaillez avec Visual Studio, vous pouvez utiliser la prise en charge intégrée de Git.</span><span class="sxs-lookup"><span data-stu-id="df043-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="df043-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="df043-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="df043-127">Cette opération est facultative, mais si vous avez [Visual Studio], ainsi que la version gratuite Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, vous disposerez d’un formidable environnement de développement intégré Python.</span><span class="sxs-lookup"><span data-stu-id="df043-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="df043-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="df043-128">Mac/Linux</span></span>
<span data-ttu-id="df043-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="df043-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-the-azure-portal"></a><span data-ttu-id="df043-130">Création d’applications web sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="df043-130">Web app creation on the Azure Portal</span></span>
<span data-ttu-id="df043-131">La première étape consiste à créer l’application web par le biais du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df043-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="df043-132">Connectez-vous au portail Azure et cliquez sur le bouton **NOUVEAU** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="df043-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="df043-133">Dans le champ de recherche, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="df043-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="df043-134">Dans les résultats de recherche, sélectionnez **Bottle**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="df043-134">In the search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="df043-135">Configurez la nouvelle application Bottle en créant un nouveau plan App Service et un nouveau groupe de ressources pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="df043-135">Configure the new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="df043-136">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="df043-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="df043-137">Configurez la publication Git de votre nouvelle application web en suivant les instructions de l’article [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="df043-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="df043-138">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="df043-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="df043-139">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="df043-139">Git repository contents</span></span>
<span data-ttu-id="df043-140">Voici une vue d’ensemble des fichiers que vous trouverez dans le référentiel Git initial, que nous allons cloner dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="df043-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="df043-141">Sources principales de l’application.</span><span class="sxs-lookup"><span data-stu-id="df043-141">Main sources for the application.</span></span> <span data-ttu-id="df043-142">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="df043-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="df043-143">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="df043-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="df043-144">Prise en charge du serveur de développement local.</span><span class="sxs-lookup"><span data-stu-id="df043-144">Local development server support.</span></span> <span data-ttu-id="df043-145">Utilisez cette option pour exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="df043-145">Use this to run the application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="df043-146">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="df043-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="df043-147">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="df043-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="df043-148">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="df043-148">External packages needed by this application.</span></span> <span data-ttu-id="df043-149">Le script de déploiement installera à l’aide de pip les packages répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="df043-149">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="df043-150">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="df043-150">IIS configuration files.</span></span> <span data-ttu-id="df043-151">Le script de déploiement utilisera le fichier web.x.y.config approprié et le copiera sous le nom web.config.</span><span class="sxs-lookup"><span data-stu-id="df043-151">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="df043-152">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="df043-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="df043-153">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="df043-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="df043-154">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="df043-154">Additional files on server</span></span>
<span data-ttu-id="df043-155">Certains fichiers existent sur le serveur, mais ne sont pas ajoutés au référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="df043-155">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="df043-156">Ils sont créés par le script de déploiement.</span><span class="sxs-lookup"><span data-stu-id="df043-156">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="df043-157">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="df043-157">IIS configuration file.</span></span> <span data-ttu-id="df043-158">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="df043-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="df043-159">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="df043-159">Python virtual environment.</span></span> <span data-ttu-id="df043-160">Créé lors du déploiement si aucun environnement virtuel compatible n’existe sur le site.</span><span class="sxs-lookup"><span data-stu-id="df043-160">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span>  <span data-ttu-id="df043-161">Les packages répertoriés dans requirements.txt sont installés à l’aide de pip. Si les packages sont déjà installés, pip ignorera l’installation.</span><span class="sxs-lookup"><span data-stu-id="df043-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="df043-162">Les trois sections suivantes expliquent comment développer des applications web dans trois environnements différents :</span><span class="sxs-lookup"><span data-stu-id="df043-162">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="df043-163">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="df043-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="df043-164">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="df043-164">Windows, with command line</span></span>
* <span data-ttu-id="df043-165">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="df043-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="df043-166">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="df043-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="df043-167">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="df043-167">Clone the repository</span></span>
<span data-ttu-id="df043-168">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df043-168">First, clone the repository using the url provided on the Azure Portal.</span></span> <span data-ttu-id="df043-169">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="df043-169">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="df043-170">Ouvrez le fichier solution (.sln) inclus dans la racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="df043-170">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="df043-171">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="df043-171">Create virtual environment</span></span>
<span data-ttu-id="df043-172">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="df043-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="df043-173">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="df043-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="df043-174">Vérifiez que l’environnement porte le nom `env`.</span><span class="sxs-lookup"><span data-stu-id="df043-174">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="df043-175">Sélectionnez l’interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="df043-175">Select the base interpreter.</span></span> <span data-ttu-id="df043-176">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="df043-176">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="df043-177">Vérifiez que l’option permettant de télécharger et d’installer les packages est cochée.</span><span class="sxs-lookup"><span data-stu-id="df043-177">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="df043-178">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="df043-178">Click **Create**.</span></span> <span data-ttu-id="df043-179">Cette opération créera l’environnement virtuel et installera les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="df043-179">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="df043-180">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="df043-180">Run using development server</span></span>
<span data-ttu-id="df043-181">Appuyez sur F5 pour lancer le débogage. Votre navigateur ouvrira automatiquement la page s’exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="df043-181">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="df043-182">Vous pouvez définir des points d’arrêt dans les sources, utiliser les fenêtres de surveillance, etc. Pour plus d’informations sur les différentes fonctionnalités, consultez la [Documentation de Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="df043-182">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="df043-183">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="df043-183">Make changes</span></span>
<span data-ttu-id="df043-184">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="df043-184">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="df043-185">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="df043-185">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="df043-186">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="df043-186">Install more packages</span></span>
<span data-ttu-id="df043-187">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="df043-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="df043-188">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="df043-188">You can install additional packages using pip.</span></span> <span data-ttu-id="df043-189">Pour installer un package, cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Installer un package Python**.</span><span class="sxs-lookup"><span data-stu-id="df043-189">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="df043-190">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="df043-190">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="df043-191">Cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Générer requirements.txt** pour mettre à jour le fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="df043-191">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="df043-192">Puis validez les modifications apportées à requirements.txt dans le référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="df043-192">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="df043-193">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="df043-193">Deploy to Azure</span></span>
<span data-ttu-id="df043-194">Pour déclencher un déploiement, cliquez sur **Synchroniser** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="df043-194">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="df043-195">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="df043-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="df043-196">Le premier déploiement mettra un certain temps à s’effectuer, car il créera un environnement virtuel, installera les packages, etc.</span><span class="sxs-lookup"><span data-stu-id="df043-196">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="df043-197">Visual Studio n’affiche pas la progression du déploiement.</span><span class="sxs-lookup"><span data-stu-id="df043-197">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="df043-198">Si vous souhaitez vérifier la sortie, consultez la section [Résolution des problèmes - Déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="df043-198">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="df043-199">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="df043-199">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="df043-200">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="df043-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="df043-201">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="df043-201">Clone the repository</span></span>
<span data-ttu-id="df043-202">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="df043-202">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="df043-203">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="df043-203">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="df043-204">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="df043-204">Create virtual environment</span></span>
<span data-ttu-id="df043-205">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="df043-205">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="df043-206">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="df043-206">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="df043-207">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="df043-207">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade for your web app in the Azure Portal)</span></span>

<span data-ttu-id="df043-208">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="df043-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="df043-209">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="df043-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="df043-210">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="df043-210">Install any external packages required by your application.</span></span> <span data-ttu-id="df043-211">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="df043-211">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="df043-212">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="df043-212">Run using development server</span></span>
<span data-ttu-id="df043-213">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="df043-213">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="df043-214">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="df043-214">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="df043-215">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="df043-215">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="df043-216">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="df043-216">Make changes</span></span>
<span data-ttu-id="df043-217">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="df043-217">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="df043-218">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="df043-218">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="df043-219">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="df043-219">Install more packages</span></span>
<span data-ttu-id="df043-220">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="df043-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="df043-221">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="df043-221">You can install additional packages using pip.</span></span> <span data-ttu-id="df043-222">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="df043-222">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="df043-223">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="df043-223">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="df043-224">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="df043-224">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="df043-225">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="df043-225">Deploy to Azure</span></span>
<span data-ttu-id="df043-226">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="df043-226">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="df043-227">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="df043-227">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="df043-228">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="df043-228">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="df043-229">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="df043-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="df043-230">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="df043-230">Clone the repository</span></span>
<span data-ttu-id="df043-231">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="df043-231">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="df043-232">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="df043-232">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="df043-233">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="df043-233">Create virtual environment</span></span>
<span data-ttu-id="df043-234">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="df043-234">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="df043-235">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="df043-235">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="df043-236">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="df043-236">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="df043-237">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="df043-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="df043-238">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="df043-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="df043-239">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="df043-239">or pyvenv env</span></span>

<span data-ttu-id="df043-240">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="df043-240">Install any external packages required by your application.</span></span> <span data-ttu-id="df043-241">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="df043-241">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="df043-242">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="df043-242">Run using development server</span></span>
<span data-ttu-id="df043-243">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="df043-243">You can launch the application under a development server with the following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="df043-244">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="df043-244">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="df043-245">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="df043-245">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="df043-246">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="df043-246">Make changes</span></span>
<span data-ttu-id="df043-247">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="df043-247">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="df043-248">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="df043-248">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="df043-249">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="df043-249">Install more packages</span></span>
<span data-ttu-id="df043-250">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="df043-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="df043-251">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="df043-251">You can install additional packages using pip.</span></span> <span data-ttu-id="df043-252">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="df043-252">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="df043-253">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="df043-253">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="df043-254">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="df043-254">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="df043-255">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="df043-255">Deploy to Azure</span></span>
<span data-ttu-id="df043-256">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="df043-256">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="df043-257">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="df043-257">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="df043-258">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="df043-258">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="df043-259">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="df043-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="df043-260">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="df043-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="df043-261">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df043-261">Next Steps</span></span>
<span data-ttu-id="df043-262">Pour plus d’informations sur Bottle et Python Tools pour Visual Studio, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="df043-262">Follow these links to learn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="df043-263">[Documentation relative à Bottle]</span><span class="sxs-lookup"><span data-stu-id="df043-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="df043-264">[Documentation de Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="df043-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="df043-265">Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :</span><span class="sxs-lookup"><span data-stu-id="df043-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="df043-266">[Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="df043-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="df043-267">[Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="df043-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="df043-268">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="df043-268">What's changed</span></span>
* <span data-ttu-id="df043-269">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="df043-269">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="df043-270">[Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="df043-270">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>
<span data-ttu-id="df043-271">[Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="df043-271">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="df043-272">[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="df043-272">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="df043-273">[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="df043-273">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="df043-274">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="df043-274">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="df043-275">[Git pour Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="df043-275">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="df043-276">[GitHub pour Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="df043-276">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="df043-277">[Python Tools pour Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="df043-277">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="df043-278">[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="df043-278">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="df043-279">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="df043-279">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="df043-280">[Documentation de Python Tools pour Visual Studio]: http://aka.ms/ptvsdocs </span><span class="sxs-lookup"><span data-stu-id="df043-280">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs </span></span>
<span data-ttu-id="df043-281">[Documentation relative à Bottle]: http://bottlepy.org/docs/dev/index.html</span><span class="sxs-lookup"><span data-stu-id="df043-281">[Bottle Documentation]: http://bottlepy.org/docs/dev/index.html</span></span>

