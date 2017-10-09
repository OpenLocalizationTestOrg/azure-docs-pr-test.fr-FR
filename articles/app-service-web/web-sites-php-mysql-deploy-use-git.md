---
title: "aaaCreate un PHP-MySQL application dans Azure App Service web et le déployer à l’aide de Git"
description: "Un didacticiel qui montre comment toocreate PHP web application qui stocke les données de MySQL et utiliser Git déploiement tooAzure."
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
ms.openlocfilehash: 9c22946777598cc973cd9dfc8d2a258bd08cc39a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a><span data-ttu-id="231c6-103">Création d’une application web PHP-MySQL dans Azure App Service et déploiement à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="231c6-103">Create a PHP-MySQL web app in Azure App Service and deploy using Git</span></span>
<span data-ttu-id="231c6-104">Ce didacticiel vous montre comment l’application web de toocreate un MySQL de PHP et toodeploy il trop[du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="231c6-104">This tutorial shows you how toocreate a PHP-MySQL web app and how toodeploy it too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) using Git.</span></span> <span data-ttu-id="231c6-105">Vous allez utiliser [PHP][install-php], hello l’outil de ligne de commande MySQL (dans le cadre du [MySQL][install-mysql]), et [Git] [ install-git] installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="231c6-105">You will use [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span> <span data-ttu-id="231c6-106">instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation, notamment Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="231c6-106">hello instructions in this tutorial can be followed on any operating system, including Windows, Mac, and  Linux.</span></span> <span data-ttu-id="231c6-107">À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="231c6-107">Upon completing this guide, you will have a PHP/MySQL web app running in Azure.</span></span>

<span data-ttu-id="231c6-108">Vous apprendrez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="231c6-108">You will learn:</span></span>

* <span data-ttu-id="231c6-109">Comment toocreate une application web et un MySQL de base de données à l’aide de hello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="231c6-109">How toocreate a web app and a MySQL database using hello [Azure Portal][management-portal].</span></span> <span data-ttu-id="231c6-110">Étant donné que PHP est activée dans [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) par défaut, rien de spécial est nécessaire toorun votre code PHP.</span><span class="sxs-lookup"><span data-stu-id="231c6-110">Because PHP is enabled in [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) by default, nothing special is required toorun your PHP code.</span></span>
* <span data-ttu-id="231c6-111">Comment toopublish et republiez votre tooAzure d’application à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="231c6-111">How toopublish and re-publish your application tooAzure using Git.</span></span>
* <span data-ttu-id="231c6-112">Des tâches de tooenable hello Composer extension tooautomate Composer à chaque `git push`.</span><span class="sxs-lookup"><span data-stu-id="231c6-112">How tooenable hello Composer extension tooautomate Composer tasks at every `git push`.</span></span>

<span data-ttu-id="231c6-113">En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP.</span><span class="sxs-lookup"><span data-stu-id="231c6-113">By following this tutorial, you will build a simple registration web app in PHP.</span></span> <span data-ttu-id="231c6-114">Hello application sera hébergée dans les applications Web.</span><span class="sxs-lookup"><span data-stu-id="231c6-114">hello application will be hosted in Web Apps.</span></span> <span data-ttu-id="231c6-115">Une capture d’écran de l’application hello terminée est ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="231c6-115">A screenshot of hello completed application is below:</span></span>

![Site Web PHP Azure][running-app]

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="231c6-117">Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="231c6-117">Set up hello development environment</span></span>
<span data-ttu-id="231c6-118">Ce didacticiel suppose que vous avez [PHP][install-php], hello l’outil de ligne de commande MySQL (dans le cadre du [MySQL][install-mysql]), et [Git] [ install-git] installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="231c6-118">This tutorial assumes you have [PHP][install-php], hello MySQL Command-Line Tool (part of [MySQL][install-mysql]), and [Git][install-git] installed on your computer.</span></span>

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a><span data-ttu-id="231c6-119">Créer une application web et configurer la publication Git</span><span class="sxs-lookup"><span data-stu-id="231c6-119">Create a web app and set up Git publishing</span></span>
<span data-ttu-id="231c6-120">Suivez ces étapes toocreate une application web et une base de données MySQL :</span><span class="sxs-lookup"><span data-stu-id="231c6-120">Follow these steps toocreate a web app and a MySQL database:</span></span>

1. <span data-ttu-id="231c6-121">Connexion toohello [Azure Portal][management-portal].</span><span class="sxs-lookup"><span data-stu-id="231c6-121">Login toohello [Azure Portal][management-portal].</span></span>
2. <span data-ttu-id="231c6-122">Cliquez sur hello **nouveau** icône.</span><span class="sxs-lookup"><span data-stu-id="231c6-122">Click hello **New** icon.</span></span>
3. <span data-ttu-id="231c6-123">Cliquez sur **voir tous les** suivant trop**Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="231c6-123">Click **See All** next too**Marketplace**.</span></span> 
4. <span data-ttu-id="231c6-124">Cliquez sur **Web et mobilité**, puis sur **Application web et MySQL**.</span><span class="sxs-lookup"><span data-stu-id="231c6-124">Click **Web + Mobile**, then **Web app + MySQL**.</span></span> <span data-ttu-id="231c6-125">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="231c6-125">Then, click **Create**.</span></span>
5. <span data-ttu-id="231c6-126">Entrez un nom valide pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="231c6-126">Enter a valid name for your resource group.</span></span>
   
    ![Définir le nom du groupe de ressources][resource-group]
6. <span data-ttu-id="231c6-128">Entrez des valeurs pour votre nouvelle application web.</span><span class="sxs-lookup"><span data-stu-id="231c6-128">Enter values for your new web app.</span></span>
   
    ![Créer une application web][new-web-app]
7. <span data-ttu-id="231c6-130">Entrez des valeurs pour votre nouvelle base de données, y compris les acceptez les conditions juridiques toohello.</span><span class="sxs-lookup"><span data-stu-id="231c6-130">Enter values for your new database, including agreeing toohello legal terms.</span></span>
   
    ![Créer une base de données MySQL][new-mysql-db]
8. <span data-ttu-id="231c6-132">Lorsque l’application hello web a été créée, vous verrez le nouveau panneau des applications web hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-132">When hello web app has been created, you will see hello new web app blade.</span></span>
9. <span data-ttu-id="231c6-133">Dans les **Paramètres**, cliquez sur **Déploiement continu**, puis cliquez sur *Configurer les paramètres requis*.</span><span class="sxs-lookup"><span data-stu-id="231c6-133">In **Settings** click on **Continuous Deployment**, then click on *Configure required settings*.</span></span>
   
    ![Configuration de la publication Git][setup-publishing]
10. <span data-ttu-id="231c6-135">Sélectionnez **référentiel Git Local** pour la source de hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-135">Select **Local Git Repository** for hello source.</span></span>
    
     ![Configurer le référentiel Git][setup-repository]
11. <span data-ttu-id="231c6-137">tooenable Git de publication, vous devez fournir un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="231c6-137">tooenable Git publishing, you must provide a user name and password.</span></span> <span data-ttu-id="231c6-138">Prenez note du nom d’utilisateur hello et vous créez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="231c6-138">Make a note of hello user name and password you create.</span></span> <span data-ttu-id="231c6-139">(si vous avez déjà configuré un référentiel Git, ignorez cette étape).</span><span class="sxs-lookup"><span data-stu-id="231c6-139">(If you have set up a Git repository before, this step will be skipped.)</span></span>
    
     ![Création des informations d’identification de publication][credentials]

## <a name="get-remote-mysql-connection-information"></a><span data-ttu-id="231c6-141">Obtention des informations de connexion MySQL distantes</span><span class="sxs-lookup"><span data-stu-id="231c6-141">Get remote MySQL connection information</span></span>
<span data-ttu-id="231c6-142">tooconnect toohello base de données MySQL qui est en cours d’exécution dans les applications Web, votre besoin hello des informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="231c6-142">tooconnect toohello MySQL database that is running in Web Apps, your will need hello connection information.</span></span> <span data-ttu-id="231c6-143">tooget les informations de connexion MySQL, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="231c6-143">tooget MySQL connection information, follow these steps:</span></span>

1. <span data-ttu-id="231c6-144">À partir de votre groupe de ressources, cliquez sur base de données hello :</span><span class="sxs-lookup"><span data-stu-id="231c6-144">From your resource group, click hello database:</span></span>
   
    ![Sélectionner la base de données][select-database]
2. <span data-ttu-id="231c6-146">À partir de la base de données hello **paramètres**, sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="231c6-146">From hello database **Settings**, select **Properties**.</span></span>
   
    ![Sélectionner les propriétés][select-properties]
3. <span data-ttu-id="231c6-148">Notez les valeurs hello pour `Database`, `Host`, `User Id`, et `Password`.</span><span class="sxs-lookup"><span data-stu-id="231c6-148">Make note of hello values for `Database`, `Host`, `User Id`, and `Password`.</span></span>
   
    ![Noter les propriétés][note-properties]

## <a name="build-and-test-your-app-locally"></a><span data-ttu-id="231c6-150">Générer et tester votre application localement</span><span class="sxs-lookup"><span data-stu-id="231c6-150">Build and test your app locally</span></span>
<span data-ttu-id="231c6-151">Après avoir créé une application web, vous pouvez la développer localement, la tester, puis la déployer.</span><span class="sxs-lookup"><span data-stu-id="231c6-151">Now that you have created a web app, you can develop your application locally, then deploy it after testing.</span></span>

<span data-ttu-id="231c6-152">Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="231c6-152">hello Registration application is a simple PHP application that allows you tooregister for an event by providing your name and email address.</span></span> <span data-ttu-id="231c6-153">Les informations relatives aux précédents inscrits sont affichées dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="231c6-153">Information about previous registrants is displayed in a table.</span></span> <span data-ttu-id="231c6-154">Les informations d'inscription sont stockées dans une base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="231c6-154">Registration information is stored in a MySQL database.</span></span> <span data-ttu-id="231c6-155">application Hello se compose d’un fichier (code de copier/coller ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="231c6-155">hello application consists of one file (copy/paste code available below):</span></span>

* <span data-ttu-id="231c6-156">**index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.</span><span class="sxs-lookup"><span data-stu-id="231c6-156">**index.php**: Displays a form for registration and a table containing registrant information.</span></span>

<span data-ttu-id="231c6-157">toobuild et application hello exécution localement, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="231c6-157">toobuild and run hello application locally, follow hello steps below.</span></span> <span data-ttu-id="231c6-158">Notez que ces étapes supposent que vous avez hello PHP et MySQL Line Tool (partie de MySQL) sur votre ordinateur local, et que vous avez activé hello [extension PDO pour MySQL][pdo-mysql].</span><span class="sxs-lookup"><span data-stu-id="231c6-158">Note that these steps assume you have hello PHP and MySQL Command-Line Tool (part of MySQL) set up on your local machine, and that you have enabled hello [PDO extension for MySQL][pdo-mysql].</span></span>

1. <span data-ttu-id="231c6-159">Connecter le serveur MySQL distant toohello, à l’aide de la valeur hello pour `Data Source`, `User Id`, `Password`, et `Database` que vous avez récupéré précédemment :</span><span class="sxs-lookup"><span data-stu-id="231c6-159">Connect toohello remote MySQL server, using hello value for `Data Source`, `User Id`, `Password`, and `Database` that you retrieved earlier:</span></span>
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. <span data-ttu-id="231c6-160">invite de commandes Hello MySQL s’affiche :</span><span class="sxs-lookup"><span data-stu-id="231c6-160">hello MySQL command prompt will appear:</span></span>
   
        mysql>
3. <span data-ttu-id="231c6-161">Coller dans les éléments suivants de hello `CREATE TABLE` commande toocreate hello `registration_tbl` table dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="231c6-161">Paste in hello following `CREATE TABLE` command toocreate hello `registration_tbl` table in your database:</span></span>
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. <span data-ttu-id="231c6-162">Dans votre dossier local d’application racine hello créer **index.php** fichier.</span><span class="sxs-lookup"><span data-stu-id="231c6-162">In hello root of your local application folder create **index.php** file.</span></span>
5. <span data-ttu-id="231c6-163">Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello suivant de code, et les modifications nécessaires hello complète marqué avec `//TODO:` commentaires.</span><span class="sxs-lookup"><span data-stu-id="231c6-163">Open hello **index.php** file in a text editor or IDE and add hello following code, and complete hello necessary changes marked with `//TODO:` comments.</span></span>

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
            // DB connection info
            //TODO: Update hello values for $host, $user, $pwd, and $db
            //using hello values you retrieved earlier from hello Azure Portal.
            $host = "value of Data Source";
            $user = "value of User Id";
            $pwd = "value of Password";
            $db = "value of Database";
            // Connect toodatabase.
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

1. <span data-ttu-id="231c6-164">Dans un terminal tooyour accédez application dossier et tapez Bonjour commande suivante :</span><span class="sxs-lookup"><span data-stu-id="231c6-164">In a terminal go tooyour application folder and type hello following command:</span></span>
   
       php -S localhost:8000

<span data-ttu-id="231c6-165">Vous pouvez maintenant rechercher trop**http://localhost : 8000 /** application hello de tootest.</span><span class="sxs-lookup"><span data-stu-id="231c6-165">You can now browse too**http://localhost:8000/** tootest hello application.</span></span>

## <a name="publish-your-app"></a><span data-ttu-id="231c6-166">Publier votre application</span><span class="sxs-lookup"><span data-stu-id="231c6-166">Publish your app</span></span>
<span data-ttu-id="231c6-167">Après avoir testé votre application localement, vous pouvez le publier des applications de tooWeb à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="231c6-167">After you have tested your app locally, you can publish it tooWeb Apps using Git.</span></span> <span data-ttu-id="231c6-168">Vous initialisez votre référentiel Git local et publier l’application hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-168">You will initialize your local Git repository and publish hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="231c6-169">Ils sont même hello les étapes présentées dans le portail Azure à fin hello Hello créer une application web et l’ensemble de hello la publication Git section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="231c6-169">These are hello same steps shown in hello Azure Portal at hello end of hello Create a web app and Set up Git Publishing section above.</span></span>
> 
> 

1. <span data-ttu-id="231c6-170">(Facultatif)  Si vous avez oublié ou mal placé votre URL de repostitory distant Git, accédez à propriétés de l’application web toohello sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="231c6-170">(Optional)  If you've forgotten or misplaced your Git remote repostitory URL, navigate toohello web app properties on hello Azure Portal.</span></span>
2. <span data-ttu-id="231c6-171">Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="231c6-171">Open GitBash (or a terminal, if Git is in your `PATH`), change directories toohello root directory of your application, and run hello following commands:</span></span>
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    <span data-ttu-id="231c6-172">Vous demandera un mot de passe hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="231c6-172">You will be prompted for hello password you created earlier.</span></span>
   
    ![Initiale tooAzure Push via Git][git-initial-push]
3. <span data-ttu-id="231c6-174">Parcourir trop**http://[site name].azurewebsites.net/index.php** toobegin à l’aide d’application hello (ces informations seront stockées sur votre tableau de bord de compte) :</span><span class="sxs-lookup"><span data-stu-id="231c6-174">Browse too**http://[site name].azurewebsites.net/index.php** toobegin using hello application (this information will be stored on your account dashboard):</span></span>
   
    ![Site Web PHP Azure][running-app]

<span data-ttu-id="231c6-176">Une fois que vous avez publié votre application, vous pouvez commencer à apporter des modifications tooit et utiliser Git toopublish les.</span><span class="sxs-lookup"><span data-stu-id="231c6-176">After you have published your app, you can begin making changes tooit and use Git toopublish them.</span></span>

## <a name="publish-changes-tooyour-app"></a><span data-ttu-id="231c6-177">Publier les modifications tooyour application</span><span class="sxs-lookup"><span data-stu-id="231c6-177">Publish changes tooyour app</span></span>
<span data-ttu-id="231c6-178">application de tooyour toopublish modifications, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="231c6-178">toopublish changes tooyour app, follow these steps:</span></span>

1. <span data-ttu-id="231c6-179">Apporter des modifications tooyour application localement.</span><span class="sxs-lookup"><span data-stu-id="231c6-179">Make changes tooyour app locally.</span></span>
2. <span data-ttu-id="231c6-180">Ouvrez GitBash (ou un terminal, informatique Git est dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="231c6-180">Open GitBash (or a terminal, it Git is in your `PATH`), change directories toohello root directory of your app, and run hello following commands:</span></span>
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    <span data-ttu-id="231c6-181">Vous demandera un mot de passe hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="231c6-181">You will be prompted for hello password you created earlier.</span></span>
   
    ![En exécutant un push de site change tooAzure via Git][git-change-push]
3. <span data-ttu-id="231c6-183">Parcourir trop**http://[site name].azurewebsites.net/index.php** toosee votre application et toutes les modifications que vous avez apportées :</span><span class="sxs-lookup"><span data-stu-id="231c6-183">Browse too**http://[site name].azurewebsites.net/index.php** toosee your app and any changes you may have made:</span></span>
   
    ![Site Web PHP Azure][running-app]

> [!NOTE]
> <span data-ttu-id="231c6-185">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="231c6-185">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="231c6-186">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="231c6-186">No credit cards required; no commitments.</span></span>
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a><span data-ttu-id="231c6-187">Activer l’automatisation de Composer avec hello extension d’éditeur</span><span class="sxs-lookup"><span data-stu-id="231c6-187">Enable Composer automation with hello Composer extension</span></span>
<span data-ttu-id="231c6-188">Par défaut, processus de déploiement git hello du Service d’applications ne fait rien avec composer.json, si vous en avez dans votre projet PHP.</span><span class="sxs-lookup"><span data-stu-id="231c6-188">By default, hello git deployment process in App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="231c6-189">Vous pouvez activer composer.json du traitement au cours `git push` par activation de l’extension de Composer hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-189">You can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

1. <span data-ttu-id="231c6-190">Dans votre PHP web lame l’application hello [portail Azure][management-portal], cliquez sur **outils** > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="231c6-190">In your PHP web app's blade in hello [Azure portal][management-portal], click **Tools** > **Extensions**.</span></span>
   
    ![Paramètres d’extension du Compositeur][composer-extension-settings]
2. <span data-ttu-id="231c6-192">Cliquez sur **Ajouter** puis sur **Compositeur**.</span><span class="sxs-lookup"><span data-stu-id="231c6-192">Click **Add**, then click **Composer**.</span></span>
   
    ![Ajout d’extension au Compositeur][composer-extension-add]
3. <span data-ttu-id="231c6-194">Cliquez sur **OK** tooaccept les conditions juridiques.</span><span class="sxs-lookup"><span data-stu-id="231c6-194">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="231c6-195">Cliquez sur **OK** à nouveau les extension tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-195">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="231c6-196">Hello **extensions installées** panneau affiche désormais les extensions de Composer hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-196">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="231c6-197">![Vue Extension du Compositeur][composer-extension-view]</span><span class="sxs-lookup"><span data-stu-id="231c6-197">![Composer Extension View][composer-extension-view]</span></span>
4. <span data-ttu-id="231c6-198">À présent, effectuer `git add`, `git commit`, et `git push` comme dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="231c6-198">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="231c6-199">Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.</span><span class="sxs-lookup"><span data-stu-id="231c6-199">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Réussite de l’extension du Compositeur][composer-extension-success]

## <a name="next-steps"></a><span data-ttu-id="231c6-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="231c6-201">Next steps</span></span>
<span data-ttu-id="231c6-202">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="231c6-202">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

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
