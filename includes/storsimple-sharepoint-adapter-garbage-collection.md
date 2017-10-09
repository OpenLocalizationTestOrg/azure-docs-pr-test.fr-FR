<!--author=SharS last changed: 9/17/15-->

<span data-ttu-id="a311d-101">Dans cette procédure, vous allez :</span><span class="sxs-lookup"><span data-stu-id="a311d-101">In this procedure, you will:</span></span>

1. <span data-ttu-id="a311d-102">[Préparer le fichier exécutable chargé de maintenance de hello toorun](#to-prepare-to-run-the-maintainer) .</span><span class="sxs-lookup"><span data-stu-id="a311d-102">[Prepare toorun hello Maintainer executable](#to-prepare-to-run-the-maintainer) .</span></span>
2. <span data-ttu-id="a311d-103">[Préparer la base de données de contenu hello et la Corbeille pour la suppression immédiate d’objets BLOB orphelins](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span><span class="sxs-lookup"><span data-stu-id="a311d-103">[Prepare hello content database and Recycle Bin for immediate deletion of orphaned BLOBs](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).</span></span>
3. <span data-ttu-id="a311d-104">[exécuter Maintainer.exe](#to-run-the-maintainer);</span><span class="sxs-lookup"><span data-stu-id="a311d-104">[Run Maintainer.exe](#to-run-the-maintainer).</span></span>
4. <span data-ttu-id="a311d-105">[Rétablir la base de données de contenu hello et les paramètres de la Corbeille](#to-revert-the-content-database-and-recycle-bin-settings).</span><span class="sxs-lookup"><span data-stu-id="a311d-105">[Revert hello content database and Recycle Bin settings](#to-revert-the-content-database-and-recycle-bin-settings).</span></span>

#### <a name="tooprepare-toorun-hello-maintainer"></a><span data-ttu-id="a311d-106">tooprepare toorun hello chargé de maintenance</span><span class="sxs-lookup"><span data-stu-id="a311d-106">tooprepare toorun hello Maintainer</span></span>
1. <span data-ttu-id="a311d-107">Sur hello serveur Web frontal, ouvrez hello SharePoint 2013 Management Shell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a311d-107">On hello Web front-end server, open hello SharePoint 2013 Management Shell as an administrator.</span></span>
2. <span data-ttu-id="a311d-108">Exploration du dossier de toohello *lecteur de démarrage*: \Program Files\Microsoft 10.50\Maintainer de stockage d’objets Blob distants SQL\.</span><span class="sxs-lookup"><span data-stu-id="a311d-108">Navigate toohello folder *boot drive*:\Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\.</span></span>
3. <span data-ttu-id="a311d-109">Renommer **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** trop**web.config**.</span><span class="sxs-lookup"><span data-stu-id="a311d-109">Rename **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** too**web.config**.</span></span>
4. <span data-ttu-id="a311d-110">Utilisez `aspnet_regiis -pdf connectionStrings` fichier web.config de hello toodecrypt.</span><span class="sxs-lookup"><span data-stu-id="a311d-110">Use `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config file.</span></span>
5. <span data-ttu-id="a311d-111">Dans fichier hello web.config déchiffrée, hello `connectionStrings` nœud, ajoutez la chaîne de connexion hello pour votre instance SQL server et hello du nom de la base de données de contenu.</span><span class="sxs-lookup"><span data-stu-id="a311d-111">In hello decrypted web.config file, under hello `connectionStrings` node, add hello connection string for your SQL server instance and hello content database name.</span></span> <span data-ttu-id="a311d-112">Consultez hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a311d-112">See hello following example.</span></span>
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. <span data-ttu-id="a311d-113">Utilisez `aspnet_regiis –pef connectionStrings` toore-chiffrer le fichier web.config de hello.</span><span class="sxs-lookup"><span data-stu-id="a311d-113">Use `aspnet_regiis –pef connectionStrings` toore-encrypt hello web.config file.</span></span> 
7. <span data-ttu-id="a311d-114">Renommez tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config de web.config.</span><span class="sxs-lookup"><span data-stu-id="a311d-114">Rename web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config.</span></span> 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a><span data-ttu-id="a311d-115">base de données tooprepare hello et la Corbeille tooimmediately suppriment des objets BLOB orphelins</span><span class="sxs-lookup"><span data-stu-id="a311d-115">tooprepare hello content database and Recycle Bin tooimmediately delete orphaned BLOBs</span></span>
1. <span data-ttu-id="a311d-116">Sur hello SQL Server, dans SQL Management Studio, exécutez hello des requêtes de mise à jour pour la base de données contenu hello cible suivantes :</span><span class="sxs-lookup"><span data-stu-id="a311d-116">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span> 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. <span data-ttu-id="a311d-117">Sur hello serveur web frontal, sous **Administration centrale**, modifier hello **les paramètres généraux de l’Application Web** pour hello souhaité disable hello la Corbeille de contenu de la base de données tootemporarily.</span><span class="sxs-lookup"><span data-stu-id="a311d-117">On hello web front-end server, under **Central Administration**, edit hello **Web Application General Settings** for hello desired content database tootemporarily disable hello Recycle Bin.</span></span> <span data-ttu-id="a311d-118">Cette action va également hello vide la Corbeille pour toutes les collections de sites connexes.</span><span class="sxs-lookup"><span data-stu-id="a311d-118">This action will also empty hello Recycle Bin for any related site collections.</span></span> <span data-ttu-id="a311d-119">toodo, cliquez sur **Administration centrale** -> **gestion des applications** -> **les Applications Web (gérer les applications web)**  ->  **SharePoint - 80** -> **les paramètres généraux de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="a311d-119">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="a311d-120">Ensemble hello **état de la Corbeille** trop**OFF**.</span><span class="sxs-lookup"><span data-stu-id="a311d-120">Set hello **Recycle Bin Status** too**OFF**.</span></span>
   
    ![Paramètres généraux de l'application Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a><span data-ttu-id="a311d-122">toorun hello chargé de maintenance</span><span class="sxs-lookup"><span data-stu-id="a311d-122">toorun hello Maintainer</span></span>
* <span data-ttu-id="a311d-123">Sur le serveur frontal de web hello, Bonjour SharePoint 2013 Management Shell, exécutez hello chargé de maintenance comme suit :</span><span class="sxs-lookup"><span data-stu-id="a311d-123">On hello web front-end server, in hello SharePoint 2013 Management Shell, run hello Maintainer as follows:</span></span>
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > <span data-ttu-id="a311d-124">Hello uniquement `GarbageCollection` est prise en charge pour StorSimple pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="a311d-124">Only hello `GarbageCollection` operation is supported for StorSimple at this time.</span></span> <span data-ttu-id="a311d-125">Notez également que les paramètres de hello émises pour Microsoft.Data.SqlRemoteBlobs.Maintainer.exe respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="a311d-125">Also note that hello parameters issued for Microsoft.Data.SqlRemoteBlobs.Maintainer.exe are case sensitive.</span></span> 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a><span data-ttu-id="a311d-126">base de données contenu toorevert hello et les paramètres de la Corbeille</span><span class="sxs-lookup"><span data-stu-id="a311d-126">toorevert hello content database and Recycle Bin settings</span></span>
1. <span data-ttu-id="a311d-127">Sur hello SQL Server, dans SQL Management Studio, exécutez hello des requêtes de mise à jour pour la base de données contenu hello cible suivantes :</span><span class="sxs-lookup"><span data-stu-id="a311d-127">On hello SQL Server, in SQL Management Studio, run hello following update queries for hello target content database:</span></span>
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. <span data-ttu-id="a311d-128">Sur le serveur frontal de web hello, dans **Administration centrale**, modifier hello **les paramètres généraux de l’Application Web** pour hello souhaité hello toore-enable de contenu de la base de données la Corbeille.</span><span class="sxs-lookup"><span data-stu-id="a311d-128">On hello web front-end server, in **Central Administration**, edit hello **Web Application General Settings** for hello desired content database toore-enable hello Recycle Bin.</span></span> <span data-ttu-id="a311d-129">toodo, cliquez sur **Administration centrale** -> **gestion des applications** -> **les Applications Web (gérer les applications web)**  ->  **SharePoint - 80** -> **les paramètres généraux de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="a311d-129">toodo this, click **Central Administration** -> **Application Management** -> **Web Applications (Manage web applications)** -> **SharePoint - 80** -> **General Application Settings**.</span></span> <span data-ttu-id="a311d-130">Définir hello état de la Corbeille trop**ON**.</span><span class="sxs-lookup"><span data-stu-id="a311d-130">Set hello Recycle Bin Status too**ON**.</span></span>

