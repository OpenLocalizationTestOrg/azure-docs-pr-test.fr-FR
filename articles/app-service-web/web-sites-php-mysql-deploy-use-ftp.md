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
# <a name="create-a-php-mysql-web-app-in-azure-app-service-and-deploy-using-ftp"></a>Créer une application web PHP-MySQL dans Azure App Service et la déployer à l’aide de FTP
Ce didacticiel vous montre comment l’application web de toocreate un MySQL de PHP et toodeploy à l’aide de FTP. Il part du principe que vous avez installé [PHP][install-php], [MySQL][install-mysql], un serveur Web et un client FTP sur votre ordinateur. instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation, notamment Windows, Mac et Linux. À la fin de ce guide, vous disposerez d’une application web PHP/MySQL s’exécutant dans Azure.

Vous apprendrez à effectuer les opérations suivantes :

* Comment une application web et un MySQL de base de données à l’aide de toocreate hello portail Azure. PHP est activé dans les applications Web par défaut, rien de spécial est nécessaire toorun votre code PHP.
* Comment toopublish votre tooAzure d’application en utilisant FTP.

En suivant ce didacticiel, vous allez générer une application web d’inscription simple dans PHP. Hello application sera hébergée dans une application Web. Une capture d’écran de l’application hello terminée est ci-dessous :

![Site Web PHP Azure][running-app]

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise, et vous ne prenez aucun engagement. 
> 
> 

## <a name="create-a-web-app-and-set-up-ftp-publishing"></a>Créer une application web et configurer la publication FTP
Suivez ces étapes toocreate une application web et une base de données MySQL :

1. Connexion toohello [Azure Portal][management-portal].
2. Cliquez sur hello **+ nouveau** icône en haut de hello à gauche de hello portail Azure.
   
    ![Créer un site Web Azure][new-website]
3. Dans le type de recherche hello **Web application + MySQL** , puis cliquez sur **Web application + MySQL**.
   
    ![Création personnalisée d'un site web][custom-create]
4. Cliquez sur **Créer**. Entrez un nom de service d’application unique, un nom valide pour le groupe de ressources hello et un nouveau plan de service.
   
    ![Définir le nom du groupe de ressources][resource-group]
5. Entrez des valeurs pour votre nouvelle base de données, y compris les acceptez les conditions juridiques toohello.
   
    ![Créer une base de données MySQL][new-mysql-db]
6. Lorsque l’application hello web a été créée, vous verrez le nouveau panneau de service application hello.
7. Cliquez sur **Paramètres** > **Informations d’identification de déploiement**. 
   
    ![Définir les informations d’identification de déploiement][set-deployment-credentials]
8. tooenable de publication FTP, vous devez fournir un nom d’utilisateur et un mot de passe. Enregistrer les informations d’identification hello et prenez note du nom d’utilisateur hello et vous créez un mot de passe.
   
    ![Création des informations d’identification de publication][portal-ftp-username-password]

## <a name="build-and-test-your-app-locally"></a>Générer et tester votre application localement
Hello demande d’enregistrement est une simple application PHP qui vous permet de tooregister pour un événement en fournissant votre nom et adresse de messagerie. Les informations relatives aux précédents inscrits sont affichées dans un tableau. Les informations d'inscription sont stockées dans une base de données MySQL. application Hello se compose de deux fichiers :

* **index.php**: affiche un formulaire d’inscription et un tableau contenant les informations des inscrits.
* **CreateTable.PHP**: crée la table de MySQL hello pour une application hello. Ce fichier sera utilisé une seule fois.

toobuild et application hello exécution localement, suivez les étapes de hello ci-dessous. Notez que ces étapes supposent que vous avez PHP, MySQL et un serveur web sur votre ordinateur local, et que vous avez activé hello [extension PDO pour MySQL][pdo-mysql].

1. Créez une base de données MySQL nommée `registration`. Vous pouvez effectuer cela à partir de l’invite de commandes hello MySQL avec cette commande :
   
        mysql> create database registration;
2. Dans le répertoire racine de votre serveur web, créez un dossier nommé `registration` et deux fichiers à l’intérieur : un fichier nommé `createtable.php` et un autre nommé `index.php`.
3. Ouvrez hello `createtable.php` dans un éditeur de texte ou un IDE et ajoutez le code hello ci-dessous. Ce code sera utilisé toocreate hello `registration_tbl` table Bonjour `registration` base de données.
   
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
   > Vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.
   > 
   > 
4. Ouvrez un navigateur web et accédez trop[http://localhost/registration/createtable.php][localhost-createtable]. Cela créera hello `registration_tbl` table hello de base de données.
5. Ouvrez hello **index.php** dans un éditeur de texte ou un IDE et ajoutez hello base code HTML et CSS pour la page de hello (hello code PHP est ajouté dans les étapes ultérieures).
   
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
6. Dans les balises PHP hello, ajoutez le code PHP pour la connexion de base de données toohello.
   
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
   > Là encore, vous avez besoin des valeurs de hello de tooupdate pour <code>$user</code> et <code>$pwd</code> avec votre nom d’utilisateur MySQL local et le mot de passe.
   > 
   > 
7. Après le code de connexion de base de données hello, ajoutez le code pour l’insertion des informations d’inscription dans la base de données hello.
   
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
8. Enfin, après le code hello ci-dessus, ajoutez du code pour récupérer des données à partir de la base de données hello.
   
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

Vous pouvez maintenant rechercher trop[http://localhost/registration/index.php] [ localhost-index] tootest hello application.

## <a name="get-mysql-and-ftp-connection-information"></a>Obtention des informations de connexion MySQL et FTP
tooconnect toohello base de données MySQL qui est en cours d’exécution dans les applications Web, votre besoin hello des informations de connexion. tooget les informations de connexion MySQL, procédez comme suit :

1. À partir du service de l’application hello Panneau de l’application web cliquez sur le lien de groupe de ressources hello :
   
    ![Sélectionner Groupe de ressources][select-resourcegroup]
2. À partir de votre groupe de ressources, cliquez sur base de données hello :
   
    ![Sélectionner la base de données][select-database]
3. À partir de la base de données de synthèse hello, sélectionnez **paramètres** > **propriétés**.
   
    ![Sélectionner les propriétés][select-properties]
4. Notez les valeurs hello pour `Database`, `Host`, `User Id`, et `Password`.
   
    ![Noter les propriétés][note-properties]
5. À partir de votre application web, cliquez sur hello **télécharger le profil de publication** lien hello coin inférieur droit de la page de hello :
   
    ![Télécharger le profil de publication][download-publish-profile]
6. Ouvrez hello `.publishsettings` fichier dans un éditeur XML. 
7. Recherche hello `<publishProfile >` élément avec `publishMethod="FTP"` qui recherche toothis similaire :
   
        <publishProfile publishMethod="FTP" publishUrl="ftp://[mysite].azurewebsites.net/site/wwwroot" ftpPassiveMode="True" userName="[username]" userPWD="[password]" destinationAppUrl="http://[name].antdf0.antares-test.windows-int.net" 
            ...
        </publishProfile>

Prenez note de hello `publishUrl`, `userName`, et `userPWD` attributs.

## <a name="publish-your-app"></a>Publier votre application
Après avoir testé votre application localement, vous pouvez le publier l’application web tooyour à l’aide de FTP. Toutefois, vous devez tout d’abord les informations de connexion de base de données de hello tooupdate dans l’application hello. À l’aide des informations de connexion de base de données hello obtenues précédemment (Bonjour **les informations de connexion MySQL d’obtenir et FTP** section), hello de mise à jour après les informations contenues dans **les deux** hello `createdatabase.php` et `index.php` fichiers par hello les valeurs appropriées :

    // DB connection info
    $host = "value of Data Source";
    $user = "value of User Id";
    $pwd = "value of Password";
    $db = "value of Database";

Maintenant vous êtes prêt à toopublish votre application à l’aide de FTP.

1. Ouvrez le client FTP de votre choix.
2. Entrez hello *partie nom d’hôte* de hello `publishUrl` attribut ci-dessus dans votre client FTP.
3. Entrez hello `userName` et `userPWD` attributs que vous avez noté ci-dessus sans modification dans votre client FTP.
4. Établissez une connexion.

Après que vous être connecté vous être en mesure de tooupload et télécharger des fichiers en fonction des besoins. Assurez-vous que vous téléchargez un répertoire racine des fichiers toohello, c'est-à-dire `/site/wwwroot`.

Après avoir téléchargé les deux `index.php` et `createtable.php`, parcourir trop**http://[site name].azurewebsites.net/createtable.php** toocreate hello MySQL de table pour l’application hello, puis parcourir trop**http://[site nom ].azurewebsites.net/index.php** toobegin à l’aide d’application hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).

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

