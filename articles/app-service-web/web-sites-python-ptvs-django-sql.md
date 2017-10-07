---
title: "aaaDjango et base de données SQL Azure avec 2.2 des outils Python pour Visual Studio"
description: "Découvrez comment toouse hello outils Python pour Visual Studio toocreate, une application web Django qui stocke les données dans une instance de la base de données SQL et le déployer tooAzure App Service Web Apps."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: 3a677e64-b5a9-4d43-b9c0-66246368b483
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: b5b2ef4f3292e7df85007465c5394c8660a7d231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="89b1d-103">Django et SQL Database sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89b1d-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="89b1d-104">Dans ce didacticiel, nous allons utiliser [outils Python pour Visual Studio] toocreate simple interroge l’application web à l’aide d’un des exemples de modèles de PTVS hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="89b1d-105">Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="89b1d-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="89b1d-106">Nous verrons comment toouse une base de données SQL hébergée sur Azure, comment tooconfigure hello toouse d’application web, une base de données SQL et comment toopublish hello web application trop[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="89b1d-106">We'll learn how toouse a SQL database hosted on Azure, how tooconfigure hello web app toouse a SQL database, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="89b1d-107">Consultez hello [centre de développement Python] autres articles qui couvrent le développement de Azure App Service Web Apps avec PTVS à l’aide d’eau, ballon Django web et infrastructures, avec les services de stockage de Table Azure, MySQL et base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="89b1d-107">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="89b1d-108">Alors que cet article se concentre sur le Service d’applications, les étapes de hello sont similaires lors du développement [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="89b1d-108">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b1d-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89b1d-109">Prerequisites</span></span>
* <span data-ttu-id="89b1d-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="89b1d-110">Visual Studio 2015</span></span>
* <span data-ttu-id="89b1d-111">[Python 2.7 32 bits]</span><span class="sxs-lookup"><span data-stu-id="89b1d-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="89b1d-112">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89b1d-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="89b1d-113">[2.2 des outils Python pour Visual Studio exemples VSIX]</span><span class="sxs-lookup"><span data-stu-id="89b1d-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="89b1d-114">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="89b1d-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="89b1d-115">Django 1.9 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="89b1d-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="89b1d-116">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="89b1d-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="89b1d-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="89b1d-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-hello-project"></a><span data-ttu-id="89b1d-118">Créer hello projet</span><span class="sxs-lookup"><span data-stu-id="89b1d-118">Create hello Project</span></span>
<span data-ttu-id="89b1d-119">Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="89b1d-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="89b1d-120">Nous allons créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="89b1d-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="89b1d-121">Nous allons créer une base de données locale à l’aide de sqlite.</span><span class="sxs-lookup"><span data-stu-id="89b1d-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="89b1d-122">Puis nous exécuterons hello web application localement.</span><span class="sxs-lookup"><span data-stu-id="89b1d-122">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="89b1d-123">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="89b1d-124">Hello des modèles de projet à partir de hello [2.2 des outils Python pour Visual Studio exemples VSIX] sont disponibles sous **Python**, **exemples**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-124">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="89b1d-125">Sélectionnez **interroge Django Web projet** et cliquez sur OK toocreate hello projet.</span><span class="sxs-lookup"><span data-stu-id="89b1d-125">Select **Polls Django Web Project** and click OK toocreate hello project.</span></span>

     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="89b1d-127">Vous serez invité à tooinstall les packages externes.</span><span class="sxs-lookup"><span data-stu-id="89b1d-127">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="89b1d-128">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-128">Select **Install into a virtual environment**.</span></span>

     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="89b1d-130">Sélectionnez **Python 2.7** comme interpréteur de base hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-130">Select **Python 2.7** as hello base interpreter.</span></span>

     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="89b1d-132">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-132">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="89b1d-133">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="89b1d-134">Vous ouvrez une Console de gestion Django et créer une base de données sqlite dans le dossier de projet hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-134">This will open a Django Management Console and create a sqlite database in hello project folder.</span></span> <span data-ttu-id="89b1d-135">Suivez les invites de hello toocreate un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89b1d-135">Follow hello prompts toocreate a user.</span></span>
7. <span data-ttu-id="89b1d-136">Vérifier que l’application hello fonctionne en appuyant sur <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="89b1d-136">Confirm that hello application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="89b1d-137">Cliquez sur **connecter** à partir de la barre de navigation hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-137">Click **Log in** from hello navigation bar at hello top.</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="89b1d-139">Entrez des informations d’identification de hello pour utilisateur hello que vous avez créé lors de la synchronisation de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-139">Enter hello credentials for hello user you created when you synchronized hello database.</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="89b1d-141">Cliquez sur **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-141">Click **Create Sample Polls**.</span></span>

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="89b1d-143">Cliquez sur un sondage et votez.</span><span class="sxs-lookup"><span data-stu-id="89b1d-143">Click on a poll and vote.</span></span>

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="89b1d-145">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="89b1d-145">Create a SQL Database</span></span>
<span data-ttu-id="89b1d-146">Pour la base de données hello, nous allons créer une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89b1d-146">For hello database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="89b1d-147">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89b1d-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="89b1d-148">Ouvrez une session sur hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="89b1d-148">Log into hello [Azure Portal].</span></span>
2. <span data-ttu-id="89b1d-149">Au bas de hello hello du volet de navigation, cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-149">At hello bottom of hello navigation pane, click **NEW**.</span></span> <span data-ttu-id="89b1d-150">Ensuite, cliquez sur **Données + stockage** > **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="89b1d-151">Configurer hello de base de données SQL en créant un nouveau groupe de ressources et sélectionnez hello emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="89b1d-151">Configure hello new SQL Database by creating a new resource group and select hello appropriate location for it.</span></span>
4. <span data-ttu-id="89b1d-152">Une fois hello de base de données SQL est créé, cliquez sur **ouvert dans Visual Studio** dans le panneau de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-152">Once hello SQL Database is created, click **Open in Visual Studio** in hello database blade.</span></span>
5. <span data-ttu-id="89b1d-153">Cliquez sur **Configurer votre pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="89b1d-154">Bonjour **les paramètres de pare-feu** panneau, ajouter une règle de pare-feu avec **IP de début** et **IP de fin** définir toohello une adresse IP publique de votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="89b1d-154">In hello **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set toohello public IP address of your development machine.</span></span> <span data-ttu-id="89b1d-155">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-155">Click **Save**.</span></span>

   <span data-ttu-id="89b1d-156">Cela permettra de serveur de base de données toohello de connexions à partir de votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="89b1d-156">This will allow connections toohello database server from your development machine.</span></span>
7. <span data-ttu-id="89b1d-157">Dans le panneau de la base de données hello, cliquez sur **propriétés**, puis cliquez sur **afficher les chaînes de connexion de base de données**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-157">Back in hello database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="89b1d-158">Utilisez hello copie bouton tooput hello valeur **ADO.NET** Presse-papiers de hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-158">Use hello copy button tooput hello value of **ADO.NET** on hello clipboard.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="89b1d-159">Configurer hello projet</span><span class="sxs-lookup"><span data-stu-id="89b1d-159">Configure hello Project</span></span>
<span data-ttu-id="89b1d-160">Dans cette section, nous allons configurer notre web application toouse hello SQL de base de données créée.</span><span class="sxs-lookup"><span data-stu-id="89b1d-160">In this section, we'll configure our web app toouse hello SQL database we just created.</span></span> <span data-ttu-id="89b1d-161">Nous allons également installer Python packages requis toouse SQL bases de données supplémentaires avec Django.</span><span class="sxs-lookup"><span data-stu-id="89b1d-161">We'll also install additional Python packages required toouse SQL databases with Django.</span></span> <span data-ttu-id="89b1d-162">Puis nous exécuterons hello web application localement.</span><span class="sxs-lookup"><span data-stu-id="89b1d-162">Then we'll run hello web app locally.</span></span>

1. <span data-ttu-id="89b1d-163">Dans Visual Studio, ouvrez **settings.py**, à partir de hello *nom_projet* dossier.</span><span class="sxs-lookup"><span data-stu-id="89b1d-163">In Visual Studio, open **settings.py**, from hello *ProjectName* folder.</span></span> <span data-ttu-id="89b1d-164">Collez temporairement chaîne de connexion hello dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-164">Temporarily paste hello connection string in hello editor.</span></span> <span data-ttu-id="89b1d-165">chaîne de connexion Hello est au format suivant :</span><span class="sxs-lookup"><span data-stu-id="89b1d-165">hello connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="89b1d-166">Modifier la définition de hello de `DATABASES` toouse les valeurs hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="89b1d-166">Edit hello definition of `DATABASES` toouse hello values above.</span></span>

        DATABASES = {
            'default': {
                'ENGINE': 'sql_server.pyodbc',
                'NAME': '<DatabaseName>',
                'USER': '<UserName>',
                'PASSWORD': '{your_password_here}',
                'HOST': '<ServerName>',
                'PORT': '<ServerPort>',
                'OPTIONS': {
                    'driver': 'SQL Server Native Client 11.0',
                    'MARS_Connection': 'True',
                }
            }
        }

1. <span data-ttu-id="89b1d-167">Dans l’Explorateur de solutions, sous **environnements Python**, avec le bouton droit sur l’environnement virtuel de hello et sélectionnez **Package d’installation de Python**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-167">In Solution Explorer, under **Python Environments**, right-click on hello virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="89b1d-168">Installer le package de hello `pyodbc` à l’aide de **pip**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-168">Install hello package `pyodbc` using **pip**.</span></span>

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="89b1d-170">Installer le package de hello `django-pyodbc-azure` à l’aide de **pip**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-170">Install hello package `django-pyodbc-azure` using **pip**.</span></span>

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="89b1d-172">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **Python**, puis sélectionnez **Django migrer**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-172">In **Solution Explorer**, right-click on hello project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="89b1d-173">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="89b1d-174">Cela va créer les tables de base de données SQL hello que nous avons créé dans la section précédente de hello hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-174">This will create hello tables for hello SQL database we created in hello previous section.</span></span> <span data-ttu-id="89b1d-175">Suivez les invites de hello toocreate un utilisateur, qui n’a pas utilisateur de hello toomatch dans la base de données sqlite hello créé dans la première section de hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-175">Follow hello prompts toocreate a user, which doesn't have toomatch hello user in hello sqlite database created in hello first section.</span></span>
5. <span data-ttu-id="89b1d-176">Exécutez l’application hello avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="89b1d-176">Run hello application with `F5`.</span></span> <span data-ttu-id="89b1d-177">Les interrogations sont créées avec **créer des sondages exemple** et données hello soumises par le vote seront sérialisées dans la base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="89b1d-177">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in hello SQL database.</span></span>

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="89b1d-178">Publier hello web application tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="89b1d-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="89b1d-179">Hello Kit de développement .NET Azure fournit un moyen simple de toodeploy votre tooAzure d’application web web App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="89b1d-179">hello Azure .NET SDK provides an easy way toodeploy your web web app tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="89b1d-180">Dans **l’Explorateur de solutions**, avec le bouton droit sur le nœud de projet hello et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>

     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="89b1d-182">Cliquez sur **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="89b1d-183">Cliquez sur **nouveau** toocreate une application web.</span><span class="sxs-lookup"><span data-stu-id="89b1d-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="89b1d-184">Renseignez hello suivant des champs, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-184">Fill in hello following fields and click **Create**.</span></span>

   * <span data-ttu-id="89b1d-185">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="89b1d-185">**Web App name**</span></span>
   * <span data-ttu-id="89b1d-186">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="89b1d-186">**App Service plan**</span></span>
   * <span data-ttu-id="89b1d-187">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="89b1d-187">**Resource group**</span></span>
   * <span data-ttu-id="89b1d-188">**Région**</span><span class="sxs-lookup"><span data-stu-id="89b1d-188">**Region**</span></span>
   * <span data-ttu-id="89b1d-189">Laissez **serveur de base de données** défini trop**aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="89b1d-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="89b1d-190">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="89b1d-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="89b1d-191">Votre navigateur web s’ouvre automatiquement toohello publié web app.</span><span class="sxs-lookup"><span data-stu-id="89b1d-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="89b1d-192">Vous devez voir le travail d’application hello web comme prévu, à l’aide de hello **SQL** base de données hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="89b1d-192">You should see hello web app working as expected, using hello **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="89b1d-193">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="89b1d-193">Congratulations!</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="89b1d-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89b1d-195">Next steps</span></span>
<span data-ttu-id="89b1d-196">Suivez ces liens de toolearn plus d’informations sur les outils Python pour Visual Studio, Django et base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="89b1d-196">Follow these links toolearn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="89b1d-197">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="89b1d-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="89b1d-198">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="89b1d-198">[Web Projects]</span></span>
  * <span data-ttu-id="89b1d-199">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="89b1d-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="89b1d-200">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="89b1d-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="89b1d-201">[Documentation Django]</span><span class="sxs-lookup"><span data-stu-id="89b1d-201">[Django Documentation]</span></span>
* <span data-ttu-id="89b1d-202">[Base de données SQL]</span><span class="sxs-lookup"><span data-stu-id="89b1d-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="89b1d-203">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="89b1d-203">What's changed</span></span>
* <span data-ttu-id="89b1d-204">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="89b1d-204">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[centre de développement Python]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[outils Python pour Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[2.2 des outils Python pour Visual Studio exemples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs
[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028
[Documentation Django]: https://www.djangoproject.com/
[Base de données SQL]: /documentation/services/sql-database/
