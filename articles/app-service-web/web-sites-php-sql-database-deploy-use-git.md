---
title: "aaaCreate une SQL PHP application web et déployer tooAzure du Service d’applications à l’aide de Git"
description: "Un didacticiel qui montre comment toocreate PHP web application qui stocke les données dans la base de données SQL Azure et utiliser Git tooAzure de déploiement du Service d’applications."
services: app-service\web, sql-database
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6b090bf6-31d8-4b74-81eb-050ef95929ca
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aaacb2fe0787bbcdafa72871912e8d08792be29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a><span data-ttu-id="116ed-103">Créer une application web de PHP-SQL et de déployer tooAzure du Service d’applications à l’aide de Git</span><span class="sxs-lookup"><span data-stu-id="116ed-103">Create a PHP-SQL web app and deploy tooAzure App Service using Git</span></span>
<span data-ttu-id="116ed-104">Ce didacticiel vous montre comment toocreate PHP web app dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) qui connecte tooAzure base de données SQL et comment toodeploy à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="116ed-104">This tutorial shows you how toocreate a PHP web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) that connects tooAzure SQL Database and how toodeploy it using Git.</span></span> <span data-ttu-id="116ed-105">Ce didacticiel suppose que vous avez [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server pour PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), et [Git] [ install-git] installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="116ed-105">This tutorial assumes you have [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server for PHP](http://www.microsoft.com/download/en/details.aspx?id=20098), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="116ed-106">À la fin de ce guide, vous disposerez d’une application web PHP-SQL s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="116ed-106">Upon completing this guide, you will have a PHP-SQL web app running in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="116ed-107">Vous pouvez installer et configurer PHP, SQL Server Express et hello Microsoft Drivers for SQL Server pour PHP à l’aide de hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="116ed-107">You can install and configure PHP, SQL Server Express, and hello Microsoft Drivers for SQL Server for PHP using hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> 
> 

<span data-ttu-id="116ed-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="116ed-108">You will learn:</span></span>

* <span data-ttu-id="116ed-109">Comment toocreate Azure web app et une base de données SQL à l’aide de hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="116ed-109">How toocreate an Azure web app and a SQL Database using hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="116ed-110">PHP est activé dans les applications Web de Service application par défaut, rien de spécial est nécessaire toorun votre code PHP.</span><span class="sxs-lookup"><span data-stu-id="116ed-110">Because PHP is enabled in App Service Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="116ed-111">Comment toopublish et republiez votre tooAzure d’application à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="116ed-111">How toopublish and re-publish your application tooAzure using Git.</span></span>

<span data-ttu-id="116ed-112">En suivant ce didacticiel, vous allez générer une application Web d'inscription simple dans PHP.</span><span class="sxs-lookup"><span data-stu-id="116ed-112">By following this tutorial, you will build a simple registration web application in PHP.</span></span> <span data-ttu-id="116ed-113">Hello application sera hébergée dans un site Web Azure.</span><span class="sxs-lookup"><span data-stu-id="116ed-113">hello application will be hosted in an Azure Website.</span></span> <span data-ttu-id="116ed-114">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="116ed-114">A screenshot of hello completed application is below:</span></span>

![Site Web PHP Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="116ed-116">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="116ed-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="116ed-117">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="116ed-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a><span data-ttu-id="116ed-118">Création d’une application web Azure et configuration de la publication Git</span><span class="sxs-lookup"><span data-stu-id="116ed-118">Create an Azure web app and set up Git publishing</span></span>
<span data-ttu-id="116ed-119">Suivez ces étapes de toocreate une application web Azure et une base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="116ed-119">Follow these steps toocreate an Azure web app and a SQL Database:</span></span>

1. <span data-ttu-id="116ed-120">Connectez-vous à toohello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="116ed-120">Log in toohello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="116ed-121">Ouvrez hello Azure Marketplace en cliquant sur hello **nouveau** icône en haut de hello à gauche du tableau de bord hello, cliquez sur **sélectionner tout** tooMarketplace suivant et en sélectionnant **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="116ed-121">Open hello Azure Marketplace by clicking hello **New** icon on hello top left of hello dashboard, click on **Select All** next tooMarketplace and selecting **Web + Mobile**.</span></span>
3. <span data-ttu-id="116ed-122">Bonjour Marketplace, sélectionnez **Web + Mobile**.</span><span class="sxs-lookup"><span data-stu-id="116ed-122">In hello Marketplace, select **Web + Mobile**.</span></span>
4. <span data-ttu-id="116ed-123">Cliquez sur hello **Web application + SQL** icône.</span><span class="sxs-lookup"><span data-stu-id="116ed-123">Click hello **Web app + SQL** icon.</span></span>
5. <span data-ttu-id="116ed-124">Après avoir lu la description hello de l’application hello Web + SQL application, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="116ed-124">After reading hello description of hello Web app + SQL app, select **Create**.</span></span>
6. <span data-ttu-id="116ed-125">Cliquez sur chaque partie (**groupe de ressources**, **Web App**, **base de données**, et **abonnement**) et entrez ou sélectionnez les valeurs pour hello requis champs :</span><span class="sxs-lookup"><span data-stu-id="116ed-125">Click on each part (**Resource Group**, **Web App**, **Database**, and **Subscription**) and enter or select values for hello required fields:</span></span>
   
   * <span data-ttu-id="116ed-126">Entrez le nom d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="116ed-126">Enter a URL name of your choice</span></span>    
   * <span data-ttu-id="116ed-127">Configuration des informations d’identification du serveur de bases de données</span><span class="sxs-lookup"><span data-stu-id="116ed-127">Configure database server credentials</span></span>
   * <span data-ttu-id="116ed-128">Sélectionnez tooyou le plus proche de la région de hello</span><span class="sxs-lookup"><span data-stu-id="116ed-128">Select hello region closest tooyou</span></span>
     
     ![Configurer une application](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. <span data-ttu-id="116ed-130">Une fois la définition de l’application hello web, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="116ed-130">When finished defining hello web app, click **Create**.</span></span>
   
    <span data-ttu-id="116ed-131">Lorsque l’application hello web a été créée, hello **Notifications** un vert clignote en bouton **réussite** et hello ressource groupe panneau ouvert tooshow deux hello web app et hello SQL de base de données dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-131">When hello web app has been created, hello **Notifications** button will flash a green **SUCCESS** and hello resource group blade open tooshow both hello web app and hello SQL database in hello group.</span></span>
8. <span data-ttu-id="116ed-132">Cliquez sur icône de l’application hello web dans le panneau de hello ressource groupe panneau tooopen hello application web.</span><span class="sxs-lookup"><span data-stu-id="116ed-132">Click hello web app's icon in hello resource group blade tooopen hello web app's blade.</span></span>
   
    ![Groupe de ressources de l’application web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. <span data-ttu-id="116ed-134">Dans **Paramètres**, cliquez sur **Déploiement continu** > **Configurer les paramètres requis**.</span><span class="sxs-lookup"><span data-stu-id="116ed-134">In **Settings** click **Continuous deployment** > **Configure required settings**.</span></span> <span data-ttu-id="116ed-135">Sélectionnez **Référentiel Git local**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="116ed-135">Select **Local Git Repository** and click **OK**.</span></span>
   
    ![où est votre code source](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    <span data-ttu-id="116ed-137">Si vous n’avez pas encore configuré de référentiel Git, vous devez fournir un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="116ed-137">If you have not set up a Git repository before, you must provide a user name and password.</span></span> <span data-ttu-id="116ed-138">toodo, cliquez sur **paramètres** > **informations d’identification de déploiement** dans le panneau de l’application hello web.</span><span class="sxs-lookup"><span data-stu-id="116ed-138">toodo this, click **Settings** > **Deployment credentials** in hello web app's blade.</span></span>
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. <span data-ttu-id="116ed-139">Dans **paramètres** cliquez sur **propriétés** toosee hello Git URL distante vous besoin de votre application PHP toouse toodeploy plus tard.</span><span class="sxs-lookup"><span data-stu-id="116ed-139">In **Settings** click on **Properties** toosee hello Git remote URL you need toouse toodeploy your PHP app later.</span></span>

## <a name="get-sql-database-connection-information"></a><span data-ttu-id="116ed-140">Obtention des informations de connexion à la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="116ed-140">Get SQL Database connection information</span></span>
<span data-ttu-id="116ed-141">instance de base de données SQL toohello tooconnect qui est lié l’application web tooyour, votre besoin hello les informations de connexion, vous avez spécifié lors de la création de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-141">tooconnect toohello SQL Database instance that is linked tooyour web app, your will need hello connection information, which you specified when you created hello database.</span></span> <span data-ttu-id="116ed-142">tooget hello informations de connexion de base de données SQL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="116ed-142">tooget hello SQL Database connection information, follow these steps:</span></span>

1. <span data-ttu-id="116ed-143">Dans le panneau du groupe de ressources hello, cliquez sur icône de hello SQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="116ed-143">Back in hello resource group's blade, click hello SQL database's icon.</span></span>
2. <span data-ttu-id="116ed-144">Dans le panneau de hello SQL de base de données, cliquez sur **paramètres** > **propriétés**, puis cliquez sur **afficher les chaînes de connexion de base de données**.</span><span class="sxs-lookup"><span data-stu-id="116ed-144">In hello SQL database's blade, click **Settings** > **Properties**, then click **Show database connection strings**.</span></span> 
   
    ![Afficher les propriétés de base de données](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. <span data-ttu-id="116ed-146">À partir de hello **PHP** section de la boîte de dialogue hello, notez les valeurs hello pour `Server`, `SQL Database`, et `User Name`.</span><span class="sxs-lookup"><span data-stu-id="116ed-146">From hello **PHP** section of hello resulting dialog, make note of hello values for `Server`, `SQL Database`, and `User Name`.</span></span> <span data-ttu-id="116ed-147">Vous utiliserez ces valeurs ultérieurement de publication lorsque votre tooAzure d’application PHP web du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="116ed-147">You will use these values later when publishing your PHP web app tooAzure App Service.</span></span>

## <a name="build-and-test-your-application-locally"></a><span data-ttu-id="116ed-148">Génération et test de votre application localement</span><span class="sxs-lookup"><span data-stu-id="116ed-148">Build and test your application locally</span></span>
<span data-ttu-id="116ed-149">Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="116ed-149">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="116ed-150">Les informations relatives aux précédents inscrits sont affichées dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="116ed-150">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="116ed-151">Les informations d'inscription sont stockées dans une instance de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="116ed-151">Registration information is stored in a SQL Database instance.</span></span> <span data-ttu-id="116ed-152">application Hello se compose de deux fichiers (code de copier/coller ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="116ed-152">hello application consists of two files (copy/paste code available below):</span></span>

* <span data-ttu-id="116ed-153">**index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.</span><span class="sxs-lookup"><span data-stu-id="116ed-153">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="116ed-154">**CreateTable.PHP**: crée la table de base de données SQL hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-154">**createtable.php**: Creates hello SQL Database table for hello application.</span></span> <span data-ttu-id="116ed-155">Ce fichier sera utilisé une seule fois.</span><span class="sxs-lookup"><span data-stu-id="116ed-155">This file will only be used once.</span></span>

<span data-ttu-id="116ed-156">application de hello toorun localement, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="116ed-156">toorun hello application locally, follow hello steps below.</span></span> <span data-ttu-id="116ed-157">Notez que ces étapes supposent que vous avez PHP et de SQL Server Express configuré sur votre ordinateur local, et que vous avez activé hello [extension PDO pour SQL Server][pdo-sqlsrv].</span><span class="sxs-lookup"><span data-stu-id="116ed-157">Note that these steps assume you have PHP and SQL Server Express set up on your local machine, and that you have enabled hello [PDO extension for SQL Server][pdo-sqlsrv].</span></span>

1. <span data-ttu-id="116ed-158">Créez une base de données SQL Server nommée `registration`.</span><span class="sxs-lookup"><span data-stu-id="116ed-158">Create a SQL Server database called `registration`.</span></span> <span data-ttu-id="116ed-159">Vous pouvez les spécifier cela via hello `sqlcmd` invite de commandes avec ces commandes :</span><span class="sxs-lookup"><span data-stu-id="116ed-159">You can do this from hello `sqlcmd` command prompt with these commands:</span></span>
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. <span data-ttu-id="116ed-160">Dans le répertoire racine de votre application, créez deux fichiers : un fichier nommé `createtable.php` et un autre nommé `index.php`.</span><span class="sxs-lookup"><span data-stu-id="116ed-160">In your application root directory, create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="116ed-161">Ouvrez hello `createtable.php` dans un éditeur de texte ou un IDE et ajoutez le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="116ed-161">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="116ed-162">Ce code sera utilisé toocreate hello `registration_tbl` table Bonjour `registration` base de données.</span><span class="sxs-lookup"><span data-stu-id="116ed-162">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
            id INT NOT NULL IDENTITY(1,1) 
            PRIMARY KEY(id),
            name VARCHAR(30),
            email VARCHAR(30),
            date DATE)";
            $conn->query($sql);
        }
        catch(Exception $e){
            die(print_r($e));
        }
        echo "<h3>Table created.</h3>";
        ?>
   
    <span data-ttu-id="116ed-163">Notez que vous aurez besoin des valeurs de hello tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur SQL Server local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="116ed-163">Note that you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local SQL Server user name and password.</span></span>
4. <span data-ttu-id="116ed-164">Dans un terminal au répertoire racine de hello Hello de type hello application commande suivante :</span><span class="sxs-lookup"><span data-stu-id="116ed-164">In a terminal at hello root directory of hello application type hello following command:</span></span>
   
        php -S localhost:8000
5. <span data-ttu-id="116ed-165">Ouvrez un navigateur web et accédez trop**http://localhost:8000/createtable.php**.</span><span class="sxs-lookup"><span data-stu-id="116ed-165">Open a web browser and browse too**http://localhost:8000/createtable.php**.</span></span> <span data-ttu-id="116ed-166">Cela créera hello `registration_tbl` table hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="116ed-166">This will create hello `registration_tbl` table in hello database.</span></span>
6. <span data-ttu-id="116ed-167">Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello base code HTML et CSS pour la page de hello (hello code PHP est ajouté dans les étapes ultérieures).</span><span class="sxs-lookup"><span data-stu-id="116ed-167">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
        <html>
        <head>
        <Title>Registration Form</Title>
        <style type="text/css">
            body { background-color: #fff; border-top: solid 10px #000;
                color: #333; font-size: .85em; margin: 20; padding: 20;
                font-family: "Segoe UI", Verdana, Helvetica, Sans-Serif;
            }
            h1, h2, h3,{ color: #000; margin-bottom: 0; padding-bottom: 0; }
            h1 { font-size: 2em; }
            h2 { font-size: 1.75em; }
            h3 { font-size: 1.2em; }
            table { margin-top: 0.75em; }
            th { font-size: 1.2em; text-align: left; border: none; padding-left: 0; }
            td { padding: 0.25em 2em 0.25em 0em; border: 0 none; }
        </style>
        </head>
        <body>
        <h1>Register here!</h1>
        <p>Fill in your name and email address, then click <strong>Submit</strong> tooregister.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
7. <span data-ttu-id="116ed-168">Dans les balises PHP hello, ajoutez le code PHP pour la connexion de base de données toohello.</span><span class="sxs-lookup"><span data-stu-id="116ed-168">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost\sqlexpress";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "sqlsrv:Server= $host ; Database = $db ", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
    <span data-ttu-id="116ed-169">Là encore, vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="116ed-169">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
8. <span data-ttu-id="116ed-170">Après le code de connexion de base de données hello, ajoutez le code pour l’insertion des informations d’inscription dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-170">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
        if(!empty($_POST)) {
        try {
            $name = $_POST['name'];
            $email = $_POST['email'];
            $date = date("Y-m-d");
            // Insert data
            $sql_insert = "INSERT INTO registration_tbl (name, email, date) 
                           VALUES (?,?,?)";
            $stmt = $conn->prepare($sql_insert);
            $stmt->bindValue(1, $name);
            $stmt->bindValue(2, $email);
            $stmt->bindValue(3, $date);
            $stmt->execute();
        }
        catch(Exception $e) {
            die(var_dump($e));
        }
        echo "<h3>Your're registered!</h3>";
        }
9. <span data-ttu-id="116ed-171">Enfin, après le code hello ci-dessus, ajoutez du code pour récupérer des données à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-171">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
        $sql_select = "SELECT * FROM registration_tbl";
        $stmt = $conn->query($sql_select);
        $registrants = $stmt->fetchAll(); 
        if(count($registrants) > 0) {
            echo "<h2>People who are registered:</h2>";
            echo "<table>";
            echo "<tr><th>Name</th>";
            echo "<th>Email</th>";
            echo "<th>Date</th></tr>";
            foreach($registrants as $registrant) {
                echo "<tr><td>".$registrant['name']."</td>";
                echo "<td>".$registrant['email']."</td>";
                echo "<td>".$registrant['date']."</td></tr>";
            }
             echo "</table>";
        } else {
            echo "<h3>No one is currently registered.</h3>";
        }

<span data-ttu-id="116ed-172">Vous pouvez maintenant rechercher trop**http://localhost:8000/index.php** application hello de tootest.</span><span class="sxs-lookup"><span data-stu-id="116ed-172">You can now browse too**http://localhost:8000/index.php** tootest hello application.</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="116ed-173">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="116ed-173">Publish your application</span></span>
<span data-ttu-id="116ed-174">Après avoir testé votre application localement, vous pouvez le publier tooApp Service Web Apps à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="116ed-174">After you have tested your application locally, you can publish it tooApp Service Web Apps using Git.</span></span> <span data-ttu-id="116ed-175">Toutefois, vous devez tout d’abord les informations de connexion de base de données de hello tooupdate dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-175">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="116ed-176">À l’aide des informations de connexion de base de données hello obtenues précédemment (Bonjour **informations de connexion à obtenir de la base de données SQL** section), hello de mise à jour après les informations contenues dans **les deux** hello `createdatabase.php` et `index.php` fichiers par hello les valeurs appropriées :</span><span class="sxs-lookup"><span data-stu-id="116ed-176">Using hello database connection information you obtained earlier (in hello **Get SQL Database connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> <span data-ttu-id="116ed-177">Bonjour <code>$host</code>, valeur hello du serveur doit être précédé de <code>tcp:</code>.</span><span class="sxs-lookup"><span data-stu-id="116ed-177">In hello <code>$host</code>, hello value of Server must be prepended with <code>tcp:</code>.</span></span>
> 
> 

<span data-ttu-id="116ed-178">Maintenant, vous êtes prêt tooset de publication Git et que vous publiez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-178">Now, you are ready tooset up Git publishing and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="116ed-179">Il s’agit hello mêmes étapes indiqué plus haut fin hello Hello **créer une application web Azure et configurer la publication Git** section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="116ed-179">These are hello same steps noted at hello end of hello **Create an Azure web app and set up Git publishing** section above.</span></span>
> 
> 

1. <span data-ttu-id="116ed-180">Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`), remplacer répertoires toohello racine de votre application (hello **inscription** active), et en exécution hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="116ed-180">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application (hello **registration** directory), and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="116ed-181">Vous demandera un mot de passe hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="116ed-181">You will be prompted for hello password you created earlier.</span></span>
2. <span data-ttu-id="116ed-182">Parcourir trop**http://[web application name].azurewebsites.net/createtable.php** table de base de données SQL toocreate hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-182">Browse too**http://[web app name].azurewebsites.net/createtable.php** toocreate hello SQL database table for hello application.</span></span>
3. <span data-ttu-id="116ed-183">Parcourir trop**http://[web application name].azurewebsites.net/index.php** toobegin à l’aide d’application hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-183">Browse too**http://[web app name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

<span data-ttu-id="116ed-184">Une fois que vous avez publié votre application, vous pouvez commencer à apporter des modifications tooit et utiliser Git toopublish les.</span><span class="sxs-lookup"><span data-stu-id="116ed-184">After you have published your application, you can begin making changes tooit and use Git toopublish them.</span></span> 

## <a name="publish-changes-tooyour-application"></a><span data-ttu-id="116ed-185">Publier les modifications tooyour application</span><span class="sxs-lookup"><span data-stu-id="116ed-185">Publish changes tooyour application</span></span>
<span data-ttu-id="116ed-186">toopublish change tooapplication, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="116ed-186">toopublish changes tooapplication, follow these steps:</span></span>

1. <span data-ttu-id="116ed-187">Apporter des modifications application tooyour localement.</span><span class="sxs-lookup"><span data-stu-id="116ed-187">Make changes tooyour application locally.</span></span>
2. <span data-ttu-id="116ed-188">Ouvrez GitBash (ou un terminal, informatique Git est dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="116ed-188">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="116ed-189">Vous demandera un mot de passe hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="116ed-189">You will be prompted for hello password you created earlier.</span></span>
3. <span data-ttu-id="116ed-190">Parcourir trop**http://[web application name].azurewebsites.net/index.php** toosee vos modifications.</span><span class="sxs-lookup"><span data-stu-id="116ed-190">Browse too**http://[web app name].azurewebsites.net/index.php** toosee your changes.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="116ed-191">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="116ed-191">What's changed</span></span>
* <span data-ttu-id="116ed-192">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="116ed-192">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

