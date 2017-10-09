<span data-ttu-id="4f6fc-101">Suivez ces étapes tooinstall et exécutez MongoDB sur une machine virtuelle exécutant Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-101">Follow these steps tooinstall and run MongoDB on a virtual machine running Windows Server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f6fc-102">Les fonctionnalités de sécurité MongoDB, comme l’authentification et la liaison d’adresse IP, ne sont pas activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-102">MongoDB security features, such as authentication and IP address binding, are not enabled by default.</span></span> <span data-ttu-id="4f6fc-103">Les fonctionnalités de sécurité doivent être activées avant de déployer l’environnement de production tooa MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-103">Security features should be enabled before deploying MongoDB tooa production environment.</span></span>  <span data-ttu-id="4f6fc-104">Pour en savoir plus, consultez la page [Sécurité et authentification](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span><span class="sxs-lookup"><span data-stu-id="4f6fc-104">For more information, see [Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication).</span></span>
>
>

1. <span data-ttu-id="4f6fc-105">Une fois que vous vous êtes connecté l’ordinateur virtuel de toohello à l’aide du Bureau à distance, ouvrez Internet Explorer à partir de hello **Démarrer** menu sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-105">After you've connected toohello virtual machine using Remote Desktop, open Internet Explorer from hello **Start** menu on hello virtual machine.</span></span>
2. <span data-ttu-id="4f6fc-106">Sélectionnez hello **outils** bouton dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-106">Select hello **Tools** button in hello upper right corner.</span></span>  <span data-ttu-id="4f6fc-107">Dans **Options Internet**, sélectionnez hello **sécurité** onglet et sélectionnez hello **Sites de confiance** icône et enfin cliquez sur hello **Sites** bouton.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-107">In **Internet Options**, select hello **Security** tab, and then select hello **Trusted Sites** icon, and finally click hello **Sites** button.</span></span> <span data-ttu-id="4f6fc-108">Ajouter *https://\*. mongodb.org* toohello la liste des sites de confiance.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-108">Add *https://\*.mongodb.org* toohello list of trusted sites.</span></span>
3. <span data-ttu-id="4f6fc-109">Accédez trop[téléchargements - MongoDB](https://www.mongodb.com/download-center#community).</span><span class="sxs-lookup"><span data-stu-id="4f6fc-109">Go too[Downloads - MongoDB](https://www.mongodb.com/download-center#community).</span></span>
4. <span data-ttu-id="4f6fc-110">Recherche hello **version Stable actuelle** de **serveur de la Communauté**, sélectionnez hello dernières **64 bits** version dans la colonne de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-110">Find hello **Current Stable Release** of **Community Server**, select hello latest **64-bit** version in hello Windows column.</span></span> <span data-ttu-id="4f6fc-111">Téléchargez, puis exécutez le programme d’installation MSI hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-111">Download, then run hello MSI installer.</span></span>
5. <span data-ttu-id="4f6fc-112">MongoDB est généralement installé sur C:\Program Files\MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-112">MongoDB is typically installed in C:\Program Files\MongoDB.</span></span> <span data-ttu-id="4f6fc-113">Recherchez les Variables d’environnement sur le bureau de hello et ajouter une variable de chemin d’accès du fichiers binaires du chemin d’accès toohello hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-113">Search for Environment Variables on hello desktop and add hello MongoDB binaries path toohello PATH variable.</span></span> <span data-ttu-id="4f6fc-114">Par exemple, vous constaterez les binaires hello à C:\Program Files\MongoDB\Server\3.4\bin sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-114">For example, you might find hello binaries at C:\Program Files\MongoDB\Server\3.4\bin on your machine.</span></span>
6. <span data-ttu-id="4f6fc-115">Créer des répertoires de journaux et de données MongoDB dans le disque de données hello (tel que le lecteur **F:**) vous avez créé dans les étapes précédentes de hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-115">Create MongoDB data and log directories in hello data disk (such as drive **F:**) you created in hello preceding steps.</span></span> <span data-ttu-id="4f6fc-116">À partir de **Démarrer**, sélectionnez **invite de commandes** tooopen une fenêtre d’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-116">From **Start**, select **Command Prompt** tooopen a command prompt window.</span></span>  <span data-ttu-id="4f6fc-117">Entrez :</span><span class="sxs-lookup"><span data-stu-id="4f6fc-117">Type:</span></span>

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. <span data-ttu-id="4f6fc-118">toorun hello base de données, exécutez :</span><span class="sxs-lookup"><span data-stu-id="4f6fc-118">toorun hello database, run:</span></span>

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    <span data-ttu-id="4f6fc-119">Tous les messages du journal sont suggéré toohello *F:\MongoLogs\mongolog.log* mongod.exe serveur démarre et pré-alloue des fichiers journaux de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-119">All log messages are directed toohello *F:\MongoLogs\mongolog.log* file as mongod.exe server starts and preallocates journal files.</span></span> <span data-ttu-id="4f6fc-120">Il peut prendre plusieurs minutes MongoDB toopreallocate les fichiers de journal hello et commence à écouter les connexions.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-120">It may take several minutes for MongoDB toopreallocate hello journal files and start listening for connections.</span></span> <span data-ttu-id="4f6fc-121">invite de commandes Hello reste se concentrent sur cette tâche pendant l’exécution de votre instance de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-121">hello command prompt stays focused on this task while your MongoDB instance is running.</span></span>
8. <span data-ttu-id="4f6fc-122">toostart hello MongoDB interpréteur de commandes d’administration, ouvrez une autre fenêtre de commande à partir de **Démarrer** et hello du type suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="4f6fc-122">toostart hello MongoDB administrative shell, open another command window from **Start** and type hello following commands:</span></span>

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

    <span data-ttu-id="4f6fc-123">base de données Hello est créé par insert de hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-123">hello database is created by hello insert.</span></span>
9. <span data-ttu-id="4f6fc-124">Vous pouvez également installer mongod.exe en tant que service :</span><span class="sxs-lookup"><span data-stu-id="4f6fc-124">Alternatively, you can install mongod.exe as a service:</span></span>

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    <span data-ttu-id="4f6fc-125">Un service nommé « MongoDB » est installé et associé à la description « Mongo DB ».</span><span class="sxs-lookup"><span data-stu-id="4f6fc-125">A service is installed named MongoDB with a description of "Mongo DB".</span></span> <span data-ttu-id="4f6fc-126">Hello `--logpath` option doit être toospecify utilisé un fichier journal, depuis hello service en cours d’exécution n’a aucun une sortie toodisplay de la fenêtre commande.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-126">hello `--logpath` option must be used toospecify a log file, since hello running service does not have a command window toodisplay output.</span></span>  <span data-ttu-id="4f6fc-127">Hello `--logappend` option spécifie qu’un redémarrage du service de hello, le fichier journal existant de sortie tooappend toohello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-127">hello `--logappend` option specifies that a restart of hello service causes output tooappend toohello existing log file.</span></span>  <span data-ttu-id="4f6fc-128">Hello `--dbpath` option spécifie l’emplacement de hello hello du répertoire de données.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-128">hello `--dbpath` option specifies hello location of hello data directory.</span></span> <span data-ttu-id="4f6fc-129">Pour plus d’informations sur les options de ligne de commande associées au service, consultez la page [Options de ligne de commande associées au service][MongoWindowsSvcOptions].</span><span class="sxs-lookup"><span data-stu-id="4f6fc-129">For more service-related command-line options, see [Service-related command-line options][MongoWindowsSvcOptions].</span></span>

    <span data-ttu-id="4f6fc-130">service de hello toostart, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4f6fc-130">toostart hello service, run this command:</span></span>

        C:\> net start MongoDB
10. <span data-ttu-id="4f6fc-131">MongoDB est installé et en cours d’exécution, vous devez tooopen un port dans le pare-feu Windows, vous pouvez connecter à distance tooMongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-131">Now that MongoDB is installed and running, you need tooopen a port in Windows Firewall so you can remotely connect tooMongoDB.</span></span>  <span data-ttu-id="4f6fc-132">À partir de hello **Démarrer** menu, sélectionnez **outils d’administration** , puis **pare-feu Windows avec fonctions avancées de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-132">From hello **Start** menu, select **Administrative Tools** and then **Windows Firewall with Advanced Security**.</span></span>
11. <span data-ttu-id="4f6fc-133">a) dans le volet gauche de hello, sélectionnez **règles de trafic entrant**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-133">a) In hello left pane, select **Inbound Rules**.</span></span>  <span data-ttu-id="4f6fc-134">Bonjour **Actions** volet hello à droite, sélectionnez **nouvelle règle...** .</span><span class="sxs-lookup"><span data-stu-id="4f6fc-134">In hello **Actions** pane on hello right, select **New Rule...**.</span></span>

    ![Pare-feu Windows][Image1]

    <span data-ttu-id="4f6fc-136">(b) dans hello **Assistant Nouvelle règle de trafic entrant**, sélectionnez **Port** puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-136">b) In hello **New Inbound Rule Wizard**, select **Port** and then click **Next**.</span></span>

    ![Pare-feu Windows][Image2]

    <span data-ttu-id="4f6fc-138">c) Sélectionnez **TCP**, puis **Ports locaux spécifiques**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-138">c) Select **TCP** and then **Specific local ports**.</span></span>  <span data-ttu-id="4f6fc-139">Spécifiez un port de « 27017 » (port par défaut hello MongoDB écoute) et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-139">Specify a port of "27017" (hello default port MongoDB listens on) and click **Next**.</span></span>

    ![Pare-feu Windows][Image3]

    <span data-ttu-id="4f6fc-141">d) sélectionnez **autoriser la connexion hello** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-141">d) Select **Allow hello connection** and click **Next**.</span></span>

    ![Pare-feu Windows][Image4]

    <span data-ttu-id="4f6fc-143">e) Cliquez à nouveau sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-143">e) Click **Next** again.</span></span>

    ![Pare-feu Windows][Image5]

    <span data-ttu-id="4f6fc-145">f) spécifiez un nom pour la règle de hello, tels que « MongoPort », puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-145">f) Specify a name for hello rule, such as "MongoPort", and click **Finish**.</span></span>

    ![Pare-feu Windows][Image6]

12. <span data-ttu-id="4f6fc-147">Si vous n’avez pas configurer un point de terminaison pour MongoDB lorsque vous avez créé l’ordinateur virtuel de hello, vous pouvez le faire maintenant.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-147">If you didn't configure an endpoint for MongoDB when you created hello virtual machine, you can do it now.</span></span> <span data-ttu-id="4f6fc-148">Vous devez règle de pare-feu hello et hello point de terminaison toobe tooconnect en mesure de tooMongoDB à distance.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-148">You need both hello firewall rule and hello endpoint toobe able tooconnect tooMongoDB remotely.</span></span>

  <span data-ttu-id="4f6fc-149">Bonjour portail Azure, cliquez sur **Machines virtuelles (classiques)**, cliquez sur nom hello de votre nouvel ordinateur virtuel, puis cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-149">In hello Azure portal, click **Virtual Machines (classic)**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>

    ![Points de terminaison][Image7]

13. <span data-ttu-id="4f6fc-151">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-151">Click **Add**.</span></span>

14. <span data-ttu-id="4f6fc-152">Ajouter un point de terminaison portant le nom « Mongo », protocole **TCP**, alors que les **Public** et **privé** ports jeu trop « 27017 ».</span><span class="sxs-lookup"><span data-stu-id="4f6fc-152">Add an endpoint with name "Mongo", protocol **TCP**, and both **Public** and **Private** ports set too"27017".</span></span> <span data-ttu-id="4f6fc-153">L’ouverture de ce port permet de toobe MongoDB accédé à distance.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-153">Opening this port allows MongoDB toobe accessed remotely.</span></span>

    ![Points de terminaison][Image9]

> [!NOTE]
> <span data-ttu-id="4f6fc-155">le port de Hello 27017 est le port par défaut de hello utilisé par MongoDB.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-155">hello port 27017 is hello default port used by MongoDB.</span></span> <span data-ttu-id="4f6fc-156">Vous pouvez modifier ce port par défaut en spécifiant hello `--port` paramètre lors du démarrage du serveur de mongod.exe hello.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-156">You can change this default port by specifying hello `--port` parameter when starting hello mongod.exe server.</span></span> <span data-ttu-id="4f6fc-157">Assurez-vous que toogive hello même numéro de port dans le pare-feu hello et hello du point de terminaison « Mongo » Bonjour précédant les instructions.</span><span class="sxs-lookup"><span data-stu-id="4f6fc-157">Make sure toogive hello same port number in hello firewall and hello "Mongo" endpoint in hello preceding instructions.</span></span>
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
