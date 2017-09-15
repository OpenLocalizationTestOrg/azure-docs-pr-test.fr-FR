<span data-ttu-id="4d6d9-101">L’écouteur de groupe de disponibilité est une adresse IP et un nom réseau sur lesquels le groupe de disponibilité de SQL Server écoute.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-101">The availability group listener is an IP address and network name that the SQL Server availability group listens on.</span></span> <span data-ttu-id="4d6d9-102">Pour créer l’écouteur de groupe de disponibilité, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4d6d9-102">To create the availability group listener, do the following:</span></span>

1. <span data-ttu-id="4d6d9-103"><a name="getnet"></a>Récupérez le nom de la ressource réseau de cluster.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-103"><a name="getnet"></a>Get the name of the cluster network resource.</span></span>

    <span data-ttu-id="4d6d9-104">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-104">a.</span></span> <span data-ttu-id="4d6d9-105">Utilisez le protocole RDP pour vous connecter à la machine virtuelle Azure qui héberge le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-105">Use RDP to connect to the Azure virtual machine that hosts the primary replica.</span></span> 

    <span data-ttu-id="4d6d9-106">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-106">b.</span></span> <span data-ttu-id="4d6d9-107">Ouvrez le Gestionnaire du cluster de basculement.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="4d6d9-108">c.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-108">c.</span></span> <span data-ttu-id="4d6d9-109">sélectionnez le nœud **Réseaux** et notez le nom de réseau du cluster.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-109">Select the **Networks** node, and note the cluster network name.</span></span> <span data-ttu-id="4d6d9-110">Utilisez ce nom dans la variable `$ClusterNetworkName` du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-110">Use this name in the `$ClusterNetworkName` variable in the PowerShell script.</span></span> <span data-ttu-id="4d6d9-111">Dans l’image suivante, le nom réseau du cluster est **Cluster Network 1** :</span><span class="sxs-lookup"><span data-stu-id="4d6d9-111">In the following image the cluster network name is **Cluster Network 1**:</span></span>

   ![Nom réseau du cluster](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="4d6d9-113"><a name="addcap"></a>Ajoutez le point d’accès client.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-113"><a name="addcap"></a>Add the client access point.</span></span>  
    <span data-ttu-id="4d6d9-114">Le point d’accès client est le nom réseau que les applications utilisent pour se connecter aux bases de données dans un groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-114">The client access point is the network name that applications use to connect to the databases in an availability group.</span></span> <span data-ttu-id="4d6d9-115">Créez le point d’accès client dans le Gestionnaire du cluster de basculement .</span><span class="sxs-lookup"><span data-stu-id="4d6d9-115">Create the client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="4d6d9-116">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-116">a.</span></span> <span data-ttu-id="4d6d9-117">Développez le nom du cluster, puis cliquez sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-117">Expand the cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="4d6d9-118">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-118">b.</span></span> <span data-ttu-id="4d6d9-119">Dans le volet **Rôles**, cliquez avec le bouton droit sur le nom du groupe de disponibilité, puis sélectionnez **Ajouter une ressource** > **Point d’accès client**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-119">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="4d6d9-121">c.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-121">c.</span></span> <span data-ttu-id="4d6d9-122">Dans la zone **Nom**, créez un nom pour ce nouvel écouteur.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-122">In the **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="4d6d9-123">Le nom du nouvel écouteur est le nom réseau que les applications utilisent pour se connecter aux bases de données dans le groupe de disponibilité de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-123">The name for the new listener is the network name that applications use to connect to databases in the SQL Server availability group.</span></span>
   
    <span data-ttu-id="4d6d9-124">d.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-124">d.</span></span> <span data-ttu-id="4d6d9-125">Pour terminer la création de l’écouteur, cliquez sur **Suivant** deux fois, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-125">To finish creating the listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="4d6d9-126">Ne mettez pas l'écouteur ou la ressource en ligne à ce stade.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-126">Do not bring the listener or resource online at this point.</span></span>

3. <span data-ttu-id="4d6d9-127"><a name="congroup"></a>Configurez la ressource IP du groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-127"><a name="congroup"></a>Configure the IP resource for the availability group.</span></span>

    <span data-ttu-id="4d6d9-128">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-128">a.</span></span> <span data-ttu-id="4d6d9-129">Cliquez sur l’onglet **Ressources**, puis développez le point d’accès client que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-129">Click the **Resources** tab, and then expand the client access point you created.</span></span>  
    <span data-ttu-id="4d6d9-130">Le point d’accès client est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-130">The client access point is offline.</span></span>

   ![Point d’accès client](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="4d6d9-132">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-132">b.</span></span> <span data-ttu-id="4d6d9-133">Cliquez avec le bouton droit sur la ressource IP, puis cliquez sur Propriétés.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-133">Right-click the IP resource, and then click properties.</span></span> <span data-ttu-id="4d6d9-134">Notez le nom de l’adresse IP et utilisez-le dans la variable `$IPResourceName` dans le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-134">Note the name of the IP address, and use it in the `$IPResourceName` variable in the PowerShell script.</span></span>

    <span data-ttu-id="4d6d9-135">c.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-135">c.</span></span> <span data-ttu-id="4d6d9-136">Sous **Adresse IP**, cliquez sur **Adresse IP statique**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="4d6d9-137">Pour l’adresse IP, utilisez l’adresse que vous avez définie pour l’équilibreur de charge sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-137">Set the IP address as the same address that you used when you set the load balancer address on the Azure portal.</span></span>

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="4d6d9-139"><a name = "dependencyGroup"></a>Créez une dépendance entre la ressource de groupe de disponibilité de SQL Server et le point d’accès client.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-139"><a name = "dependencyGroup"></a>Make the SQL Server availability group resource dependent on the client access point.</span></span>

    <span data-ttu-id="4d6d9-140">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-140">a.</span></span> <span data-ttu-id="4d6d9-141">Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="4d6d9-142">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-142">b.</span></span> <span data-ttu-id="4d6d9-143">Dans l’onglet **Ressources**, sous **Autres ressources**, cliquez avec le bouton droit sur la ressource de groupe de disponibilité, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-143">On the **Resources** tab, under **Other Resources**, right-click the availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="4d6d9-144">c.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-144">c.</span></span> <span data-ttu-id="4d6d9-145">Dans l’onglet Dépendances, ajoutez le nom de la ressource du point d’accès client (écouteur).</span><span class="sxs-lookup"><span data-stu-id="4d6d9-145">On the dependencies tab, add the name of the client access point (the listener) resource.</span></span>

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="4d6d9-147">d.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-147">d.</span></span> <span data-ttu-id="4d6d9-148">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-148">Click **OK**.</span></span>

5. <span data-ttu-id="4d6d9-149"><a name="listname"></a>Créez une dépendance entre la ressource du point d’accès client et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-149"><a name="listname"></a>Make the client access point resource dependent on the IP address.</span></span>

    <span data-ttu-id="4d6d9-150">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-150">a.</span></span> <span data-ttu-id="4d6d9-151">Dans le Gestionnaire du cluster de basculement, cliquez sur **Rôles**, puis sur votre groupe de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="4d6d9-152">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-152">b.</span></span> <span data-ttu-id="4d6d9-153">Dans l’onglet **Ressources**, cliquez avec le bouton droit sur la ressource du point d’accès client sous **Nom du serveur**, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-153">On the **Resources** tab, right-click the client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="4d6d9-155">c.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-155">c.</span></span> <span data-ttu-id="4d6d9-156">Cliquez sur l'onglet **Dépendances** .</span><span class="sxs-lookup"><span data-stu-id="4d6d9-156">Click the **Dependencies** tab.</span></span> <span data-ttu-id="4d6d9-157">Vérifiez que l’adresse IP est une dépendance.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-157">Verify that the IP address is a dependency.</span></span> <span data-ttu-id="4d6d9-158">Si tel n’est pas le cas, définissez une dépendance sur l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-158">If it is not, set a dependency on the IP address.</span></span> <span data-ttu-id="4d6d9-159">Si plusieurs ressources sont répertoriées, vérifiez que les adresses IP ont des dépendances OR (et non des dépendances AND).</span><span class="sxs-lookup"><span data-stu-id="4d6d9-159">If there are multiple resources listed, verify that the IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="4d6d9-160">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-160">Click **OK**.</span></span> 

   ![Ressource IP](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="4d6d9-162">d.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-162">d.</span></span> <span data-ttu-id="4d6d9-163">Cliquez avec le bouton droit sur le nom de l’écouteur, puis cliquez sur **Mettre en ligne**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-163">Right-click the listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="4d6d9-164">Vous pouvez vérifier que les dépendances sont correctement configurées.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-164">You can validate that the dependencies are correctly configured.</span></span> <span data-ttu-id="4d6d9-165">Dans le Gestionnaire du cluster de basculement, accédez à Rôles, cliquez avez le bouton droit sur le groupe de disponibilité, et cliquez sur **Autres actions**, puis sur **Afficher le rapport de dépendance**.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-165">In Failover Cluster Manager, go to Roles, right-click the availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="4d6d9-166">Lorsque les dépendances sont correctement configurées, le groupe de disponibilité dépend du nom réseau, et le nom réseau dépend de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-166">When the dependencies are correctly configured, the availability group is dependent on the network name, and the network name is dependent on the IP address.</span></span> 


6. <span data-ttu-id="4d6d9-167"><a name="setparam"></a>Définissez les paramètres de cluster dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-167"><a name="setparam"></a>Set the cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="4d6d9-168">a.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-168">a.</span></span> <span data-ttu-id="4d6d9-169">Copiez le script PowerShell suivant sur l’une de vos instances SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-169">Copy the following PowerShell script to one of your SQL Server instances.</span></span> <span data-ttu-id="4d6d9-170">Mettez à jour les variables de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-170">Update the variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
    $IPResourceName = "<IPResourceName>" # the IP Address resource name
    $ILBIP = “<n.n.n.n>” # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="4d6d9-171">b.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-171">b.</span></span> <span data-ttu-id="4d6d9-172">Définissez les paramètres du cluster en exécutant le script PowerShell sur l’un des nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-172">Set the cluster parameters by running the PowerShell script on one of the cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="4d6d9-173">Si vos instances SQL Server se trouvent dans différentes régions, vous devez exécuter le script PowerShell à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-173">If your SQL Server instances are in separate regions, you need to run the PowerShell script twice.</span></span> <span data-ttu-id="4d6d9-174">La première fois, utilisez `$ILBIP` et `$ProbePort` à partir de la première région.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-174">The first time, use the `$ILBIP` and `$ProbePort` from the first region.</span></span> <span data-ttu-id="4d6d9-175">La seconde fois, utilisez `$ILBIP` et `$ProbePort` à partir de la seconde région.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-175">The second time, use the `$ILBIP` and `$ProbePort` from the second region.</span></span> <span data-ttu-id="4d6d9-176">Le nom réseau du cluster et le nom de ressource IP du cluster sont identiques.</span><span class="sxs-lookup"><span data-stu-id="4d6d9-176">The cluster network name and the cluster IP resource name are the same.</span></span> 
