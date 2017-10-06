---
title: applications web aaaCreating avec Django dans Azure
description: "Un didacticiel qui vous présente toorunning application web Python dans Azure App Service Web Apps."
services: app-service\web
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 9be1a05a-9460-49ae-94fb-9798f82c11cf
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2016
ms.author: huvalo
ms.openlocfilehash: 26a131da358748bd6fe4ee5c114d0a8f91b83cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="f711c-103">Création d’applications web avec Django dans Azure</span><span class="sxs-lookup"><span data-stu-id="f711c-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="f711c-104">Ce didacticiel décrit comment tooget démarré Python [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f711c-104">This tutorial describes how tooget started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f711c-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="f711c-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="f711c-106">Comme votre application se développe, vous pouvez basculer toopaid d’hébergement, et vous pouvez également intégrer avec tous les hello autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="f711c-106">As your app grows, you can switch toopaid hosting, and you can also integrate with all of hello other Azure services.</span></span>

<span data-ttu-id="f711c-107">Vous allez créer une application à l’aide hello Django web framework (voir les autres versions de ce didacticiel pour [ballon](web-sites-python-create-deploy-flask-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="f711c-107">You will create an application using hello Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="f711c-108">Vous crée l’application web hello de hello Azure Marketplace, configurer le déploiement de Git et cloner le référentiel hello localement.</span><span class="sxs-lookup"><span data-stu-id="f711c-108">You will create hello web app from hello Azure Marketplace, set up Git deployment, and clone hello repository locally.</span></span> <span data-ttu-id="f711c-109">Puis vous serez exécuté application hello localement, apporter des modifications, validez et envoyez les tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f711c-109">Then you will run hello application locally, make changes, commit and push them tooAzure.</span></span> <span data-ttu-id="f711c-110">Hello didacticiel montre comment toodo à partir de Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="f711c-110">hello tutorial shows how toodo this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="f711c-111">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="f711c-111">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="f711c-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="f711c-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f711c-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f711c-113">Prerequisites</span></span>
* <span data-ttu-id="f711c-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="f711c-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="f711c-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="f711c-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="f711c-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="f711c-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="f711c-117">Git</span><span class="sxs-lookup"><span data-stu-id="f711c-117">Git</span></span>
* <span data-ttu-id="f711c-118">[Python Tools pour Visual Studio][Python Tools pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="f711c-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="f711c-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="f711c-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="f711c-120">Windows</span><span class="sxs-lookup"><span data-stu-id="f711c-120">Windows</span></span>
<span data-ttu-id="f711c-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f711c-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="f711c-122">Cela installe la version 32 bits de hello de Python, setuptools, pip, virtualenv, etc. (32 bits Python est ce qui est installé sur les ordinateurs hôte Azure hello).</span><span class="sxs-lookup"><span data-stu-id="f711c-122">This installs hello 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on hello Azure host machines).</span></span> <span data-ttu-id="f711c-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="f711c-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="f711c-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="f711c-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="f711c-125">Si vous utilisez Visual Studio, vous pouvez utiliser la prise en charge de Git hello intégré.</span><span class="sxs-lookup"><span data-stu-id="f711c-125">If you use Visual Studio, you can use hello integrated Git support.</span></span>

<span data-ttu-id="f711c-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f711c-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="f711c-127">Cette option est facultative, mais si vous avez [Visual Studio], y compris hello libre Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, puis vous obtenez ainsi un remarquable IDE Python.</span><span class="sxs-lookup"><span data-stu-id="f711c-127">This is optional, but if you have [Visual Studio], including hello free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="f711c-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="f711c-128">Mac/Linux</span></span>
<span data-ttu-id="f711c-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="f711c-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="f711c-130">Création d’une application web sur le portail</span><span class="sxs-lookup"><span data-stu-id="f711c-130">Web App Creation on Portal</span></span>
<span data-ttu-id="f711c-131">première étape de la création de votre application Hello est l’application web via hello toocreate hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f711c-131">hello first step in creating your app is toocreate hello web app via hello [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="f711c-132">Ouvrez une session hello portail Azure, puis cliquez sur hello **nouveau** bouton hello bas à gauche.</span><span class="sxs-lookup"><span data-stu-id="f711c-132">Log into hello Azure Portal and click hello **NEW** button in hello bottom left corner.</span></span>
2. <span data-ttu-id="f711c-133">Dans la zone de recherche de hello, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="f711c-133">In hello search box, type "python".</span></span>
3. <span data-ttu-id="f711c-134">Dans les résultats de recherche de hello, sélectionnez **Django** (publié par PTVS), puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="f711c-134">In hello search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="f711c-135">Configurer nouveau Django application hello, telles que la création d’un nouveau plan App Service et un groupe de ressources pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="f711c-135">Configure hello new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="f711c-136">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f711c-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="f711c-137">Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f711c-137">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="f711c-138">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="f711c-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="f711c-139">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="f711c-139">Git repository contents</span></span>
<span data-ttu-id="f711c-140">Voici une vue d’ensemble des fichiers hello que vous trouverez dans le référentiel Git initiale hello, lequel nous allons cloner dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-140">Here's an overview of hello files you'll find in hello initial Git repository, which we'll clone in hello next section.</span></span>

    \app\__init__.py
    \app\forms.py
    \app\models.py
    \app\tests.py
    \app\views.py
    \app\static\content\
    \app\static\fonts\
    \app\static\scripts\
    \app\templates\about.html
    \app\templates\contact.html
    \app\templates\index.html
    \app\templates\layout.html
    \app\templates\login.html
    \app\templates\loginpartial.html
    \DjangoWebProject\__init__.py
    \DjangoWebProject\settings.py
    \DjangoWebProject\urls.py
    \DjangoWebProject\wsgi.py

<span data-ttu-id="f711c-141">Sources principales pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-141">Main sources for hello application.</span></span> <span data-ttu-id="f711c-142">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="f711c-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="f711c-143">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="f711c-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="f711c-144">Prise en charge du serveur d’administration et de développement local.</span><span class="sxs-lookup"><span data-stu-id="f711c-144">Local management and development server support.</span></span> <span data-ttu-id="f711c-145">Utiliser cette application de hello toorun localement, synchroniser la base de données hello, etc..</span><span class="sxs-lookup"><span data-stu-id="f711c-145">Use this toorun hello application locally, synchronize hello database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="f711c-146">Base de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="f711c-146">Default database.</span></span> <span data-ttu-id="f711c-147">Inclut les tables nécessaires de hello pour hello application toorun, mais ne contient pas tous les utilisateurs (synchronisation hello toocreate de base de données utilisateur).</span><span class="sxs-lookup"><span data-stu-id="f711c-147">Includes hello necessary tables for hello application toorun, but does not contain any users (synchronize hello database toocreate a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="f711c-148">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="f711c-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="f711c-149">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="f711c-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="f711c-150">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="f711c-150">External packages needed by this application.</span></span> <span data-ttu-id="f711c-151">script de déploiement Hello sera pip des packages d’installation de hello répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="f711c-151">hello deployment script will pip install hello packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="f711c-152">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="f711c-152">IIS configuration files.</span></span> <span data-ttu-id="f711c-153">script de déploiement Hello utilise web.x.y.config approprié de hello et copiez-le en tant que fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="f711c-153">hello deployment script will use hello appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="f711c-154">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="f711c-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="f711c-155">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="f711c-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="f711c-156">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="f711c-156">Additional files on server</span></span>
<span data-ttu-id="f711c-157">Certains fichiers existent sur le serveur de hello mais ne sont pas ajoutés de référentiel git de toohello.</span><span class="sxs-lookup"><span data-stu-id="f711c-157">Some files exist on hello server but are not added toohello git repository.</span></span> <span data-ttu-id="f711c-158">Ceux-ci sont créés par le script de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-158">These are created by hello deployment script.</span></span>

    \web.config

<span data-ttu-id="f711c-159">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="f711c-159">IIS configuration file.</span></span> <span data-ttu-id="f711c-160">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="f711c-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="f711c-161">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="f711c-161">Python virtual environment.</span></span> <span data-ttu-id="f711c-162">Si un environnement virtuel compatible n’existe pas déjà sur l’application web de hello, créé pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f711c-162">Created during deployment if a compatible virtual environment doesn't already exist on hello web app.</span></span> <span data-ttu-id="f711c-163">Packages répertoriés dans requirements.txt sont pip installé, mais pip ignorera l’installation si hello packages sont déjà installés.</span><span class="sxs-lookup"><span data-stu-id="f711c-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if hello packages are already installed.</span></span>

<span data-ttu-id="f711c-164">Hello 3 sections décrivent comment tooproceed avec hello web sous 3 différents environnements le développement d’applications :</span><span class="sxs-lookup"><span data-stu-id="f711c-164">hello next 3 sections describe how tooproceed with hello web app development under 3 different environments:</span></span>

* <span data-ttu-id="f711c-165">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="f711c-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="f711c-166">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="f711c-166">Windows, with command line</span></span>
* <span data-ttu-id="f711c-167">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="f711c-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="f711c-168">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f711c-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f711c-169">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="f711c-169">Clone hello repository</span></span>
<span data-ttu-id="f711c-170">Tout d’abord, cloner le référentiel de hello à l’aide des URL hello fournie sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f711c-170">First, clone hello repository using hello URL provided on hello Azure Portal.</span></span> <span data-ttu-id="f711c-171">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f711c-171">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="f711c-172">Ouvrez le fichier de solution hello (.sln) qui est inclus dans la racine de hello du référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-172">Open hello solution file (.sln) that is included in hello root of hello repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="f711c-173">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f711c-173">Create virtual environment</span></span>
<span data-ttu-id="f711c-174">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="f711c-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="f711c-175">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="f711c-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="f711c-176">Assurez-vous que le nom de l’environnement de hello hello est `env`.</span><span class="sxs-lookup"><span data-stu-id="f711c-176">Make sure hello name of hello environment is `env`.</span></span>
* <span data-ttu-id="f711c-177">Sélectionnez l’interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-177">Select hello base interpreter.</span></span> <span data-ttu-id="f711c-178">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans runtime.txt ou hello **paramètres de l’Application** Panneau de votre application web Bonjour portail Azure).</span><span class="sxs-lookup"><span data-stu-id="f711c-178">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello **Application Settings** blade of your web app in hello Azure Portal).</span></span>
* <span data-ttu-id="f711c-179">Vérifiez que hello option toodownload et installer les packages est activée.</span><span class="sxs-lookup"><span data-stu-id="f711c-179">Make sure hello option toodownload and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="f711c-180">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f711c-180">Click **Create**.</span></span> <span data-ttu-id="f711c-181">Cela créer un environnement virtuel hello et installer les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f711c-181">This will create hello virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="f711c-182">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="f711c-182">Create a superuser</span></span>
<span data-ttu-id="f711c-183">base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini.</span><span class="sxs-lookup"><span data-stu-id="f711c-183">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f711c-184">Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f711c-184">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f711c-185">Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :</span><span class="sxs-lookup"><span data-stu-id="f711c-185">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f711c-186">Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..</span><span class="sxs-lookup"><span data-stu-id="f711c-186">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f711c-187">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f711c-187">Run using development server</span></span>
<span data-ttu-id="f711c-188">Appuyez sur F5 toostart est le débogage et que votre navigateur web seront ouvre automatiquement page toohello en cours d’exécution localement.</span><span class="sxs-lookup"><span data-stu-id="f711c-188">Press F5 toostart debugging, and your web browser will open automatically toohello page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="f711c-189">Vous pouvez définir des points d’arrêt dans les sources de hello, utilisez hello espion, etc.. Consultez hello [outils Python pour Visual Studio Documentation] pour plus d’informations sur hello différentes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f711c-189">You can set breakpoints in hello sources, use hello watch windows, etc. See hello [Python Tools for Visual Studio Documentation] for more information on hello various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="f711c-190">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f711c-190">Make changes</span></span>
<span data-ttu-id="f711c-191">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="f711c-191">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f711c-192">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="f711c-192">After you've tested your changes, commit them toohello Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="f711c-193">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f711c-193">Install more packages</span></span>
<span data-ttu-id="f711c-194">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="f711c-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f711c-195">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f711c-195">You can install additional packages using pip.</span></span> <span data-ttu-id="f711c-196">tooinstall un package, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.</span><span class="sxs-lookup"><span data-stu-id="f711c-196">tooinstall a package, right-click on hello virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="f711c-197">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="f711c-197">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="f711c-198">Avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **générer requirements.txt** tooupdate requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f711c-198">Right-click on hello virtual environment and select **Generate requirements.txt** tooupdate requirements.txt.</span></span>

<span data-ttu-id="f711c-199">Ensuite, validez le référentiel Git toohello hello modifications toorequirements.txt.</span><span class="sxs-lookup"><span data-stu-id="f711c-199">Then, commit hello changes toorequirements.txt toohello Git repository.</span></span>

### <a name="deploy-tooazure"></a><span data-ttu-id="f711c-200">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="f711c-200">Deploy tooAzure</span></span>
<span data-ttu-id="f711c-201">tootrigger un déploiement, cliquez sur **synchronisation** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="f711c-201">tootrigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="f711c-202">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="f711c-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="f711c-203">premier déploiement de Hello prend un certain temps, comme il crée un environnement virtuel, les packages d’installation de périphérique.</span><span class="sxs-lookup"><span data-stu-id="f711c-203">hello first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="f711c-204">Visual Studio n’affiche pas les cours hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-204">Visual Studio doesn't show hello progress of hello deployment.</span></span> <span data-ttu-id="f711c-205">Si vous souhaitez que la sortie de hello tooreview, consultez la section de hello sur [dépannage - déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="f711c-205">If you'd like tooreview hello output, see hello section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="f711c-206">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f711c-206">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="f711c-207">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="f711c-207">Web app development - Windows - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f711c-208">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="f711c-208">Clone hello repository</span></span>
<span data-ttu-id="f711c-209">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="f711c-209">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f711c-210">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f711c-210">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f711c-211">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f711c-211">Create virtual environment</span></span>
<span data-ttu-id="f711c-212">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="f711c-212">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f711c-213">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="f711c-213">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f711c-214">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application de votre application web Bonjour Azure Portal runtime.txt ou hello).</span><span class="sxs-lookup"><span data-stu-id="f711c-214">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f711c-215">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="f711c-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="f711c-216">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="f711c-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="f711c-217">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="f711c-217">Install any external packages required by your application.</span></span> <span data-ttu-id="f711c-218">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="f711c-218">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f711c-219">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="f711c-219">Create a superuser</span></span>
<span data-ttu-id="f711c-220">base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini.</span><span class="sxs-lookup"><span data-stu-id="f711c-220">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f711c-221">Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f711c-221">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f711c-222">Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :</span><span class="sxs-lookup"><span data-stu-id="f711c-222">Run this from hello command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="f711c-223">Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..</span><span class="sxs-lookup"><span data-stu-id="f711c-223">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f711c-224">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f711c-224">Run using development server</span></span>
<span data-ttu-id="f711c-225">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f711c-225">You can launch hello application under a development server with hello following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="f711c-226">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="f711c-226">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="f711c-227">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="f711c-227">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f711c-228">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f711c-228">Make changes</span></span>
<span data-ttu-id="f711c-229">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="f711c-229">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f711c-230">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="f711c-230">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f711c-231">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f711c-231">Install more packages</span></span>
<span data-ttu-id="f711c-232">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="f711c-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f711c-233">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f711c-233">You can install additional packages using pip.</span></span> <span data-ttu-id="f711c-234">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="f711c-234">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="f711c-235">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="f711c-235">Make sure tooupdate requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="f711c-236">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="f711c-236">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f711c-237">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="f711c-237">Deploy tooAzure</span></span>
<span data-ttu-id="f711c-238">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="f711c-238">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f711c-239">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="f711c-239">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f711c-240">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f711c-240">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="f711c-241">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="f711c-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-hello-repository"></a><span data-ttu-id="f711c-242">Référentiel de hello clone</span><span class="sxs-lookup"><span data-stu-id="f711c-242">Clone hello repository</span></span>
<span data-ttu-id="f711c-243">Tout d’abord, cloner le référentiel hello à l’aide des URL hello fournie sur hello portail Azure, puis ajoutez hello Azure référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="f711c-243">First, clone hello repository using hello URL provided on hello Azure Portal, and add hello Azure repository as a remote.</span></span> <span data-ttu-id="f711c-244">Pour plus d’informations, consultez [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f711c-244">For more information, see [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="f711c-245">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f711c-245">Create virtual environment</span></span>
<span data-ttu-id="f711c-246">Nous allons créer un nouvel environnement virtuel pour le développement (ne l’ajoutez pas toohello référentiel).</span><span class="sxs-lookup"><span data-stu-id="f711c-246">We'll create a new virtual environment for development purposes (do not add it toohello repository).</span></span> <span data-ttu-id="f711c-247">Environnements virtuels dans Python ne sont pas transférable, chaque développeur travaille sur une application hello allez donc créer leur propres localement.</span><span class="sxs-lookup"><span data-stu-id="f711c-247">Virtual environments in Python are not relocatable, so every developer working on hello application will create their own locally.</span></span>

<span data-ttu-id="f711c-248">Assurez-vous que toouse hello même version de Python est sélectionné pour votre application web (dans le panneau Paramètres de l’Application de votre application web Bonjour Azure Portal runtime.txt ou hello).</span><span class="sxs-lookup"><span data-stu-id="f711c-248">Make sure toouse hello same version of Python that is selected for your web app (in runtime.txt or hello Application Settings blade of your web app in hello Azure Portal).</span></span>

<span data-ttu-id="f711c-249">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="f711c-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="f711c-250">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="f711c-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="f711c-251">ou</span><span class="sxs-lookup"><span data-stu-id="f711c-251">or</span></span>

    pyvenv env

<span data-ttu-id="f711c-252">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="f711c-252">Install any external packages required by your application.</span></span> <span data-ttu-id="f711c-253">Vous pouvez utiliser le fichier de requirements.txt hello à racine hello hello référentiel tooinstall hello des packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="f711c-253">You can use hello requirements.txt file at hello root of hello repository tooinstall hello packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="f711c-254">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="f711c-254">Create a superuser</span></span>
<span data-ttu-id="f711c-255">base de données Hello inclus avec l’application hello n’a pas de n’importe quel superutilisateur défini.</span><span class="sxs-lookup"><span data-stu-id="f711c-255">hello database included with hello application does not have any superuser defined.</span></span> <span data-ttu-id="f711c-256">Dans l’ordre toouse hello fonctionnalité de connexion dans l’application hello ou l’interface d’administration hello Django (si vous décidez de tooenable il), vous devez toocreate un super utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f711c-256">In order toouse hello sign-in functionality in hello application, or hello Django admin interface (if you decide tooenable it), you'll need toocreate a superuser.</span></span>

<span data-ttu-id="f711c-257">Exécutez ceci à partir hello de ligne de commande à partir de votre dossier de projet :</span><span class="sxs-lookup"><span data-stu-id="f711c-257">Run this from hello command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="f711c-258">Suivez le nom d’utilisateur hello invites tooset hello, mot de passe, etc..</span><span class="sxs-lookup"><span data-stu-id="f711c-258">Follow hello prompts tooset hello user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="f711c-259">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="f711c-259">Run using development server</span></span>
<span data-ttu-id="f711c-260">Vous pouvez lancer l’application hello sous un serveur de développement avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f711c-260">You can launch hello application under a development server with hello following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="f711c-261">Hello console affiche hello URL et port hello serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="f711c-261">hello console will display hello URL and port hello server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="f711c-262">Ensuite, ouvrez votre URL toothat du navigateur web.</span><span class="sxs-lookup"><span data-stu-id="f711c-262">Then, open your web browser toothat URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="f711c-263">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="f711c-263">Make changes</span></span>
<span data-ttu-id="f711c-264">Maintenant, vous pouvez tester en apportant des modifications toohello application sources et/ou des modèles.</span><span class="sxs-lookup"><span data-stu-id="f711c-264">Now you can experiment by making changes toohello application sources and/or templates.</span></span>

<span data-ttu-id="f711c-265">Une fois que vous avez testé vos modifications, les valider toohello Git référentiel :</span><span class="sxs-lookup"><span data-stu-id="f711c-265">After you've tested your changes, commit them toohello Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="f711c-266">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="f711c-266">Install more packages</span></span>
<span data-ttu-id="f711c-267">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="f711c-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="f711c-268">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="f711c-268">You can install additional packages using pip.</span></span> <span data-ttu-id="f711c-269">Par exemple, tooinstall hello Azure SDK pour Python, ce qui vous donne accès tooAzure stockage, service bus et autres services Azure, le type :</span><span class="sxs-lookup"><span data-stu-id="f711c-269">For example, tooinstall hello Azure SDK for Python, which gives you access tooAzure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="f711c-270">Assurez-vous que tooupdate requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="f711c-270">Make sure tooupdate requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="f711c-271">Valider les modifications de hello :</span><span class="sxs-lookup"><span data-stu-id="f711c-271">Commit hello changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-tooazure"></a><span data-ttu-id="f711c-272">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="f711c-272">Deploy tooAzure</span></span>
<span data-ttu-id="f711c-273">tootrigger un déploiement, hello de push modifie tooAzure :</span><span class="sxs-lookup"><span data-stu-id="f711c-273">tootrigger a deployment, push hello changes tooAzure:</span></span>

    git push azure master

<span data-ttu-id="f711c-274">Vous verrez un résultat de hello du script de déploiement hello, y compris la création d’un environnement virtuel, l’installation des packages, la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="f711c-274">You will see hello output of hello deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="f711c-275">Accédez à toohello URL Azure tooview vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f711c-275">Browse toohello Azure URL tooview your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="f711c-276">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="f711c-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="f711c-277">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="f711c-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="f711c-278">Résolution des problèmes - Fichiers statiques</span><span class="sxs-lookup"><span data-stu-id="f711c-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="f711c-279">Django a un concept hello de collecte de fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="f711c-279">Django has hello concept of collecting static files.</span></span> <span data-ttu-id="f711c-280">Cela prend tous les fichiers statiques hello à partir de leur emplacement d’origine et les copie tooa seul dossier.</span><span class="sxs-lookup"><span data-stu-id="f711c-280">This takes all hello static files from their original location and copies them tooa single folder.</span></span> <span data-ttu-id="f711c-281">Pour cette application, ils sont copiés trop`/static`.</span><span class="sxs-lookup"><span data-stu-id="f711c-281">For this application, they are copied too`/static`.</span></span>

<span data-ttu-id="f711c-282">Cette opération est effectuée, car les fichiers statiques peuvent provenir de différentes applications Django.</span><span class="sxs-lookup"><span data-stu-id="f711c-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="f711c-283">Par exemple, les fichiers statiques hello à partir des interfaces d’administration hello Django se trouvent dans un sous-dossier de la bibliothèque Django dans un environnement virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-283">For example, hello static files from hello Django admin interfaces are located in a Django library subfolder in hello virtual environment.</span></span> <span data-ttu-id="f711c-284">Les fichiers statiques définis par cette application se trouvent dans `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="f711c-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="f711c-285">Plus vous utiliserez d’applications Django, plus vous aurez de fichiers statiques dans différents emplacements.</span><span class="sxs-lookup"><span data-stu-id="f711c-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="f711c-286">Lorsque vous exécutez l’application hello en mode débogage, application hello prend en charge hello des fichiers statiques à partir de leur emplacement d’origine.</span><span class="sxs-lookup"><span data-stu-id="f711c-286">When running hello application in debug mode, hello application serves hello static files from their original location.</span></span>

<span data-ttu-id="f711c-287">Lorsque vous exécutez l’application hello en mode version finale, application hello est **pas** hello les fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="f711c-287">When running hello application in release mode, hello application does **not** serve hello static files.</span></span> <span data-ttu-id="f711c-288">Il incombe hello des fichiers de hello tooserve hello web server.</span><span class="sxs-lookup"><span data-stu-id="f711c-288">It is hello responsibility of hello web server tooserve hello files.</span></span> <span data-ttu-id="f711c-289">Pour cette application, IIS servira à partir des fichiers statiques hello `/static`.</span><span class="sxs-lookup"><span data-stu-id="f711c-289">For this application, IIS will serve hello static files from `/static`.</span></span>

<span data-ttu-id="f711c-290">collection de Hello des fichiers statiques s’effectue automatiquement en tant que fichiers de la partie du script de déploiement hello, effacement précédemment collecté.</span><span class="sxs-lookup"><span data-stu-id="f711c-290">hello collection of static files is done automatically as part of hello deployment script, clearing previously collected files.</span></span> <span data-ttu-id="f711c-291">Cela signifie la collecte de hello se produit sur chaque déploiement, ralentir de déploiement, mais il garantit que les fichiers obsolètes n’est pas disponibles, ce qui évite d’un problème de sécurité potentiel.</span><span class="sxs-lookup"><span data-stu-id="f711c-291">This means hello collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="f711c-292">Si vous souhaitez collection tooskip des fichiers statiques pour votre application Django :</span><span class="sxs-lookup"><span data-stu-id="f711c-292">If you want tooskip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="f711c-293">Vous devez collection de hello toodo manuellement sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="f711c-293">Then you'll need toodo hello collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="f711c-294">Puis supprimez hello `\static` dossier `.gitignore` et ajoutez-le référentiel Git de toohello.</span><span class="sxs-lookup"><span data-stu-id="f711c-294">Then remove hello `\static` folder from `.gitignore` and add it toohello Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="f711c-295">Résolution des problèmes - Paramètres</span><span class="sxs-lookup"><span data-stu-id="f711c-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="f711c-296">Différents paramètres d’application hello peuvent être modifiées dans `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="f711c-296">Various settings for hello application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="f711c-297">Pour simplifier le développement, le mode débogage est activé.</span><span class="sxs-lookup"><span data-stu-id="f711c-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="f711c-298">Un effet secondaire intéressant de qui est que vous serez en mesure de toosee images et autre contenu statique lors de l’exécution localement, sans avoir toocollect des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="f711c-298">One nice side effect of that is you'll be able toosee images and other static content when running locally, without having toocollect static files.</span></span>

<span data-ttu-id="f711c-299">mode de débogage toodisable :</span><span class="sxs-lookup"><span data-stu-id="f711c-299">toodisable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="f711c-300">Lorsque le débogage est désactivé, hello valeur pour `ALLOWED_HOSTS` besoins toobe mis à jour le nom de l’hôte Azure tooinclude hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-300">When debug is disabled, hello value for `ALLOWED_HOSTS` needs toobe updated tooinclude hello Azure host name.</span></span> <span data-ttu-id="f711c-301">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f711c-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="f711c-302">ou tooenable tout :</span><span class="sxs-lookup"><span data-stu-id="f711c-302">or tooenable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="f711c-303">Dans la pratique, vous souhaiterez toodo toodeal plus complexe avec le changement entre déboguer et le mode et le nom d’hôte hello lors de l’obtention de la version.</span><span class="sxs-lookup"><span data-stu-id="f711c-303">In practice, you may want toodo something more complex toodeal with switching between debug and release mode, and getting hello host name.</span></span>

<span data-ttu-id="f711c-304">Vous pouvez définir des variables d’environnement via le portail Azure de hello **configurer** page hello **paramètres de l’application** section.</span><span class="sxs-lookup"><span data-stu-id="f711c-304">You can set environment variables through hello Azure portal **CONFIGURE** page, in hello **app settings** section.</span></span>  <span data-ttu-id="f711c-305">Cela peut être utile pour définir les valeurs que vous ne souhaitez pas tooappear dans les sources de hello (chaînes de connexion, les mots de passe, etc.), ou que vous souhaitez tooset différemment entre Azure et sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f711c-305">This can be useful for setting values that you may not want tooappear in hello sources (connection strings, passwords, etc), or that you want tooset differently between Azure and your local machine.</span></span> <span data-ttu-id="f711c-306">Dans `settings.py`, vous pouvez interroger les variables d’environnement hello à l’aide de `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="f711c-306">In `settings.py`, you can query hello environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="f711c-307">Utilisation d’une base de données</span><span class="sxs-lookup"><span data-stu-id="f711c-307">Using a Database</span></span>
<span data-ttu-id="f711c-308">base de données Hello est inclus dans l’application hello est une base de données sqlite.</span><span class="sxs-lookup"><span data-stu-id="f711c-308">hello database that is included with hello application is a sqlite database.</span></span> <span data-ttu-id="f711c-309">Il s’agit d’un toouse de la base de données par défaut pratique et utile pour le développement, car il nécessite presque sans le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="f711c-309">This is a convenient and useful default database toouse for development, as it requires almost no setup.</span></span> <span data-ttu-id="f711c-310">base de données Hello est stocké dans le fichier de db.sqlite3 hello dans le dossier de projet hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-310">hello database is stored in hello db.sqlite3 file in hello project folder.</span></span>

<span data-ttu-id="f711c-311">Azure fournit des services de base de données qui sont toouse facile à partir d’une application Django.</span><span class="sxs-lookup"><span data-stu-id="f711c-311">Azure provides database services which are easy toouse from a Django application.</span></span> <span data-ttu-id="f711c-312">Didacticiels pour l’utilisation de [base de données SQL] et [MySQL] à partir d’une application de Django afficher les étapes de hello service de base de données hello toocreate nécessaire, de modifier les paramètres de base de données hello dans `DjangoWebProject/settings.py`et hello bibliothèques requis tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f711c-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show hello steps necessary toocreate hello database service, change hello database settings in `DjangoWebProject/settings.py`, and hello libraries required tooinstall.</span></span>

<span data-ttu-id="f711c-313">Bien entendu, si vous préférez toomanage vos propres serveurs de base de données, vous pouvez effectuer à l’aide de Windows ou Linux des machines virtuelles s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f711c-313">Of course, if you prefer toomanage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="f711c-314">Interface d’administration Django</span><span class="sxs-lookup"><span data-stu-id="f711c-314">Django Admin Interface</span></span>
<span data-ttu-id="f711c-315">Une fois que vous démarrez la création de vos modèles, vous souhaiterez toopopulate de la base de données hello avec des données.</span><span class="sxs-lookup"><span data-stu-id="f711c-315">Once you start building your models, you'll want toopopulate hello database with some data.</span></span> <span data-ttu-id="f711c-316">Facilement toodo ajouter et modifier interactivement le contenu est l’interface d’administration Django toouse hello.</span><span class="sxs-lookup"><span data-stu-id="f711c-316">An easy way toodo add and edit content interactively is toouse hello Django administration interface.</span></span>

<span data-ttu-id="f711c-317">code Hello pour l’interface d’administration hello est commentée dans les sources d’application hello, mais elle est marquée clairement afin de vous pouvez facilement activer (recherchez « admin »).</span><span class="sxs-lookup"><span data-stu-id="f711c-317">hello code for hello admin interface is commented out in hello application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="f711c-318">Une fois qu’il est activé, synchroniser hello de base de données, exécutez l’application hello et accédez trop`/admin`.</span><span class="sxs-lookup"><span data-stu-id="f711c-318">After it's enabled, synchronize hello database, run hello application and navigate too`/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f711c-319">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f711c-319">Next Steps</span></span>
<span data-ttu-id="f711c-320">Suivez ces liens de toolearn plus d’informations sur les Django et les outils Python pour Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="f711c-320">Follow these links toolearn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="f711c-321">[Documentation Django]</span><span class="sxs-lookup"><span data-stu-id="f711c-321">[Django Documentation]</span></span>
* <span data-ttu-id="f711c-322">[outils Python pour Visual Studio Documentation]</span><span class="sxs-lookup"><span data-stu-id="f711c-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="f711c-323">Pour plus d’informations sur l’utilisation de Base de données SQL et de MySQL :</span><span class="sxs-lookup"><span data-stu-id="f711c-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="f711c-324">[Django et MySQL sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f711c-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="f711c-325">[Django et SQL Database sur Azure avec Python pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="f711c-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="f711c-326">Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="f711c-326">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="f711c-327">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="f711c-327">What's changed</span></span>
* <span data-ttu-id="f711c-328">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="f711c-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django et MySQL sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django et SQL Database sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-django-sql.md
[base de données SQL]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

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
[Documentation Django]: https://www.djangoproject.com/
