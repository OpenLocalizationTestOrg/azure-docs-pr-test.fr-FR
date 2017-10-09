---
title: applications web aaaCreating avec ballon dans Azure
description: "Un didacticiel qui vous présente toorunning une application de web Python dans Azure."
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
ms.openlocfilehash: 3362047b3106b4380b5971e47cbd8042d38a792b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-flask-in-azure"></a><span data-ttu-id="53b5b-103">Création d’applications web avec Flask dans Azure</span><span class="sxs-lookup"><span data-stu-id="53b5b-103">Creating web apps with Flask in Azure</span></span>
<span data-ttu-id="53b5b-104">Ce didacticiel décrit comment tooget démarré Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="53b5b-104">This tutorial describes how tooget started running Python in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>  <span data-ttu-id="53b5b-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="53b5b-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span>  <span data-ttu-id="53b5b-106">Comme votre application se développe, vous pouvez basculer toopaid d’hébergement, et vous pouvez également intégrer avec tous les hello autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="53b5b-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="53b5b-107">Vous allez créer une application à l’aide hello ballon web framework (voir les autres versions de ce didacticiel pour [Django](web-sites-python-create-deploy-django-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="53b5b-107">You will create an application using hello Flask web framework (see alternate versions of this tutorial for [Django](web-sites-python-create-deploy-django-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span>  <span data-ttu-id="53b5b-108">Vous crée un site Web de hello à partir de la galerie Azure de hello, configurer le déploiement de Git et cloner le référentiel hello localement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-108">You will create hello website from hello Azure gallery, set up Git deployment, and clone hello repository locally.</span></span>  <span data-ttu-id="53b5b-109">Puis vous serez exécuté application hello localement, apporter des modifications, validez et envoyez les tooAzure.</span><span class="sxs-lookup"><span data-stu-id="53b5b-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span>  <span data-ttu-id="53b5b-110">Hello didacticiel montre comment toodo à partir de Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="53b5b-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="53b5b-111">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="53b5b-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="53b5b-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="53b5b-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="53b5b-113">Prerequisites</span></span>
* <span data-ttu-id="53b5b-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="53b5b-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="53b5b-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="53b5b-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="53b5b-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="53b5b-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="53b5b-117">Git</span><span class="sxs-lookup"><span data-stu-id="53b5b-117">Git</span></span>
* <span data-ttu-id="53b5b-118">[Python Tools pour Visual Studio][Python Tools pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="53b5b-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="53b5b-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="53b5b-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="53b5b-120">Windows</span><span class="sxs-lookup"><span data-stu-id="53b5b-120">Windows</span></span>
<span data-ttu-id="53b5b-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="53b5b-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span>  <span data-ttu-id="53b5b-122">Cela installe la version 32 bits de hello de Python, setuptools, pip, virtualenv, etc. (32 bits Python est ce qui est installé sur les ordinateurs hôte Azure hello).</span><span class="sxs-lookup"><span data-stu-id="53b5b-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span>  <span data-ttu-id="53b5b-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="53b5b-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="53b5b-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="53b5b-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span>  <span data-ttu-id="53b5b-125">Si vous utilisez Visual Studio, vous pouvez utiliser la prise en charge de Git hello intégré.</span><span class="sxs-lookup"><span data-stu-id="53b5b-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="53b5b-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="53b5b-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span>  <span data-ttu-id="53b5b-127">Cette option est facultative, mais si vous avez [Visual Studio], y compris hello libre Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, puis vous obtenez ainsi un remarquable IDE Python.</span><span class="sxs-lookup"><span data-stu-id="53b5b-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="53b5b-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="53b5b-128">Mac/Linux</span></span>
<span data-ttu-id="53b5b-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="53b5b-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-create-on-hello-azure-portal"></a><span data-ttu-id="53b5b-130">Application Web créer sur hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="53b5b-130">Web app create on hello Azure Portal</span></span>
<span data-ttu-id="53b5b-131">première étape de la création de votre application Hello est l’application web via hello toocreate hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="53b5b-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span> 

1. <span data-ttu-id="53b5b-132">Ouvrez une session hello portail Azure, puis cliquez sur hello **nouveau** bouton hello bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="53b5b-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span> 
2. <span data-ttu-id="53b5b-133">Cliquez sur **web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-133">Click **Web + Mobile**.</span></span>
3. <span data-ttu-id="53b5b-134">Dans la zone de recherche de hello, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="53b5b-134">In hello search box, type "python".</span></span>
4. <span data-ttu-id="53b5b-135">Dans les résultats de recherche de hello, sélectionnez **ballon**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-135">In hello search results, select **Flask**, then click **Create**.</span></span>
5. <span data-ttu-id="53b5b-136">Configurer nouveau ballon application hello, telles que la création d’un nouveau plan App Service et un groupe de ressources pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="53b5b-136">Configure hello new Flask app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="53b5b-137">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-137">Then, click **Create**.</span></span>
6. <span data-ttu-id="53b5b-138">Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53b5b-138">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="53b5b-139">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="53b5b-139">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="53b5b-140">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="53b5b-140">Git repository contents</span></span>
<span data-ttu-id="53b5b-141">Voici une vue d’ensemble des fichiers hello que vous trouverez dans le référentiel Git initiale hello, lequel nous allons cloner dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-141">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \FlaskWebProject\__init__.py
    \FlaskWebProject\views.py
    \FlaskWebProject\static\content\
    \FlaskWebProject\static\fonts\
    \FlaskWebProject\static\scripts\
    \FlaskWebProject\templates\about.html
    \FlaskWebProject\templates\contact.html
    \FlaskWebProject\templates\index.html
    \FlaskWebProject\templates\layout.html

<span data-ttu-id="53b5b-142">Sources principales pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-142">Main sources for hello application.</span></span>  <span data-ttu-id="53b5b-143">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="53b5b-143">Consists of 3 pages (index, about, contact) with a master layout.</span></span>  <span data-ttu-id="53b5b-144">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="53b5b-144">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \runserver.py

<span data-ttu-id="53b5b-145">Prise en charge du serveur de développement local.</span><span class="sxs-lookup"><span data-stu-id="53b5b-145">Local development server support.</span></span> <span data-ttu-id="53b5b-146">Utilisez cette application de hello toorun localement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-146">Use this toorun hello application locally.</span></span>

    \FlaskWebProject.pyproj
    \FlaskWebProject.sln

<span data-ttu-id="53b5b-147">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="53b5b-147">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="53b5b-148">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="53b5b-148">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="53b5b-149">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="53b5b-149">External packages needed by this application.</span></span> <span data-ttu-id="53b5b-150">script de déploiement Hello sera pip des packages d’installation de hello répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="53b5b-150">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="53b5b-151">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="53b5b-151">IIS configuration files.</span></span>  <span data-ttu-id="53b5b-152">script de déploiement Hello utilise web.x.y.config approprié de hello et copiez-le en tant que fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="53b5b-152">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="53b5b-153">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="53b5b-153">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-customizing-deployment](../../includes/web-sites-python-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="53b5b-154">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="53b5b-154">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="53b5b-155">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="53b5b-155">Additional files on server</span></span>
<span data-ttu-id="53b5b-156">Certains fichiers existent sur le serveur de hello mais ne sont pas ajoutés de référentiel git de toohello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-156">Some files exist on hello server but are not added toohello git repository.</span></span>  <span data-ttu-id="53b5b-157">Ceux-ci sont créés par le script de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-157">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="53b5b-158">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="53b5b-158">IIS configuration file.</span></span>  <span data-ttu-id="53b5b-159">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-159">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="53b5b-160">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="53b5b-160">Python virtual environment.</span></span>  <span data-ttu-id="53b5b-161">Si un environnement virtuel compatible n’existe pas déjà sur l’application hello, créé au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-161">Created during deployment if a compatible virtual environment doesn't already exist on hello app.</span></span>  <span data-ttu-id="53b5b-162">Packages répertoriés dans requirements.txt sont pip installé, mais pip ignorera l’installation si hello packages sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="53b5b-162">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="53b5b-163">Hello 3 sections décrivent comment tooproceed avec hello web sous 3 différents environnements le développement d’applications :</span><span class="sxs-lookup"><span data-stu-id="53b5b-163">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="53b5b-164">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="53b5b-164">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="53b5b-165">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="53b5b-165">Windows, with command line</span></span>
* <span data-ttu-id="53b5b-166">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="53b5b-166">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="53b5b-167">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53b5b-167">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="53b5b-168">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="53b5b-168">Clone hello repository</span></span>
<span data-ttu-id="53b5b-169">Tout d’abord, cloner le référentiel de hello à l’aide des URL hello fournie sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53b5b-169">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="53b5b-170">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53b5b-170">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="53b5b-171">Ouvrez le fichier de solution hello (.sln) qui est inclus dans la racine de hello du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-171">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-solution-flask.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="53b5b-172">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="53b5b-172">Create virtual environment</span></span>
<span data-ttu-id="53b5b-173">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="53b5b-173">Now we'll create a virtual environment for local development.</span></span>  <span data-ttu-id="53b5b-174">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-174">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="53b5b-175">Assurez-vous que le nom de l’environnement de hello hello est `env`.</span><span class="sxs-lookup"><span data-stu-id="53b5b-175">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="53b5b-176">Sélectionnez l’interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-176">Select hello base interpreter.</span></span>  <span data-ttu-id="53b5b-177">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="53b5b-177">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="53b5b-178">Vérifiez que hello option toodownload et installer les packages est activée.</span><span class="sxs-lookup"><span data-stu-id="53b5b-178">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="53b5b-179">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-179">Click **Create**.</span></span>  <span data-ttu-id="53b5b-180">Cela créer un environnement virtuel hello et installer les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="53b5b-180">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="53b5b-181">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="53b5b-181">Run using development server</span></span>
<span data-ttu-id="53b5b-182">Appuyez sur F5 toostart est le débogage et que votre navigateur web seront ouvre automatiquement page toohello en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-182">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

<span data-ttu-id="53b5b-183">Vous pouvez définir des points d’arrêt dans les sources de hello, utilisez hello espion, etc..  Consultez hello [outils Python pour Visual Studio Documentation] pour plus d’informations sur hello différentes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="53b5b-183">You can set breakpoints in hello sources, use hello watch windows, etc.  See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="53b5b-184">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="53b5b-184">Make changes</span></span>
<span data-ttu-id="53b5b-185">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="53b5b-185">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="53b5b-186">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="53b5b-186">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-commit-flask.png)

### <a name="install-more-packages"></a><span data-ttu-id="53b5b-187">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="53b5b-187">Install more packages</span></span>
<span data-ttu-id="53b5b-188">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="53b5b-188">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="53b5b-189">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="53b5b-189">You can install additional packages using pip.</span></span>  <span data-ttu-id="53b5b-190">tooinstall un package, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-190">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="53b5b-191">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="53b5b-191">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-install-package-dialog.png)

<span data-ttu-id="53b5b-192">Avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **générer requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="53b5b-192">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="53b5b-193">Ensuite, validez le référentiel Git toohello hello modifications toorequirements.txt.</span><span class="sxs-lookup"><span data-stu-id="53b5b-193">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="53b5b-194">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="53b5b-194">Deploy tooAzure</span></span>
<span data-ttu-id="53b5b-195">tootrigger un déploiement, cliquez sur **synchronisation** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="53b5b-195">tootrigger a deployment, click on **Sync** or **Push**.</span></span>  <span data-ttu-id="53b5b-196">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="53b5b-196">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/ptvs-git-push.png)

<span data-ttu-id="53b5b-197">premier déploiement de Hello prend un certain temps, comme il crée un environnement virtuel, les packages d’installation de périphérique.</span><span class="sxs-lookup"><span data-stu-id="53b5b-197">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="53b5b-198">Visual Studio n’affiche pas les cours hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="53b5b-198">Visual Studio doesn't show hello progress of hello deployment.</span></span>  <span data-ttu-id="53b5b-199">Si vous souhaitez que la sortie de hello tooreview, consultez la section de hello sur [dépannage - déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="53b5b-199">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="53b5b-200">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="53b5b-200">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="53b5b-201">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="53b5b-201">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="53b5b-202">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="53b5b-202">Clone hello repository</span></span>
<span data-ttu-id="53b5b-203">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="53b5b-203">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="53b5b-204">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53b5b-204">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="53b5b-205">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="53b5b-205">Create virtual environment</span></span>
<span data-ttu-id="53b5b-206">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="53b5b-206">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="53b5b-207">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-207">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="53b5b-208">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="53b5b-208">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="53b5b-209">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="53b5b-209">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="53b5b-210">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="53b5b-210">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="53b5b-211">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="53b5b-211">Install any external packages required by your application.</span></span> <span data-ttu-id="53b5b-212">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="53b5b-212">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="53b5b-213">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="53b5b-213">Run using development server</span></span>
<span data-ttu-id="53b5b-214">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="53b5b-214">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python runserver.py

<span data-ttu-id="53b5b-215">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="53b5b-215">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-run-local-flask.png)

<span data-ttu-id="53b5b-216">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="53b5b-216">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/windows-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="53b5b-217">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="53b5b-217">Make changes</span></span>
<span data-ttu-id="53b5b-218">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="53b5b-218">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="53b5b-219">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="53b5b-219">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="53b5b-220">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="53b5b-220">Install more packages</span></span>
<span data-ttu-id="53b5b-221">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="53b5b-221">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="53b5b-222">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="53b5b-222">You can install additional packages using pip.</span></span>  <span data-ttu-id="53b5b-223">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="53b5b-223">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="53b5b-224">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="53b5b-224">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="53b5b-225">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="53b5b-225">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="53b5b-226">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="53b5b-226">Deploy tooAzure</span></span>
<span data-ttu-id="53b5b-227">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="53b5b-227">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="53b5b-228">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="53b5b-228">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="53b5b-229">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="53b5b-229">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="53b5b-230">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="53b5b-230">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="53b5b-231">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="53b5b-231">Clone hello repository</span></span>
<span data-ttu-id="53b5b-232">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="53b5b-232">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="53b5b-233">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="53b5b-233">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url> 

### <a name="create-virtual-environment"></a><span data-ttu-id="53b5b-234">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="53b5b-234">Create virtual environment</span></span>
<span data-ttu-id="53b5b-235">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="53b5b-235">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span>  <span data-ttu-id="53b5b-236">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="53b5b-236">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="53b5b-237">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="53b5b-237">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="53b5b-238">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="53b5b-238">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="53b5b-239">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="53b5b-239">For Python 3.4:</span></span>

    python -m venv env
<span data-ttu-id="53b5b-240">or pyvenv env</span><span class="sxs-lookup"><span data-stu-id="53b5b-240">or pyvenv env</span></span>

<span data-ttu-id="53b5b-241">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="53b5b-241">Install any external packages required by your application.</span></span> <span data-ttu-id="53b5b-242">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="53b5b-242">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="run-using-development-server"></a><span data-ttu-id="53b5b-243">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="53b5b-243">Run using development server</span></span>
<span data-ttu-id="53b5b-244">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="53b5b-244">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python runserver.py

<span data-ttu-id="53b5b-245">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="53b5b-245">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-run-local-flask.png)

<span data-ttu-id="53b5b-246">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="53b5b-246">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-flask-app/mac-browser-flask.png)

### <a name="make-changes"></a><span data-ttu-id="53b5b-247">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="53b5b-247">Make changes</span></span>
<span data-ttu-id="53b5b-248">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="53b5b-248">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="53b5b-249">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="53b5b-249">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="53b5b-250">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="53b5b-250">Install more packages</span></span>
<span data-ttu-id="53b5b-251">Votre application peut comporter des dépendances au-delà de Python et de Flask.</span><span class="sxs-lookup"><span data-stu-id="53b5b-251">Your application may have dependencies beyond Python and Flask.</span></span>

<span data-ttu-id="53b5b-252">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="53b5b-252">You can install additional packages using pip.</span></span>  <span data-ttu-id="53b5b-253">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="53b5b-253">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="53b5b-254">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="53b5b-254">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="53b5b-255">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="53b5b-255">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="53b5b-256">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="53b5b-256">Deploy tooAzure</span></span>
<span data-ttu-id="53b5b-257">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="53b5b-257">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="53b5b-258">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="53b5b-258">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="53b5b-259">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="53b5b-259">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="53b5b-260">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="53b5b-260">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="53b5b-261">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="53b5b-261">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="53b5b-262">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53b5b-262">Next Steps</span></span>
<span data-ttu-id="53b5b-263">Suivez ces liens de toolearn plus d’informations sur ballon et les outils Python pour Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="53b5b-263">Follow these links toolearn more about Flask and Python Tools for Visual Studio:</span></span> 

* <span data-ttu-id="53b5b-264">[Documentation relative à Flask]</span><span class="sxs-lookup"><span data-stu-id="53b5b-264">[Flask Documentation]</span></span>
* <span data-ttu-id="53b5b-265">[outils Python pour Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="53b5b-265">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="53b5b-266">Pour obtenir des informations concernant l’utilisation du stockage de tables Azure et MongoDB :</span><span class="sxs-lookup"><span data-stu-id="53b5b-266">For information on using Azure Table Storage and MongoDB:</span></span>

* <span data-ttu-id="53b5b-267">[Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="53b5b-267">[Flask and MongoDB on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="53b5b-268">[Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="53b5b-268">[Flask and Azure Table Storage on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="53b5b-269">Pour plus d’informations, consultez également hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="53b5b-269">For more information, see also hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="53b5b-270">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="53b5b-270">What's changed</span></span>
* <span data-ttu-id="53b5b-271">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="53b5b-271">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Flask et MongoDB sur Azure avec Python Tools pour Visual Studio]: https://github.com/microsoft/ptvs/wiki/Flask-and-MongoDB-on-Azure
[Flask et stockage des tables Azure sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-flask-table-storage.md

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
[Documentation relative à Flask]: http://flask.pocoo.org/ 

