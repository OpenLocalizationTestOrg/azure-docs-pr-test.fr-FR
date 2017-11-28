---
title: "Création d’une application web PHP-MySQL dans Azure App Service et déploiement à l’aide de Git."
description: "Didacticiel expliquant comment créer une application web PHP stockant les données dans MySQL et comment utiliser un déploiement Git dans Azure"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
tags: mysql
ms.assetid: 7454475f-e275-4bc7-9f09-1ef07382e5da
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: aa845eb474dbd42ae2c31880690d4ced059eb448
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="1e51f-103">Création d’une application web PHP-MySQL dans Azure App Service et déploiement à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="1e51f-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="1e51f-104">Ce didacticiel vous explique comment créer une application web PHP-MySQL et déployer dans [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="1e51f-104">This tutorial shows you how to create a PHP-MySQL web app and how to deploy it to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="1e51f-105">Vous allez utiliser [PHP][install-php], l’outil de ligne de commande MySQL (inclus dans [MySQL][install-mysql]), et [Git][install-git] qui sont installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1e51f-105">You will use [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="1e51f-106">Les instructions de ce didacticiel s’appliquent à n’importe quel système d’exploitation, notamment Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="1e51f-106">The instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="1e51f-107">À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1e51f-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="1e51f-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e51f-108">You will learn:</span></span>

* <span data-ttu-id="1e51f-109">création d’une application web et d’une base de données MySQL à l’aide du [portail Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="1e51f-109">How to create a web app and a MySQL database using the [Azure Portal][management-portal].</span></span> <span data-ttu-id="1e51f-110">PHP étant activé par défaut dans [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) , l’exécution de votre code PHP ne requiert aucune action particulière) ;</span><span class="sxs-lookup"><span data-stu-id="1e51f-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required to run your PHP code.</span></span>
* <span data-ttu-id="1e51f-111">publication et republication de votre application dans Azure en utilisant Git.</span><span class="sxs-lookup"><span data-stu-id="1e51f-111">How to publish and re-publish your application to Azure using Git.</span></span>
* <span data-ttu-id="1e51f-112">activation de l’extension du compositeur pour automatiser les tâches de compositeur à chaque `git push`.</span><span class="sxs-lookup"><span data-stu-id="1e51f-112">How to enable the Composer extension to automate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="1e51f-113">En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP.</span><span class="sxs-lookup"><span data-stu-id="1e51f-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="1e51f-114">Cette application sera hébergée dans Web Apps.</span><span class="sxs-lookup"><span data-stu-id="1e51f-114">The application will be hosted in Web Apps.</span></span> <span data-ttu-id="1e51f-115">Voici une capture d’écran de l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="1e51f-115">A screenshot of the completed application is below:</span></span>

![Site Web PHP Azure][running-app]

## <a name="set-up-the-development-environment"></a><span data-ttu-id="1e51f-117">Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="1e51f-117">Set up the development environment</span></span>
<span data-ttu-id="1e51f-118">Ce didacticiel part du principe que [PHP][install-php], l’outil de ligne de commande MySQL (qui fait partie de [MySQL][install-mysql]) et [Git][install-git] sont installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1e51f-118">This tutorial assumes you have [PHP][install-php], the MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="1e51f-119">Créer une application web et configurer la publication Git</span><span class="sxs-lookup"><span data-stu-id="1e51f-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="1e51f-120">Pour créer une application web et une base de données MySQL, suivez la procédure ci-après :</span><span class="sxs-lookup"><span data-stu-id="1e51f-120">Follow these steps to create a web app and a MySQL database:</span></span>

1. <span data-ttu-id="1e51f-121">Connectez-vous au [portail Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="1e51f-121">Login to the [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="1e51f-122">Cliquez sur l'icône **Nouveau** .</span><span class="sxs-lookup"><span data-stu-id="1e51f-122">Click the **New** icon.</span></span>
3. <span data-ttu-id="1e51f-123">Cliquez sur **Afficher tout** en regard de **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-123">Click **See All** next to **Marketplace**.</span></span> 
4. <span data-ttu-id="1e51f-124">Cliquez sur **Web et mobilité**, puis sur **Application web et MySQL**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="1e51f-125">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="1e51f-126">Entrez un nom valide pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1e51f-126">Enter a valid name for your resource group.</span></span>
   
    ![Définir le nom du groupe de ressources][resource-group]
6. <span data-ttu-id="1e51f-128">Entrez des valeurs pour votre nouvelle application web.</span><span class="sxs-lookup"><span data-stu-id="1e51f-128">Enter values for your new web app.</span></span>
   
    ![Créer une application web][new-web-app]
7. <span data-ttu-id="1e51f-130">Entrez des valeurs pour votre nouvelle base de données, notamment l’acceptation des conditions juridiques.</span><span class="sxs-lookup"><span data-stu-id="1e51f-130">Enter values for your new database, including agreeing to the legal terms.</span></span>
   
    ![Créer une base de données MySQL][new-mysql-db]
8. <span data-ttu-id="1e51f-132">Une fois que l'application web a été créée, vous voyez apparaître le nouveau volet d'application web.</span><span class="sxs-lookup"><span data-stu-id="1e51f-132">When the web app has been created, you will see the new web app blade.</span></span>
9. <span data-ttu-id="1e51f-133">Dans les **Paramètres**, cliquez sur **Déploiement continu**, puis cliquez sur *Configurer les paramètres requis*.</span><span class="sxs-lookup"><span data-stu-id="1e51f-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configuration de la publication Git][setup-publishing]
10. <span data-ttu-id="1e51f-135">Sélectionnez **Référentiel Git local** comme source.</span><span class="sxs-lookup"><span data-stu-id="1e51f-135">Select **Local Git Repository** for the source.</span></span>
    
     ![Configurer le référentiel Git][setup-repository]
11. <span data-ttu-id="1e51f-137">Pour activer la publication Git, vous devez fournir un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1e51f-137">To enable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="1e51f-138">Notez le nom d'utilisateur et le mot de passe que vous créez</span><span class="sxs-lookup"><span data-stu-id="1e51f-138">Make a note of the user name and password you create.</span></span> <span data-ttu-id="1e51f-139">(si vous avez déjà configuré un référentiel Git, ignorez cette étape).</span><span class="sxs-lookup"><span data-stu-id="1e51f-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Création des informations d’identification de publication][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="1e51f-141">Obtention des informations de connexion MySQL distantes</span><span class="sxs-lookup"><span data-stu-id="1e51f-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="1e51f-142">Pour vous connecter à la base de données MySQL qui s’exécute dans Web Apps, vous devez disposer des informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="1e51f-142">To connect to the MySQL database that is running in Web Apps, your will need the connection information.</span></span> <span data-ttu-id="1e51f-143">Pour obtenir vos informations de connexion MySQL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e51f-143">To get MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="1e51f-144">À partir de votre groupe de ressources, cliquez sur la base de données :</span><span class="sxs-lookup"><span data-stu-id="1e51f-144">From your resource group, click the database:</span></span>
   
    ![Sélectionner la base de données][select-database]
2. <span data-ttu-id="1e51f-146">Dans les **Paramètres** de la base de données, sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-146">From the database **Settings**, select **Properties**.</span></span>
   
    ![Sélectionner les propriétés][select-properties]
3. <span data-ttu-id="1e51f-148">Notez les valeurs de `Database`, `Host`, `User Id` et `Password`.</span><span class="sxs-lookup"><span data-stu-id="1e51f-148">Make note of the values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Noter les propriétés][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="1e51f-150">Générer et tester votre application localement</span><span class="sxs-lookup"><span data-stu-id="1e51f-150">Build and test your app locally</span></span>
<span data-ttu-id="1e51f-151">Après avoir créé une application web, vous pouvez la développer localement, la tester, puis la déployer.</span><span class="sxs-lookup"><span data-stu-id="1e51f-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="1e51f-152">L'application d'inscription est une simple application PHP qui vous permet de vous inscrire à un événement en entrant votre nom et votre adresse électronique.</span><span class="sxs-lookup"><span data-stu-id="1e51f-152">The Registration application is a simple PHP application that allows you to register for an event by providing your name and email address.</span></span> <span data-ttu-id="1e51f-153">Les informations relatives aux précédents inscrits sont affichées dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="1e51f-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="1e51f-154">Les informations d'inscription sont stockées dans une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="1e51f-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="1e51f-155">L'application se compose d'un seul fichier (dont le code est disponible ci-dessous pour un copier/coller) :</span><span class="sxs-lookup"><span data-stu-id="1e51f-155">The application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="1e51f-156">**index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.</span><span class="sxs-lookup"><span data-stu-id="1e51f-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="1e51f-157">Pour générer et exécuter l'application en local, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e51f-157">To build and run the application locally, follow the steps below.</span></span> <span data-ttu-id="1e51f-158">Notez que ces étapes partent du principe que PHP et l’outil de ligne de commande MySQL (inclus dans MySQL) sont installés sur votre ordinateur local, et que vous avez activé l’[extension PDO pour MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="1e51f-158">Note that these steps assume you have the PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled the [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="1e51f-159">Connectez-vous au serveur MySQL distant en utilisant les valeurs `Data Source`, `User Id`, `Password` et `Database` récupérées précédemment :</span><span class="sxs-lookup"><span data-stu-id="1e51f-159">Connect to the remote MySQL server, using the value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="1e51f-160">L'invite de commandes MySQL s'affiche :</span><span class="sxs-lookup"><span data-stu-id="1e51f-160">The MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="1e51f-161">Copiez la commande `CREATE TABLE` suivante pour créer la table `registration_tbl` dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="1e51f-161">Paste in the following `CREATE TABLE` command to create the `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="1e51f-162">Dans la racine de votre dossier d'application en local, créez le fichier **index.php** .</span><span class="sxs-lookup"><span data-stu-id="1e51f-162">In the root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="1e51f-163">Ouvrez le fichier **index.php** dans un éditeur de texte ou un environnement de développement intégré (IDE), puis ajoutez le code suivant en y apportant les modifications nécessaires, indiquées par les commentaires `//TODO:`.</span><span class="sxs-lookup"><span data-stu-id="1e51f-163">Open the **index.php** file in a text editor or IDE and add the following code, and complete the necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update the values for $host, $user, $pwd, and $db
            //using the values you retrieved earlier from the Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect to database.
            try {
                $conn = new PDO( "mysql:host=$host;dbname=$db", $user, $pwd);
                $conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );
            }
            catch(Exception $e){
                die(var_dump($e));
            }
            // Insert registration info
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
            // Retrieve data
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
        ?>
        </body>
        </html>

1. <span data-ttu-id="1e51f-164">Sur un terminal, accédez à votre dossier d'application et tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1e51f-164">In a terminal go to your application folder and type the following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="1e51f-165">Vous pouvez maintenant accéder à **http://localhost:8000/** pour tester l’application.</span><span class="sxs-lookup"><span data-stu-id="1e51f-165">You can now browse to **http://localhost:8000/** to test the application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="1e51f-166">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="1e51f-166">Publish your app</span></span>
<span data-ttu-id="1e51f-167">Après avoir testé votre application localement, vous pouvez la publier dans Web Apps à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="1e51f-167">After you have tested your app locally, you can publish it to Web Apps using Git.</span></span> <span data-ttu-id="1e51f-168">Vous allez initialiser votre référentiel Git, puis publier l'application.</span><span class="sxs-lookup"><span data-stu-id="1e51f-168">You will initialize your local Git repository and publish the application.</span></span>

> [!NOTE]
> <span data-ttu-id="1e51f-169">Cette procédure est identique à celle affichée dans le portail Azure à la fin de la section « Créer une application web et configurer la publication Git » précédente.</span><span class="sxs-lookup"><span data-stu-id="1e51f-169">These are the same steps shown in the Azure Portal at the end of the Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="1e51f-170">(Facultatif) Si vous avez oublié ou mal placé l’URL de votre référentiel distant Git, accédez aux propriétés de l’application web sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1e51f-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate to the web app properties on the Azure Portal.</span></span>
2. <span data-ttu-id="1e51f-171">Ouvrez GitBash (ou un terminal, si Git est dans votre `PATH`), remplacez les répertoires du répertoire racine de votre application, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e51f-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories to the root directory of your application, and run the following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="1e51f-172">Vous êtes invité à entrer le mot de passe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1e51f-172">You will be prompted for the password you created earlier.</span></span>
   
    ![Transmission initiale vers Azure via Git][git-initial-push]
3. <span data-ttu-id="1e51f-174">Accédez à **http://[nom du site].azurewebsites.net/index.php** pour commencer à utiliser l’application (ces informations seront stockées dans le tableau de bord de votre compte) :</span><span class="sxs-lookup"><span data-stu-id="1e51f-174">Browse to **http://[site name].azurewebsites.net/index.php** to begin using the application (this information will be stored on your account dashboard):</span></span>
   
    ![Site Web PHP Azure][running-app]

<span data-ttu-id="1e51f-176">Après avoir publié votre application, vous pouvez y apporter des modifications, puis publier ces dernières à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="1e51f-176">After you have published your app, you can begin making changes to it and use Git to publish them.</span></span>

## <a name="publish-changes-to-your-app"></a><span data-ttu-id="1e51f-177">Publier les modifications apportées à votre application</span><span class="sxs-lookup"><span data-stu-id="1e51f-177">Publish changes to your app</span></span>
<span data-ttu-id="1e51f-178">Pour publier les modifications apportées à votre application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e51f-178">To publish changes to your app, follow these steps:</span></span>

1. <span data-ttu-id="1e51f-179">Modifiez votre application localement.</span><span class="sxs-lookup"><span data-stu-id="1e51f-179">Make changes to your app locally.</span></span>
2. <span data-ttu-id="1e51f-180">Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`), remplacez les répertoires par le répertoire racine de votre application, puis exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e51f-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories to the root directory of your app, and run the following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="1e51f-181">Vous êtes invité à entrer le mot de passe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="1e51f-181">You will be prompted for the password you created earlier.</span></span>
   
    ![Publication des modifications apportées au site dans Azure via Git][git-change-push]
3. <span data-ttu-id="1e51f-183">Accédez à **http://[nom du site].azurewebsites.net/index.php** pour afficher votre application, ainsi que les modifications apportées :</span><span class="sxs-lookup"><span data-stu-id="1e51f-183">Browse to **http://[site name].azurewebsites.net/index.php** to see your app and any changes you may have made:</span></span>
   
    ![Site Web PHP Azure][running-app]

> [!NOTE]
> <span data-ttu-id="1e51f-185">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="1e51f-185">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1e51f-186">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="1e51f-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a><span data-ttu-id="1e51f-187">Activation de l’automatisation du Compositeur avec l’extension du Compositeur</span><span class="sxs-lookup"><span data-stu-id="1e51f-187">Enable Composer automation with the Composer extension</span></span>
<span data-ttu-id="1e51f-188">Par défaut, le processus de déploiement de git dans le Service d’application ne fait rien avec composer.json, si vous en avez un dans votre projet PHP.</span><span class="sxs-lookup"><span data-stu-id="1e51f-188">By default, the git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="1e51f-189">Vous pouvez activer le traitement du composer.json pendant `git push` en activant l’extension du Compositeur.</span><span class="sxs-lookup"><span data-stu-id="1e51f-189">You can enable composer.json processing during `git push` by enabling the Composer extension.</span></span>

1. <span data-ttu-id="1e51f-190">Dans le panneau de l’application web PHP (dans le [portail Azure][management-portal]), cliquez sur **Outils** > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-190">In your PHP web app's blade in the [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Paramètres d’extension du Compositeur][composer-extension-settings]
2. <span data-ttu-id="1e51f-192">Cliquez sur **Ajouter** puis sur **Compositeur**.</span><span class="sxs-lookup"><span data-stu-id="1e51f-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Ajout d’extension au Compositeur][composer-extension-add]
3. <span data-ttu-id="1e51f-194">Cliquez sur **OK** pour accepter les conditions juridiques.</span><span class="sxs-lookup"><span data-stu-id="1e51f-194">Click **OK** to accept legal terms.</span></span> <span data-ttu-id="1e51f-195">Cliquez à nouveau sur **OK** pour ajouter l’extension.</span><span class="sxs-lookup"><span data-stu-id="1e51f-195">Click **OK** again to add the extension.</span></span>
   
    <span data-ttu-id="1e51f-196">Le panneau **Extensions installées** affiche désormais l’extension du Compositeur.</span><span class="sxs-lookup"><span data-stu-id="1e51f-196">The **Installed extensions** blade will now show the Composer extension.</span></span>  
    <span data-ttu-id="1e51f-197">![Vue Extension du Compositeur][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="1e51f-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="1e51f-198">Maintenant, exécutez `git add`, `git commit` et `git push` comme dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="1e51f-198">Now, perform `git add`, `git commit`, and `git push` like in the previous section.</span></span> <span data-ttu-id="1e51f-199">Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.</span><span class="sxs-lookup"><span data-stu-id="1e51f-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Réussite de l’extension du Compositeur][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="1e51f-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e51f-201">Next steps</span></span>
<span data-ttu-id="1e51f-202">Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="1e51f-202">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

<!-- URL List -->

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[install-mysql]: http://dev.mysql.com/downloads/mysql/
[pdo-mysql]: http://www.php.net/manual/en/ref.pdo-mysql.php
[management-portal]: https://portal.azure.com
[sql-database-editions]: http://msdn.microsoft.com/library/windowsazure/ee621788.aspx

<!-- IMG List -->

[running-app]: ./media/web-sites-php-mysql-deploy-use-git/running_app_2.png
[new-website]: ./media/web-sites-php-mysql-deploy-use-git/new_website2.png
[custom-create]: ./media/web-sites-php-mysql-deploy-use-git/create_web_mysql.png
[new-mysql-db]: ./media/web-sites-php-mysql-deploy-use-git/create_db.png
[go-to-webapp]: ./media/web-sites-php-mysql-deploy-use-git/select_webapp.png
[setup-git-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_git_publishing.png
[credentials]: ./media/web-sites-php-mysql-deploy-use-git/save_credentials.png
[resource-group]: ./media/web-sites-php-mysql-deploy-use-git/set_group.png
[new-web-app]: ./media/web-sites-php-mysql-deploy-use-git/create_wa.png
[setup-publishing]: ./media/web-sites-php-mysql-deploy-use-git/setup_deploy.png
[setup-repository]: ./media/web-sites-php-mysql-deploy-use-git/select_local_git.png
[select-database]: ./media/web-sites-php-mysql-deploy-use-git/select_database.png
[select-properties]: ./media/web-sites-php-mysql-deploy-use-git/select_properties.png
[note-properties]: ./media/web-sites-php-mysql-deploy-use-git/note-properties.png

[git-instructions]: ./media/web-sites-php-mysql-deploy-use-git/git-instructions.png
[git-change-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-change-push.png
[git-initial-push]: ./media/web-sites-php-mysql-deploy-use-git/php-git-initial-push.png

[composer-extension-settings]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-settings.png
[composer-extension-add]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-add.png
[composer-extension-view]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-view.png
[composer-extension-success]: ./media/web-sites-php-mysql-deploy-use-git/composer-extension-success.png
