---
title: "Création d’applications web avec Flask dans Azure"
description: "Un didacticiel qui vous présente l’exécution d’une application web Python sur Azure."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: b7f4ca3a-0b52-4108-90a7-f7e07ac73da0
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/20/2016
ms.author: huvalo
ms.openlocfilehash: 29457a39ee3df0bbdbc9869cdce0e14bd85b7302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="f34de-103">Création d’applications web avec Flask dans Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="f34de-104">Ce didacticiel décrit comment exécuter Python dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f34de-104">This tutorial describes how to get started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="f34de-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="f34de-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="f34de-106">À mesure que votre application croît, vous pouvez passer à un hébergement payant, et vous pouvez également intégrer l’application à tous les autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="f34de-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="f34de-107">Vous allez créer une application à l’aide de l’infrastructure web Flask (consultez d’autres versions de ce didacticiel pour [Django](web-sites-python-create-deploy-django-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f34de-107">You will create an application using the Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="f34de-108">Vous allez créer le site web à partir de la galerie Azure, configurer le déploiement Git et cloner le référentiel localement.</span><span class="sxs-lookup"><span data-stu-id="f34de-108">You will create the website from the Azure gallery, set up Git deployment, and clone the repository locally.</span></span>  <span data-ttu-id="f34de-109">Ensuite, vous exécuterez l’application localement, puis vous apporterez des modifications que vous validerez et transmettrez à Azure.</span><span class="sxs-lookup"><span data-stu-id="f34de-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span>  <span data-ttu-id="f34de-110">Ce didacticiel vous explique comment procéder depuis Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="f34de-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f34de-111">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="f34de-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f34de-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="f34de-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f34de-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f34de-113">Prerequisites</span></span>
* <span data-ttu-id="f34de-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="f34de-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f34de-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="f34de-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f34de-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="f34de-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f34de-117">Git</span><span class="sxs-lookup"><span data-stu-id="f34de-117">Git</span></span>
* <span data-ttu-id="f34de-118">[Python Tools pour Visual Studio][Python Tools pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="f34de-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f34de-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="f34de-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f34de-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f34de-120">Windows</span></span>
<span data-ttu-id="f34de-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f34de-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="f34de-122">Cette opération installe la version 32 bits de Python, setuptools, pip, virtualenv, etc. (Python 32 bits est installé sur les machines hôtes Azure).</span><span class="sxs-lookup"><span data-stu-id="f34de-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span>  <span data-ttu-id="f34de-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="f34de-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f34de-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="f34de-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="f34de-125">Si vous travaillez avec Visual Studio, vous pouvez utiliser la prise en charge intégrée de Git.</span><span class="sxs-lookup"><span data-stu-id="f34de-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="f34de-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f34de-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="f34de-127">Cette opération est facultative, mais si vous avez [Visual Studio], ainsi que la version gratuite Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, vous disposerez d’un formidable environnement de développement intégré Python.</span><span class="sxs-lookup"><span data-stu-id="f34de-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f34de-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f34de-128">Mac/Linux</span></span>
<span data-ttu-id="f34de-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="f34de-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-the-azure-portal"></a><span data-ttu-id="f34de-130">Création d'une application web sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-130">Web app create on the Azure Portal</span></span>
<span data-ttu-id="f34de-131">La première étape consiste à créer l’application web par le biais du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f34de-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="f34de-132">Connectez-vous au portail Azure et cliquez sur le bouton **NOUVEAU** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="f34de-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span> 
2. <span data-ttu-id="f34de-133">Cliquez sur **web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="f34de-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="f34de-134">Dans le champ de recherche, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="f34de-134">In the search box, type "python".</span></span>
4. <span data-ttu-id="f34de-135">Dans les résultats de recherche, sélectionnez **Flask**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f34de-135">In the search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="f34de-136">Configurez la nouvelle application Flask en créant un nouveau plan App Service et un nouveau groupe de ressources pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="f34de-136">Configure the new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f34de-137">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f34de-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="f34de-138">Configurez la publication Git de votre nouvelle application web en suivant les instructions de l’article [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f34de-138">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f34de-139">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="f34de-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f34de-140">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="f34de-140">Git repository contents</span></span>
<span data-ttu-id="f34de-141">Voici une vue d’ensemble des fichiers que vous trouverez dans le référentiel Git initial, que nous allons cloner dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="f34de-141">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="f34de-142">Sources principales de l’application.</span><span class="sxs-lookup"><span data-stu-id="f34de-142">Main sources for the application.</span></span>  <span data-ttu-id="f34de-143">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="f34de-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="f34de-144">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="f34de-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="f34de-145">Prise en charge du serveur de développement local.</span><span class="sxs-lookup"><span data-stu-id="f34de-145">Local development server support.</span></span> <span data-ttu-id="f34de-146">Utilisez cette option pour exécuter l’application localement.</span><span class="sxs-lookup"><span data-stu-id="f34de-146">Use this to run the application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="f34de-147">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f34de-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f34de-148">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="f34de-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f34de-149">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="f34de-149">External packages needed by this application.</span></span> <span data-ttu-id="f34de-150">Le script de déploiement installera à l’aide de pip les packages répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="f34de-150">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f34de-151">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="f34de-151">IIS configuration files.</span></span>  <span data-ttu-id="f34de-152">Le script de déploiement utilisera le fichier web.x.y.config approprié et le copiera sous le nom web.config.</span><span class="sxs-lookup"><span data-stu-id="f34de-152">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f34de-153">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="f34de-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f34de-154">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="f34de-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f34de-155">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="f34de-155">Additional files on server</span></span>
<span data-ttu-id="f34de-156">Certains fichiers existent sur le serveur, mais ne sont pas ajoutés au référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="f34de-156">Some files exist on the server but are not added to the git repository.</span></span>  <span data-ttu-id="f34de-157">Ils sont créés par le script de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f34de-157">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="f34de-158">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="f34de-158">IIS configuration file.</span></span>  <span data-ttu-id="f34de-159">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="f34de-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f34de-160">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="f34de-160">Python virtual environment.</span></span>  <span data-ttu-id="f34de-161">Créé lors du déploiement si un environnement virtuel compatible n’existe pas déjà sur l’application.</span><span class="sxs-lookup"><span data-stu-id="f34de-161">Created during deployment if a compatible virtual environment doesn't already exist on the app.</span></span>  <span data-ttu-id="f34de-162">Les packages répertoriés dans requirements.txt sont installés à l’aide de pip. Si les packages sont déjà installés, pip ignorera l’installation.</span><span class="sxs-lookup"><span data-stu-id="f34de-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="f34de-163">Les trois sections suivantes expliquent comment développer des applications web dans trois environnements différents :</span><span class="sxs-lookup"><span data-stu-id="f34de-163">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="f34de-164">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="f34de-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f34de-165">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="f34de-165">Windows, with command line</span></span>
* <span data-ttu-id="f34de-166">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="f34de-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f34de-167">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f34de-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f34de-168">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="f34de-168">Clone the repository</span></span>
<span data-ttu-id="f34de-169">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f34de-169">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="f34de-170">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f34de-170">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f34de-171">Ouvrez le fichier solution (.sln) inclus dans la racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="f34de-171">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f34de-172">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f34de-172">Create virtual environment</span></span>
<span data-ttu-id="f34de-173">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="f34de-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="f34de-174">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="f34de-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f34de-175">Vérifiez que l’environnement porte le nom `env`.</span><span class="sxs-lookup"><span data-stu-id="f34de-175">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="f34de-176">Sélectionnez l’interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="f34de-176">Select the base interpreter.</span></span>  <span data-ttu-id="f34de-177">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="f34de-177">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="f34de-178">Vérifiez que l’option permettant de télécharger et d’installer les packages est cochée.</span><span class="sxs-lookup"><span data-stu-id="f34de-178">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f34de-179">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f34de-179">Click **Create**.</span></span>  <span data-ttu-id="f34de-180">Cette opération créera l’environnement virtuel et installera les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f34de-180">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f34de-181">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f34de-181">Run using development server</span></span>
<span data-ttu-id="f34de-182">Appuyez sur F5 pour lancer le débogage. Votre navigateur ouvrira automatiquement la page s’exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="f34de-182">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="f34de-183">Vous pouvez définir des points d’arrêt dans les sources, utiliser les fenêtres de surveillance, etc.  Pour plus d’informations sur les différentes fonctionnalités, consultez la [Documentation de Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f34de-183">You can set breakpoints in the sources, use the watch windows, etc.  See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f34de-184">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f34de-184">Make changes</span></span>
<span data-ttu-id="f34de-185">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="f34de-185">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f34de-186">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="f34de-186">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="f34de-187">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f34de-187">Install more packages</span></span>
<span data-ttu-id="f34de-188">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="f34de-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f34de-189">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f34de-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="f34de-190">Pour installer un package, cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Installer un package Python**.</span><span class="sxs-lookup"><span data-stu-id="f34de-190">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f34de-191">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="f34de-191">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f34de-192">Cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Générer requirements.txt** pour mettre à jour le fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f34de-192">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="f34de-193">Puis validez les modifications apportées à requirements.txt dans le référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="f34de-193">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="f34de-194">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-194">Deploy to Azure</span></span>
<span data-ttu-id="f34de-195">Pour déclencher un déploiement, cliquez sur **Synchroniser** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="f34de-195">To trigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="f34de-196">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="f34de-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="f34de-197">Le premier déploiement mettra un certain temps à s’effectuer, car il créera un environnement virtuel, installera les packages, etc.</span><span class="sxs-lookup"><span data-stu-id="f34de-197">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f34de-198">Visual Studio n’affiche pas la progression du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f34de-198">Visual Studio doesn't show the progress of the deployment.</span></span>  <span data-ttu-id="f34de-199">Si vous souhaitez vérifier la sortie, consultez la section [Résolution des problèmes - Déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f34de-199">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f34de-200">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="f34de-200">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f34de-201">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="f34de-201">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f34de-202">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="f34de-202">Clone the repository</span></span>
<span data-ttu-id="f34de-203">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="f34de-203">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="f34de-204">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f34de-204">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="f34de-205">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f34de-205">Create virtual environment</span></span>
<span data-ttu-id="f34de-206">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="f34de-206">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="f34de-207">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="f34de-207">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="f34de-208">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="f34de-208">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="f34de-209">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="f34de-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f34de-210">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="f34de-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f34de-211">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="f34de-211">Install any external packages required by your application.</span></span> <span data-ttu-id="f34de-212">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="f34de-212">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="f34de-213">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f34de-213">Run using development server</span></span>
<span data-ttu-id="f34de-214">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f34de-214">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="f34de-215">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="f34de-215">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="f34de-216">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="f34de-216">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="f34de-217">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f34de-217">Make changes</span></span>
<span data-ttu-id="f34de-218">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="f34de-218">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f34de-219">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="f34de-219">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f34de-220">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f34de-220">Install more packages</span></span>
<span data-ttu-id="f34de-221">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="f34de-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f34de-222">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f34de-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="f34de-223">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="f34de-223">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f34de-224">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="f34de-224">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f34de-225">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="f34de-225">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="f34de-226">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-226">Deploy to Azure</span></span>
<span data-ttu-id="f34de-227">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="f34de-227">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="f34de-228">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="f34de-228">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f34de-229">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="f34de-229">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f34de-230">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="f34de-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="f34de-231">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="f34de-231">Clone the repository</span></span>
<span data-ttu-id="f34de-232">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="f34de-232">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="f34de-233">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f34de-233">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="f34de-234">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f34de-234">Create virtual environment</span></span>
<span data-ttu-id="f34de-235">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="f34de-235">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span>  <span data-ttu-id="f34de-236">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="f34de-236">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="f34de-237">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="f34de-237">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="f34de-238">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="f34de-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f34de-239">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="f34de-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="f34de-240">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="f34de-240">or pyvenv env</span></span>

<span data-ttu-id="f34de-241">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="f34de-241">Install any external packages required by your application.</span></span> <span data-ttu-id="f34de-242">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="f34de-242">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="f34de-243">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f34de-243">Run using development server</span></span>
<span data-ttu-id="f34de-244">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f34de-244">You can launch the application under a development server with the following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="f34de-245">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="f34de-245">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="f34de-246">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="f34de-246">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="f34de-247">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f34de-247">Make changes</span></span>
<span data-ttu-id="f34de-248">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="f34de-248">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="f34de-249">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="f34de-249">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f34de-250">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f34de-250">Install more packages</span></span>
<span data-ttu-id="f34de-251">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="f34de-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="f34de-252">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f34de-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="f34de-253">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="f34de-253">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f34de-254">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="f34de-254">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f34de-255">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="f34de-255">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="f34de-256">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-256">Deploy to Azure</span></span>
<span data-ttu-id="f34de-257">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="f34de-257">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="f34de-258">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="f34de-258">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f34de-259">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="f34de-259">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f34de-260">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="f34de-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f34de-261">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f34de-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="f34de-262">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f34de-262">Next Steps</span></span>
<span data-ttu-id="f34de-263">Pour plus d’informations sur Flask et Python Tools pour Visual Studio, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="f34de-263">Follow these links to learn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="f34de-264">[Documentation relative à Flask]</span><span class="sxs-lookup"><span data-stu-id="f34de-264">[Flask Documentation]</span></span>
* <span data-ttu-id="f34de-265">[Documentation de Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f34de-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f34de-266">Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :</span><span class="sxs-lookup"><span data-stu-id="f34de-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="f34de-267">[Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f34de-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f34de-268">[Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f34de-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f34de-269">Pour plus d'informations, consultez également le [Centre pour développeurs Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f34de-269">For more information, see also the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f34de-270">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="f34de-270">What's changed</span></span>
* <span data-ttu-id="f34de-271">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f34de-271">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="f34de-272">[Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span><span class="sxs-lookup"><span data-stu-id="f34de-272">[Flask and MongoDB on Azure with Python Tools for Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure</span></span>
<span data-ttu-id="f34de-273">[Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span><span class="sxs-lookup"><span data-stu-id="f34de-273">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]: web-sites-python-ptvs-flask-table-storage.md</span></span>

<!--External Link references-->
<span data-ttu-id="f34de-274">[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span><span class="sxs-lookup"><span data-stu-id="f34de-274">[Azure SDK for Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281</span></span>
<span data-ttu-id="f34de-275">[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span><span class="sxs-lookup"><span data-stu-id="f34de-275">[Azure SDK for Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990</span></span>
<span data-ttu-id="f34de-276">[python.org]: http://www.python.org/</span><span class="sxs-lookup"><span data-stu-id="f34de-276">[python.org]: http://www.python.org/</span></span>
<span data-ttu-id="f34de-277">[Git pour Windows]: http://msysgit.github.io/</span><span class="sxs-lookup"><span data-stu-id="f34de-277">[Git for Windows]: http://msysgit.github.io/</span></span>
<span data-ttu-id="f34de-278">[GitHub pour Windows]: https://windows.github.com/</span><span class="sxs-lookup"><span data-stu-id="f34de-278">[GitHub for Windows]: https://windows.github.com/</span></span>
<span data-ttu-id="f34de-279">[Python Tools pour Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="f34de-279">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="f34de-280">[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="f34de-280">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="f34de-281">[Visual Studio]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="f34de-281">[Visual Studio]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="f34de-282">[Documentation de Python Tools pour Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="f34de-282">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="f34de-283">[Documentation relative à Flask]: http://flask.pocoo.org/</span><span class="sxs-lookup"><span data-stu-id="f34de-283">[Flask Documentation]: http://flask.pocoo.org/</span></span> 

