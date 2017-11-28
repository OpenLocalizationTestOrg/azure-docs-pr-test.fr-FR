<span data-ttu-id="7deb4-101">Dans cette étape, vous créez manuellement l’écouteur du groupe de disponibilité dans le Gestionnaire du cluster de basculement et SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="7deb4-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="7deb4-102">Ouvrez le Gestionnaire du cluster de basculement à partir du nœud qui héberge le réplica principal.</span><span class="sxs-lookup"><span data-stu-id="7deb4-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="7deb4-103">Sélectionnez le nœud **Réseaux**, puis notez le nom de réseau du cluster.</span><span class="sxs-lookup"><span data-stu-id="7deb4-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="7deb4-104">Ce nom est utilisé dans la variable $ClusterNetworkName dans le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7deb4-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="7deb4-105">Développez le nom du cluster, puis cliquez sur **Rôles**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="7deb4-106">Dans le volet **Rôles**, cliquez avec le bouton droit sur le nom du groupe de disponibilité, puis sélectionnez **Ajouter une ressource** > **Point d’accès client**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Ajouter un point d’accès client pour le groupe de disponibilité](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="7deb4-108">Dans la zone **Nom**, créez un nom pour ce nouvel écouteur, cliquez à deux reprises sur **Suivant**, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="7deb4-109">Ne mettez pas l'écouteur ou la ressource en ligne à ce stade.</span><span class="sxs-lookup"><span data-stu-id="7deb4-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="7deb4-110">Cliquez sur l’onglet **Ressources**, puis développez le point d’accès client vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="7deb4-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="7deb4-111">La ressource d’adresse IP de chaque réseau de cluster dans votre cluster est affichée.</span><span class="sxs-lookup"><span data-stu-id="7deb4-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="7deb4-112">S’il s’agit d’une solution basée uniquement sur Azure, une seule ressource d’adresse IP est affichée.</span><span class="sxs-lookup"><span data-stu-id="7deb4-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="7deb4-113">Effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="7deb4-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="7deb4-114">Pour configurer une solution hybride :</span><span class="sxs-lookup"><span data-stu-id="7deb4-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="7deb4-115">a.</span><span class="sxs-lookup"><span data-stu-id="7deb4-115">a.</span></span> <span data-ttu-id="7deb4-116">Cliquez avec le bouton droit sur la ressource d’adresse IP qui correspond à votre sous-réseau local, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="7deb4-117">Notez le nom de l’adresse IP et le nom du réseau.</span><span class="sxs-lookup"><span data-stu-id="7deb4-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="7deb4-118">b.</span><span class="sxs-lookup"><span data-stu-id="7deb4-118">b.</span></span> <span data-ttu-id="7deb4-119">Sélectionnez **Adresse IP statique**, affectez une adresse IP inutilisée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="7deb4-120">Pour configurer une solution basée uniquement sur Azure :</span><span class="sxs-lookup"><span data-stu-id="7deb4-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="7deb4-121">a.</span><span class="sxs-lookup"><span data-stu-id="7deb4-121">a.</span></span> <span data-ttu-id="7deb4-122">Cliquez avec le bouton droit sur la ressource d’adresse IP qui correspond à votre sous-réseau Azure, puis sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="7deb4-123">Si la mise en ligne de l’écouteur échoue par la suite en raison d’un conflit avec l’adresse IP sélectionnée par DHCP, vous pouvez configurer une adresse IP statique valide dans cette fenêtre de propriétés.</span><span class="sxs-lookup"><span data-stu-id="7deb4-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="7deb4-124">b.</span><span class="sxs-lookup"><span data-stu-id="7deb4-124">b.</span></span> <span data-ttu-id="7deb4-125">Dans la même fenêtre de propriétés **Adresse IP**, modifiez le **Nom de l’adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="7deb4-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="7deb4-126">Ce nom est utilisé dans la variable $IPResourceName du script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7deb4-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="7deb4-127">Si votre solution couvre plusieurs réseaux virtuels Azure, répétez cette étape pour chaque ressource IP.</span><span class="sxs-lookup"><span data-stu-id="7deb4-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

