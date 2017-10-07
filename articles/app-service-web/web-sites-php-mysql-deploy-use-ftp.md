---
title: "aaaCreate un PHP-MySQL application dans Azure App Service web et le déployer à l’aide de FTP"
description: "Un didacticiel qui montre comment toocreate PHP web application qui stocke les données de MySQL et utilisez tooAzure de déploiement FTP."
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
ms.openlocfilehash: 4d3b56a8ac63d0eba0dc0aec1b62e6d12f601bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a><span data-ttu-id="a06c6-103">Créer une application web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="a06c6-103">Create a PHP-MySQL web app in Azure App Service and deploy using FTP</span></span>
<span data-ttu-id="a06c6-104">Ce didacticiel vous montre comment l’application web de toocreate un MySQL de PHP et toodeploy à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it using FTP.</span></span> <span data-ttu-id="a06c6-105">Il part du principe que vous avez installé [PHP][install-php], [MySQL][install-mysql], un serveur Web et un client FTP sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a06c6-105">This tutorial assumes you have [PHP][install-php], [MySQL][install-mysql], a web server, and an FTP client installed on your computer.</span></span> <span data-ttu-id="a06c6-106">instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation, notamment Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="a06c6-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="a06c6-107">À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a06c6-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="a06c6-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a06c6-108">You will learn:</span></span>

* <span data-ttu-id="a06c6-109">Comment une application web et un MySQL de base de données à l’aide de toocreate hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a06c6-109">How toocreate a web app and a MySQL database using hello Azure Portal.</span></span> <span data-ttu-id="a06c6-110">PHP est activé dans les applications Web par défaut, rien de spécial est nécessaire toorun votre code PHP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-110">Because PHP is enabled in Web Apps by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="a06c6-111">Comment toopublish votre tooAzure d’application en utilisant FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-111">How toopublish your application tooAzure using FTP.</span></span>

<span data-ttu-id="a06c6-112">En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-112">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="a06c6-113">Hello application sera hébergée dans une application Web.</span><span class="sxs-lookup"><span data-stu-id="a06c6-113">hello application will be hosted in a Web App.</span></span> <span data-ttu-id="a06c6-114">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a06c6-114">A screenshot of hello completed application is below:</span></span>

![Site Web PHP Azure][running-app]

> [!NOTE]
> <span data-ttu-id="a06c6-116">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="a06c6-116">If you want tooget started with Azure App Service before signing up for an account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a06c6-117">Aucune carte de crédit n’est requise, et vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="a06c6-117">No credit cards required, no commitments.</span></span> 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a><span data-ttu-id="a06c6-118">Créer une application web et configurer la publication FTP</span><span class="sxs-lookup"><span data-stu-id="a06c6-118">Create a web app and set up FTP publishing</span></span>
<span data-ttu-id="a06c6-119">Suivez ces étapes toocreate une application web et une base de données MySQL :</span><span class="sxs-lookup"><span data-stu-id="a06c6-119">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="a06c6-120">Connexion toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a06c6-120">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="a06c6-121">Cliquez sur hello **+ nouveau** icône en haut de hello à gauche de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a06c6-121">Click hello **+ New** icon on hello top left of hello Azure Portal.</span></span>
   
    ![Créer un site Web Azure][new-website]
3. <span data-ttu-id="a06c6-123">Dans le type de recherche hello **Web application + MySQL** , puis cliquez sur **Web application + MySQL**.</span><span class="sxs-lookup"><span data-stu-id="a06c6-123">In hello search type **Web app + MySQL** and click on **Web app + MySQL**.</span></span>
   
    ![Création personnalisée d'un site web][custom-create]
4. <span data-ttu-id="a06c6-125">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a06c6-125">Click **Create**.</span></span> <span data-ttu-id="a06c6-126">Entrez un nom de service d’application unique, un nom valide pour le groupe de ressources hello et un nouveau plan de service.</span><span class="sxs-lookup"><span data-stu-id="a06c6-126">Enter a unique app service name, a valid name for hello resource group and a new service plan.</span></span>
   
    ![Définir le nom du groupe de ressources][resource-group]
5. <span data-ttu-id="a06c6-128">Entrez des valeurs pour votre nouvelle base de données, y compris les acceptez les conditions juridiques toohello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-128">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Créer une base de données MySQL][new-mysql-db]
6. <span data-ttu-id="a06c6-130">Lorsque l’application hello web a été créée, vous verrez le nouveau panneau de service application hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-130">When hello web app has been created, you will see hello new app service blade.</span></span>
7. <span data-ttu-id="a06c6-131">Cliquez sur **Paramètres** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="a06c6-131">Click on **Settings** > **Deployment credentials**.</span></span> 
   
    ![Définir les informations d’identification de déploiement][set-deployment-credentials]
8. <span data-ttu-id="a06c6-133">tooenable de publication FTP, vous devez fournir un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a06c6-133">tooenable FTP publishing, you must provide a user name and password.</span></span> <span data-ttu-id="a06c6-134">Enregistrer les informations d’identification hello et prenez note du nom d’utilisateur hello et vous créez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a06c6-134">Save hello credentials and make a note of hello user name and password you create.</span></span>
   
    ![Création des informations d’identification de publication][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="a06c6-136">Générer et tester votre application localement</span><span class="sxs-lookup"><span data-stu-id="a06c6-136">Build and test your app locally</span></span>
<span data-ttu-id="a06c6-137">Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a06c6-137">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="a06c6-138">Les informations relatives aux précédents inscrits sont affichées dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="a06c6-138">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="a06c6-139">Les informations d'inscription sont stockées dans une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="a06c6-139">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="a06c6-140">application Hello se compose de deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="a06c6-140">hello app consists of two files:</span></span>

* <span data-ttu-id="a06c6-141">**index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.</span><span class="sxs-lookup"><span data-stu-id="a06c6-141">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>
* <span data-ttu-id="a06c6-142">**CreateTable.PHP**: crée la table de MySQL hello pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-142">**createtable.php**: Creates hello MySQL table for hello application.</span></span> <span data-ttu-id="a06c6-143">Ce fichier sera utilisé une seule fois.</span><span class="sxs-lookup"><span data-stu-id="a06c6-143">This file will only be used once.</span></span>

<span data-ttu-id="a06c6-144">toobuild et application hello exécution localement, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a06c6-144">toobuild and run hello app locally, follow hello steps below.</span></span> <span data-ttu-id="a06c6-145">Notez que ces étapes supposent que vous avez PHP, MySQL et un serveur web sur votre ordinateur local, et que vous avez activé hello [extension PDO pour MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="a06c6-145">Note that these steps assume you have PHP, MySQL, and a web server set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="a06c6-146">Créez une base de données MySQL nommée `registration`.</span><span class="sxs-lookup"><span data-stu-id="a06c6-146">Create a MySQL database called `registration`.</span></span> <span data-ttu-id="a06c6-147">Vous pouvez effectuer cela à partir de l’invite de commandes hello MySQL avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="a06c6-147">You can do this from hello MySQL command prompt with this command:</span></span>
   
        mysql> create database registration;
2. <span data-ttu-id="a06c6-148">Dans le répertoire racine de votre serveur web, créez un dossier nommé `registration` et deux fichiers à l’intérieur : un fichier nommé `createtable.php` et un autre nommé `index.php`.</span><span class="sxs-lookup"><span data-stu-id="a06c6-148">In your web server's root directory, create a folder called `registration` and create two files in it - one called `createtable.php` and one called `index.php`.</span></span>
3. <span data-ttu-id="a06c6-149">Ouvrez hello `createtable.php` dans un éditeur de texte ou un IDE et ajoutez le code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a06c6-149">Open hello `createtable.php` file in a text editor or IDE and add hello code below.</span></span> <span data-ttu-id="a06c6-150">Ce code sera utilisé toocreate hello `registration_tbl` table Bonjour `registration` base de données.</span><span class="sxs-lookup"><span data-stu-id="a06c6-150">This code will be used toocreate hello `registration_tbl` table in hello `registration` database.</span></span>
   
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
   > <span data-ttu-id="a06c6-151">Vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a06c6-151">You will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
4. <span data-ttu-id="a06c6-152">Ouvrez un navigateur web et accédez trop[http://localhost/registration/createtable.php][localhost-createtable].</span><span class="sxs-lookup"><span data-stu-id="a06c6-152">Open a web browser and browse too[http://localhost/registration/createtable.php][localhost-createtable].</span></span> <span data-ttu-id="a06c6-153">Cela créera hello `registration_tbl` table hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="a06c6-153">This will create hello `registration_tbl` table in hello database.</span></span>
5. <span data-ttu-id="a06c6-154">Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello base code HTML et CSS pour la page de hello (hello code PHP est ajouté dans les étapes ultérieures).</span><span class="sxs-lookup"><span data-stu-id="a06c6-154">Open hello **index.php** file in a text editor or IDE and add hello basic HTML and CSS code for hello page (hello PHP code will be added in later steps).</span></span>
   
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
6. <span data-ttu-id="a06c6-155">Dans les balises PHP hello, ajoutez le code PHP pour la connexion de base de données toohello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-155">Within hello PHP tags, add PHP code for connecting toohello database.</span></span>
   
        // DB connection info
        $host = "localhost";
        $user = "user name";
        $pwd = "password";
        $db = "registration";
        // Connect toodatabase.
        try {
            $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
            $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
        }
        catch(Exception $e){
            die(var_dump($e));
        }
   
   > [!NOTE]
   > <span data-ttu-id="a06c6-156">Là encore, vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a06c6-156">Again, you will need tooupdate hello values for <code>$user</code> and <code>$pwd</code> with your local MySQL user name and password.</span></span>
   > 
   > 
7. <span data-ttu-id="a06c6-157">Après le code de connexion de base de données hello, ajoutez le code pour l’insertion des informations d’inscription dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-157">Following hello database connection code, add code for inserting registration information into hello database.</span></span>
   
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
8. <span data-ttu-id="a06c6-158">Enfin, après le code hello ci-dessus, ajoutez du code pour récupérer des données à partir de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-158">Finally, following hello code above, add code for retrieving data from hello database.</span></span>
   
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

<span data-ttu-id="a06c6-159">Vous pouvez maintenant rechercher trop[http://localhost/registration/index.php] [ localhost-index] tootest hello application.</span><span class="sxs-lookup"><span data-stu-id="a06c6-159">You can now browse too[http://localhost/registration/index.php][localhost-index] tootest hello app.</span></span>

## <a name="get-mysql-and-ftp-connection-information"></a><span data-ttu-id="a06c6-160">Obtention des informations de connexion MySQL et FTP</span><span class="sxs-lookup"><span data-stu-id="a06c6-160">Get MySQL and FTP connection information</span></span>
<span data-ttu-id="a06c6-161">tooconnect toohello base de données MySQL qui est en cours d’exécution dans les applications Web, votre besoin hello des informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="a06c6-161">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="a06c6-162">tooget les informations de connexion MySQL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a06c6-162">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="a06c6-163">À partir du service de l’application hello Panneau de l’application web cliquez sur le lien de groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="a06c6-163">From hello app service web app blade click on hello resource group link:</span></span>
   
    ![Sélectionner Groupe de ressources][select-resourcegroup]
2. <span data-ttu-id="a06c6-165">À partir de votre groupe de ressources, cliquez sur base de données hello :</span><span class="sxs-lookup"><span data-stu-id="a06c6-165">From your resource group, click hello database:</span></span>
   
    ![Sélectionner la base de données][select-database]
3. <span data-ttu-id="a06c6-167">À partir de la base de données de synthèse hello, sélectionnez **paramètres** > **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="a06c6-167">From hello database summary, select **Settings** > **Properties**.</span></span>
   
    ![Sélectionner les propriétés][select-properties]
4. <span data-ttu-id="a06c6-169">Notez les valeurs hello pour `Database`, `Host`, `User Id`, et `Password`.</span><span class="sxs-lookup"><span data-stu-id="a06c6-169">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Noter les propriétés][note-properties]
5. <span data-ttu-id="a06c6-171">À partir de votre application web, cliquez sur hello **télécharger le profil de publication** lien hello coin inférieur droit de la page de hello :</span><span class="sxs-lookup"><span data-stu-id="a06c6-171">From your web app, click hello **Download publish profile** link at hello bottom right corner of hello page:</span></span>
   
    ![Télécharger le profil de publication][download-publish-profile]
6. <span data-ttu-id="a06c6-173">Ouvrez hello `.publishsettings` fichier dans un éditeur XML.</span><span class="sxs-lookup"><span data-stu-id="a06c6-173">Open hello `.publishsettings` file in an XML editor.</span></span> 
7. <span data-ttu-id="a06c6-174">Recherche hello `<publishProfile >` élément avec `publishMethod="FTP"` qui recherche toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="a06c6-174">Find hello `<publishProfile >` element with `publishMethod="FTP"` that looks similar toothis:</span></span>
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

<span data-ttu-id="a06c6-175">Prenez note de hello `publishUrl`, `userName`, et `userPWD` attributs.</span><span class="sxs-lookup"><span data-stu-id="a06c6-175">Make note of hello `publishUrl`, `userName`, and `userPWD` attributes.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="a06c6-176">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="a06c6-176">Publish your app</span></span>
<span data-ttu-id="a06c6-177">Après avoir testé votre application localement, vous pouvez le publier l’application web tooyour à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-177">After you have tested your app locally, you can publish it tooyour web app using FTP.</span></span> <span data-ttu-id="a06c6-178">Toutefois, vous devez tout d’abord les informations de connexion de base de données de hello tooupdate dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-178">However, you first need tooupdate hello database connection information in hello application.</span></span> <span data-ttu-id="a06c6-179">À l’aide des informations de connexion de base de données hello obtenues précédemment (Bonjour **les informations de connexion MySQL d’obtenir et FTP** section), hello de mise à jour après les informations contenues dans **les deux** hello `createdatabase.php` et `index.php` fichiers par hello les valeurs appropriées :</span><span class="sxs-lookup"><span data-stu-id="a06c6-179">Using hello database connection information you obtained earlier (in hello **Get MySQL and FTP connection information** section), update hello following information in **both** hello `createdatabase.php` and `index.php` files with hello appropriate values:</span></span>

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

<span data-ttu-id="a06c6-180">Maintenant vous êtes prêt à toopublish votre application à l’aide de FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-180">Now you are ready toopublish your app using FTP.</span></span>

1. <span data-ttu-id="a06c6-181">Ouvrez le client FTP de votre choix.</span><span class="sxs-lookup"><span data-stu-id="a06c6-181">Open your FTP client of choice.</span></span>
2. <span data-ttu-id="a06c6-182">Entrez hello *partie nom d’hôte* de hello `publishUrl` attribut ci-dessus dans votre client FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-182">Enter hello *host name portion* from hello `publishUrl` attribute you noted above into your FTP client.</span></span>
3. <span data-ttu-id="a06c6-183">Entrez hello `userName` et `userPWD` attributs que vous avez noté ci-dessus sans modification dans votre client FTP.</span><span class="sxs-lookup"><span data-stu-id="a06c6-183">Enter hello `userName` and `userPWD` attributes you noted above unchanged into your FTP client.</span></span>
4. <span data-ttu-id="a06c6-184">Établissez une connexion.</span><span class="sxs-lookup"><span data-stu-id="a06c6-184">Establish a connection.</span></span>

<span data-ttu-id="a06c6-185">Après que vous être connecté vous être en mesure de tooupload et télécharger des fichiers en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="a06c6-185">After you have connected you will be able tooupload and download files as needed.</span></span> <span data-ttu-id="a06c6-186">Assurez-vous que vous téléchargez un répertoire racine des fichiers toohello, c'est-à-dire `/site/wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="a06c6-186">Be sure that you are uploading files toohello root directory, which is `/site/wwwroot`.</span></span>

<span data-ttu-id="a06c6-187">Après avoir téléchargé les deux `index.php` et `createtable.php`, parcourir trop**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL de table pour l’application hello, puis parcourir trop**http://[site nom ].azurewebsites.net/index.php** toobegin à l’aide d’application hello.</span><span class="sxs-lookup"><span data-stu-id="a06c6-187">After uploading both `index.php` and `createtable.php`, browse too**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL table for hello application, then browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a06c6-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a06c6-188">Next steps</span></span>
<span data-ttu-id="a06c6-189">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="a06c6-189">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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

