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
# <a name="create-a-php-sql-web-app-and-deploy-tooazure-app-service-using-git"></a>Créer une application web de PHP-SQL et de déployer tooAzure du Service d’applications à l’aide de Git
Ce didacticiel vous montre comment toocreate PHP web app dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) qui connecte tooAzure base de données SQL et comment toodeploy à l’aide de Git. Ce didacticiel suppose que vous avez [PHP][install-php], [SQL Server Express][install-SQLExpress], hello [Microsoft Drivers for SQL Server pour PHP ](http://www.microsoft.com/download/en/details.aspx?id=20098), et [Git] [ install-git] installé sur votre ordinateur. À la fin de ce guide, vous disposerez d’une application web PHP-SQL s’exécutant dans Azure.

> [!NOTE]
> Vous pouvez installer et configurer PHP, SQL Server Express et hello Microsoft Drivers for SQL Server pour PHP à l’aide de hello [Microsoft Web Platform Installer](http://www.microsoft.com/web/downloads/platform.aspx).
> 
> 

Vous apprendrez à effectuer les opérations suivantes :

* Comment toocreate Azure web app et une base de données SQL à l’aide de hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715). PHP est activé dans les applications Web de Service application par défaut, rien de spécial est nécessaire toorun votre code PHP.
* Comment toopublish et republiez votre tooAzure d’application à l’aide de Git.

En suivant ce didacticiel, vous allez générer une application Web d'inscription simple dans PHP. Hello application sera hébergée dans un site Web Azure. Une capture d’écran de l’application hello terminée est ci-dessous :

![Site Web PHP Azure](./media/web-sites-php-sql-database-deploy-use-git/running_app_3.png)

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="create-an-azure-web-app-and-set-up-git-publishing"></a>Création d’une application web Azure et configuration de la publication Git
Suivez ces étapes de toocreate une application web Azure et une base de données SQL :

1. Connectez-vous à toohello [Azure Portal](https://portal.azure.com/).
2. Ouvrez hello Azure Marketplace en cliquant sur hello **nouveau** icône en haut de hello à gauche du tableau de bord hello, cliquez sur **sélectionner tout** tooMarketplace suivant et en sélectionnant **Web + Mobile**.
3. Bonjour Marketplace, sélectionnez **Web + Mobile**.
4. Cliquez sur hello **Web application + SQL** icône.
5. Après avoir lu la description hello de l’application hello Web + SQL application, sélectionnez **créer**.
6. Cliquez sur chaque partie (**groupe de ressources**, **Web App**, **base de données**, et **abonnement**) et entrez ou sélectionnez les valeurs pour hello requis champs :
   
   * Entrez le nom d’URL de votre choix.    
   * Configuration des informations d’identification du serveur de bases de données
   * Sélectionnez tooyou le plus proche de la région de hello
     
     ![Configurer une application](./media/web-sites-php-sql-database-deploy-use-git/configure-db-settings.png)
7. Une fois la définition de l’application hello web, cliquez sur **créer**.
   
    Lorsque l’application hello web a été créée, hello **Notifications** un vert clignote en bouton **réussite** et hello ressource groupe panneau ouvert tooshow deux hello web app et hello SQL de base de données dans le groupe de hello.
8. Cliquez sur icône de l’application hello web dans le panneau de hello ressource groupe panneau tooopen hello application web.
   
    ![Groupe de ressources de l’application web](./media/web-sites-php-sql-database-deploy-use-git/resource-group-blade.png)
9. Dans **Paramètres**, cliquez sur **Déploiement continu** > **Configurer les paramètres requis**. Sélectionnez **Référentiel Git local**, puis cliquez sur **OK**.
   
    ![où est votre code source](./media/web-sites-php-sql-database-deploy-use-git/setup-local-git.png)
   
    Si vous n’avez pas encore configuré de référentiel Git, vous devez fournir un nom d’utilisateur et un mot de passe. toodo, cliquez sur **paramètres** > **informations d’identification de déploiement** dans le panneau de l’application hello web.
   
    ![](./media/web-sites-php-sql-database-deploy-use-git/deployment-credentials.png)
10. Dans **paramètres** cliquez sur **propriétés** toosee hello Git URL distante vous besoin de votre application PHP toouse toodeploy plus tard.

## <a name="get-sql-database-connection-information"></a>Obtention des informations de connexion à la base de données SQL
instance de base de données SQL toohello tooconnect qui est lié l’application web tooyour, votre besoin hello les informations de connexion, vous avez spécifié lors de la création de la base de données hello. tooget hello informations de connexion de base de données SQL, procédez comme suit :

1. Dans le panneau du groupe de ressources hello, cliquez sur icône de hello SQL de base de données.
2. Dans le panneau de hello SQL de base de données, cliquez sur **paramètres** > **propriétés**, puis cliquez sur **afficher les chaînes de connexion de base de données**. 
   
    ![Afficher les propriétés de base de données](./media/web-sites-php-sql-database-deploy-use-git/view-database-properties.png)
3. À partir de hello **PHP** section de la boîte de dialogue hello, notez les valeurs hello pour `Server`, `SQL Database`, et `User Name`. Vous utiliserez ces valeurs ultérieurement de publication lorsque votre tooAzure d’application PHP web du Service d’applications.

## <a name="build-and-test-your-application-locally"></a>Génération et test de votre application localement
Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie. Les informations relatives aux précédents inscrits sont affichées dans un tableau. Les informations d'inscription sont stockées dans une instance de base de données SQL. application Hello se compose de deux fichiers (code de copier/coller ci-dessous) :

* **index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.
* **CreateTable.PHP**: crée la table de base de données SQL hello pour une application hello. Ce fichier sera utilisé une seule fois.

application de hello toorun localement, suivez les étapes de hello ci-dessous. Notez que ces étapes supposent que vous avez PHP et de SQL Server Express configuré sur votre ordinateur local, et que vous avez activé hello [extension PDO pour SQL Server][pdo-sqlsrv].

1. Créez une base de données SQL Server nommée `registration`. Vous pouvez les spécifier cela via hello `sqlcmd` invite de commandes avec ces commandes :
   
        >sqlcmd -S localhost\sqlexpress -U <local user name> -P <local password>
        1> create database registration
        2> GO    
2. Dans le répertoire racine de votre application, créez deux fichiers : un fichier nommé `createtable.php` et un autre nommé `index.php`.
3. Ouvrez hello `createtable.php` dans un éditeur de texte ou un IDE et ajoutez le code hello ci-dessous. Ce code sera utilisé toocreate hello `registration_tbl` table Bonjour `registration` base de données.
   
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
   
    Notez que vous aurez besoin des valeurs de hello tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur SQL Server local et le mot de passe.
4. Dans un terminal au répertoire racine de hello Hello de type hello application commande suivante :
   
        php -S localhost:8000
5. Ouvrez un navigateur web et accédez trop**http://localhost:8000/createtable.php**. Cela créera hello `registration_tbl` table hello de base de données.
6. Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello base code HTML et CSS pour la page de hello (hello code PHP est ajouté dans les étapes ultérieures).
   
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
7. Dans les balises PHP hello, ajoutez le code PHP pour la connexion de base de données toohello.
   
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
   
    Là encore, vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.
8. Après le code de connexion de base de données hello, ajoutez le code pour l’insertion des informations d’inscription dans la base de données hello.
   
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
9. Enfin, après le code hello ci-dessus, ajoutez du code pour récupérer des données à partir de la base de données hello.
   
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

Vous pouvez maintenant rechercher trop**http://localhost:8000/index.php** application hello de tootest.

## <a name="publish-your-application"></a>Publication de votre application
Après avoir testé votre application localement, vous pouvez le publier tooApp Service Web Apps à l’aide de Git. Toutefois, vous devez tout d’abord les informations de connexion de base de données de hello tooupdate dans l’application hello. À l’aide des informations de connexion de base de données hello obtenues précédemment (Bonjour **informations de connexion à obtenir de la base de données SQL** section), hello de mise à jour après les informations contenues dans **les deux** hello `createdatabase.php` et `index.php` fichiers par hello les valeurs appropriées :

    // DB connection info
    $host = "tcp:<value of Server>";
    $user = "<value of User Name>";
    $pwd = "<your password>";
    $db = "<value of SQL Database>";

> [!NOTE]
> Bonjour <code>$host</code>, valeur hello du serveur doit être précédé de <code>tcp:</code>.
> 
> 

Maintenant, vous êtes prêt tooset de publication Git et que vous publiez l’application hello.

> [!NOTE]
> Il s’agit hello mêmes étapes indiqué plus haut fin hello Hello **créer une application web Azure et configurer la publication Git** section ci-dessus.
> 
> 

1. Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`), remplacer répertoires toohello racine de votre application (hello **inscription** active), et en exécution hello suivant de commandes :
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Vous demandera un mot de passe hello que vous avez créé précédemment.
2. Parcourir trop**http://[web application name].azurewebsites.net/createtable.php** table de base de données SQL toocreate hello pour une application hello.
3. Parcourir trop**http://[web application name].azurewebsites.net/index.php** toobegin à l’aide d’application hello.

Une fois que vous avez publié votre application, vous pouvez commencer à apporter des modifications tooit et utiliser Git toopublish les. 

## <a name="publish-changes-tooyour-application"></a>Publier les modifications tooyour application
toopublish change tooapplication, procédez comme suit :

1. Apporter des modifications application tooyour localement.
2. Ouvrez GitBash (ou un terminal, informatique Git est dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Vous demandera un mot de passe hello que vous avez créé précédemment.
3. Parcourir trop**http://[web application name].azurewebsites.net/index.php** toosee vos modifications.

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[install-php]: http://www.php.net/manual/en/install.php
[install-SQLExpress]: http://www.microsoft.com/download/details.aspx?id=29062
[install-Drivers]: http://www.microsoft.com/download/details.aspx?id=20098
[install-git]: http://git-scm.com/
[pdo-sqlsrv]: http://php.net/pdo_sqlsrv

