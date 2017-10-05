---
title: "Créer une application web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP"
description: "Didacticiel expliquant comment créer une application web PHP stockant les données dans MySQL et comment utiliser un déploiement FTP dans Azure."
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6d9d1de5-5868-48fd-8bad-decb4979cd65
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: d428dffc6b810a692be0ec39a5f9cca05f5439e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="c1063-103">Créer une application web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="c1063-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="c1063-104">Ce didacticiel vous indique comment créer une application web PHP-MySQL et comment la déployer à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="c1063-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it using FTP.</span></span> <span data-ttu-id="c1063-105">Il part du principe que vous avez installé [PHP][install-php], [MySQL][install-mysql], un serveur Web et un client FTP sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c1063-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="c1063-106">Les instructions de ce didacticiel s’appliquent à n’importe quel système d’exploitation, notamment Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="c1063-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="c1063-107">À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c1063-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="c1063-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c1063-108">You will learn:</span></span>

* <span data-ttu-id="c1063-109">création d’une application web et d’une base de données MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c1063-109">How to create a web app and a MySQL database using the Azure Portal.</span></span> <span data-ttu-id="c1063-110">(PHP étant activé par défaut dans Web Apps, l’exécution de votre code PHP ne requiert aucune action particulière) ;</span><span class="sxs-lookup"><span data-stu-id="c1063-110">Because PHP is enabled in Web Apps by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="c1063-111">publier votre application sur Azure avec FTP.</span><span class="sxs-lookup"><span data-stu-id="c1063-111">How to publish your application to Azure using FTP.</span></span>

<span data-ttu-id="c1063-112">En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP.</span><span class="sxs-lookup"><span data-stu-id="c1063-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="c1063-113">Cette application sera hébergée dans une application web.</span><span class="sxs-lookup"><span data-stu-id="c1063-113">The application will be hosted in a Web App.</span></span> <span data-ttu-id="c1063-114">Voici une capture d’écran de l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="c1063-114">A screenshot of the completed application is below:</span></span>

![Site Web PHP Azure][running-app]

> [!NOTE]
> <span data-ttu-id="c1063-116">Si vous souhaitez commencer à utiliser Azure App Service avant d’ouvrir un compte, accédez au site [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pouvez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="c1063-116">If you want to get started with Azure App Service before signing up for an account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c1063-117">Aucune carte de crédit n’est requise, et vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="c1063-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="c1063-118">Créer une application web et configurer la publication FTP</span><span class="sxs-lookup"><span data-stu-id="c1063-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="c1063-119">Pour créer une application web et une base de données MySQL, suivez la procédure ci-après :</span><span class="sxs-lookup"><span data-stu-id="c1063-119">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="c1063-120">Connectez-vous au [portail Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="c1063-120">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="c1063-121">Cliquez sur l’icône **+ Nouveau** dans le coin supérieur gauche du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c1063-121">Click the **+ New** icon on the top left of the Azure Portal.</span></span>
   
    ![Créer un site Web Azure][new-website]
3. <span data-ttu-id="c1063-123">Dans la recherche, tapez **Application web + MySQL**, puis cliquez sur **Application web + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="c1063-123">In the search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Création personnalisée d'un site web][custom-create]
4. <span data-ttu-id="c1063-125">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c1063-125">Click **Create**.</span></span> <span data-ttu-id="c1063-126">Saisissez un nom de service d’application unique, un nom valide pour le groupe de ressources et un plan de service.</span><span class="sxs-lookup"><span data-stu-id="c1063-126">Enter a unique app service name, a valid name for the resource group and a new service plan.</span></span>
   
    ![Définir le nom du groupe de ressources][resource-group]
5. <span data-ttu-id="c1063-128">Entrez des valeurs pour votre nouvelle base de données, notamment l’acceptation des conditions juridiques.</span><span class="sxs-lookup"><span data-stu-id="c1063-128">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Créer une base de données MySQL][new-mysql-db]
6. <span data-ttu-id="c1063-130">Une fois que l’application web a été créée, vous voyez apparaître le nouveau volet service d’application.</span><span class="sxs-lookup"><span data-stu-id="c1063-130">When the web app has been created, you will see the new app service blade.</span></span>
7. <span data-ttu-id="c1063-131">Cliquez sur **Paramètres** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="c1063-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Définir les informations d’identification de déploiement][set-deployment-credentials]
8. <span data-ttu-id="c1063-133">Pour activer la publication FTP, vous devez fournir un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1063-133">To enable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="c1063-134">Enregistrez les informations d’identification et notez le nom d’utilisateur et le mot de passe que vous créez.</span><span class="sxs-lookup"><span data-stu-id="c1063-134">Save the credentials and make a note of the user name and password you create.</span></span>
   
    ![Création des informations d’identification de publication][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="c1063-136">Générer et tester votre application localement</span><span class="sxs-lookup"><span data-stu-id="c1063-136">Build and test your app locally</span></span>
<span data-ttu-id="c1063-137">L'application d'inscription est une simple application PHP qui vous permet de vous inscrire à un événement en entrant votre nom et votre adresse électronique.</span><span class="sxs-lookup"><span data-stu-id="c1063-137">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="c1063-138">Les informations relatives aux précédents inscrits sont affichées dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="c1063-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="c1063-139">Les informations d'inscription sont stockées dans une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="c1063-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="c1063-140">L’application se compose de deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="c1063-140">The app consists of two files:</span></span>

* <span data-ttu-id="c1063-141">**index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.</span><span class="sxs-lookup"><span data-stu-id="c1063-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="c1063-142">**createtable.php**: crée la table MySQL de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1063-142">**createtable.php**: Creates the MySQL table for the application.</span></span> <span data-ttu-id="c1063-143">Ce fichier sera utilisé une seule fois.</span><span class="sxs-lookup"><span data-stu-id="c1063-143">This file will only be used once.</span></span>

<span data-ttu-id="c1063-144">Pour générer et exécuter l’application localement, suivez la procédure ci-après.</span><span class="sxs-lookup"><span data-stu-id="c1063-144">To build and run the app locally, follow the steps below.</span></span> <span data-ttu-id="c1063-145">Notez que ces étapes partent du principe que PHP, MySQL et un serveur Web sont installés sur votre ordinateur local et que vous avez activé l’[extension PDO pour MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="c1063-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="c1063-146">Créez une base de données MySQL nommée `registration`.</span><span class="sxs-lookup"><span data-stu-id="c1063-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="c1063-147">Pour cela, utilisez l'invite de commandes MySQL avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="c1063-147">You can do this from the MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="c1063-148">Dans le répertoire racine de votre serveur web, créez un dossier nommé `registration` et deux fichiers à l’intérieur : un fichier nommé `createtable.php` et un autre nommé `index.php`.</span><span class="sxs-lookup"><span data-stu-id="c1063-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="c1063-149">Ouvrez le fichier `createtable.php` dans un éditeur de texte ou un environnement de développement intégré (IDE), puis ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="c1063-149">Open the `createtable.php` file in a text editor or IDE and add the code below.</span></span> <span data-ttu-id="c1063-150">Ce code permet de créer la table `registration_tbl` dans la base de données `registration`.</span><span class="sxs-lookup"><span data-stu-id="c1063-150">This code will be used to create the `registration_tbl` table in the `registration` database.</span></span>
   
        <?php
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        try{
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            $sql = "CREATE TABLE registration_tbl(
                        id INT NOT NULL AUTO_INCREMENT, 
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
   
   > [!NOTE]
   > <span data-ttu-id="c1063-151">Vous devez mettre à jour les valeurs de <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1063-151">You will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="c1063-152">Ouvrez un navigateur Web et accédez à [http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="c1063-152">Open a web browser and browse to [http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="c1063-153">La table `registration_tbl` est créée dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="c1063-153">This will create the `registration_tbl` table in the database.</span></span>
5. <span data-ttu-id="c1063-154">Ouvrez le fichier **index.php** dans un éditeur de texte ou un IDE et ajoutez les codes HTML et CSS de base pour la page (le code PHP sera ajouté plus tard).</span><span class="sxs-lookup"><span data-stu-id="c1063-154">Open the **index.php** file in a text editor or IDE and add the basic HTML and CSS code for the page (the PHP code will be added in later steps).</span></span>
   
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
        <p>Fill in your name and email address, then click <strong>Submit</strong> to register.</p>
        <form method="post" action="index.php" enctype="multipart/form-data" >
              Name  <input type="text" name="name" id="name"/></br>
              Email <input type="text" name="email" id="email"/></br>
              <input type="submit" name="submit" value="Submit" />
        </form>
        <?php
   
        ?>
        </body>
        </html>
6. <span data-ttu-id="c1063-155">Ajoutez le code PHP dans les balises PHP pour la connexion à la base de données.</span><span class="sxs-lookup"><span data-stu-id="c1063-155">Within the PHP tags, add PHP code for connecting to the database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect to database.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="c1063-156">Là encore, vous devez mettre à jour les valeurs de <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c1063-156">Again, you will need to update the values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="c1063-157">À la suite du code de connexion à la base de données, ajoutez le code pour l'insertion des informations d'inscription à la base de données.</span><span class="sxs-lookup"><span data-stu-id="c1063-157">Following the database connection code, add code for inserting registration information into the database.</span></span>
   
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
8. <span data-ttu-id="c1063-158">Pour finir, à la suite du code précédent, ajoutez le code de récupération des données de la base de données.</span><span class="sxs-lookup"><span data-stu-id="c1063-158">Finally, following the code above, add code for retrieving data from the database.</span></span>
   
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

<span data-ttu-id="c1063-159">Vous pouvez maintenant accéder à [http://localhost/registration/index.php][localhost-index] pour tester l’application.</span><span class="sxs-lookup"><span data-stu-id="c1063-159">You can now browse to [http://localhost/registration/index.php][localhost-index] to test the app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="c1063-160">Obtention des informations de connexion MySQL et FTP</span><span class="sxs-lookup"><span data-stu-id="c1063-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="c1063-161">Pour vous connecter à la base de données MySQL qui s’exécute dans Web Apps, vous devez disposer des informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="c1063-161">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="c1063-162">Pour obtenir vos informations de connexion MySQL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1063-162">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="c1063-163">À partir du panneau Application web du service d’application Azure, cliquez sur le lien vers le groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="c1063-163">From the app service web app blade click on the resource group link:</span></span>
   
    ![Sélectionner Groupe de ressources][select-resourcegroup]
2. <span data-ttu-id="c1063-165">À partir de votre groupe de ressources, cliquez sur la base de données :</span><span class="sxs-lookup"><span data-stu-id="c1063-165">From your resource group, click the database:</span></span>
   
    ![Sélectionner la base de données][select-database]
3. <span data-ttu-id="c1063-167">Dans le récapitulatif de base de données, sélectionnez **Paramètres** > **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="c1063-167">From the database summary, select **Settings** > **Properties**.</span></span>
   
    ![Sélectionner les propriétés][select-properties]
4. <span data-ttu-id="c1063-169">Notez les valeurs de `Database`, `Host`, `User Id` et `Password`.</span><span class="sxs-lookup"><span data-stu-id="c1063-169">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Noter les propriétés][note-properties]
5. <span data-ttu-id="c1063-171">Dans votre application web, cliquez sur le lien **Télécharger le profil de publication** dans le coin inférieur droit de la page :</span><span class="sxs-lookup"><span data-stu-id="c1063-171">From your web app, click the **Download publish profile** link at the bottom right corner of the page:</span></span>
   
    ![Télécharger le profil de publication][download-publish-profile]
6. <span data-ttu-id="c1063-173">Ouvrez le fichier `.publishsettings` dans un éditeur XML.</span><span class="sxs-lookup"><span data-stu-id="c1063-173">Open the `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="c1063-174">Recherchez l’élément `<publishProfile >` dont la structure de publication `publishMethod="FTP"` est semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="c1063-174">Find the `<publishProfile >` element with `publishMethod="FTP"` that looks similar to this:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="c1063-175">Notez les attributs `publishUrl`, `userName` et `userPWD`.</span><span class="sxs-lookup"><span data-stu-id="c1063-175">Make note of the `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="c1063-176">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="c1063-176">Publish your app</span></span>
<span data-ttu-id="c1063-177">Après avoir testé votre application localement, vous pouvez la publier dans votre application web à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="c1063-177">After you have tested your app locally, you can publish it to your web app using FTP.</span></span> <span data-ttu-id="c1063-178">Cependant, vous devez d'abord mettre à jour les informations de connexion à la base de données dans l'application.</span><span class="sxs-lookup"><span data-stu-id="c1063-178">However, you first need to update the database connection information in the application.</span></span> <span data-ttu-id="c1063-179">En utilisant les informations de connexion à la base de données obtenues précédemment (dans la section **Obtention des informations de connexion MySQL et FTP**), mettez à jour les informations suivantes dans les **deux** fichiers `createdatabase.php` et `index.php` avec les valeurs appropriées :</span><span class="sxs-lookup"><span data-stu-id="c1063-179">Using the database connection information you obtained earlier (in the **Get MySQL and FTP connection information** section), update the following information in **both** the `createdatabase.php` and `index.php` files with the appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="c1063-180">Vous pouvez à présent publier votre application à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="c1063-180">Now you are ready to publish your app using FTP.</span></span>

1. <span data-ttu-id="c1063-181">Ouvrez le client FTP de votre choix.</span><span class="sxs-lookup"><span data-stu-id="c1063-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="c1063-182">Entrez la *partie du nom d’hôte* de l’attribut `publishUrl`, que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="c1063-182">Enter the *host name portion* from the `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="c1063-183">Entrez également les attributs `userName` et `userPWD` tels que vous les avez notés précédemment.</span><span class="sxs-lookup"><span data-stu-id="c1063-183">Enter the `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="c1063-184">Établissez une connexion.</span><span class="sxs-lookup"><span data-stu-id="c1063-184">Establish a connection.</span></span>

<span data-ttu-id="c1063-185">Une fois connecté, vous pouvez télécharger les fichiers.</span><span class="sxs-lookup"><span data-stu-id="c1063-185">After you have connected you will be able to upload and download files as needed.</span></span> <span data-ttu-id="c1063-186">Veillez à charger les fichiers dans le répertoire racine `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="c1063-186">Be sure that you are uploading files to the root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="c1063-187">Après avoir téléchargé les deux fichiers `index.php` et `createtable.php`, accédez à **http://[site name].azurewebsites.net/createtable.php** pour créer la table MySQL pour l’application, puis accédez à **http://[nom du site].azurewebsites.net/index.php** pour commencer à utiliser l’application.</span><span class="sxs-lookup"><span data-stu-id="c1063-187">After uploading both `index.php` and `createtable.php`, browse to **http://[site name].azurewebsites.net/createtable.php** to create the MySQL table for the application, then browse to **http://[site name].azurewebsites.net/index.php** to begin using the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1063-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1063-188">Next steps</span></span>
<span data-ttu-id="c1063-189">Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="c1063-189">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[install-mysql]: http://dev.mysql.com/doc/refman/5.6/en/installing.html
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[localhost-createtable]: http://localhost/tasklist/createtable.php
[localhost-index]: http://localhost/tasklist/index.php
[running-app]: ./media/web-sites-php-mysql-deploy-use-ftp/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-ftp/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-ftp/create_web_mysql.png
[website-details]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/website_details.jpg
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-ftp/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-ftp/select_webapp.png
[set-deployment-credentials]: ./media/web-sites-php-mysql-deploy-use-ftp/set_credentials.png
[portal-ftp-username-password]: ./media/web-sites-php-mysql-deploy-use-ftp/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-ftp/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-ftp/create_wa.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-ftp/select_database.png
[select-resourcegroup]: ./media/web-sites-php-mysql-deploy-use-ftp/select_resourcegroup.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-ftp/note-properties.png

[connection-string-info]: ./media/web-sites-php-web-site-mysql-deploy-use-ftp/connection_string_info.png
[management-portal]: https://portal.azure.com
[download-publish-profile]: ./media/web-sites-php-mysql-deploy-use-ftp/download_publish_profile_3.png

