<span data-ttu-id="cad19-101">écouteur du groupe de disponibilité Hello est un nom de réseau et d’adresse IP qui hello SQL Server écoute le groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cad19-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="cad19-102">écouteur du groupe de disponibilité toocreate hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="cad19-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="cad19-103"><a name="getnet"></a>Obtenir le nom de hello de ressource de réseau de clusters hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="cad19-104">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-104">a.</span></span> <span data-ttu-id="cad19-105">Utilisez RDP tooconnect toohello machine virtuelle Azure qui héberge le réplica principal de hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="cad19-106">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-106">b.</span></span> <span data-ttu-id="cad19-107">Ouvrez le Gestionnaire du cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="cad19-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="cad19-108">c.</span><span class="sxs-lookup"><span data-stu-id="cad19-108">c.</span></span> <span data-ttu-id="cad19-109">Sélectionnez hello **réseaux** nœud et le nom de réseau du cluster Remarque hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="cad19-110">Utilisez ce nom Bonjour `$ClusterNetworkName` variable Bonjour script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad19-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="cad19-111">Bonjour, suivant le nom de réseau du cluster image hello est **réseau du Cluster 1**:</span><span class="sxs-lookup"><span data-stu-id="cad19-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![Nom réseau du cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="cad19-113"><a name="addcap"></a>Ajouter un point d’accès client hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="cad19-114">point d’accès client Hello est le nom de réseau hello que les applications utilisent des bases de données tooconnect toohello dans un groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cad19-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="cad19-115">Créer le point d’accès client hello Gestionnaire du Cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="cad19-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="cad19-116">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-116">a.</span></span> <span data-ttu-id="cad19-117">Développez le nom du cluster hello, puis cliquez sur **rôles**.</span><span class="sxs-lookup"><span data-stu-id="cad19-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="cad19-118">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-118">b.</span></span> <span data-ttu-id="cad19-119">Bonjour **rôles** volet, le groupe de disponibilité avec le bouton hello nom et sélectionnez **ajouter une ressource** > **Point d’accès Client**.</span><span class="sxs-lookup"><span data-stu-id="cad19-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="cad19-121">c.</span><span class="sxs-lookup"><span data-stu-id="cad19-121">c.</span></span> <span data-ttu-id="cad19-122">Bonjour **nom** zone, créez un nom pour ce nouvel écouteur.</span><span class="sxs-lookup"><span data-stu-id="cad19-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="cad19-123">Hello nom d’écouteur de nouveau hello est hello réseau que les applications utilisent tooconnect toodatabases dans le groupe de disponibilité de SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="cad19-124">d.</span><span class="sxs-lookup"><span data-stu-id="cad19-124">d.</span></span> <span data-ttu-id="cad19-125">toofinish de la création du récepteur hello, cliquez sur **suivant** à deux reprises, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="cad19-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="cad19-126">Ne mettez pas hello port d’écoute ou ressource en ligne à ce stade.</span><span class="sxs-lookup"><span data-stu-id="cad19-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="cad19-127"><a name="congroup"></a>Configurez la ressource IP de hello pour le groupe de disponibilité hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="cad19-128">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-128">a.</span></span> <span data-ttu-id="cad19-129">Cliquez sur hello **ressources** onglet, puis cliquez sur point d’accès client hello vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="cad19-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="cad19-130">point d’accès client Hello est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="cad19-130">hello client access point is offline.</span></span>

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="cad19-132">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-132">b.</span></span> <span data-ttu-id="cad19-133">Avec le bouton droit de la ressource IP hello, puis cliquez sur Propriétés.</span><span class="sxs-lookup"><span data-stu-id="cad19-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="cad19-134">Notez le nom hello d’adresse IP de hello et l’utiliser dans hello `$IPResourceName` variable Bonjour script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad19-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="cad19-135">c.</span><span class="sxs-lookup"><span data-stu-id="cad19-135">c.</span></span> <span data-ttu-id="cad19-136">Sous **Adresse IP**, cliquez sur **Adresse IP statique**.</span><span class="sxs-lookup"><span data-stu-id="cad19-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="cad19-137">Définir l’adresse IP de hello comme hello même adresse que vous avez utilisé lorsque vous définissez l’adresse d’équilibrage de charge de hello sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cad19-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="cad19-139"><a name = "dependencyGroup"></a>Faites en sorte que ressource de groupe de disponibilité de SQL Server hello dépendante sur le point d’accès client hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="cad19-140">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-140">a.</span></span> <span data-ttu-id="cad19-141">Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cad19-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="cad19-142">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-142">b.</span></span> <span data-ttu-id="cad19-143">Sur hello **ressources** sous l’onglet sous **autres ressources**, cliquez sur le groupe de ressources hello disponibilité, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="cad19-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="cad19-144">c.</span><span class="sxs-lookup"><span data-stu-id="cad19-144">c.</span></span> <span data-ttu-id="cad19-145">Sous l’onglet Dépendances de hello, ajoutez le nom de hello de ressource de hello client access point (écouteur hello).</span><span class="sxs-lookup"><span data-stu-id="cad19-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="cad19-147">d.</span><span class="sxs-lookup"><span data-stu-id="cad19-147">d.</span></span> <span data-ttu-id="cad19-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cad19-148">Click **OK**.</span></span>

5. <span data-ttu-id="cad19-149"><a name="listname"></a>Hello d’accès client aux ressources dépendant de l’adresse IP de hello de point.</span><span class="sxs-lookup"><span data-stu-id="cad19-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="cad19-150">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-150">a.</span></span> <span data-ttu-id="cad19-151">Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="cad19-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="cad19-152">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-152">b.</span></span> <span data-ttu-id="cad19-153">Sur hello **ressources** onglet, cliquez sur la ressource de point d’accès hello client sous **nom du serveur**, puis cliquez sur **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="cad19-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="cad19-155">c.</span><span class="sxs-lookup"><span data-stu-id="cad19-155">c.</span></span> <span data-ttu-id="cad19-156">Cliquez sur hello **dépendances** onglet. Vérifiez que les adresses IP de hello est une dépendance.</span><span class="sxs-lookup"><span data-stu-id="cad19-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="cad19-157">Si elle n’est pas le cas, définir une dépendance sur l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="cad19-158">S’il existe plusieurs ressources sont répertoriés, vérifiez que les adresses IP hello ont ou non et dépendances.</span><span class="sxs-lookup"><span data-stu-id="cad19-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="cad19-159">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cad19-159">Click **OK**.</span></span> 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="cad19-161">d.</span><span class="sxs-lookup"><span data-stu-id="cad19-161">d.</span></span> <span data-ttu-id="cad19-162">Cliquez sur le nom d’écouteur hello, puis cliquez sur **mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="cad19-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="cad19-163">Vous pouvez valider ce hello dépendances sont correctement configurées.</span><span class="sxs-lookup"><span data-stu-id="cad19-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="cad19-164">Dans le Gestionnaire de Cluster de basculement, accédez à tooRoles, cliquez sur le groupe de disponibilité hello, cliquez sur **autres Actions**, puis cliquez sur **afficher le rapport de dépendance**.</span><span class="sxs-lookup"><span data-stu-id="cad19-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="cad19-165">Lorsque hello dépendances sont correctement configurées, le groupe de disponibilité hello dépend du nom de réseau hello et nom de réseau hello dépend de l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="cad19-166"><a name="setparam"></a>Définir les paramètres de cluster hello dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cad19-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="cad19-167">a.</span><span class="sxs-lookup"><span data-stu-id="cad19-167">a.</span></span> <span data-ttu-id="cad19-168">Copiez hello suivant tooone de script PowerShell de vos instances de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cad19-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="cad19-169">Mettre à jour les variables hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="cad19-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="cad19-170">b.</span><span class="sxs-lookup"><span data-stu-id="cad19-170">b.</span></span> <span data-ttu-id="cad19-171">Définir les paramètres de cluster de hello en hello script PowerShell en cours d’exécution sur l’un des nœuds de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cad19-172">Si vos instances de SQL Server se trouvent dans des régions distinctes, vous avez besoin toorun hello PowerShell script à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="cad19-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="cad19-173">Hello la première fois, utilisez hello `$ILBIP` et `$ProbePort` à partir de la première région de hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="cad19-174">Hello la deuxième fois, utilisez hello `$ILBIP` et `$ProbePort` à partir de la deuxième zone de hello.</span><span class="sxs-lookup"><span data-stu-id="cad19-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="cad19-175">nom réseau du cluster Hello et le nom de la ressource cluster IP hello sont hello même.</span><span class="sxs-lookup"><span data-stu-id="cad19-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
