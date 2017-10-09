Suivez ces étapes tooinstall et exécutez MongoDB sur une machine virtuelle exécutant Windows Server.

> [!IMPORTANT]
> Les fonctionnalités de sécurité MongoDB, comme l’authentification et la liaison d’adresse IP, ne sont pas activées par défaut. Les fonctionnalités de sécurité doivent être activées avant de déployer l’environnement de production tooa MongoDB.  Pour en savoir plus, consultez la page [Sécurité et authentification](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Une fois que vous vous êtes connecté l’ordinateur virtuel de toohello à l’aide du Bureau à distance, ouvrez Internet Explorer à partir de hello **Démarrer** menu sur l’ordinateur virtuel de hello.
2. Sélectionnez hello **outils** bouton dans le coin supérieur droit de hello.  Dans **Options Internet**, sélectionnez hello **sécurité** onglet et sélectionnez hello **Sites de confiance** icône et enfin cliquez sur hello **Sites** bouton. Ajouter *https://\*. mongodb.org* toohello la liste des sites de confiance.
3. Accédez trop[téléchargements - MongoDB](https://www.mongodb.com/download-center#community).
4. Recherche hello **version Stable actuelle** de **serveur de la Communauté**, sélectionnez hello dernières **64 bits** version dans la colonne de Windows hello. Téléchargez, puis exécutez le programme d’installation MSI hello.
5. MongoDB est généralement installé sur C:\Program Files\MongoDB. Recherchez les Variables d’environnement sur le bureau de hello et ajouter une variable de chemin d’accès du fichiers binaires du chemin d’accès toohello hello MongoDB. Par exemple, vous constaterez les binaires hello à C:\Program Files\MongoDB\Server\3.4\bin sur votre ordinateur.
6. Créer des répertoires de journaux et de données MongoDB dans le disque de données hello (tel que le lecteur **F:**) vous avez créé dans les étapes précédentes de hello. À partir de **Démarrer**, sélectionnez **invite de commandes** tooopen une fenêtre d’invite de commandes.  Entrez :

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun hello base de données, exécutez :

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Tous les messages du journal sont suggéré toohello *F:\MongoLogs\mongolog.log* mongod.exe serveur démarre et pré-alloue des fichiers journaux de fichiers. Il peut prendre plusieurs minutes MongoDB toopreallocate les fichiers de journal hello et commence à écouter les connexions. invite de commandes Hello reste se concentrent sur cette tâche pendant l’exécution de votre instance de MongoDB.
8. toostart hello MongoDB interpréteur de commandes d’administration, ouvrez une autre fenêtre de commande à partir de **Démarrer** et hello du type suivant de commandes :

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    base de données Hello est créé par insert de hello.
9. Vous pouvez également installer mongod.exe en tant que service :

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Un service nommé « MongoDB » est installé et associé à la description « Mongo DB ». Hello `--logpath` option doit être toospecify utilisé un fichier journal, depuis hello service en cours d’exécution n’a aucun une sortie toodisplay de la fenêtre commande.  Hello `--logappend` option spécifie qu’un redémarrage du service de hello, le fichier journal existant de sortie tooappend toohello.  Hello `--dbpath` option spécifie l’emplacement de hello hello du répertoire de données. Pour plus d’informations sur les options de ligne de commande associées au service, consultez la page [Options de ligne de commande associées au service][MongoWindowsSvcOptions].

    service de hello toostart, exécutez la commande suivante :

        C:\> net start MongoDB
10. MongoDB est installé et en cours d’exécution, vous devez tooopen un port dans le pare-feu Windows, vous pouvez connecter à distance tooMongoDB.  À partir de hello **Démarrer** menu, sélectionnez **outils d’administration** , puis **pare-feu Windows avec fonctions avancées de sécurité**.
11. a) dans le volet gauche de hello, sélectionnez **règles de trafic entrant**.  Bonjour **Actions** volet hello à droite, sélectionnez **nouvelle règle...** .

    ![Pare-feu Windows][Image1]

    (b) dans hello **Assistant Nouvelle règle de trafic entrant**, sélectionnez **Port** puis cliquez sur **suivant**.

    ![Pare-feu Windows][Image2]

    c) Sélectionnez **TCP**, puis **Ports locaux spécifiques**.  Spécifiez un port de « 27017 » (port par défaut hello MongoDB écoute) et cliquez sur **suivant**.

    ![Pare-feu Windows][Image3]

    d) sélectionnez **autoriser la connexion hello** et cliquez sur **suivant**.

    ![Pare-feu Windows][Image4]

    e) Cliquez à nouveau sur **Suivant**.

    ![Pare-feu Windows][Image5]

    f) spécifiez un nom pour la règle de hello, tels que « MongoPort », puis cliquez sur **Terminer**.

    ![Pare-feu Windows][Image6]

12. Si vous n’avez pas configurer un point de terminaison pour MongoDB lorsque vous avez créé l’ordinateur virtuel de hello, vous pouvez le faire maintenant. Vous devez règle de pare-feu hello et hello point de terminaison toobe tooconnect en mesure de tooMongoDB à distance.

  Bonjour portail Azure, cliquez sur **Machines virtuelles (classiques)**, cliquez sur nom hello de votre nouvel ordinateur virtuel, puis cliquez sur **points de terminaison**.

    ![Points de terminaison][Image7]

13. Cliquez sur **Add**.

14. Ajouter un point de terminaison portant le nom « Mongo », protocole **TCP**, alors que les **Public** et **privé** ports jeu trop « 27017 ». L’ouverture de ce port permet de toobe MongoDB accédé à distance.

    ![Points de terminaison][Image9]

> [!NOTE]
> le port de Hello 27017 est le port par défaut de hello utilisé par MongoDB. Vous pouvez modifier ce port par défaut en spécifiant hello `--port` paramètre lors du démarrage du serveur de mongod.exe hello. Assurez-vous que toogive hello même numéro de port dans le pare-feu hello et hello du point de terminaison « Mongo » Bonjour précédant les instructions.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
