<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> <span data-ttu-id="e1171-101">Quand vous apportez des modifications toohello l’adaptateur StorSimple pour la configuration de SharePoint RBS, vous devez être connecté avec un compte d’utilisateur auquel appartient le groupe Admins du domaine de toohello.</span><span class="sxs-lookup"><span data-stu-id="e1171-101">When making changes toohello StorSimple Adapter for SharePoint RBS configuration, you must be logged on with a user account that belongs toohello Domain Admins group.</span></span> <span data-ttu-id="e1171-102">En outre, vous devez accéder page de configuration hello à partir d’un navigateur en cours d’exécution sur le même hôte que l’Administration centrale de hello.</span><span class="sxs-lookup"><span data-stu-id="e1171-102">Additionally, you must access hello configuration page from a browser running on hello same host as Central Administration.</span></span>
> 
> 

#### <a name="tooconfigure-rbs"></a><span data-ttu-id="e1171-103">tooconfigure RBS</span><span class="sxs-lookup"><span data-stu-id="e1171-103">tooconfigure RBS</span></span>
1. <span data-ttu-id="e1171-104">Ouvrez la page d’Administration centrale de SharePoint hello et parcourir trop**paramètres système**.</span><span class="sxs-lookup"><span data-stu-id="e1171-104">Open hello SharePoint Central Administration page, and browse too**System Settings**.</span></span> 
2. <span data-ttu-id="e1171-105">Bonjour **Azure StorSimple** , cliquez sur **configurer l’adaptateur StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="e1171-105">In hello **Azure StorSimple** section, click **Configure StorSimple Adapter**.</span></span>
   
    ![Configurer hello l’adaptateur StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. <span data-ttu-id="e1171-107">Sur hello **configurer l’adaptateur StorSimple** page :</span><span class="sxs-lookup"><span data-stu-id="e1171-107">On hello **Configure StorSimple Adapter** page:</span></span>
   
   1. <span data-ttu-id="e1171-108">Vérifiez que hello **activer le chemin de l’édition** case à cocher est activée.</span><span class="sxs-lookup"><span data-stu-id="e1171-108">Make sure that hello **Enable editing path** check box is selected.</span></span>
   2. <span data-ttu-id="e1171-109">Dans la zone de texte hello, tapez le chemin de Universal Naming Convention (UNC) de hello du magasin d’objets BLOB hello.</span><span class="sxs-lookup"><span data-stu-id="e1171-109">In hello text box, type hello Universal Naming Convention (UNC) path of hello BLOB store.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e1171-110">volume du magasin d’objets BLOB Hello doit être hébergé sur un volume iSCSI configuré sur l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="e1171-110">hello BLOB store volume must be hosted on an iSCSI volume configured on hello StorSimple device.</span></span>

   3. <span data-ttu-id="e1171-111">Cliquez sur hello **activer** situé sous chacune des bases de données contenu hello que vous souhaitez tooconfigure pour le stockage étendu.</span><span class="sxs-lookup"><span data-stu-id="e1171-111">Click hello **Enable** button below each of hello content databases that you want tooconfigure for remote storage.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e1171-112">magasin d’objets BLOB Hello doit être partagé par tous les serveurs web frontaux (WFE) et le compte d’utilisateur hello est configuré pour la batterie de serveurs SharePoint hello doit avoir accès toohello partagé.</span><span class="sxs-lookup"><span data-stu-id="e1171-112">hello BLOB store must be shared and reachable by all web front-end (WFE) servers, and hello user account that is configured for hello SharePoint server farm must have access toohello share.</span></span>
      
      ![Activer le fournisseur RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      <span data-ttu-id="e1171-114">Lorsque vous activez ou désactivez RBS, vous verrez également hello message suivant.</span><span class="sxs-lookup"><span data-stu-id="e1171-114">When you enable or disable RBS, you will also see hello following message.</span></span>
      
      ![Désactivation activation Configuration de l’adaptateur StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. <span data-ttu-id="e1171-116">Cliquez sur hello **mise à jour** configuration hello tooapply du bouton.</span><span class="sxs-lookup"><span data-stu-id="e1171-116">Click hello **Update** button tooapply hello configuration.</span></span> <span data-ttu-id="e1171-117">Lorsque vous cliquez sur hello **mise à jour** bouton, hello état RBS de la configuration sera mise à jour sur tous les serveurs Web frontaux et ensemble de la batterie hello sera activée pour RBS.</span><span class="sxs-lookup"><span data-stu-id="e1171-117">When you click hello **Update** button, hello RBS configuration status will be updated on all WFE servers, and hello entire farm will be RBS-enabled.</span></span> <span data-ttu-id="e1171-118">Hello message suivant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="e1171-118">hello following message appears.</span></span>
      
      ![Message de configuration de l’adaptateur](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > <span data-ttu-id="e1171-120">Si vous configurez RBS pour une batterie de serveurs SharePoint avec un très grand nombre de bases de données (plus de 200), la page web de l’Administration centrale de SharePoint hello peut expirer. Si cela se produit, actualisez la page de hello.</span><span class="sxs-lookup"><span data-stu-id="e1171-120">If you are configuring RBS for a SharePoint farm with a very large number of databases (greater than 200), hello SharePoint Central Administration web page might time out. If that occurs, refresh hello page.</span></span> <span data-ttu-id="e1171-121">Cela n’affecte pas le processus de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="e1171-121">This does not affect hello configuration process.</span></span>

4. <span data-ttu-id="e1171-122">Vérifier la configuration de hello :</span><span class="sxs-lookup"><span data-stu-id="e1171-122">Verify hello configuration:</span></span>
   
   1. <span data-ttu-id="e1171-123">Ouvrez une session sur le site Web d’Administration centrale de SharePoint toohello et parcourir toohello **configurer l’adaptateur StorSimple** page.</span><span class="sxs-lookup"><span data-stu-id="e1171-123">Log on toohello SharePoint Central Administration website, and browse toohello **Configure StorSimple Adapter** page.</span></span>
   2. <span data-ttu-id="e1171-124">Vérifiez hello configuration détails toomake assurer qu’ils correspondent aux paramètres hello que vous avez entré.</span><span class="sxs-lookup"><span data-stu-id="e1171-124">Check hello configuration details toomake sure that they match hello settings that you entered.</span></span> 
5. <span data-ttu-id="e1171-125">Vérifiez que RBS fonctionne correctement :</span><span class="sxs-lookup"><span data-stu-id="e1171-125">Verify that RBS works correctly:</span></span>
   
   1. <span data-ttu-id="e1171-126">Télécharger un document tooSharePoint.</span><span class="sxs-lookup"><span data-stu-id="e1171-126">Upload a document tooSharePoint.</span></span> 
   2. <span data-ttu-id="e1171-127">Parcourir le chemin d’accès UNC toohello que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="e1171-127">Browse toohello UNC path that you configured.</span></span> <span data-ttu-id="e1171-128">Assurez-vous que la structure de répertoire RBS hello a été créé et qu’il contient l’objet de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e1171-128">Make sure that hello RBS directory structure was created and that it contains hello uploaded object.</span></span>
6. <span data-ttu-id="e1171-129">(Facultatif) Vous pouvez utiliser hello Microsoft RBS `Migrate()` inclus avec SharePoint toomigrate BLOB contenu toohello StorSimple unité de l’applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1171-129">(Optional) You can use hello Microsoft RBS `Migrate()` PowerShell cmdlet included with SharePoint toomigrate existing BLOB content toohello StorSimple device.</span></span> <span data-ttu-id="e1171-130">Pour plus d’informations, consultez [migrer le contenu dans ou hors de RBS dans SharePoint 2013] [ 6] ou [migrer le contenu dans ou hors de RBS (SharePoint Foundation 2010)] [7].</span><span class="sxs-lookup"><span data-stu-id="e1171-130">For more information, see [Migrate content into or out of RBS in SharePoint 2013][6] or [Migrate content into or out of RBS (SharePoint Foundation 2010)][7].</span></span>
7. <span data-ttu-id="e1171-131">(Facultatif) Sur les installations de test, vous pouvez vérifier que hello BLOB ont été déplacés en dehors de la base de données de contenu hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1171-131">(Optional) On test installations, you can verify that hello BLOBs were moved out of hello content database as follows:</span></span> 
   
   1. <span data-ttu-id="e1171-132">Démarrez SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e1171-132">Start SQL Management Studio.</span></span>
   2. <span data-ttu-id="e1171-133">Exécutez la requête ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql de hello, comme suit.</span><span class="sxs-lookup"><span data-stu-id="e1171-133">Run hello ListBlobsInDB_2010.sql or ListBlobsInDB_2013.sql query, as follows.</span></span>
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      <span data-ttu-id="e1171-134">Si RBS est correctement configuré, une valeur NULL doit apparaître dans la colonne de SizeOfContentInDB hello pour tout objet qui a été téléchargé et effectivement externalisé avec RBS.</span><span class="sxs-lookup"><span data-stu-id="e1171-134">If RBS was configured correctly, a NULL value should appear in hello SizeOfContentInDB column for any object that was uploaded and successfully externalized with RBS.</span></span>
8. <span data-ttu-id="e1171-135">(Facultatif) Après avoir configuré RBS et déplacer tous les objets BLOB de toohello contenu appareil StorSimple, vous pouvez déplacer l’appareil de toohello hello contenu de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e1171-135">(Optional) After you configure RBS and move all BLOB content toohello StorSimple device, you can move hello content database toohello device.</span></span> <span data-ttu-id="e1171-136">Si vous choisissez la base de données de contenu de hello toomove, nous vous recommandons de configurer stockage de base de données de contenu hello sur périphérique hello comme volume principal.</span><span class="sxs-lookup"><span data-stu-id="e1171-136">If you choose toomove hello content database, we recommend that you configure hello content database storage on hello device as a primary volume.</span></span> <span data-ttu-id="e1171-137">Ensuite, utilisez établie SQL Server de meilleures pratiques pour l’appareil StorSimple toohello toomigrate hello contenu de la base de données.</span><span class="sxs-lookup"><span data-stu-id="e1171-137">Then, use established SQL Server best practices toomigrate hello content database toohello StorSimple device.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e1171-138">Déplacement hello contenu de la base de données toohello est uniquement pris en charge pour la série de hello StorSimple 8000 (il n’est pas compatible avec la série de hello 5000 ou 7000).</span><span class="sxs-lookup"><span data-stu-id="e1171-138">Moving hello content database toohello device is only supported for hello StorSimple 8000 series (it is not supported for hello 5000 or 7000 series).</span></span>
   
   <span data-ttu-id="e1171-139">Si vous stockez des objets BLOB et base de données de contenu hello dans des volumes distincts sur l’appareil StorSimple hello, nous vous recommandons de configurer les Bonjour même conteneur de volume.</span><span class="sxs-lookup"><span data-stu-id="e1171-139">If you store BLOBs and hello content database in separate volumes on hello StorSimple device, we recommend that you configure them in hello same volume container.</span></span> <span data-ttu-id="e1171-140">Cela garantit qu’ils seront sauvegardés ensemble.</span><span class="sxs-lookup"><span data-stu-id="e1171-140">This ensures that they will be backed up together.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="e1171-141">Si vous n’avez pas activé RBS, il est déconseillé de déplacement de l’appareil StorSimple hello contenu de la base de données toohello.</span><span class="sxs-lookup"><span data-stu-id="e1171-141">If you have not enabled RBS, we do not recommend moving hello content database toohello StorSimple device.</span></span> <span data-ttu-id="e1171-142">Il s'agit d'une configuration non testée.</span><span class="sxs-lookup"><span data-stu-id="e1171-142">This is an untested configuration.</span></span>
   
9. <span data-ttu-id="e1171-143">Étape suivante de toohello accédez : [configurer le garbage collection](#configure-garbage-collection).</span><span class="sxs-lookup"><span data-stu-id="e1171-143">Go toohello next step: [Configure garbage collection](#configure-garbage-collection).</span></span>

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
