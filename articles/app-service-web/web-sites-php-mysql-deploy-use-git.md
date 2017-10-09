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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-git"></a>Création d’une application web PHP-MySQL dans Azure App Service et déploiement à l’aide de Git.
Ce didacticiel vous montre comment l’application web de toocreate un MySQL de PHP et toodeploy il trop[du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) à l’aide de Git. Vous allez utiliser [PHP][install-php], hello l’outil de ligne de commande MySQL (dans le cadre du [MySQL][install-mysql]), et [Git] [ install-git] installé sur votre ordinateur. instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation, notamment Windows, Mac et Linux. À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.

Vous apprendrez à effectuer les opérations suivantes :

* Comment toocreate une application web et un MySQL de base de données à l’aide de hello [Azure Portal][management-portal]. Étant donné que PHP est activée dans [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) par défaut, rien de spécial est nécessaire toorun votre code PHP.
* Comment toopublish et republiez votre tooAzure d’application à l’aide de Git.
* Des tâches de tooenable hello Composer extension tooautomate Composer à chaque `git push`.

En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP. Hello application sera hébergée dans les applications Web. Une capture d’écran de l’application hello terminée est ci-dessous :

![Site Web PHP Azure][running-app]

## <a name="set-up-hello-development-environment"></a>Configuration d’environnement de développement hello
Ce didacticiel suppose que vous avez [PHP][install-php], hello l’outil de ligne de commande MySQL (dans le cadre du [MySQL][install-mysql]), et [Git] [ install-git] installé sur votre ordinateur.

<a id="create-web-site-and-set-up-git"></a>

## <a name="create-a-web-app-and-set-up-git-publishing"></a>Créer une application web et configurer la publication Git
Suivez ces étapes toocreate une application web et une base de données MySQL :

1. Connexion toohello [Azure Portal][management-portal].
2. Cliquez sur hello **nouveau** icône.
3. Cliquez sur **voir tous les** suivant trop**Marketplace**. 
4. Cliquez sur **Web et mobilité**, puis sur **Application web et MySQL**. Cliquez sur **Créer**.
5. Entrez un nom valide pour votre groupe de ressources.
   
    ![Définir le nom du groupe de ressources][resource-group]
6. Entrez des valeurs pour votre nouvelle application web.
   
    ![Créer une application web][new-web-app]
7. Entrez des valeurs pour votre nouvelle base de données, y compris les acceptez les conditions juridiques toohello.
   
    ![Créer une base de données MySQL][new-mysql-db]
8. Lorsque l’application hello web a été créée, vous verrez le nouveau panneau des applications web hello.
9. Dans les **Paramètres**, cliquez sur **Déploiement continu**, puis cliquez sur *Configurer les paramètres requis*.
   
    ![Configuration de la publication Git][setup-publishing]
10. Sélectionnez **référentiel Git Local** pour la source de hello.
    
     ![Configurer le référentiel Git][setup-repository]
11. tooenable Git de publication, vous devez fournir un nom d’utilisateur et un mot de passe. Prenez note du nom d’utilisateur hello et vous créez un mot de passe. (si vous avez déjà configuré un référentiel Git, ignorez cette étape).
    
     ![Création des informations d’identification de publication][credentials]

## <a name="get-remote-mysql-connection-information"></a>Obtention des informations de connexion MySQL distantes
tooconnect toohello base de données MySQL qui est en cours d’exécution dans les applications Web, votre besoin hello des informations de connexion. tooget les informations de connexion MySQL, procédez comme suit :

1. À partir de votre groupe de ressources, cliquez sur base de données hello :
   
    ![Sélectionner la base de données][select-database]
2. À partir de la base de données hello **paramètres**, sélectionnez **propriétés**.
   
    ![Sélectionner les propriétés][select-properties]
3. Notez les valeurs hello pour `Database`, `Host`, `User Id`, et `Password`.
   
    ![Noter les propriétés][note-properties]

## <a name="build-and-test-your-app-locally"></a>Générer et tester votre application localement
Après avoir créé une application web, vous pouvez la développer localement, la tester, puis la déployer.

Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie. Les informations relatives aux précédents inscrits sont affichées dans un tableau. Les informations d'inscription sont stockées dans une base de données MySQL. application Hello se compose d’un fichier (code de copier/coller ci-dessous) :

* **index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.

toobuild et application hello exécution localement, suivez les étapes de hello ci-dessous. Notez que ces étapes supposent que vous avez hello PHP et MySQL Line Tool (partie de MySQL) sur votre ordinateur local, et que vous avez activé hello [extension PDO pour MySQL][pdo-mysql].

1. Connecter le serveur MySQL distant toohello, à l’aide de la valeur hello pour `Data Source`, `User Id`, `Password`, et `Database` que vous avez récupéré précédemment :
   
        mysql -h{Data Source] -u[User Id] -p[Password] -D[Database]
2. invite de commandes Hello MySQL s’affiche :
   
        mysql>
3. Coller dans les éléments suivants de hello `CREATE TABLE` commande toocreate hello `registration_tbl` table dans votre base de données :
   
        CREATE TABLE registration_tbl(id INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(id), name VARCHAR(30), email VARCHAR(30), date DATE);
4. Dans votre dossier local d’application racine hello créer **index.php** fichier.
5. Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello suivant de code, et les modifications nécessaires hello complète marqué avec `//TODO:` commentaires.

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

1. Dans un terminal tooyour accédez application dossier et tapez Bonjour commande suivante :
   
       php -S localhost:8000

Vous pouvez maintenant rechercher trop**http://localhost : 8000 /** application hello de tootest.

## <a name="publish-your-app"></a>Publier votre application
Après avoir testé votre application localement, vous pouvez le publier des applications de tooWeb à l’aide de Git. Vous initialisez votre référentiel Git local et publier l’application hello.

> [!NOTE]
> Ils sont même hello les étapes présentées dans le portail Azure à fin hello Hello créer une application web et l’ensemble de hello la publication Git section ci-dessus.
> 
> 

1. (Facultatif)  Si vous avez oublié ou mal placé votre URL de repostitory distant Git, accédez à propriétés de l’application web toohello sur hello portail Azure.
2. Ouvrez GitBash (ou un terminal, si Git se trouve dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :
   
        git init
        git add .
        git commit -m "initial commit"
        git remote add azure [URL for remote repository]
        git push azure master
   
    Vous demandera un mot de passe hello que vous avez créé précédemment.
   
    ![Initiale tooAzure Push via Git][git-initial-push]
3. Parcourir trop**http://[site name].azurewebsites.net/index.php** toobegin à l’aide d’application hello (ces informations seront stockées sur votre tableau de bord de compte) :
   
    ![Site Web PHP Azure][running-app]

Une fois que vous avez publié votre application, vous pouvez commencer à apporter des modifications tooit et utiliser Git toopublish les.

## <a name="publish-changes-tooyour-app"></a>Publier les modifications tooyour application
application de tooyour toopublish modifications, procédez comme suit :

1. Apporter des modifications tooyour application localement.
2. Ouvrez GitBash (ou un terminal, informatique Git est dans votre `PATH`) répertoire toohello de répertoires de votre application, et modifier hello suivant de commandes :
   
        git add .
        git commit -m "comment describing changes"
        git push azure master
   
    Vous demandera un mot de passe hello que vous avez créé précédemment.
   
    ![En exécutant un push de site change tooAzure via Git][git-change-push]
3. Parcourir trop**http://[site name].azurewebsites.net/index.php** toosee votre application et toutes les modifications que vous avez apportées :
   
    ![Site Web PHP Azure][running-app]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

<a name="composer"></a>

## <a name="enable-composer-automation-with-hello-composer-extension"></a>Activer l’automatisation de Composer avec hello extension d’éditeur
Par défaut, processus de déploiement git hello du Service d’applications ne fait rien avec composer.json, si vous en avez dans votre projet PHP. Vous pouvez activer composer.json du traitement au cours `git push` par activation de l’extension de Composer hello.

1. Dans votre PHP web lame l’application hello [portail Azure][management-portal], cliquez sur **outils** > **Extensions**.
   
    ![Paramètres d’extension du Compositeur][composer-extension-settings]
2. Cliquez sur **Ajouter** puis sur **Compositeur**.
   
    ![Ajout d’extension au Compositeur][composer-extension-add]
3. Cliquez sur **OK** tooaccept les conditions juridiques. Cliquez sur **OK** à nouveau les extension tooadd hello.
   
    Hello **extensions installées** panneau affiche désormais les extensions de Composer hello.  
    ![Vue Extension du Compositeur][composer-extension-view]
4. À présent, effectuer `git add`, `git commit`, et `git push` comme dans la section précédente de hello. Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.
   
    ![Réussite de l’extension du Compositeur][composer-extension-success]

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).

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
