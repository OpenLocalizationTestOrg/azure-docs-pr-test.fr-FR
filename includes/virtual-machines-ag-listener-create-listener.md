<span data-ttu-id="7e78c-101">Dans cette étape, vous créez manuellement l’écouteur du groupe de disponibilité hello dans le Gestionnaire du Cluster de basculement et de SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="7e78c-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="7e78c-102">Ouvrez le Gestionnaire du Cluster de basculement à partir du nœud hello qui héberge le réplica principal de hello.</span><span class="sxs-lookup"><span data-stu-id="7e78c-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="7e78c-103">Sélectionnez hello **réseaux** nœud, puis le nom de réseau du cluster Remarque hello.</span><span class="sxs-lookup"><span data-stu-id="7e78c-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="7e78c-104">Ce nom est utilisé dans la variable hello $ClusterNetworkName Bonjour script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e78c-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="7e78c-105">Développez le nom du cluster hello, puis cliquez sur **rôles**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="7e78c-106">Bonjour **rôles** volet, le groupe de disponibilité avec le bouton hello nom et sélectionnez **ajouter une ressource** > **Point d’accès Client**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![Ajouter un point d’accès client pour le groupe de disponibilité](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="7e78c-108">Bonjour **nom** , créez un nom pour ce nouveau port d’écoute, cliquez sur **suivant** à deux reprises, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="7e78c-109">Ne mettez pas hello port d’écoute ou ressource en ligne à ce stade.</span><span class="sxs-lookup"><span data-stu-id="7e78c-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="7e78c-110">Cliquez sur hello **ressources** onglet, puis cliquez sur point d’accès client hello vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="7e78c-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="7e78c-111">ressource d’adresse IP Hello pour chaque réseau de cluster dans votre cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7e78c-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="7e78c-112">S’il s’agit d’une solution basée uniquement sur Azure, une seule ressource d’adresse IP est affichée.</span><span class="sxs-lookup"><span data-stu-id="7e78c-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="7e78c-113">Effectuez une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="7e78c-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="7e78c-114">tooconfigure une solution hybride :</span><span class="sxs-lookup"><span data-stu-id="7e78c-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="7e78c-115">a.</span><span class="sxs-lookup"><span data-stu-id="7e78c-115">a.</span></span> <span data-ttu-id="7e78c-116">Cliquez sur la ressource d’adresse IP hello qui correspond le sous-réseau local de tooyour, puis sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="7e78c-117">Notez le nom de l’adresse IP hello et nom de réseau.</span><span class="sxs-lookup"><span data-stu-id="7e78c-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="7e78c-118">b.</span><span class="sxs-lookup"><span data-stu-id="7e78c-118">b.</span></span> <span data-ttu-id="7e78c-119">Sélectionnez **Adresse IP statique**, affectez une adresse IP inutilisée, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="7e78c-120">tooconfigure une solution Azure uniquement :</span><span class="sxs-lookup"><span data-stu-id="7e78c-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="7e78c-121">a.</span><span class="sxs-lookup"><span data-stu-id="7e78c-121">a.</span></span> <span data-ttu-id="7e78c-122">Cliquez sur la ressource d’adresse IP hello correspondant tooyour sous-réseau Azure, puis sélectionnez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="7e78c-123">Si l’écouteur de hello échoue ultérieurement toocome en ligne en raison d’une adresse IP conflictuelle par DHCP, vous pouvez configurer une adresse IP statique valide dans cette fenêtre de propriétés.</span><span class="sxs-lookup"><span data-stu-id="7e78c-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="7e78c-124">b.</span><span class="sxs-lookup"><span data-stu-id="7e78c-124">b.</span></span> <span data-ttu-id="7e78c-125">Dans hello même **adresse IP** fenêtre Propriétés, modification hello **nom de l’adresse IP**.</span><span class="sxs-lookup"><span data-stu-id="7e78c-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="7e78c-126">Ce nom est utilisé dans la variable hello $IPResourceName Hello script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e78c-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="7e78c-127">Si votre solution couvre plusieurs réseaux virtuels Azure, répétez cette étape pour chaque ressource IP.</span><span class="sxs-lookup"><span data-stu-id="7e78c-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

