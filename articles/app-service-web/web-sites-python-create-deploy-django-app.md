---
title: "Création d’applications web avec Django dans Azure"
description: "Didacticiel expliquant comment exécuter une application web Python dans Azure App Service Web Apps."
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
ms.openlocfilehash: 388a2db21dd1669b48b3204aaa322d7915905506
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-web-apps-with-django-in-azure"></a><span data-ttu-id="c1283-103">Création d’applications web avec Django dans Azure</span><span class="sxs-lookup"><span data-stu-id="c1283-103">Creating web apps with Django in Azure</span></span>
<span data-ttu-id="c1283-104">Ce didacticiel décrit comment exécuter Python dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="c1283-104">This tutorial describes how to get started running Python on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="c1283-105">Web Apps offre un hébergement gratuit limité ainsi qu’un déploiement rapide, et vous permet d’utiliser Python.</span><span class="sxs-lookup"><span data-stu-id="c1283-105">Web Apps provides limited free hosting and rapid deployment, and you can use Python!</span></span> <span data-ttu-id="c1283-106">À mesure que votre application croît, vous pouvez passer à un hébergement payant, et vous pouvez également intégrer l’application à tous les autres services Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-106">As your app grows, you can switch to paid hosting, and you can also integrate with all of the other Azure services.</span></span>

<span data-ttu-id="c1283-107">Vous allez créer une application à l’aide de l’infrastructure web Django (consultez les autres versions de ce didacticiel pour [Flask](web-sites-python-create-deploy-flask-app.md) et [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span><span class="sxs-lookup"><span data-stu-id="c1283-107">You will create an application using the Django web framework (see alternate versions of this tutorial for [Flask](web-sites-python-create-deploy-flask-app.md) and [Bottle](web-sites-python-create-deploy-bottle-app.md)).</span></span> <span data-ttu-id="c1283-108">Vous allez créer l’application web dans Azure Marketplace, configurer le déploiement de Git et cloner le référentiel localement.</span><span class="sxs-lookup"><span data-stu-id="c1283-108">You will create the web app from the Azure Marketplace, set up Git deployment, and clone the repository locally.</span></span> <span data-ttu-id="c1283-109">Ensuite, vous exécuterez l’application localement, puis vous apporterez des modifications que vous validerez et transmettrez à Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-109">Then you will run the application locally, make changes, commit and push them to Azure.</span></span> <span data-ttu-id="c1283-110">Ce didacticiel vous explique comment procéder depuis Windows ou Mac/Linux.</span><span class="sxs-lookup"><span data-stu-id="c1283-110">The tutorial shows how to do this from Windows or Mac/Linux.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="c1283-111">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="c1283-111">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c1283-112">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="c1283-112">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c1283-113">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="c1283-113">Prerequisites</span></span>
* <span data-ttu-id="c1283-114">Windows, Mac ou Linux</span><span class="sxs-lookup"><span data-stu-id="c1283-114">Windows, Mac or Linux</span></span>
* <span data-ttu-id="c1283-115">Python 2.7 ou 3.4</span><span class="sxs-lookup"><span data-stu-id="c1283-115">Python 2.7 or 3.4</span></span>
* <span data-ttu-id="c1283-116">setuptools, pip, virtualenv (Python 2.7 uniquement)</span><span class="sxs-lookup"><span data-stu-id="c1283-116">setuptools, pip, virtualenv (Python 2.7 only)</span></span>
* <span data-ttu-id="c1283-117">Git</span><span class="sxs-lookup"><span data-stu-id="c1283-117">Git</span></span>
* <span data-ttu-id="c1283-118">[Python Tools pour Visual Studio][Python Tools pour Visual Studio] (PTVS) - Remarque : ceci est facultatif</span><span class="sxs-lookup"><span data-stu-id="c1283-118">[Python Tools for Visual Studio][Python Tools for Visual Studio] (PTVS) - Note: this is optional</span></span>

<span data-ttu-id="c1283-119">**Remarque**: la publication de TFS n’est actuellement pas prise en charge pour les projets Python.</span><span class="sxs-lookup"><span data-stu-id="c1283-119">**Note**: TFS publishing is currently not supported for Python projects.</span></span>

### <a name="windows"></a><span data-ttu-id="c1283-120">Windows</span><span class="sxs-lookup"><span data-stu-id="c1283-120">Windows</span></span>
<span data-ttu-id="c1283-121">Si vous n’avez pas encore installé Python 2.7 ou 3.4 (32 bits), nous vous recommandons d’installer le [Kit de développement logiciel (SDK) Azure pour Python 2.7] ou le [Kit de développement logiciel (SDK) Azure pour Python 3.4] à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c1283-121">If you don't already have Python 2.7 or 3.4 installed (32-bit), we recommend installing [Azure SDK for Python 2.7] or [Azure SDK for Python 3.4] using Web Platform Installer.</span></span> <span data-ttu-id="c1283-122">Cette opération installe la version 32 bits de Python, setuptools, pip, virtualenv, etc. (Python 32 bits est installé sur les machines hôtes Azure).</span><span class="sxs-lookup"><span data-stu-id="c1283-122">This installs the 32-bit version of Python, setuptools, pip, virtualenv, etc (32-bit Python is what's installed on the Azure host machines).</span></span> <span data-ttu-id="c1283-123">Vous pouvez également obtenir Python sur le site [python.org].</span><span class="sxs-lookup"><span data-stu-id="c1283-123">Alternatively, you can get Python from [python.org].</span></span>

<span data-ttu-id="c1283-124">Pour Git, nous vous recommandons d’utiliser [Git pour Windows] ou [GitHub pour Windows].</span><span class="sxs-lookup"><span data-stu-id="c1283-124">For Git, we recommend [Git for Windows] or [GitHub for Windows].</span></span> <span data-ttu-id="c1283-125">Si vous travaillez avec Visual Studio, vous pouvez utiliser la prise en charge intégrée de Git.</span><span class="sxs-lookup"><span data-stu-id="c1283-125">If you use Visual Studio, you can use the integrated Git support.</span></span>

<span data-ttu-id="c1283-126">Nous vous recommandons également d’installer [Python Tools 2.2 pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c1283-126">We also recommend installing [Python Tools 2.2 for Visual Studio].</span></span> <span data-ttu-id="c1283-127">Cette opération est facultative, mais si vous avez [Visual Studio], ainsi que la version gratuite Visual Studio Community 2013 ou Visual Studio Express 2013 pour le Web, vous disposerez d’un formidable environnement de développement intégré Python.</span><span class="sxs-lookup"><span data-stu-id="c1283-127">This is optional, but if you have [Visual Studio], including the free Visual Studio Community 2013 or Visual Studio Express 2013 for Web, then this will give you a great Python IDE.</span></span>

### <a name="maclinux"></a><span data-ttu-id="c1283-128">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="c1283-128">Mac/Linux</span></span>
<span data-ttu-id="c1283-129">Vous devez avoir installé Python et Git, mais vérifiez que vous disposez de Python 2.7 ou 3.4.</span><span class="sxs-lookup"><span data-stu-id="c1283-129">You should have Python and Git already installed, but make sure you have either Python 2.7 or 3.4.</span></span>

## <a name="web-app-creation-on-portal"></a><span data-ttu-id="c1283-130">Création d’une application web sur le portail</span><span class="sxs-lookup"><span data-stu-id="c1283-130">Web App Creation on Portal</span></span>
<span data-ttu-id="c1283-131">La première étape consiste à créer l’application web par le biais du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c1283-131">The first step in creating your app is to create the web app via the [Azure Portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="c1283-132">Connectez-vous au portail Azure et cliquez sur le bouton **NOUVEAU** dans le coin inférieur gauche.</span><span class="sxs-lookup"><span data-stu-id="c1283-132">Log into the Azure Portal and click the **NEW** button in the bottom left corner.</span></span>
2. <span data-ttu-id="c1283-133">Dans le champ de recherche, tapez « python ».</span><span class="sxs-lookup"><span data-stu-id="c1283-133">In the search box, type "python".</span></span>
3. <span data-ttu-id="c1283-134">Dans les résultats de recherche, sélectionnez **Django** (publié par PTVS), puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c1283-134">In the search results, select **Django** (published by PTVS), then click **Create**.</span></span>
4. <span data-ttu-id="c1283-135">Configurez la nouvelle application Django, en créant un plan App Service et un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c1283-135">Configure the new Django app, such as creating a new App Service plan and a new resource group for it.</span></span> <span data-ttu-id="c1283-136">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c1283-136">Then, click **Create**.</span></span>
5. <span data-ttu-id="c1283-137">Configurez la publication Git de votre nouvelle application web en suivant les instructions de l’article [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c1283-137">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

## <a name="application-overview"></a><span data-ttu-id="c1283-138">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="c1283-138">Application Overview</span></span>
### <a name="git-repository-contents"></a><span data-ttu-id="c1283-139">Contenu du référentiel Git</span><span class="sxs-lookup"><span data-stu-id="c1283-139">Git repository contents</span></span>
<span data-ttu-id="c1283-140">Voici une vue d’ensemble des fichiers que vous trouverez dans le référentiel Git initial, que nous allons cloner dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="c1283-140">Here's an overview of the files you'll find in the initial Git repository, which we'll clone in the next section.</span></span>

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

<span data-ttu-id="c1283-141">Sources principales de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1283-141">Main sources for the application.</span></span> <span data-ttu-id="c1283-142">Correspondent à 3 pages (index, à propos de, contact) dotées d’une mise en page principale.</span><span class="sxs-lookup"><span data-stu-id="c1283-142">Consists of 3 pages (index, about, contact) with a master layout.</span></span> <span data-ttu-id="c1283-143">Le contenu statique et les scripts comprennent bootstrap, jquery, modernizr et respond.</span><span class="sxs-lookup"><span data-stu-id="c1283-143">Static content and scripts include bootstrap, jquery, modernizr and respond.</span></span>

    \manage.py

<span data-ttu-id="c1283-144">Prise en charge du serveur d’administration et de développement local.</span><span class="sxs-lookup"><span data-stu-id="c1283-144">Local management and development server support.</span></span> <span data-ttu-id="c1283-145">Utilisez ce fichier pour exécuter l’application localement, synchroniser la base de données, etc.</span><span class="sxs-lookup"><span data-stu-id="c1283-145">Use this to run the application locally, synchronize the database, etc.</span></span>

    \db.sqlite3

<span data-ttu-id="c1283-146">Base de données par défaut.</span><span class="sxs-lookup"><span data-stu-id="c1283-146">Default database.</span></span> <span data-ttu-id="c1283-147">Inclut les tables nécessaires à l’exécution de l’application, mais ne contient aucun utilisateur (synchronisez la base de données pour créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="c1283-147">Includes the necessary tables for the application to run, but does not contain any users (synchronize the database to create a user).</span></span>

    \DjangoWebProject.pyproj
    \DjangoWebProject.sln

<span data-ttu-id="c1283-148">Fichiers de projet à utiliser avec [Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c1283-148">Project files for use with [Python Tools for Visual Studio].</span></span>

    \ptvs_virtualenv_proxy.py

<span data-ttu-id="c1283-149">Proxy IIS pour les environnements virtuels et prise en charge du débogage à distance PTVS.</span><span class="sxs-lookup"><span data-stu-id="c1283-149">IIS proxy for virtual environments and PTVS remote debugging support.</span></span>

    \requirements.txt

<span data-ttu-id="c1283-150">Packages externes requis par cette application.</span><span class="sxs-lookup"><span data-stu-id="c1283-150">External packages needed by this application.</span></span> <span data-ttu-id="c1283-151">Le script de déploiement installera à l’aide de pip les packages répertoriés dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="c1283-151">The deployment script will pip install the packages listed in this file.</span></span>

    \web.2.7.config
    \web.3.4.config

<span data-ttu-id="c1283-152">Fichiers de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="c1283-152">IIS configuration files.</span></span> <span data-ttu-id="c1283-153">Le script de déploiement utilisera le fichier web.x.y.config approprié et le copiera sous le nom web.config.</span><span class="sxs-lookup"><span data-stu-id="c1283-153">The deployment script will use the appropriate web.x.y.config and copy it as web.config.</span></span>

### <a name="optional-files---customizing-deployment"></a><span data-ttu-id="c1283-154">Fichiers facultatifs - Personnalisation du déploiement</span><span class="sxs-lookup"><span data-stu-id="c1283-154">Optional files - Customizing deployment</span></span>
[!INCLUDE [web-sites-python-django-customizing-deployment](../../includes/web-sites-python-django-customizing-deployment.md)]

### <a name="optional-files---python-runtime"></a><span data-ttu-id="c1283-155">Fichiers facultatifs - Runtime Python</span><span class="sxs-lookup"><span data-stu-id="c1283-155">Optional files - Python runtime</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

### <a name="additional-files-on-server"></a><span data-ttu-id="c1283-156">Fichiers supplémentaires sur le serveur</span><span class="sxs-lookup"><span data-stu-id="c1283-156">Additional files on server</span></span>
<span data-ttu-id="c1283-157">Certains fichiers existent sur le serveur, mais ne sont pas ajoutés au référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="c1283-157">Some files exist on the server but are not added to the git repository.</span></span> <span data-ttu-id="c1283-158">Ils sont créés par le script de déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1283-158">These are created by the deployment script.</span></span>

    \web.config

<span data-ttu-id="c1283-159">Fichier de configuration IIS.</span><span class="sxs-lookup"><span data-stu-id="c1283-159">IIS configuration file.</span></span> <span data-ttu-id="c1283-160">Créé à partir du fichier web.x.y.config lors de chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1283-160">Created from web.x.y.config on every deployment.</span></span>

    \env\

<span data-ttu-id="c1283-161">Environnement virtuel Python.</span><span class="sxs-lookup"><span data-stu-id="c1283-161">Python virtual environment.</span></span> <span data-ttu-id="c1283-162">Créé lors du déploiement si aucun environnement virtuel compatible n’existe sur le site.</span><span class="sxs-lookup"><span data-stu-id="c1283-162">Created during deployment if a compatible virtual environment doesn't already exist on the web app.</span></span> <span data-ttu-id="c1283-163">Les packages répertoriés dans requirements.txt sont installés à l’aide de pip. Si les packages sont déjà installés, pip ignorera l’installation.</span><span class="sxs-lookup"><span data-stu-id="c1283-163">Packages listed in requirements.txt are pip installed, but pip will skip installation if the packages are already installed.</span></span>

<span data-ttu-id="c1283-164">Les trois sections suivantes expliquent comment développer des applications web dans trois environnements différents :</span><span class="sxs-lookup"><span data-stu-id="c1283-164">The next 3 sections describe how to proceed with the web app development under 3 different environments:</span></span>

* <span data-ttu-id="c1283-165">Windows, avec Python Tools pour Visual Studio ;</span><span class="sxs-lookup"><span data-stu-id="c1283-165">Windows, with Python Tools for Visual Studio</span></span>
* <span data-ttu-id="c1283-166">Windows, avec la ligne de commande ;</span><span class="sxs-lookup"><span data-stu-id="c1283-166">Windows, with command line</span></span>
* <span data-ttu-id="c1283-167">Mac/Linux, avec la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="c1283-167">Mac/Linux, with command line</span></span>

## <a name="web-app-development---windows---python-tools-for-visual-studio"></a><span data-ttu-id="c1283-168">Développement d’applications web - Windows - Python Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c1283-168">Web app development - Windows - Python Tools for Visual Studio</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c1283-169">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="c1283-169">Clone the repository</span></span>
<span data-ttu-id="c1283-170">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-170">First, clone the repository using the URL provided on the Azure Portal.</span></span> <span data-ttu-id="c1283-171">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c1283-171">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

<span data-ttu-id="c1283-172">Ouvrez le fichier solution (.sln) inclus dans la racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="c1283-172">Open the solution file (.sln) that is included in the root of the repository.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-solution-django.png)

### <a name="create-virtual-environment"></a><span data-ttu-id="c1283-173">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="c1283-173">Create virtual environment</span></span>
<span data-ttu-id="c1283-174">Nous allons à présent créer un environnement virtuel pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="c1283-174">Now we'll create a virtual environment for local development.</span></span> <span data-ttu-id="c1283-175">Cliquez avec le bouton droit sur **Environnements Python** et sélectionnez **Ajouter un environnement virtuel...**.</span><span class="sxs-lookup"><span data-stu-id="c1283-175">Right-click on **Python Environments** select **Add Virtual Environment...**.</span></span>

* <span data-ttu-id="c1283-176">Vérifiez que l’environnement porte le nom `env`.</span><span class="sxs-lookup"><span data-stu-id="c1283-176">Make sure the name of the environment is `env`.</span></span>
* <span data-ttu-id="c1283-177">Sélectionnez l’interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="c1283-177">Select the base interpreter.</span></span> <span data-ttu-id="c1283-178">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau **Paramètres de l’application** de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="c1283-178">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the **Application Settings** blade of your web app in the Azure Portal).</span></span>
* <span data-ttu-id="c1283-179">Vérifiez que l’option permettant de télécharger et d’installer les packages est cochée.</span><span class="sxs-lookup"><span data-stu-id="c1283-179">Make sure the option to download and install packages is checked.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-add-virtual-env-27.png)

<span data-ttu-id="c1283-180">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1283-180">Click **Create**.</span></span> <span data-ttu-id="c1283-181">Cette opération créera l’environnement virtuel et installera les dépendances répertoriées dans requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c1283-181">This will create the virtual environment, and install dependencies listed in requirements.txt.</span></span>

### <a name="create-a-superuser"></a><span data-ttu-id="c1283-182">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="c1283-182">Create a superuser</span></span>
<span data-ttu-id="c1283-183">Aucun superutilisateur n’a été défini dans la base de données de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1283-183">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c1283-184">Pour utiliser la fonctionnalité de connexion de l’application ou l’interface d’administration Django (si vous décidez de l’activer), vous devrez créer un superutilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1283-184">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c1283-185">Exécutez la commande ci-après depuis la ligne de commande du dossier de votre projet :</span><span class="sxs-lookup"><span data-stu-id="c1283-185">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c1283-186">Suivez les invites pour définir le nom d’utilisateur, le mot de passe, etc.</span><span class="sxs-lookup"><span data-stu-id="c1283-186">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c1283-187">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="c1283-187">Run using development server</span></span>
<span data-ttu-id="c1283-188">Appuyez sur F5 pour lancer le débogage. Votre navigateur ouvrira automatiquement la page s’exécutant localement.</span><span class="sxs-lookup"><span data-stu-id="c1283-188">Press F5 to start debugging, and your web browser will open automatically to the page running locally.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

<span data-ttu-id="c1283-189">Vous pouvez définir des points d’arrêt dans les sources, utiliser les fenêtres de surveillance, etc. Pour plus d’informations sur les différentes fonctionnalités, consultez la [Documentation de Python Tools pour Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="c1283-189">You can set breakpoints in the sources, use the watch windows, etc. See the [Python Tools for Visual Studio Documentation] for more information on the various features.</span></span>

### <a name="make-changes"></a><span data-ttu-id="c1283-190">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="c1283-190">Make changes</span></span>
<span data-ttu-id="c1283-191">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="c1283-191">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c1283-192">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="c1283-192">After you've tested your changes, commit them to the Git repository:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-commit-django.png)

### <a name="install-more-packages"></a><span data-ttu-id="c1283-193">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="c1283-193">Install more packages</span></span>
<span data-ttu-id="c1283-194">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-194">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c1283-195">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="c1283-195">You can install additional packages using pip.</span></span> <span data-ttu-id="c1283-196">Pour installer un package, cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Installer un package Python**.</span><span class="sxs-lookup"><span data-stu-id="c1283-196">To install a package, right-click on the virtual environment and select **Install Python Package**.</span></span>

<span data-ttu-id="c1283-197">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez `azure`:</span><span class="sxs-lookup"><span data-stu-id="c1283-197">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, enter `azure`:</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-install-package-dialog.png)

<span data-ttu-id="c1283-198">Cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Générer requirements.txt** pour mettre à jour le fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="c1283-198">Right-click on the virtual environment and select **Generate requirements.txt** to update requirements.txt.</span></span>

<span data-ttu-id="c1283-199">Puis validez les modifications apportées à requirements.txt dans le référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="c1283-199">Then, commit the changes to requirements.txt to the Git repository.</span></span>

### <a name="deploy-to-azure"></a><span data-ttu-id="c1283-200">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="c1283-200">Deploy to Azure</span></span>
<span data-ttu-id="c1283-201">Pour déclencher un déploiement, cliquez sur **Synchroniser** ou **Push**.</span><span class="sxs-lookup"><span data-stu-id="c1283-201">To trigger a deployment, click on **Sync** or **Push**.</span></span> <span data-ttu-id="c1283-202">La synchronisation effectue à la fois une transmission de type push et une transmission de type pull.</span><span class="sxs-lookup"><span data-stu-id="c1283-202">Sync does both a push and a pull.</span></span>

![](./media/web-sites-python-create-deploy-django-app/ptvs-git-push.png)

<span data-ttu-id="c1283-203">Le premier déploiement mettra un certain temps à s’effectuer, car il créera un environnement virtuel, installera les packages, etc.</span><span class="sxs-lookup"><span data-stu-id="c1283-203">The first deployment will take some time, as it will create a virtual environment, install packages, etc.</span></span>

<span data-ttu-id="c1283-204">Visual Studio n’affiche pas la progression du déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1283-204">Visual Studio doesn't show the progress of the deployment.</span></span> <span data-ttu-id="c1283-205">Si vous souhaitez vérifier la sortie, consultez la section [Résolution des problèmes - Déploiement](#troubleshooting-deployment).</span><span class="sxs-lookup"><span data-stu-id="c1283-205">If you'd like to review the output, see the section on [Troubleshooting - Deployment](#troubleshooting-deployment).</span></span>

<span data-ttu-id="c1283-206">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="c1283-206">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---windows---command-line"></a><span data-ttu-id="c1283-207">Développement d’applications web - Windows - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="c1283-207">Web app development - Windows - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c1283-208">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="c1283-208">Clone the repository</span></span>
<span data-ttu-id="c1283-209">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="c1283-209">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c1283-210">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c1283-210">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c1283-211">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="c1283-211">Create virtual environment</span></span>
<span data-ttu-id="c1283-212">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="c1283-212">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c1283-213">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="c1283-213">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c1283-214">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="c1283-214">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c1283-215">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="c1283-215">For Python 2.7:</span></span>

    c:\python27\python.exe -m virtualenv env

<span data-ttu-id="c1283-216">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="c1283-216">For Python 3.4:</span></span>

    c:\python34\python.exe -m venv env

<span data-ttu-id="c1283-217">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="c1283-217">Install any external packages required by your application.</span></span> <span data-ttu-id="c1283-218">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="c1283-218">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env\scripts\pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c1283-219">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="c1283-219">Create a superuser</span></span>
<span data-ttu-id="c1283-220">Aucun superutilisateur n’a été défini dans la base de données de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1283-220">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c1283-221">Pour utiliser la fonctionnalité de connexion de l’application ou l’interface d’administration Django (si vous décidez de l’activer), vous devrez créer un superutilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1283-221">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c1283-222">Exécutez la commande ci-après depuis la ligne de commande du dossier de votre projet :</span><span class="sxs-lookup"><span data-stu-id="c1283-222">Run this from the command-line from your project folder:</span></span>

    env\scripts\python manage.py createsuperuser

<span data-ttu-id="c1283-223">Suivez les invites pour définir le nom d’utilisateur, le mot de passe, etc.</span><span class="sxs-lookup"><span data-stu-id="c1283-223">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c1283-224">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="c1283-224">Run using development server</span></span>
<span data-ttu-id="c1283-225">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c1283-225">You can launch the application under a development server with the following command:</span></span>

    env\scripts\python manage.py runserver

<span data-ttu-id="c1283-226">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="c1283-226">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-run-local-django.png)

<span data-ttu-id="c1283-227">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="c1283-227">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/windows-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c1283-228">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="c1283-228">Make changes</span></span>
<span data-ttu-id="c1283-229">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="c1283-229">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c1283-230">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="c1283-230">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c1283-231">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="c1283-231">Install more packages</span></span>
<span data-ttu-id="c1283-232">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-232">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c1283-233">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="c1283-233">You can install additional packages using pip.</span></span> <span data-ttu-id="c1283-234">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="c1283-234">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env\scripts\pip install azure

<span data-ttu-id="c1283-235">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="c1283-235">Make sure to update requirements.txt:</span></span>

    env\scripts\pip freeze > requirements.txt

<span data-ttu-id="c1283-236">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="c1283-236">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c1283-237">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="c1283-237">Deploy to Azure</span></span>
<span data-ttu-id="c1283-238">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="c1283-238">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c1283-239">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="c1283-239">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c1283-240">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="c1283-240">Browse to the Azure URL to view your changes.</span></span>

## <a name="web-app-development---maclinux---command-line"></a><span data-ttu-id="c1283-241">Développement d’applications web - Mac/Linux - Ligne de commande</span><span class="sxs-lookup"><span data-stu-id="c1283-241">Web app development - Mac/Linux - command line</span></span>
### <a name="clone-the-repository"></a><span data-ttu-id="c1283-242">Cloner le référentiel</span><span class="sxs-lookup"><span data-stu-id="c1283-242">Clone the repository</span></span>
<span data-ttu-id="c1283-243">Commencez par cloner le référentiel à l’aide de l’URL fournie sur le portail Azure, puis ajoutez le référentiel Azure en tant que référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="c1283-243">First, clone the repository using the URL provided on the Azure Portal, and add the Azure repository as a remote.</span></span> <span data-ttu-id="c1283-244">Pour plus d’informations, voir [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="c1283-244">For more information, see [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span>

    git clone <repo-url>
    cd <repo-folder>
    git remote add azure <repo-url>

### <a name="create-virtual-environment"></a><span data-ttu-id="c1283-245">Créer un environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="c1283-245">Create virtual environment</span></span>
<span data-ttu-id="c1283-246">Nous allons créer un environnement virtuel pour le développement (ne l’ajoutez pas au référentiel).</span><span class="sxs-lookup"><span data-stu-id="c1283-246">We'll create a new virtual environment for development purposes (do not add it to the repository).</span></span> <span data-ttu-id="c1283-247">Les environnements virtuels dans Python ne sont pas déplaçables. De ce fait, chaque développeur travaillant sur l’application créera ses propres environnements localement.</span><span class="sxs-lookup"><span data-stu-id="c1283-247">Virtual environments in Python are not relocatable, so every developer working on the application will create their own locally.</span></span>

<span data-ttu-id="c1283-248">Veillez à utiliser la même version de Python que celle sélectionnée pour votre application web (dans runtime.txt ou le panneau Paramètres de l’application de votre application web dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="c1283-248">Make sure to use the same version of Python that is selected for your web app (in runtime.txt or the Application Settings blade of your web app in the Azure Portal).</span></span>

<span data-ttu-id="c1283-249">Pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="c1283-249">For Python 2.7:</span></span>

    python -m virtualenv env

<span data-ttu-id="c1283-250">Pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="c1283-250">For Python 3.4:</span></span>

    python -m venv env

<span data-ttu-id="c1283-251">ou</span><span class="sxs-lookup"><span data-stu-id="c1283-251">or</span></span>

    pyvenv env

<span data-ttu-id="c1283-252">Installez tous les packages externes requis par votre application.</span><span class="sxs-lookup"><span data-stu-id="c1283-252">Install any external packages required by your application.</span></span> <span data-ttu-id="c1283-253">Vous pouvez utiliser le fichier requirements.txt à la racine du référentiel pour installer les packages dans votre environnement virtuel :</span><span class="sxs-lookup"><span data-stu-id="c1283-253">You can use the requirements.txt file at the root of the repository to install the packages in your virtual environment:</span></span>

    env/bin/pip install -r requirements.txt

### <a name="create-a-superuser"></a><span data-ttu-id="c1283-254">Créer un superutilisateur</span><span class="sxs-lookup"><span data-stu-id="c1283-254">Create a superuser</span></span>
<span data-ttu-id="c1283-255">Aucun superutilisateur n’a été défini dans la base de données de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1283-255">The database included with the application does not have any superuser defined.</span></span> <span data-ttu-id="c1283-256">Pour utiliser la fonctionnalité de connexion de l’application ou l’interface d’administration Django (si vous décidez de l’activer), vous devrez créer un superutilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1283-256">In order to use the sign-in functionality in the application, or the Django admin interface (if you decide to enable it), you'll need to create a superuser.</span></span>

<span data-ttu-id="c1283-257">Exécutez la commande ci-après depuis la ligne de commande du dossier de votre projet :</span><span class="sxs-lookup"><span data-stu-id="c1283-257">Run this from the command-line from your project folder:</span></span>

    env/bin/python manage.py createsuperuser

<span data-ttu-id="c1283-258">Suivez les invites pour définir le nom d’utilisateur, le mot de passe, etc.</span><span class="sxs-lookup"><span data-stu-id="c1283-258">Follow the prompts to set the user name, password, etc.</span></span>

### <a name="run-using-development-server"></a><span data-ttu-id="c1283-259">Exécuter à l’aide d’un serveur de développement</span><span class="sxs-lookup"><span data-stu-id="c1283-259">Run using development server</span></span>
<span data-ttu-id="c1283-260">Vous pouvez lancer l’application sous un serveur de développement à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c1283-260">You can launch the application under a development server with the following command:</span></span>

    env/bin/python manage.py runserver

<span data-ttu-id="c1283-261">La console affichera l’URL et le port que le serveur écoute :</span><span class="sxs-lookup"><span data-stu-id="c1283-261">The console will display the URL and port the server listens to:</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-run-local-django.png)

<span data-ttu-id="c1283-262">Puis ouvrez votre navigateur web en accédant à cette URL.</span><span class="sxs-lookup"><span data-stu-id="c1283-262">Then, open your web browser to that URL.</span></span>

![](./media/web-sites-python-create-deploy-django-app/mac-browser-django.png)

### <a name="make-changes"></a><span data-ttu-id="c1283-263">Apporter des modifications</span><span class="sxs-lookup"><span data-stu-id="c1283-263">Make changes</span></span>
<span data-ttu-id="c1283-264">Vous pouvez à présent tenter d’apporter des modifications aux sources de l’application et/ou aux modèles.</span><span class="sxs-lookup"><span data-stu-id="c1283-264">Now you can experiment by making changes to the application sources and/or templates.</span></span>

<span data-ttu-id="c1283-265">Après avoir testé vos modifications, validez-les sur le référentiel Git :</span><span class="sxs-lookup"><span data-stu-id="c1283-265">After you've tested your changes, commit them to the Git repository:</span></span>

    git add <modified-file>
    git commit -m "<commit-comment>"

### <a name="install-more-packages"></a><span data-ttu-id="c1283-266">Installer d’autres packages</span><span class="sxs-lookup"><span data-stu-id="c1283-266">Install more packages</span></span>
<span data-ttu-id="c1283-267">Votre application peut comporter des dépendances au-delà de Python et de Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-267">Your application may have dependencies beyond Python and Django.</span></span>

<span data-ttu-id="c1283-268">Vous pouvez installer des packages supplémentaires à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="c1283-268">You can install additional packages using pip.</span></span> <span data-ttu-id="c1283-269">Par exemple, pour installer le Kit de développement logiciel (SDK) Azure pour Python, qui vous permet d’accéder au stockage Azure, au bus des services et à d’autres services Azure, entrez :</span><span class="sxs-lookup"><span data-stu-id="c1283-269">For example, to install the Azure SDK for Python, which gives you access to Azure storage, service bus and other Azure services, type:</span></span>

    env/bin/pip install azure

<span data-ttu-id="c1283-270">Veillez à mettre à jour requirements.txt :</span><span class="sxs-lookup"><span data-stu-id="c1283-270">Make sure to update requirements.txt:</span></span>

    env/bin/pip freeze > requirements.txt

<span data-ttu-id="c1283-271">Validez les modifications :</span><span class="sxs-lookup"><span data-stu-id="c1283-271">Commit the changes:</span></span>

    git add requirements.txt
    git commit -m "Added azure package"

### <a name="deploy-to-azure"></a><span data-ttu-id="c1283-272">Déploiement sur Azure</span><span class="sxs-lookup"><span data-stu-id="c1283-272">Deploy to Azure</span></span>
<span data-ttu-id="c1283-273">Pour déclencher un déploiement, transmettez les modifications à Azure :</span><span class="sxs-lookup"><span data-stu-id="c1283-273">To trigger a deployment, push the changes to Azure:</span></span>

    git push azure master

<span data-ttu-id="c1283-274">Vous découvrirez la sortie du script de déploiement, notamment la création de l’environnement virtuel, l’installation des packages et la création du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="c1283-274">You will see the output of the deployment script, including virtual environment creation, installation of packages, creation of web.config.</span></span>

<span data-ttu-id="c1283-275">Accédez à l’URL Azure pour visualiser les modifications que vous avez apportées.</span><span class="sxs-lookup"><span data-stu-id="c1283-275">Browse to the Azure URL to view your changes.</span></span>

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="c1283-276">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="c1283-276">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="c1283-277">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="c1283-277">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="troubleshooting---static-files"></a><span data-ttu-id="c1283-278">Résolution des problèmes - Fichiers statiques</span><span class="sxs-lookup"><span data-stu-id="c1283-278">Troubleshooting - Static Files</span></span>
<span data-ttu-id="c1283-279">Django se charge de collecter les fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="c1283-279">Django has the concept of collecting static files.</span></span> <span data-ttu-id="c1283-280">Il récupère tous les fichiers statiques à partir de leur emplacement d’origine et les copie dans un dossier unique.</span><span class="sxs-lookup"><span data-stu-id="c1283-280">This takes all the static files from their original location and copies them to a single folder.</span></span> <span data-ttu-id="c1283-281">Pour cette application, les fichiers sont copiés dans `/static`.</span><span class="sxs-lookup"><span data-stu-id="c1283-281">For this application, they are copied to `/static`.</span></span>

<span data-ttu-id="c1283-282">Cette opération est effectuée, car les fichiers statiques peuvent provenir de différentes applications Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-282">This is done because static files may come from different Django 'apps'.</span></span> <span data-ttu-id="c1283-283">Par exemple, les fichiers statiques des interfaces d’administration Django sont situés dans un sous-dossier de bibliothèque Django dans l’environnement virtuel.</span><span class="sxs-lookup"><span data-stu-id="c1283-283">For example, the static files from the Django admin interfaces are located in a Django library subfolder in the virtual environment.</span></span> <span data-ttu-id="c1283-284">Les fichiers statiques définis par cette application se trouvent dans `/app/static`.</span><span class="sxs-lookup"><span data-stu-id="c1283-284">Static files defined by this application are located in `/app/static`.</span></span> <span data-ttu-id="c1283-285">Plus vous utiliserez d’applications Django, plus vous aurez de fichiers statiques dans différents emplacements.</span><span class="sxs-lookup"><span data-stu-id="c1283-285">As you use more Django 'apps', you'll have static files located in multiple places.</span></span>

<span data-ttu-id="c1283-286">Lorsque l’application s’exécute en mode débogage, elle traite les fichiers statiques à partir de leur emplacement d’origine.</span><span class="sxs-lookup"><span data-stu-id="c1283-286">When running the application in debug mode, the application serves the static files from their original location.</span></span>

<span data-ttu-id="c1283-287">Quand l’application s’exécute en mode version finale, elle ne traite **aucun** fichier statique.</span><span class="sxs-lookup"><span data-stu-id="c1283-287">When running the application in release mode, the application does **not** serve the static files.</span></span> <span data-ttu-id="c1283-288">Le serveur web se charge de traiter ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="c1283-288">It is the responsibility of the web server to serve the files.</span></span> <span data-ttu-id="c1283-289">Pour cette application, IIS traite les fichiers statiques depuis `/static`.</span><span class="sxs-lookup"><span data-stu-id="c1283-289">For this application, IIS will serve the static files from `/static`.</span></span>

<span data-ttu-id="c1283-290">Les fichiers statiques sont automatiquement collectés dans le cadre du script de déploiement et suppriment ainsi les fichiers précédemment collectés.</span><span class="sxs-lookup"><span data-stu-id="c1283-290">The collection of static files is done automatically as part of the deployment script, clearing previously collected files.</span></span> <span data-ttu-id="c1283-291">Cela signifie que cette collecte s’effectue lors de chaque déploiement, ce qui ralentit quelque peu ce dernier, mais permet d’éliminer les fichiers obsolètes qui représentent un risque pour la sécurité.</span><span class="sxs-lookup"><span data-stu-id="c1283-291">This means the collection occurs on every deployment, slowing down deployment a bit, but it ensures that obsolete files won't be available, avoiding a potential security issue.</span></span>

<span data-ttu-id="c1283-292">Si vous souhaitez ignorer les fichiers statiques pour votre application Django :</span><span class="sxs-lookup"><span data-stu-id="c1283-292">If you want to skip collection of static files for your Django application:</span></span>

    \.skipDjango

<span data-ttu-id="c1283-293">Vous devrez alors effectuer la collecte manuellement sur votre ordinateur local :</span><span class="sxs-lookup"><span data-stu-id="c1283-293">Then you'll need to do the collection manually on your local machine:</span></span>

    env\scripts\python manage.py collectstatic

<span data-ttu-id="c1283-294">Puis supprimez le dossier `\static` de `.gitignore` et ajoutez-le au référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="c1283-294">Then remove the `\static` folder from `.gitignore` and add it to the Git repository.</span></span>

## <a name="troubleshooting---settings"></a><span data-ttu-id="c1283-295">Résolution des problèmes - Paramètres</span><span class="sxs-lookup"><span data-stu-id="c1283-295">Troubleshooting - Settings</span></span>
<span data-ttu-id="c1283-296">Vous pouvez modifier différents paramètres dans `DjangoWebProject/settings.py`.</span><span class="sxs-lookup"><span data-stu-id="c1283-296">Various settings for the application can be changed in `DjangoWebProject/settings.py`.</span></span>

<span data-ttu-id="c1283-297">Pour simplifier le développement, le mode débogage est activé.</span><span class="sxs-lookup"><span data-stu-id="c1283-297">For developer convenience, debug mode is enabled.</span></span> <span data-ttu-id="c1283-298">Ce mode vous permettra de visualiser les images et d’autres contenus statiques lors de l’exécution locale, sans nécessiter la collecte des fichiers statiques.</span><span class="sxs-lookup"><span data-stu-id="c1283-298">One nice side effect of that is you'll be able to see images and other static content when running locally, without having to collect static files.</span></span>

<span data-ttu-id="c1283-299">Pour désactiver le mode débogage :</span><span class="sxs-lookup"><span data-stu-id="c1283-299">To disable debug mode:</span></span>

    DEBUG = False

<span data-ttu-id="c1283-300">Lorsque le débogage est désactivé, la valeur de `ALLOWED_HOSTS` doit être mise à jour de façon à inclure le nom d’hôte Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-300">When debug is disabled, the value for `ALLOWED_HOSTS` needs to be updated to include the Azure host name.</span></span> <span data-ttu-id="c1283-301">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c1283-301">For example:</span></span>

    ALLOWED_HOSTS = (
        'pythonapp.azurewebsites.net',
    )

<span data-ttu-id="c1283-302">Cette valeur doit également être mise à jour pour activer des hôtes :</span><span class="sxs-lookup"><span data-stu-id="c1283-302">or to enable any:</span></span>

    ALLOWED_HOSTS = (
        '*',
    )

<span data-ttu-id="c1283-303">Dans la pratique, vous pouvez également opter pour une solution un peu plus complexe qui vous permet de basculer entre le mode débogage et le mode version finale, et d’obtenir le nom d’hôte.</span><span class="sxs-lookup"><span data-stu-id="c1283-303">In practice, you may want to do something more complex to deal with switching between debug and release mode, and getting the host name.</span></span>

<span data-ttu-id="c1283-304">Vous pouvez définir des variables d’environnement dans la section **Paramètres de l’application** de la page **CONFIGURER** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-304">You can set environment variables through the Azure portal **CONFIGURE** page, in the **app settings** section.</span></span>  <span data-ttu-id="c1283-305">Cette opération peut vous permettre de définir les valeurs que vous ne souhaitez pas voir apparaître dans les sources (chaînes de connexion, mots de passe, etc.) ou que vous souhaitez définir différemment entre Azure et votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c1283-305">This can be useful for setting values that you may not want to appear in the sources (connection strings, passwords, etc), or that you want to set differently between Azure and your local machine.</span></span> <span data-ttu-id="c1283-306">Dans `settings.py`, vous pouvez interroger les variables d’environnement à l’aide de `os.getenv`.</span><span class="sxs-lookup"><span data-stu-id="c1283-306">In `settings.py`, you can query the environment variables using `os.getenv`.</span></span>

## <a name="using-a-database"></a><span data-ttu-id="c1283-307">Utilisation d’une base de données</span><span class="sxs-lookup"><span data-stu-id="c1283-307">Using a Database</span></span>
<span data-ttu-id="c1283-308">La base de données fournie avec l’application est une base de données sqlite.</span><span class="sxs-lookup"><span data-stu-id="c1283-308">The database that is included with the application is a sqlite database.</span></span> <span data-ttu-id="c1283-309">Cette base de données par défaut se révèle très utile pour le développement, car elle ne requiert quasiment aucune configuration.</span><span class="sxs-lookup"><span data-stu-id="c1283-309">This is a convenient and useful default database to use for development, as it requires almost no setup.</span></span> <span data-ttu-id="c1283-310">Elle est stockée dans le fichier db.sqlite3 situé dans le dossier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="c1283-310">The database is stored in the db.sqlite3 file in the project folder.</span></span>

<span data-ttu-id="c1283-311">Azure fournit des services de base de données faciles à utiliser à partir d’une application Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-311">Azure provides database services which are easy to use from a Django application.</span></span> <span data-ttu-id="c1283-312">Des didacticiels expliquant comment utiliser [SQL Database] et [MySQL] à partir d’une application Django vous indiquent la procédure à suivre pour créer le service de base de données et pour modifier les paramètres de base de données dans `DjangoWebProject/settings.py`, ainsi que les bibliothèques à installer.</span><span class="sxs-lookup"><span data-stu-id="c1283-312">Tutorials for using [SQL Database] and [MySQL] from a Django application show the steps necessary to create the database service, change the database settings in `DjangoWebProject/settings.py`, and the libraries required to install.</span></span>

<span data-ttu-id="c1283-313">Si vous préférez gérer vos propres serveurs de base de données, vous pouvez utiliser des machines virtuelles Windows ou Linux s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="c1283-313">Of course, if you prefer to manage your own database servers, you can do so using Windows or Linux virtual machines running on Azure.</span></span>

## <a name="django-admin-interface"></a><span data-ttu-id="c1283-314">Interface d’administration Django</span><span class="sxs-lookup"><span data-stu-id="c1283-314">Django Admin Interface</span></span>
<span data-ttu-id="c1283-315">Lorsque vous commencerez à créer vos modèles, vous souhaiterez probablement remplir la base de données avec certaines données.</span><span class="sxs-lookup"><span data-stu-id="c1283-315">Once you start building your models, you'll want to populate the database with some data.</span></span> <span data-ttu-id="c1283-316">Pour ajouter et modifier facilement du contenu de manière interactive, utilisez l’interface d’administration Django.</span><span class="sxs-lookup"><span data-stu-id="c1283-316">An easy way to do add and edit content interactively is to use the Django administration interface.</span></span>

<span data-ttu-id="c1283-317">Le code de l’interface d’administration est mis en commentaire dans les sources de l’application, mais il est clairement identifié pour que vous puissiez facilement l’activer (recherchez « admin »).</span><span class="sxs-lookup"><span data-stu-id="c1283-317">The code for the admin interface is commented out in the application sources, but it's clearly marked so you can easily enable it (search for 'admin').</span></span>

<span data-ttu-id="c1283-318">Une fois ce code activé, synchronisez la base de données, exécutez l’application, puis accédez à `/admin`.</span><span class="sxs-lookup"><span data-stu-id="c1283-318">After it's enabled, synchronize the database, run the application and navigate to `/admin`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1283-319">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1283-319">Next Steps</span></span>
<span data-ttu-id="c1283-320">Pour plus d’informations sur Django et sur Python Tools pour Visual Studio, sélectionnez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="c1283-320">Follow these links to learn more about Django and Python Tools for Visual Studio:</span></span>

* <span data-ttu-id="c1283-321">[Documentation Django]</span><span class="sxs-lookup"><span data-stu-id="c1283-321">[Django Documentation]</span></span>
* <span data-ttu-id="c1283-322">[Documentation de Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c1283-322">[Python Tools for Visual Studio Documentation]</span></span>

<span data-ttu-id="c1283-323">Pour plus d’informations sur l’utilisation de Base de données SQL et de MySQL :</span><span class="sxs-lookup"><span data-stu-id="c1283-323">For information on using SQL Database and MySQL:</span></span>

* <span data-ttu-id="c1283-324">[Django et MySQL sur Azure avec Python Tools pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c1283-324">[Django and MySQL on Azure with Python Tools for Visual Studio]</span></span>
* <span data-ttu-id="c1283-325">[Django et SQL Database sur Azure avec Python pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="c1283-325">[Django and SQL Database on Azure with Python Tools for Visual Studio]</span></span>

<span data-ttu-id="c1283-326">Pour plus d’informations, consultez le [Centre pour développeurs Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="c1283-326">For more information, see the [Python Developer Center](/develop/python/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c1283-327">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="c1283-327">What's changed</span></span>
* <span data-ttu-id="c1283-328">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c1283-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Django et MySQL sur Azure avec Python Tools pour Visual Studio]: web-sites-python-ptvs-django-mysql.md
[Django et SQL Database sur Azure avec Python pour Visual Studio]: web-sites-python-ptvs-django-sql.md
[SQL Database]: web-sites-python-ptvs-django-sql.md
[MySQL]: web-sites-python-ptvs-django-mysql.md

<!--External Link references-->
[Kit de développement logiciel (SDK) Azure pour Python 2.7]: http://go.microsoft.com/fwlink/?linkid=254281
[Kit de développement logiciel (SDK) Azure pour Python 3.4]: http://go.microsoft.com/fwlink/?linkid=516990
[python.org]: http://www.python.org/
[Git pour Windows]: http://msysgit.github.io/
[GitHub pour Windows]: https://windows.github.com/
[Python Tools pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Visual Studio]: http://www.visualstudio.com/
[Documentation de Python Tools pour Visual Studio]: http://aka.ms/ptvsdocs
[Documentation Django]: https://www.djangoproject.com/
