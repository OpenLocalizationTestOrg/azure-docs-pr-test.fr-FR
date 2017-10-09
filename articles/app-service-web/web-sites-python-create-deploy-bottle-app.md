---
title: applications web aaaPython avec Bottle dans Azure
description: "Un didacticiel qui vous présente toorunning application web Python dans Azure App Service Web Apps."
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
ms.openlocfilehash: 98acd7d8fcdbba326625121c20f9237d2663ea1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-bottle-in-azure"></a><span data-ttu-id="13df2-103">Création d’applications web avec Bottle dans Azure</span><span class="sxs-lookup"><span data-stu-id="13df2-103">Creating web apps with Bottle in Azure</span></span>
<span data-ttu-id="13df2-104">Ce didacticiel explique comment tooget démarré Python dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="13df2-104">This tutorial describes how tooget started running Python in Azure App Service Web Apps.</span></span> <span data-ttu-id="13df2-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="13df2-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="13df2-106">Comme votre application se développe, vous pouvez basculer toopaid d’hébergement, et vous pouvez également intégrer avec tous les hello autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="13df2-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="13df2-107">Vous allez créer une application web à l’aide hello Bottle web framework (voir les autres versions de ce didacticiel pour [Django](web-sites-python-create-deploy-django-app.md) et [ballon](web-sites-python-create-deploy-flask-app.md)).</span><span class="sxs-lookup"><span data-stu-id="13df2-107">You will create a web app using hello Bottle web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Flask](web-sites-python-create-deploy-flask-app.md)).</span></span> <span data-ttu-id="13df2-108">Vous crée l’application web hello de hello Azure Marketplace, configurer le déploiement de Git et cloner le référentiel hello localement.</span><span class="sxs-lookup"><span data-stu-id="13df2-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="13df2-109">Puis vous exécutez l’application hello web localement, apporter des modifications, valide et les push trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="13df2-109">Then you will run hello web app locally, make changes, commit and push them too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="13df2-110">Hello didacticiel montre comment toodo à partir de Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="13df2-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="13df2-111">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="13df2-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="13df2-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="13df2-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="13df2-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="13df2-113">Prerequisites</span></span>
* <span data-ttu-id="13df2-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="13df2-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="13df2-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="13df2-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="13df2-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="13df2-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="13df2-117">Git</span><span class="sxs-lookup"><span data-stu-id="13df2-117">Git</span></span>
* <span data-ttu-id="13df2-118">[Python Tools 2.2 pour Visual Studio][Python Tools 2.2 pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="13df2-118">[Python Tools 2.2 for Visual Studio][Python Tools 2.2 for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="13df2-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="13df2-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="13df2-120">Windows</span><span class="sxs-lookup"><span data-stu-id="13df2-120">Windows</span></span>
<span data-ttu-id="13df2-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="13df2-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="13df2-122">Cela installe la version 32 bits de hello de Python, setuptools, pip, virtualenv, etc. (32 bits Python est ce qui est installé sur les ordinateurs hôte Azure hello).</span><span class="sxs-lookup"><span data-stu-id="13df2-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="13df2-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="13df2-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="13df2-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="13df2-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="13df2-125">Si vous utilisez Visual Studio, vous pouvez utiliser la prise en charge de Git hello intégré.</span><span class="sxs-lookup"><span data-stu-id="13df2-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="13df2-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="13df2-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="13df2-127">Cette option est facultative, mais si vous avez [Visual Studio], y compris hello libre Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, puis vous obtenez ainsi un remarquable IDE Python.</span><span class="sxs-lookup"><span data-stu-id="13df2-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="13df2-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="13df2-128">Mac/Linux</span></span>
<span data-ttu-id="13df2-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="13df2-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-hello-azure-portal"></a><span data-ttu-id="13df2-130">Création d’application Web sur hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="13df2-130">Web app creation on hello Azure Portal</span></span>
<span data-ttu-id="13df2-131">première étape de la création de votre application Hello est l’application web via hello toocreate hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13df2-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>  

1. <span data-ttu-id="13df2-132">Ouvrez une session hello portail Azure, puis cliquez sur hello **nouveau** bouton hello bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="13df2-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="13df2-133">Dans la zone de recherche de hello, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="13df2-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="13df2-134">Dans les résultats de recherche de hello, sélectionnez **Bottle**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="13df2-134">In hello search results, select **Bottle**, then click **Create**.</span></span>
4. <span data-ttu-id="13df2-135">Configurer un nouvel Bottle application hello, telles que la création d’un nouveau plan App Service et un groupe de ressources pour qu’il.</span><span class="sxs-lookup"><span data-stu-id="13df2-135">Configure hello new Bottle app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="13df2-136">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="13df2-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="13df2-137">Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="13df2-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="13df2-138">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="13df2-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="13df2-139">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="13df2-139">Git repository contents</span></span>
<span data-ttu-id="13df2-140">Voici une vue d’ensemble des fichiers hello que vous trouverez dans le référentiel Git initiale hello, lequel nous allons cloner dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \routes.py
    \static\content\
    \static\fonts\
    \static\scripts\
    \views\about.tpl
    \views\contact.tpl
    \views\index.tpl
    \views\layout.tpl

<span data-ttu-id="13df2-141">Sources principales pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-141">Main sources for hello application.</span></span> <span data-ttu-id="13df2-142">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="13df2-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="13df2-143">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="13df2-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \app.py

<span data-ttu-id="13df2-144">Prise en charge du serveur de développement local.</span><span class="sxs-lookup"><span data-stu-id="13df2-144">Local development server support.</span></span> <span data-ttu-id="13df2-145">Utilisez cette application de hello toorun localement.</span><span class="sxs-lookup"><span data-stu-id="13df2-145">Use this toorun hello application locally.</span></span>

    \BottleWebProject.pyproj
    \BottleWebProject.sln

<span data-ttu-id="13df2-146">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="13df2-146">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="13df2-147">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="13df2-147">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="13df2-148">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="13df2-148">External packages needed by this application.</span></span> <span data-ttu-id="13df2-149">script de déploiement Hello sera pip des packages d’installation de hello répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="13df2-149">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="13df2-150">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="13df2-150">IIS configuration files.</span></span> <span data-ttu-id="13df2-151">script de déploiement Hello utilise web.x.y.config approprié de hello et copiez-le en tant que fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="13df2-151">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="13df2-152">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="13df2-152">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="13df2-153">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="13df2-153">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="13df2-154">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="13df2-154">Additional files on server</span></span>
<span data-ttu-id="13df2-155">Certains fichiers existent sur le serveur de hello mais ne sont pas ajoutés de référentiel git de toohello.</span><span class="sxs-lookup"><span data-stu-id="13df2-155">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="13df2-156">Ceux-ci sont créés par le script de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-156">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="13df2-157">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="13df2-157">IIS configuration file.</span></span> <span data-ttu-id="13df2-158">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="13df2-158">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="13df2-159">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="13df2-159">Python virtual environment.</span></span> <span data-ttu-id="13df2-160">Si un environnement virtuel compatible n’existe pas déjà sur l’application web de hello, créé pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="13df2-160">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span>  <span data-ttu-id="13df2-161">Packages répertoriés dans requirements.txt sont pip installé, mais pip ignorera l’installation si hello packages sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="13df2-161">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="13df2-162">Hello 3 sections décrivent comment tooproceed avec hello web sous 3 différents environnements le développement d’applications :</span><span class="sxs-lookup"><span data-stu-id="13df2-162">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="13df2-163">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="13df2-163">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="13df2-164">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="13df2-164">Windows, with command line</span></span>
* <span data-ttu-id="13df2-165">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="13df2-165">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="13df2-166">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="13df2-166">Web App development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="13df2-167">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="13df2-167">Clone hello repository</span></span>
<span data-ttu-id="13df2-168">Tout d’abord, cloner le référentiel de hello à l’aide des url hello fournie sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13df2-168">First, clone hello repository using hello url provided on hello Azure Portal.</span></span> <span data-ttu-id="13df2-169">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="13df2-169">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="13df2-170">Ouvrez le fichier de solution hello (.sln) qui est inclus dans la racine de hello du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-170">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-solution-bottle.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="13df2-171">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="13df2-171">Create virtual environment</span></span>
<span data-ttu-id="13df2-172">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="13df2-172">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="13df2-173">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="13df2-173">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="13df2-174">Assurez-vous que le nom de l’environnement de hello hello est `env`.</span><span class="sxs-lookup"><span data-stu-id="13df2-174">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="13df2-175">Sélectionnez l’interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-175">Select hello base interpreter.</span></span> <span data-ttu-id="13df2-176">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="13df2-176">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="13df2-177">Vérifiez que hello option toodownload et installer les packages est activée.</span><span class="sxs-lookup"><span data-stu-id="13df2-177">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="13df2-178">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="13df2-178">Click **Create**.</span></span> <span data-ttu-id="13df2-179">Cela créer un environnement virtuel hello et installer les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="13df2-179">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="13df2-180">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="13df2-180">Run using development server</span></span>
<span data-ttu-id="13df2-181">Appuyez sur F5 toostart est le débogage et que votre navigateur web seront ouvre automatiquement page toohello en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="13df2-181">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

<span data-ttu-id="13df2-182">Vous pouvez définir des points d’arrêt dans les sources de hello, utilisez hello espion, etc.. Consultez hello [outils Python pour Visual Studio Documentation] pour plus d’informations sur hello différentes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="13df2-182">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="13df2-183">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="13df2-183">Make changes</span></span>
<span data-ttu-id="13df2-184">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="13df2-184">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="13df2-185">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="13df2-185">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-commit-bottle.png)

### <a name="install-more-packages"></a><span data-ttu-id="13df2-186">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="13df2-186">Install more packages</span></span>
<span data-ttu-id="13df2-187">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="13df2-187">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="13df2-188">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="13df2-188">You can install additional packages using pip.</span></span> <span data-ttu-id="13df2-189">tooinstall un package, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.</span><span class="sxs-lookup"><span data-stu-id="13df2-189">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="13df2-190">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="13df2-190">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-install-package-dialog.png)

<span data-ttu-id="13df2-191">Avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **générer requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="13df2-191">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="13df2-192">Ensuite, validez le référentiel Git toohello hello modifications toorequirements.txt.</span><span class="sxs-lookup"><span data-stu-id="13df2-192">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="13df2-193">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="13df2-193">Deploy tooAzure</span></span>
<span data-ttu-id="13df2-194">tootrigger un déploiement, cliquez sur **synchronisation** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="13df2-194">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="13df2-195">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="13df2-195">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/ptvs-git-push.png)

<span data-ttu-id="13df2-196">premier déploiement de Hello prend un certain temps, comme il crée un environnement virtuel, les packages d’installation de périphérique.</span><span class="sxs-lookup"><span data-stu-id="13df2-196">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="13df2-197">Visual Studio n’affiche pas les cours hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="13df2-197">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="13df2-198">Si vous souhaitez que la sortie de hello tooreview, consultez la section de hello sur [dépannage - déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="13df2-198">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="13df2-199">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="13df2-199">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="13df2-200">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="13df2-200">Web app development - Windows - Command Line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="13df2-201">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="13df2-201">Clone hello repository</span></span>
<span data-ttu-id="13df2-202">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="13df2-202">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="13df2-203">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="13df2-203">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="13df2-204">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="13df2-204">Create virtual environment</span></span>
<span data-ttu-id="13df2-205">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="13df2-205">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="13df2-206">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="13df2-206">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="13df2-207">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application pour votre application web Bonjour Azure Portal runtime.txt ou hello)</span><span class="sxs-lookup"><span data-stu-id="13df2-207">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade for your web app in hello Azure Portal)</span></span>

<span data-ttu-id="13df2-208">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="13df2-208">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="13df2-209">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="13df2-209">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="13df2-210">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="13df2-210">Install any external packages required by your application.</span></span> <span data-ttu-id="13df2-211">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="13df2-211">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="13df2-212">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="13df2-212">Run using development server</span></span>
<span data-ttu-id="13df2-213">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="13df2-213">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python app.py

<span data-ttu-id="13df2-214">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="13df2-214">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-run-local-bottle.png)

<span data-ttu-id="13df2-215">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="13df2-215">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/windows-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="13df2-216">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="13df2-216">Make changes</span></span>
<span data-ttu-id="13df2-217">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="13df2-217">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="13df2-218">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="13df2-218">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="13df2-219">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="13df2-219">Install more packages</span></span>
<span data-ttu-id="13df2-220">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="13df2-220">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="13df2-221">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="13df2-221">You can install additional packages using pip.</span></span> <span data-ttu-id="13df2-222">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="13df2-222">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="13df2-223">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="13df2-223">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="13df2-224">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="13df2-224">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="13df2-225">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="13df2-225">Deploy tooAzure</span></span>
<span data-ttu-id="13df2-226">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="13df2-226">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="13df2-227">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="13df2-227">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="13df2-228">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="13df2-228">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="13df2-229">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="13df2-229">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="13df2-230">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="13df2-230">Clone hello repository</span></span>
<span data-ttu-id="13df2-231">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="13df2-231">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="13df2-232">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="13df2-232">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="13df2-233">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="13df2-233">Create virtual environment</span></span>
<span data-ttu-id="13df2-234">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="13df2-234">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="13df2-235">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="13df2-235">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="13df2-236">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application de votre application web Bonjour Azure Portal runtime.txt ou hello).</span><span class="sxs-lookup"><span data-stu-id="13df2-236">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="13df2-237">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="13df2-237">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="13df2-238">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="13df2-238">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="13df2-239">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="13df2-239">or pyvenv env</span></span>

<span data-ttu-id="13df2-240">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="13df2-240">Install any external packages required by your application.</span></span> <span data-ttu-id="13df2-241">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="13df2-241">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="13df2-242">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="13df2-242">Run using development server</span></span>
<span data-ttu-id="13df2-243">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="13df2-243">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python app.py

<span data-ttu-id="13df2-244">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="13df2-244">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-run-local-bottle.png)

<span data-ttu-id="13df2-245">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="13df2-245">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-bottle-app/mac-browser-bottle.png)

### <a name="make-changes"></a><span data-ttu-id="13df2-246">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="13df2-246">Make changes</span></span>
<span data-ttu-id="13df2-247">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="13df2-247">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="13df2-248">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="13df2-248">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="13df2-249">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="13df2-249">Install more packages</span></span>
<span data-ttu-id="13df2-250">Votre application peut comporter des dépendances au-delà de Python et de Bottle.</span><span class="sxs-lookup"><span data-stu-id="13df2-250">Your application may have dependencies beyond Python and Bottle.</span></span>

<span data-ttu-id="13df2-251">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="13df2-251">You can install additional packages using pip.</span></span> <span data-ttu-id="13df2-252">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="13df2-252">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="13df2-253">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="13df2-253">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="13df2-254">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="13df2-254">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="13df2-255">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="13df2-255">Deploy tooAzure</span></span>
<span data-ttu-id="13df2-256">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="13df2-256">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="13df2-257">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="13df2-257">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="13df2-258">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="13df2-258">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="13df2-259">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="13df2-259">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="13df2-260">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="13df2-260">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="13df2-261">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13df2-261">Next Steps</span></span>
<span data-ttu-id="13df2-262">Suivez ces liens de toolearn plus d’informations sur l’eau et les outils Python pour Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="13df2-262">Follow these links toolearn more about Bottle and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="13df2-263">[Documentation relative à Bottle]</span><span class="sxs-lookup"><span data-stu-id="13df2-263">[Bottle Documentation]</span></span>
* <span data-ttu-id="13df2-264">[outils Python pour Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="13df2-264">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="13df2-265">Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :</span><span class="sxs-lookup"><span data-stu-id="13df2-265">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="13df2-266">[Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="13df2-266">[Bottle and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="13df2-267">[Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="13df2-267">[Bottle and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="13df2-268">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="13df2-268">What's changed</span></span>
* <span data-ttu-id="13df2-269">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="13df2-269">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Bottle et MongoDB sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md
[Bottle et stockage de tables Azure sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-bottle-table-storage.md

<!--External Link references-->
[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git pour Windows]: http://msysgit.github.io/
[GitHub pour Windows]: https://windows.github.com/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[outils Python pour Visual Studio Documentation]: http://aka.ms/ptvsdocs 
[Documentation relative à Bottle]: http://bottlepy.org/docs/dev/index.html

