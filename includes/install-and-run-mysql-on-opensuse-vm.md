
1. privilèges tooescalate, type :
   
        sudo -s
   
    Saisissez votre mot de passe.
2. tooinstall MySQL Community Server edition, tapez :
   
        zypper install mysql-community-server
   
    Patientez lors du téléchargement et de l’installation de MySQL.
3. tooset MySQL toostart démarrage hello système, tapez :
   
        insserv mysql
4. Démarrer le démon de MySQL hello (mysqld) manuellement avec cette commande :
   
        rcmysql start
   
    état de hello toocheck Hello MySQL démon, tapez :
   
        rcmysql status
   
    toostop hello MySQL démon, tapez :
   
        rcmysql stop
   
   > [!IMPORTANT]
   > Après l’installation, le mot de passe racine hello MySQL est vide par défaut. Il est recommandé d’exécuter le script **mysql\_secure\_installation** qui permet de sécuriser MySQL. script de Hello vous invite de mot de passe racine toochange hello MySQL, supprimer des comptes d’utilisateurs anonymes, désactiver les connexions à distance racine, supprimez les bases de données de test et recharger la table de privilèges hello. Il est recommandé que vous répondez Oui les tooall de ces options et modifiez le mot de passe racine hello.
   > 
   > 
5. Tapez ce script de hello toorun script d’installation MySQL :
   
        mysql_secure_installation
6. Ouvrez une session dans tooMySQL :
   
        mysql -u root -p
   
    Entrez le mot de passe racine de MySQL hello (que vous avez modifié à l’étape précédente de hello) et vous verrez une invite de commandes où vous pouvez émettre toointeract d’instructions SQL avec la base de données hello.
7. toocreate un nouvel utilisateur MySQL, exécutez hello suivante hello **mysql >** invite de commandes :
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Notez que les points-virgules hello ( ;) à fin hello Hello lignes sont cruciaux pour la fin des commandes hello.
8. toocreate un hello de base de données et grant `mysqluser` autorisations utilisateur sur celui-ci, hello du problème suivant de commandes :
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    Notez que les noms d’utilisateur de base de données et les mots de passe sont utilisés uniquement par les scripts de connexion de base de données toohello.  Noms de compte d’utilisateur de base de données ne représentent pas nécessairement les comptes d’utilisateur réels sur le système de hello.
9. toolog dans à partir d’un autre ordinateur, tapez :
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    où `ip-address` est l’adresse IP de hello d’ordinateur hello à partir de laquelle vous vous connecterez tooMySQL.
10. tooexit hello utilitaire d’administration de base de données MySQL, tapez :
    
        quit

## <a name="add-an-endpoint"></a>Ajout d’un point de terminaison
1. Une fois que MySQL est installé, vous devez tooconfigure une tooaccess de point de terminaison MySQL à distance. Connectez-vous à toohello [portail Azure classic][AzurePortal]. Cliquez sur **virtuels**, cliquez sur nom hello de votre nouvel ordinateur virtuel, puis cliquez sur **points de terminaison**.
2. Cliquez sur **ajouter** bas hello de page de hello.
3. Ajouter un point de terminaison nommé « MySQL » avec le protocole **TCP**, et **Public** et **privé** ports jeu trop « 3306 ».
4. tooremotely connecter toohello virtuels à partir de votre ordinateur, tapez :
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    Par exemple, à l’aide de la machine virtuelle de hello que nous avons créé dans ce didacticiel, tapez cette commande :
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
