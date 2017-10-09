
1. <span data-ttu-id="64209-101">privilèges tooescalate, type :</span><span class="sxs-lookup"><span data-stu-id="64209-101">tooescalate privileges, type:</span></span>
   
        sudo -s
   
    <span data-ttu-id="64209-102">Saisissez votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="64209-102">Enter your password.</span></span>
2. <span data-ttu-id="64209-103">tooinstall MySQL Community Server edition, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-103">tooinstall MySQL Community Server edition, type:</span></span>
   
        zypper install mysql-community-server
   
    <span data-ttu-id="64209-104">Patientez lors du téléchargement et de l’installation de MySQL.</span><span class="sxs-lookup"><span data-stu-id="64209-104">Wait while MySQL downloads and installs.</span></span>
3. <span data-ttu-id="64209-105">tooset MySQL toostart démarrage hello système, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-105">tooset MySQL toostart when hello system boots, type:</span></span>
   
        insserv mysql
4. <span data-ttu-id="64209-106">Démarrer le démon de MySQL hello (mysqld) manuellement avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="64209-106">Start hello MySQL daemon (mysqld) manually with this command:</span></span>
   
        rcmysql start
   
    <span data-ttu-id="64209-107">état de hello toocheck Hello MySQL démon, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-107">toocheck hello status of hello MySQL daemon, type:</span></span>
   
        rcmysql status
   
    <span data-ttu-id="64209-108">toostop hello MySQL démon, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-108">toostop hello MySQL daemon, type:</span></span>
   
        rcmysql stop
   
   > [!IMPORTANT]
   > <span data-ttu-id="64209-109">Après l’installation, le mot de passe racine hello MySQL est vide par défaut.</span><span class="sxs-lookup"><span data-stu-id="64209-109">After installation, hello MySQL root password is empty by default.</span></span> <span data-ttu-id="64209-110">Il est recommandé d’exécuter le script **mysql\_secure\_installation** qui permet de sécuriser MySQL.</span><span class="sxs-lookup"><span data-stu-id="64209-110">We recommended that you run **mysql\_secure\_installation**, a script that helps secure MySQL.</span></span> <span data-ttu-id="64209-111">script de Hello vous invite de mot de passe racine toochange hello MySQL, supprimer des comptes d’utilisateurs anonymes, désactiver les connexions à distance racine, supprimez les bases de données de test et recharger la table de privilèges hello.</span><span class="sxs-lookup"><span data-stu-id="64209-111">hello script prompts you toochange hello MySQL root password, remove anonymous user accounts, disable remote root logins, remove test databases, and reload hello privileges table.</span></span> <span data-ttu-id="64209-112">Il est recommandé que vous répondez Oui les tooall de ces options et modifiez le mot de passe racine hello.</span><span class="sxs-lookup"><span data-stu-id="64209-112">We recommended that you answer yes tooall of these options and change hello root password.</span></span>
   > 
   > 
5. <span data-ttu-id="64209-113">Tapez ce script de hello toorun script d’installation MySQL :</span><span class="sxs-lookup"><span data-stu-id="64209-113">Type this toorun hello script MySQL installation script:</span></span>
   
        mysql_secure_installation
6. <span data-ttu-id="64209-114">Ouvrez une session dans tooMySQL :</span><span class="sxs-lookup"><span data-stu-id="64209-114">Log in tooMySQL:</span></span>
   
        mysql -u root -p
   
    <span data-ttu-id="64209-115">Entrez le mot de passe racine de MySQL hello (que vous avez modifié à l’étape précédente de hello) et vous verrez une invite de commandes où vous pouvez émettre toointeract d’instructions SQL avec la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="64209-115">Enter hello MySQL root password (which you changed in hello previous step) and you'll be presented with a prompt where you can issue SQL statements toointeract with hello database.</span></span>
7. <span data-ttu-id="64209-116">toocreate un nouvel utilisateur MySQL, exécutez hello suivante hello **mysql >** invite de commandes :</span><span class="sxs-lookup"><span data-stu-id="64209-116">toocreate a new MySQL user, run hello following at hello **mysql>** prompt:</span></span>
   
        CREATE USER 'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="64209-117">Notez que les points-virgules hello ( ;) à fin hello Hello lignes sont cruciaux pour la fin des commandes hello.</span><span class="sxs-lookup"><span data-stu-id="64209-117">Note, hello semi-colons (;) at hello end of hello lines are crucial for ending hello commands.</span></span>
8. <span data-ttu-id="64209-118">toocreate un hello de base de données et grant `mysqluser` autorisations utilisateur sur celui-ci, hello du problème suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="64209-118">toocreate a database and grant hello `mysqluser` user permissions on it, issue hello following commands:</span></span>
   
        CREATE DATABASE testdatabase;
        GRANT ALL ON testdatabase.* too'mysqluser'@'localhost' IDENTIFIED BY 'password';
   
    <span data-ttu-id="64209-119">Notez que les noms d’utilisateur de base de données et les mots de passe sont utilisés uniquement par les scripts de connexion de base de données toohello.</span><span class="sxs-lookup"><span data-stu-id="64209-119">Note that database user names and passwords are only used by scripts connecting toohello database.</span></span>  <span data-ttu-id="64209-120">Noms de compte d’utilisateur de base de données ne représentent pas nécessairement les comptes d’utilisateur réels sur le système de hello.</span><span class="sxs-lookup"><span data-stu-id="64209-120">Database user account names do not necessarily represent actual user accounts on hello system.</span></span>
9. <span data-ttu-id="64209-121">toolog dans à partir d’un autre ordinateur, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-121">toolog in from another computer, type:</span></span>
   
        GRANT ALL ON testdatabase.* too'mysqluser'@'<ip-address>' IDENTIFIED BY 'password';
   
    <span data-ttu-id="64209-122">où `ip-address` est l’adresse IP de hello d’ordinateur hello à partir de laquelle vous vous connecterez tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="64209-122">where `ip-address` is hello IP address of hello computer from which you will connect tooMySQL.</span></span>
10. <span data-ttu-id="64209-123">tooexit hello utilitaire d’administration de base de données MySQL, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-123">tooexit hello MySQL database administration utility, type:</span></span>
    
        quit

## <a name="add-an-endpoint"></a><span data-ttu-id="64209-124">Ajout d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="64209-124">Add an endpoint</span></span>
1. <span data-ttu-id="64209-125">Une fois que MySQL est installé, vous devez tooconfigure une tooaccess de point de terminaison MySQL à distance.</span><span class="sxs-lookup"><span data-stu-id="64209-125">After MySQL is installed, you'll need tooconfigure an endpoint tooaccess MySQL remotely.</span></span> <span data-ttu-id="64209-126">Connectez-vous à toohello [portail Azure classic][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="64209-126">Log in toohello [Azure  classic portal][AzurePortal].</span></span> <span data-ttu-id="64209-127">Cliquez sur **virtuels**, cliquez sur nom hello de votre nouvel ordinateur virtuel, puis cliquez sur **points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="64209-127">Click **Virtual Machines**, click hello name of your new virtual machine, and then click **Endpoints**.</span></span>
2. <span data-ttu-id="64209-128">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="64209-128">Click **Add** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="64209-129">Ajouter un point de terminaison nommé « MySQL » avec le protocole **TCP**, et **Public** et **privé** ports jeu trop « 3306 ».</span><span class="sxs-lookup"><span data-stu-id="64209-129">Add an endpoint named "MySQL" with protocol **TCP**, and **Public** and **Private** ports set too"3306".</span></span>
4. <span data-ttu-id="64209-130">tooremotely connecter toohello virtuels à partir de votre ordinateur, tapez :</span><span class="sxs-lookup"><span data-stu-id="64209-130">tooremotely connect toohello virtual machine from your computer, type:</span></span>
   
        mysql -u mysqluser -p -h <yourservicename>.cloudapp.net
   
    <span data-ttu-id="64209-131">Par exemple, à l’aide de la machine virtuelle de hello que nous avons créé dans ce didacticiel, tapez cette commande :</span><span class="sxs-lookup"><span data-stu-id="64209-131">For example, using hello virual machine we created in this tutorial, type this command:</span></span>
   
        mysql -u mysqluser -p -h testlinuxvm.cloudapp.net

[MySQLDocs]: http://dev.mysql.com/doc/
[AzurePortal]: http://manage.windowsazure.com

[Image9]: ./media/install-and-run-mysql-on-opensuse-vm/LinuxVmAddEndpointMySQL.png
