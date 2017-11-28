---
title: aaaDjango et MySQL sur Azure avec 2.2 des outils Python pour Visual Studio
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application web Django qui stocke les données dans une instance de la base de données MySQL et déployez-le tooAzure App Service Web Apps."
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: c60a50b5-8b5e-4818-a442-16362273dabb
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1597c391d20c8e8ef629b4e4d05c9eb64c83bffc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-mysql-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="b8236-103">Django et MySQL sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8236-103">Django and MySQL on Azure with Python Tools 2.2 for Visual Studio</span></span>
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

<span data-ttu-id="b8236-104">Dans ce didacticiel, vous allez utiliser [outils Python pour Visual Studio](https://www.visualstudio.com/vs/python) toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-104">In this tutorial, you'll use [Python Tools for Visual Studio](https://www.visualstudio.com/vs/python) toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="b8236-105">Vous allez apprendre comment toouse un service MySQL hébergé sur Azure, comment tooconfigure hello web application toouse MySQL et comment toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b8236-105">You'll learn how toouse a MySQL service hosted on Azure, how tooconfigure hello web app toouse MySQL, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

> [!NOTE]
> <span data-ttu-id="b8236-106">les informations de Hello contenues dans ce didacticiel sont également disponibles dans hello suivant vidéo :</span><span class="sxs-lookup"><span data-stu-id="b8236-106">hello information contained in this tutorial is also available in hello following video:</span></span>
> 
> <span data-ttu-id="b8236-107">[PTVS 2.1 : application Django avec MySQL][video]</span><span class="sxs-lookup"><span data-stu-id="b8236-107">[PTVS 2.1: Django app with MySQL][video]</span></span>
> 
> 

<span data-ttu-id="b8236-108">Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services de base de données SQL, MySQL et stockage de Table Azure.</span><span class="sxs-lookup"><span data-stu-id="b8236-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL, and SQL Database services.</span></span> <span data-ttu-id="b8236-109">Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="b8236-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8236-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b8236-110">Prerequisites</span></span>
* <span data-ttu-id="b8236-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b8236-111">Visual Studio 2015</span></span>
* <span data-ttu-id="b8236-112">[Python 2.7 32 bits] ou [Python 3.4 32 bits]</span><span class="sxs-lookup"><span data-stu-id="b8236-112">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>
* <span data-ttu-id="b8236-113">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b8236-113">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="b8236-114">[2.2 des outils Python pour Visual Studio exemples VSIX]</span><span class="sxs-lookup"><span data-stu-id="b8236-114">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="b8236-115">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="b8236-115">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="b8236-116">Django 1.9 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="b8236-116">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<!-- This note should not render as part of hello hello previous include. -->

> [!NOTE]
> <span data-ttu-id="b8236-117">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="b8236-117">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b8236-118">Aucune carte de crédit n’est nécessaire et vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="b8236-118">No credit card is required, and no commitments are necessary.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="b8236-119">Créer hello projet</span><span class="sxs-lookup"><span data-stu-id="b8236-119">Create hello Project</span></span>
<span data-ttu-id="b8236-120">Dans cette section, vous allez créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="b8236-120">In this section, you'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="b8236-121">Vous allez créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="b8236-121">You'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="b8236-122">Vous allez créer une base de données locale à l’aide de sqlite.</span><span class="sxs-lookup"><span data-stu-id="b8236-122">You'll create a local database using sqlite.</span></span> <span data-ttu-id="b8236-123">Ensuite, vous allez exécuter application hello localement.</span><span class="sxs-lookup"><span data-stu-id="b8236-123">Then you'll run hello application locally.</span></span>

1. <span data-ttu-id="b8236-124">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="b8236-124">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="b8236-125">Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**.</span><span class="sxs-lookup"><span data-stu-id="b8236-125">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="b8236-126">Sélectionnez **interroge Django Web projet** et cliquez sur OK toocreate hello projet.</span><span class="sxs-lookup"><span data-stu-id="b8236-126">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>
   
    ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-django-mysql/PollsDjangoNewProject.png)
3. <span data-ttu-id="b8236-128">Vous serez invité à tooinstall les packages externes.</span><span class="sxs-lookup"><span data-stu-id="b8236-128">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="b8236-129">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="b8236-129">Select **Install into a virtual environment**.</span></span>
   
    ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-django-mysql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="b8236-131">Sélectionnez **Python 2.7** ou **Python 3.4** comme interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-131">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
    ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-django-mysql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="b8236-133">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.</span><span class="sxs-lookup"><span data-stu-id="b8236-133">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b8236-134">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="b8236-134">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="b8236-135">Vous ouvrez une Console de gestion Django et créer une base de données sqlite dans le dossier de projet hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-135">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="b8236-136">Suivez les invites de hello toocreate un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8236-136">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="b8236-137">Vérifier que l’application hello fonctionne en appuyant sur `F5`.</span><span class="sxs-lookup"><span data-stu-id="b8236-137">Confirm that hello application works by pressing `F5`.</span></span>
8. <span data-ttu-id="b8236-138">Cliquez sur **connecter** à partir de la barre de navigation hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-138">Click **Log in** from hello navigation bar at hello top.</span></span>
   
    ![Barre de navigation Django](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="b8236-140">Entrez des informations d’identification de hello pour utilisateur hello que vous avez créé lors de la synchronisation de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-140">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>
   
    ![Formulaire de connexion](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="b8236-142">Cliquez sur **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="b8236-142">Click **Create Sample Polls**.</span></span>
    
     ![Create Sample Polls](./media/web-sites-python-ptvs-django-mysql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="b8236-144">Cliquez sur un sondage et votez.</span><span class="sxs-lookup"><span data-stu-id="b8236-144">Click on a poll and vote.</span></span>
    
     ![Vote dans les exemples de sondage](./media/web-sites-python-ptvs-django-mysql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-mysql-database"></a><span data-ttu-id="b8236-146">Création d’une base de données MySQL</span><span class="sxs-lookup"><span data-stu-id="b8236-146">Create a MySQL Database</span></span>
<span data-ttu-id="b8236-147">Pour la base de données hello, vous allez créer une base de données ClearDB MySQL hébergé sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b8236-147">For hello database, you'll create a ClearDB MySQL hosted database on Azure.</span></span>

<span data-ttu-id="b8236-148">Vous pouvez également créer votre propre machine virtuelle s'exécutant dans Azure, puis installer et administrer MySQL vous-même.</span><span class="sxs-lookup"><span data-stu-id="b8236-148">As an alternative, you can create your own Virtual Machine running in Azure, then install and administer MySQL yourself.</span></span>

<span data-ttu-id="b8236-149">Pour créer une base de données avec un plan gratuit, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8236-149">You can create a database with a free plan by following these steps.</span></span>

1. <span data-ttu-id="b8236-150">Connectez-vous à toohello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="b8236-150">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="b8236-151">En hello haut hello du volet de navigation, cliquez sur **nouveau**, puis cliquez sur **données + stockage**, puis cliquez sur **base de données MySQL**.</span><span class="sxs-lookup"><span data-stu-id="b8236-151">At hello Top of hello navigation pane, click **NEW**, then click **Data + Storage**, and then click **MySQL Database**.</span></span>
3. <span data-ttu-id="b8236-152">Configurer la base de données MySQL hello en créant un nouveau groupe de ressources et sélectionner l’emplacement approprié d’hello pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="b8236-152">Configure hello new MySQL database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="b8236-153">Une fois la base de données MySQL hello est créé, cliquez sur **propriétés** dans Panneau de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-153">Once hello MySQL database is created, click **Properties** in hello database blade.</span></span>
5. <span data-ttu-id="b8236-154">Utilisez hello copie bouton tooput hello valeur **chaîne de connexion** Presse-papiers de hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-154">Use hello copy button tooput hello value of **CONNECTION STRING** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="b8236-155">Configurer hello projet</span><span class="sxs-lookup"><span data-stu-id="b8236-155">Configure hello Project</span></span>
<span data-ttu-id="b8236-156">Dans cette section, vous allez configurer notre web application toouse hello base de données MySQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="b8236-156">In this section, you'll configure our web app toouse hello MySQL database you just created.</span></span> <span data-ttu-id="b8236-157">Vous allez également installer Python packages requis toouse MySQL bases de données supplémentaires avec Django.</span><span class="sxs-lookup"><span data-stu-id="b8236-157">You'll also install additional Python packages required toouse MySQL databases with Django.</span></span> <span data-ttu-id="b8236-158">Ensuite, vous allez exécuter l’application hello web localement.</span><span class="sxs-lookup"><span data-stu-id="b8236-158">Then you'll run hello web app locally.</span></span>

1. <span data-ttu-id="b8236-159">Dans Visual Studio, ouvrez **settings.py**, à partir de hello *nom_projet* dossier.</span><span class="sxs-lookup"><span data-stu-id="b8236-159">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="b8236-160">Collez temporairement chaîne de connexion hello dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-160">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="b8236-161">chaîne de connexion Hello est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b8236-161">hello connection string is in this format:</span></span>
   
        Database=<NAME>;Data Source=<HOST>;User Id=<USER>;Password=<PASSWORD>
   
    <span data-ttu-id="b8236-162">Base de données par défaut modifiée hello **moteur** toouse MySQL et ensemble de valeurs pour hello **nom**, **utilisateur**, **mot de passe** et  **HÔTE** de hello **CONNECTIONSTRING**.</span><span class="sxs-lookup"><span data-stu-id="b8236-162">Change hello default database **ENGINE** toouse MySQL, and set hello values for **NAME**, **USER**, **PASSWORD** and **HOST** from hello **CONNECTIONSTRING**.</span></span>
   
        DATABASES = {
            'default': {
                'ENGINE': 'django.db.backends.mysql',
                'NAME': '<Database>',
                'USER': '<User Id>',
                'PASSWORD': '<Password>',
                'HOST': '<Data Source>',
                'PORT': '',
            }
        }
2. <span data-ttu-id="b8236-163">Dans l’Explorateur de solutions, sous **environnements Python**, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.</span><span class="sxs-lookup"><span data-stu-id="b8236-163">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
3. <span data-ttu-id="b8236-164">Installer le package de hello `mysqlclient` à l’aide de **pip**.</span><span class="sxs-lookup"><span data-stu-id="b8236-164">Install hello package `mysqlclient` using **pip**.</span></span>
   
    ![Boîte de dialogue Installer le package](./media/web-sites-python-ptvs-django-mysql/PollsDjangoMySQLInstallPackage.png)
4. <span data-ttu-id="b8236-166">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.</span><span class="sxs-lookup"><span data-stu-id="b8236-166">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="b8236-167">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="b8236-167">Then select **Django Create Superuser**.</span></span>
   
    <span data-ttu-id="b8236-168">Cela va créer les tables de base de données MySQL hello que vous avez créé dans la section précédente de hello hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-168">This will create hello tables for hello MySQL database you created in hello previous section.</span></span> <span data-ttu-id="b8236-169">Suivez les invites de hello toocreate un utilisateur, qui ne dispose pas utilisateur de hello toomatch dans la base de données sqlite hello créé dans hello première section de cet article.</span><span class="sxs-lookup"><span data-stu-id="b8236-169">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section of this article.</span></span>
5. <span data-ttu-id="b8236-170">Exécutez l’application hello avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="b8236-170">Run hello application with `F5`.</span></span> <span data-ttu-id="b8236-171">Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans la base de données MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="b8236-171">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello MySQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="b8236-172">Publier hello web application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="b8236-172">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="b8236-173">Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="b8236-173">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="b8236-174">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="b8236-174">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
    ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-django-mysql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="b8236-176">Cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="b8236-176">Click on **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="b8236-177">Cliquez sur **nouveau** toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="b8236-177">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="b8236-178">Renseignez hello suivant des champs, cliquez sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="b8236-178">Fill in hello following fields and click **Create**:</span></span>
   
   * <span data-ttu-id="b8236-179">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="b8236-179">**Web App name**</span></span>
   * <span data-ttu-id="b8236-180">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="b8236-180">**App Service plan**</span></span>
   * <span data-ttu-id="b8236-181">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="b8236-181">**Resource group**</span></span>
   * <span data-ttu-id="b8236-182">**Région**</span><span class="sxs-lookup"><span data-stu-id="b8236-182">**Region**</span></span>
   * <span data-ttu-id="b8236-183">Laissez **serveur de base de données** défini trop**aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="b8236-183">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="b8236-184">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="b8236-184">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="b8236-185">Votre navigateur web s’ouvre automatiquement toohello publié web app.</span><span class="sxs-lookup"><span data-stu-id="b8236-185">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="b8236-186">Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **MySQL** base de données hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b8236-186">You should see hello web app working as expected, using hello **MySQL** database hosted on Azure.</span></span>
   
    ![Navigateur web](./media/web-sites-python-ptvs-django-mysql/PollsDjangoAzureBrowser.png)
   
    <span data-ttu-id="b8236-188">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="b8236-188">Congratulations!</span></span> <span data-ttu-id="b8236-189">Vous avez publié votre tooAzure d’application web basée sur MySQL.</span><span class="sxs-lookup"><span data-stu-id="b8236-189">You have successfully published your MySQL-based web app tooAzure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8236-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8236-190">Next steps</span></span>
<span data-ttu-id="b8236-191">Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, Django et MySQL.</span><span class="sxs-lookup"><span data-stu-id="b8236-191">Follow these links toolearn more about Python Tools for Visual Studio, Django and MySQL.</span></span>

* <span data-ttu-id="b8236-192">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="b8236-192">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="b8236-193">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="b8236-193">[Web Projects]</span></span>
  * <span data-ttu-id="b8236-194">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="b8236-194">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="b8236-195">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="b8236-195">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="b8236-196">[Documentation Django]</span><span class="sxs-lookup"><span data-stu-id="b8236-196">[Django Documentation]</span></span>
* <span data-ttu-id="b8236-197">[MySQL]</span><span class="sxs-lookup"><span data-stu-id="b8236-197">[MySQL]</span></span>

<span data-ttu-id="b8236-198">Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b8236-198">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

<!--Link references-->

[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->

[Azure Portal]: https://portal.azure.com
[Python Tools for Visual Studio]: https://www.visualstudio.com/vs/python/
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentation Django]: https://www.djangoproject.com/
[MySQL]: http://www.mysql.com/
[video]: http://youtu.be/oKCApIrS0Lo
