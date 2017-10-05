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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Création d’une application web PHP-MySQL dans Azure App Service et déploiement à l’aide de Git.
Ce didacticiel vous explique comment créer une application web PHP-MySQL et déployer dans [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de Git. Vous allez utiliser [PHP][install-php], l’outil de ligne de commande MySQL (inclus dans [MySQL][install-mysql]), et [Git][install-git] qui sont installés sur votre ordinateur. Les instructions de ce didacticiel s’appliquent à n’importe quel système d’exploitation, notamment Windows, Mac et Linux. À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.

Vous apprendrez à effectuer les opérations suivantes :

* création d’une application web et d’une base de données MySQL à l’aide du [portail Azure][management-portal]. PHP étant activé par défaut dans [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) , l’exécution de votre code PHP ne requiert aucune action particulière) ;
* publication et republication de votre application dans Azure en utilisant Git.
* activation de l’extension du compositeur pour automatiser les tâches de compositeur à chaque `git push`.

En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP. Cette application sera hébergée dans Web Apps. Voici une capture d’écran de l’application terminée :

![Site Web PHP Azure][running-app]

## <a name="set-up-the-development-environment"></a>Configuration de l’environnement de développement
Ce didacticiel part du principe que [PHP][install-php], l’outil de ligne de commande MySQL (qui fait partie de [MySQL][install-mysql]) et [Git][install-git] sont installés sur votre ordinateur.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Créer une application web et configurer la publication Git
Pour créer une application web et une base de données MySQL, suivez la procédure ci-après :

1. Connectez-vous au [portail Azure][management-portal].
2. Cliquez sur l'icône **Nouveau** .
3. Cliquez sur **Afficher tout** en regard de **Marketplace**. 
4. Cliquez sur **Web et mobilité**, puis sur **Application web et MySQL**. Cliquez sur **Créer**.
5. Entrez un nom valide pour votre groupe de ressources.
   
    ![Définir le nom du groupe de ressources][resource-group]
6. Entrez des valeurs pour votre nouvelle application web.
   
    ![Créer une application web][new-web-app]
7. Entrez des valeurs pour votre nouvelle base de données, notamment l’acceptation des conditions juridiques.
   
    ![Créer une base de données MySQL][new-mysql-db]
8. Une fois que l'application web a été créée, vous voyez apparaître le nouveau volet d'application web.
9. Dans les **Paramètres**, cliquez sur **Déploiement continu**, puis cliquez sur *Configurer les paramètres requis*.
   
    ![Configuration de la publication Git][setup-publishing]
10. Sélectionnez **Référentiel Git local** comme source.
    
     ![Configurer le référentiel Git][setup-repository]
11. Pour activer la publication Git, vous devez fournir un nom d'utilisateur et un mot de passe. Notez le nom d'utilisateur et le mot de passe que vous créez (si vous avez déjà configuré un référentiel Git, ignorez cette étape).
    
     ![Création des informations d’identification de publication][credentials]

## <a name="get-remote-mysql-connection-information"></a>Obtention des informations de connexion MySQL distantes
Pour vous connecter à la base de données MySQL qui s’exécute dans Web Apps, vous devez disposer des informations de connexion. Pour obtenir vos informations de connexion MySQL, procédez comme suit :

1. À partir de votre groupe de ressources, cliquez sur la base de données :
   
    ![Sélectionner la base de données][select-database]
2. Dans les **Paramètres** de la base de données, sélectionnez **Propriétés**.
   
    ![Sélectionner les propriétés][select-properties]
3. Notez les valeurs de `Database`, `Host`, `User Id` et `Password`.
   
    ![Noter les propriétés][note-properties]

## <a name="build-and-test-your-app-locally"></a>Générer et tester votre application localement
Après avoir créé une application web, vous pouvez la développer localement, la tester, puis la déployer.

L'application d'inscription est une simple application PHP qui vous permet de vous inscrire à un événement en entrant votre nom et votre adresse électronique. Les informations relatives aux précédents inscrits sont affichées dans un tableau. Les informations d'inscription sont stockées dans une base de données MySQL. L'application se compose d'un seul fichier (dont le code est disponible ci-dessous pour un copier/coller) :

* **index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.

Pour générer et exécuter l'application en local, procédez comme suit : Notez que ces étapes partent du principe que PHP et l’outil de ligne de commande MySQL (inclus dans MySQL) sont installés sur votre ordinateur local, et que vous avez activé l’[extension PDO pour MySQL][pdo-mysql].

1. Connectez-vous au serveur MySQL distant en utilisant les valeurs `Data Source`, `User Id`, `Password` et `Database` récupérées précédemment :
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. L'invite de commandes MySQL s'affiche :
   
        mysql>
3. Copiez la commande `CREATE TABLE` suivante pour créer la table `registration_tbl` dans votre base de données :
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Dans la racine de votre dossier d'application en local, créez le fichier **index.php** .
5. Ouvrez le fichier **index.php** dans un éditeur de texte ou un environnement de développement intégré (IDE), puis ajoutez le code suivant en y apportant les modifications nécessaires, indiquées par les commentaires `//TODO:`.

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

1. Sur un terminal, accédez à votre dossier d'application et tapez la commande suivante :
   
       php -S localhost:8000

Vous pouvez maintenant accéder à **http://localhost:8000/** pour tester l’application.

## <a name="publish-your-app"></a>Publier votre application
Après avoir testé votre application localement, vous pouvez la publier dans Web Apps à l’aide de Git. Vous allez initialiser votre référentiel Git, puis publier l'application.

> [!NOTE]
> Cette procédure est identique à celle affichée dans le portail Azure à la fin de la section « Créer une application web et configurer la publication Git » précédente.
> 
> 

1. (Facultatif) Si vous avez oublié ou mal placé l’URL de votre référentiel distant Git, accédez aux propriétés de l’application web sur le portail Azure.
2. Ouvrez GitBash (ou un terminal, si Git est dans votre `PATH`), remplacez les répertoires du répertoire racine de votre application, puis exécutez les commandes suivantes :
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Vous êtes invité à entrer le mot de passe que vous avez créé précédemment.
   
    ![Transmission initiale vers Azure via Git][git-initial-push]
3. Accédez à **http://[nom du site].azurewebsites.net/index.php** pour commencer à utiliser l’application (ces informations seront stockées dans le tableau de bord de votre compte) :
   
    ![Site Web PHP Azure][running-app]

Après avoir publié votre application, vous pouvez y apporter des modifications, puis publier ces dernières à l’aide de Git.

## <a name="publish-changes-to-your-app"></a>Publier les modifications apportées à votre application
Pour publier les modifications apportées à votre application, procédez comme suit :

1. Modifiez votre application localement.
2. Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`), remplacez les répertoires par le répertoire racine de votre application, puis exécutez les commandes suivantes :
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Vous êtes invité à entrer le mot de passe que vous avez créé précédemment.
   
    ![Publication des modifications apportées au site dans Azure via Git][git-change-push]
3. Accédez à **http://[nom du site].azurewebsites.net/index.php** pour afficher votre application, ainsi que les modifications apportées :
   
    ![Site Web PHP Azure][running-app]

> [!NOTE]
> Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-the-composer-extension"></a>Activation de l’automatisation du Compositeur avec l’extension du Compositeur
Par défaut, le processus de déploiement de git dans le Service d’application ne fait rien avec composer.json, si vous en avez un dans votre projet PHP. Vous pouvez activer le traitement du composer.json pendant `git push` en activant l’extension du Compositeur.

1. Dans le panneau de l’application web PHP (dans le [portail Azure][management-portal]), cliquez sur **Outils** > **Extensions**.
   
    ![Paramètres d’extension du Compositeur][composer-extension-settings]
2. Cliquez sur **Ajouter** puis sur **Compositeur**.
   
    ![Ajout d’extension au Compositeur][composer-extension-add]
3. Cliquez sur **OK** pour accepter les conditions juridiques. Cliquez à nouveau sur **OK** pour ajouter l’extension.
   
    Le panneau **Extensions installées** affiche désormais l’extension du Compositeur.  
    ![Vue Extension du Compositeur][composer-extension-view]
4. Maintenant, exécutez `git add`, `git commit` et `git push` comme dans la section précédente. Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.
   
    ![Réussite de l’extension du Compositeur][composer-extension-success]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).

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
