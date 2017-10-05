---
title: "Django et SQL Database sur Azure avec Python Tools 2.2 pour Visual Studio"
description: "Découvrez comment utiliser Python Tools pour Visual Studio afin de créer une application web Django qui stocke les données dans une instance de base de données SQL et de la déployer dans Azure App Service Web Apps."
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
ms.openlocfilehash: 65b59dee2b7bddca77d31c692dab713c68d67e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="django-and-sql-database-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="0e309-103">Django et SQL Database sur Azure avec Python Tools 2.2 pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e309-103">Django and SQL Database on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="0e309-104">Dans ce didacticiel, nous allons utiliser [Python Tools pour Visual Studio] afin de créer une application web de sondage simple, à l’aide de l’un des exemples de modèle PTVS.</span><span class="sxs-lookup"><span data-stu-id="0e309-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="0e309-105">Ce didacticiel est également disponible en [vidéo](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span><span class="sxs-lookup"><span data-stu-id="0e309-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=ZwcoGcIeHF4).</span></span>

<span data-ttu-id="0e309-106">Nous allons découvrir comment utiliser une base de données SQL hébergée sur Azure, comment configurer l’application web pour utiliser une base de données SQL et comment publier l’application web sur [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="0e309-106">We'll learn how to use a SQL database hosted on Azure, how to configure the web app to use a SQL database, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="0e309-107">Visitez le [Centre de développement Python] pour consulter d’autres articles sur le développement d’applications Azure App Service Web Apps avec PTVS à l’aide des infrastructures web Bottle, Flask et Django, ainsi que des services Azure Table Storage, MySQL et Base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0e309-107">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="0e309-108">Cet article concerne App Service, mais les étapes sont similaires lorsque vous développez pour [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="0e309-108">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e309-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0e309-109">Prerequisites</span></span>
* <span data-ttu-id="0e309-110">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0e309-110">Visual Studio 2015</span></span>
* <span data-ttu-id="0e309-111">[Python 2.7 32 bits]</span><span class="sxs-lookup"><span data-stu-id="0e309-111">[Python 2.7 32-bit]</span></span>
* <span data-ttu-id="0e309-112">[Python Tools 2.2 pour Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="0e309-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="0e309-113">[Python Tools 2.2 pour Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="0e309-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="0e309-114">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]</span><span class="sxs-lookup"><span data-stu-id="0e309-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="0e309-115">Django 1.9 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="0e309-115">Django 1.9 or later</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="0e309-116">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="0e309-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0e309-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="0e309-117">No credit cards required; no commitments.</span></span>
>
>

## <a name="create-the-project"></a><span data-ttu-id="0e309-118">Création du projet</span><span class="sxs-lookup"><span data-stu-id="0e309-118">Create the Project</span></span>
<span data-ttu-id="0e309-119">Dans cette section, nous allons créer un projet Visual Studio à l’aide d’un exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="0e309-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="0e309-120">Nous allons créer un environnement virtuel et installer les packages requis.</span><span class="sxs-lookup"><span data-stu-id="0e309-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="0e309-121">Nous allons créer une base de données locale à l’aide de sqlite.</span><span class="sxs-lookup"><span data-stu-id="0e309-121">We'll create a local database using sqlite.</span></span> <span data-ttu-id="0e309-122">Nous exécuterons ensuite l’application web en local.</span><span class="sxs-lookup"><span data-stu-id="0e309-122">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="0e309-123">Dans Visual Studio, sélectionnez **Fichier**, **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="0e309-123">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="0e309-124">Les modèles de projet issus de [Python Tools 2.2 pour Visual Studio Samples VSIX] sont disponibles sous **Python**, **Exemples**.</span><span class="sxs-lookup"><span data-stu-id="0e309-124">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="0e309-125">Sélectionnez **Polls Django Web Project** et cliquez sur OK pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="0e309-125">Select **Polls Django Web Project** and click OK to create the project.</span></span>

     ![Boîte de dialogue Nouveau projet](./media/web-sites-python-ptvs-django-sql/PollsDjangoNewProject.png)
3. <span data-ttu-id="0e309-127">Vous allez être invité à installer des packages externes.</span><span class="sxs-lookup"><span data-stu-id="0e309-127">You will be prompted to install external packages.</span></span> <span data-ttu-id="0e309-128">Sélectionnez **Installer dans un environnement virtuel**.</span><span class="sxs-lookup"><span data-stu-id="0e309-128">Select **Install into a virtual environment**.</span></span>

     ![Boîte de dialogue Packages externes](./media/web-sites-python-ptvs-django-sql/PollsDjangoExternalPackages.png)
4. <span data-ttu-id="0e309-130">Sélectionnez **Python 2.7** comme interpréteur de base.</span><span class="sxs-lookup"><span data-stu-id="0e309-130">Select **Python 2.7** as the base interpreter.</span></span>

     ![Boîte de dialogue Ajouter un environnement virtuel](./media/web-sites-python-ptvs-django-sql/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="0e309-132">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet, sélectionnez **Python**, puis **Django Migrate (Migration de Django)**.</span><span class="sxs-lookup"><span data-stu-id="0e309-132">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="0e309-133">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="0e309-133">Then select **Django Create Superuser**.</span></span>
6. <span data-ttu-id="0e309-134">Une console de gestion Django s’ouvre, et une base de données sqlite est créée dans le dossier du projet.</span><span class="sxs-lookup"><span data-stu-id="0e309-134">This will open a Django Management Console and create a sqlite database in the project folder.</span></span> <span data-ttu-id="0e309-135">Suivez les invites pour créer un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0e309-135">Follow the prompts to create a user.</span></span>
7. <span data-ttu-id="0e309-136">Vérifiez que l’application fonctionne en appuyant sur <kbd>F5</kbd>.</span><span class="sxs-lookup"><span data-stu-id="0e309-136">Confirm that the application works by pressing <kbd>F5</kbd>.</span></span>
8. <span data-ttu-id="0e309-137">Cliquez sur **Log in** dans la barre de navigation en haut.</span><span class="sxs-lookup"><span data-stu-id="0e309-137">Click **Log in** from the navigation bar at the top.</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalMenu.png)
9. <span data-ttu-id="0e309-139">Saisissez les informations d’identification de l’utilisateur que vous avez créé quand vous avez synchronisé la base de données.</span><span class="sxs-lookup"><span data-stu-id="0e309-139">Enter the credentials for the user you created when you synchronized the database.</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserLocalLogin.png)
10. <span data-ttu-id="0e309-141">Cliquez sur **Create Sample Polls**.</span><span class="sxs-lookup"><span data-stu-id="0e309-141">Click **Create Sample Polls**.</span></span>

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoCommonBrowserNoPolls.png)
11. <span data-ttu-id="0e309-143">Cliquez sur un sondage et votez.</span><span class="sxs-lookup"><span data-stu-id="0e309-143">Click on a poll and vote.</span></span>

      ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqliteBrowser.png)

## <a name="create-a-sql-database"></a><span data-ttu-id="0e309-145">Création d’une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="0e309-145">Create a SQL Database</span></span>
<span data-ttu-id="0e309-146">Pour la base de données, nous allons créer une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0e309-146">For the database, we'll create an Azure SQL database.</span></span>

<span data-ttu-id="0e309-147">Pour cela, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0e309-147">You can create a database by following these steps.</span></span>

1. <span data-ttu-id="0e309-148">Connectez-vous au [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="0e309-148">Log into the [Azure Portal].</span></span>
2. <span data-ttu-id="0e309-149">En bas du volet de navigation, cliquez sur **NOUVEAU**.</span><span class="sxs-lookup"><span data-stu-id="0e309-149">At the bottom of the navigation pane, click **NEW**.</span></span> <span data-ttu-id="0e309-150">Ensuite, cliquez sur **Données + stockage** > **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="0e309-150">, click **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="0e309-151">Configurez la nouvelle base de données SQL en créant un nouveau groupe de ressources, puis sélectionnez l’emplacement approprié pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="0e309-151">Configure the new SQL Database by creating a new resource group and select the appropriate location for it.</span></span>
4. <span data-ttu-id="0e309-152">Une fois la base de données SQL créée, cliquez sur **Ouvrir dans Visual Studio** dans le panneau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="0e309-152">Once the SQL Database is created, click **Open in Visual Studio** in the database blade.</span></span>
5. <span data-ttu-id="0e309-153">Cliquez sur **Configurer votre pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="0e309-153">Click **Configure your firewall**.</span></span>
6. <span data-ttu-id="0e309-154">Dans le panneau **Paramètres de pare-feu**, ajoutez une règle de pare-feu avec les champs **IP de début** et **IP de fin** définis sur l’adresse IP publique de votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="0e309-154">In the **Firewall Settings** blade, add a firewall rule with **START IP** and **END IP** set to the public IP address of your development machine.</span></span> <span data-ttu-id="0e309-155">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0e309-155">Click **Save**.</span></span>

   <span data-ttu-id="0e309-156">Les connexions au serveur de base de données de votre ordinateur de développement sont alors autorisées.</span><span class="sxs-lookup"><span data-stu-id="0e309-156">This will allow connections to the database server from your development machine.</span></span>
7. <span data-ttu-id="0e309-157">De retour sur le panneau de la base de données, cliquez sur **Propriétés**, puis sur **Afficher les chaînes de connexion de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="0e309-157">Back in the database blade, click **Properties**, then click **Show database connection strings**.</span></span>
8. <span data-ttu-id="0e309-158">Vous pouvez utiliser le bouton de copie pour placer la valeur de **ADO.NET** dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="0e309-158">Use the copy button to put the value of **ADO.NET** on the clipboard.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="0e309-159">Configurer le projet</span><span class="sxs-lookup"><span data-stu-id="0e309-159">Configure the Project</span></span>
<span data-ttu-id="0e309-160">Dans cette section, nous allons configurer notre application web pour utiliser la base de données SQL que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="0e309-160">In this section, we'll configure our web app to use the SQL database we just created.</span></span> <span data-ttu-id="0e309-161">Nous allons également installer les packages Python supplémentaires requis pour utiliser des bases de données SQL avec Django.</span><span class="sxs-lookup"><span data-stu-id="0e309-161">We'll also install additional Python packages required to use SQL databases with Django.</span></span> <span data-ttu-id="0e309-162">Nous exécuterons ensuite l’application web en local.</span><span class="sxs-lookup"><span data-stu-id="0e309-162">Then we'll run the web app locally.</span></span>

1. <span data-ttu-id="0e309-163">Dans Visual Studio, ouvrez **settings.py**à partir du dossier *ProjectName* .</span><span class="sxs-lookup"><span data-stu-id="0e309-163">In Visual Studio, open **settings.py**, from the *ProjectName* folder.</span></span> <span data-ttu-id="0e309-164">Collez temporairement la chaîne de connexion dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="0e309-164">Temporarily paste the connection string in the editor.</span></span> <span data-ttu-id="0e309-165">Celle-ci se présente au format suivant :</span><span class="sxs-lookup"><span data-stu-id="0e309-165">The connection string is in this format:</span></span>

       Server=<ServerName>,<ServerPort>;Database=<DatabaseName>;User ID=<UserName>;Password={your_password_here};Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;

<span data-ttu-id="0e309-166">Modifiez la définition de `DATABASES` pour utiliser les valeurs ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0e309-166">Edit the definition of `DATABASES` to use the values above.</span></span>

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

1. <span data-ttu-id="0e309-167">Dans l’Explorateur de solutions, sous **Environnements Python**, cliquez avec le bouton droit sur l’environnement virtuel et sélectionnez **Installer le package Python**.</span><span class="sxs-lookup"><span data-stu-id="0e309-167">In Solution Explorer, under **Python Environments**, right-click on the virtual environment and select **Install Python Package**.</span></span>
2. <span data-ttu-id="0e309-168">Installez le package `pyodbc` en utilisant **pip**.</span><span class="sxs-lookup"><span data-stu-id="0e309-168">Install the package `pyodbc` using **pip**.</span></span>

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackagePyodbc.png)
3. <span data-ttu-id="0e309-170">Installez le package `django-pyodbc-azure` en utilisant **pip**.</span><span class="sxs-lookup"><span data-stu-id="0e309-170">Install the package `django-pyodbc-azure` using **pip**.</span></span>

     ![Boîte de dialogue Installer le package Python](./media/web-sites-python-ptvs-django-sql/PollsDjangoSqlInstallPackageDjangoPyodbcAzure.png)
4. <span data-ttu-id="0e309-172">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet, sélectionnez **Python**, puis **Django Migrate (Migration de Django)**.</span><span class="sxs-lookup"><span data-stu-id="0e309-172">In **Solution Explorer**, right-click on the project node and select **Python**, and then select **Django Migrate**.</span></span>  <span data-ttu-id="0e309-173">Sélectionnez ensuite **Django Create Superuser (Créer un superutilisateur Django)**.</span><span class="sxs-lookup"><span data-stu-id="0e309-173">Then select **Django Create Superuser**.</span></span>

   <span data-ttu-id="0e309-174">Les tables de la base de données SQL que nous avons créée dans la section précédente sont alors elles-aussi créées.</span><span class="sxs-lookup"><span data-stu-id="0e309-174">This will create the tables for the SQL database we created in the previous section.</span></span> <span data-ttu-id="0e309-175">Suivez les invites pour créer un utilisateur, qui ne doit pas forcément correspondre à l’utilisateur inclus dans la base de données sqlite que nous avons créée dans la première section.</span><span class="sxs-lookup"><span data-stu-id="0e309-175">Follow the prompts to create a user, which doesn't have to match the user in the sqlite database created in the first section.</span></span>
5. <span data-ttu-id="0e309-176">Exécutez l’application avec `F5`.</span><span class="sxs-lookup"><span data-stu-id="0e309-176">Run the application with `F5`.</span></span> <span data-ttu-id="0e309-177">Les sondages créés à l’aide de la fonction **Create Sample Polls** et les données soumises par vote sont sérialisés dans la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0e309-177">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in the SQL database.</span></span>

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="0e309-178">Publication de l’application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0e309-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="0e309-179">Le Kit de développement logiciel (SDK) Azure .NET offre un moyen simple de déployer votre application web dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="0e309-179">The Azure .NET SDK provides an easy way to deploy your web web app to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="0e309-180">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud du projet et sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0e309-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>

     ![Boîte de dialogue Publier le site Web](./media/web-sites-python-ptvs-django-sql/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="0e309-182">Cliquez sur **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="0e309-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="0e309-183">Cliquez sur **Nouveau** pour créer une application web.</span><span class="sxs-lookup"><span data-stu-id="0e309-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="0e309-184">Renseignez les champs suivants et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0e309-184">Fill in the following fields and click **Create**.</span></span>

   * <span data-ttu-id="0e309-185">**Nom de l’application web**</span><span class="sxs-lookup"><span data-stu-id="0e309-185">**Web App name**</span></span>
   * <span data-ttu-id="0e309-186">**Plan App Service**</span><span class="sxs-lookup"><span data-stu-id="0e309-186">**App Service plan**</span></span>
   * <span data-ttu-id="0e309-187">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="0e309-187">**Resource group**</span></span>
   * <span data-ttu-id="0e309-188">**Région**</span><span class="sxs-lookup"><span data-stu-id="0e309-188">**Region**</span></span>
   * <span data-ttu-id="0e309-189">Dans **Serveur de base de données**, conservez **Aucune base de données**</span><span class="sxs-lookup"><span data-stu-id="0e309-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="0e309-190">Acceptez toutes les valeurs par défaut et cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0e309-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="0e309-191">Votre navigateur web ouvre automatiquement l’application web publiée.</span><span class="sxs-lookup"><span data-stu-id="0e309-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="0e309-192">L’application doit fonctionner comme prévu et utiliser la base de données **SQL** hébergée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0e309-192">You should see the web app working as expected, using the **SQL** database hosted on Azure.</span></span>

   <span data-ttu-id="0e309-193">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="0e309-193">Congratulations!</span></span>

     ![Navigateur web](./media/web-sites-python-ptvs-django-sql/PollsDjangoAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="0e309-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e309-195">Next steps</span></span>
<span data-ttu-id="0e309-196">Suivez ces liens pour en savoir plus sur Python Tools pour Visual Studio, Django et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0e309-196">Follow these links to learn more about Python Tools for Visual Studio, Django and SQL Database.</span></span>

* <span data-ttu-id="0e309-197">[Documentation relative à Python Tools for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="0e309-197">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="0e309-198">[Projets web]</span><span class="sxs-lookup"><span data-stu-id="0e309-198">[Web Projects]</span></span>
  * <span data-ttu-id="0e309-199">[Projets de service cloud]</span><span class="sxs-lookup"><span data-stu-id="0e309-199">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="0e309-200">[Débogage à distance sur Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="0e309-200">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="0e309-201">[Documentation Django]</span><span class="sxs-lookup"><span data-stu-id="0e309-201">[Django Documentation]</span></span>
* <span data-ttu-id="0e309-202">[Base de données SQL]</span><span class="sxs-lookup"><span data-stu-id="0e309-202">[SQL Database]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="0e309-203">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="0e309-203">What's changed</span></span>
* <span data-ttu-id="0e309-204">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="0e309-204">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
<span data-ttu-id="0e309-205">[Centre de développement Python]: /develop/python/</span><span class="sxs-lookup"><span data-stu-id="0e309-205">[Python Developer Center]: /develop/python/</span></span>
<span data-ttu-id="0e309-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span><span class="sxs-lookup"><span data-stu-id="0e309-206">[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md</span></span>

<!--External Link references-->
<span data-ttu-id="0e309-207">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0e309-207">[Azure Portal]: https://portal.azure.com</span></span>
<span data-ttu-id="0e309-208">[Python Tools pour Visual Studio]: http://aka.ms/ptvs</span><span class="sxs-lookup"><span data-stu-id="0e309-208">[Python Tools for Visual Studio]: http://aka.ms/ptvs</span></span>
<span data-ttu-id="0e309-209">[Python Tools 2.2 pour Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="0e309-209">[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="0e309-210">[Python Tools 2.2 pour Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span><span class="sxs-lookup"><span data-stu-id="0e309-210">[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025</span></span>
<span data-ttu-id="0e309-211">[Outils du Kit de développement logiciel (SDK) Azure pour Visual Studio 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span><span class="sxs-lookup"><span data-stu-id="0e309-211">[Azure SDK Tools for VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003</span></span>
<span data-ttu-id="0e309-212">[Python 2.7 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190</span><span class="sxs-lookup"><span data-stu-id="0e309-212">[Python 2.7 32-bit]: http://go.microsoft.com/fwlink/?LinkId=517190</span></span>
<span data-ttu-id="0e309-213">[Documentation relative à Python Tools for Visual Studio]: http://aka.ms/ptvsdocs</span><span class="sxs-lookup"><span data-stu-id="0e309-213">[Python Tools for Visual Studio Documentation]: http://aka.ms/ptvsdocs</span></span>
<span data-ttu-id="0e309-214">[Débogage à distance sur Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span><span class="sxs-lookup"><span data-stu-id="0e309-214">[Remote Debugging on Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026</span></span>
<span data-ttu-id="0e309-215">[Projets web]: http://go.microsoft.com/fwlink/?LinkId=624027</span><span class="sxs-lookup"><span data-stu-id="0e309-215">[Web Projects]: http://go.microsoft.com/fwlink/?LinkId=624027</span></span>
<span data-ttu-id="0e309-216">[Projets de service cloud]: http://go.microsoft.com/fwlink/?LinkId=624028</span><span class="sxs-lookup"><span data-stu-id="0e309-216">[Cloud Service Projects]: http://go.microsoft.com/fwlink/?LinkId=624028</span></span>
<span data-ttu-id="0e309-217">[Documentation Django]: https://www.djangoproject.com/</span><span class="sxs-lookup"><span data-stu-id="0e309-217">[Django Documentation]: https://www.djangoproject.com/</span></span>
<span data-ttu-id="0e309-218">[Base de données SQL]: /documentation/services/sql-database/</span><span class="sxs-lookup"><span data-stu-id="0e309-218">[SQL Database]: /documentation/services/sql-database/</span></span>
