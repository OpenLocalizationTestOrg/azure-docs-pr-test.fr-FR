
<span data-ttu-id="6bd7a-101">Vous pouvez découvrir la diffusion mondiale de Azure Cosmos DB dans cette vidéo Azure Friday avec Scott Hanselman et Karthik Raman, responsable principal de l’ingénierie.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="6bd7a-102">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="6bd7a-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="6bd7a-103"><a id="addregion"></a>Ajouter des zones globales de la base de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6bd7a-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="6bd7a-104">Azure Cosmos DB est disponible dans toutes les [régions Azure][azureregions] à travers le monde.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="6bd7a-105">Après avoir sélectionné le niveau de cohérence hello par défaut pour votre compte de base de données, vous pouvez associer une ou plusieurs régions (selon le choix de vos besoins en matière de distribution globale et au niveau de cohérence par défaut).</span><span class="sxs-lookup"><span data-stu-id="6bd7a-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="6bd7a-106">Bonjour [portail Azure](https://portal.azure.com/)hello barre gauche, cliquez sur dans **base de données Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="6bd7a-107">Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello de base de données compte toomodify.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="6bd7a-108">Dans le panneau de compte hello, cliquez sur **répliquer des données globalement** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="6bd7a-109">Bonjour **répliquer des données globalement** panneau, sélectionnez hello régions tooadd ou supprimer en cliquant sur les régions de carte de hello, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="6bd7a-110">Il existe un régions tooadding de coût, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/) ou hello [distribuer des données globalement avec DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Cliquez sur les zones hello dans hello carte tooadd ou les supprimer][1]
    
<span data-ttu-id="6bd7a-112">Une fois que vous ajoutez une autre zone, hello **basculement manuel** option est activée sur hello **répliquer des données globalement** panneau dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="6bd7a-113">Vous pouvez utiliser ce processus de basculement option tootest hello ou modifier la région primaire écriture hello.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="6bd7a-114">Une fois que vous ajoutez une région de tiers, hello **basculement priorités** option est activée sur hello même panneau afin que vous puissiez modifier ordre de basculement hello pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="6bd7a-115">Sélection de régions de base de données mondiale</span><span class="sxs-lookup"><span data-stu-id="6bd7a-115">Selecting global database regions</span></span>
<span data-ttu-id="6bd7a-116">Il existe deux scénarios courants pour la configuration de deux ou plusieurs régions :</span><span class="sxs-lookup"><span data-stu-id="6bd7a-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="6bd7a-117">Fournir l’accès à faible latence aux utilisateurs de tooend toodata, quel que soit leur emplacement monde hello</span><span class="sxs-lookup"><span data-stu-id="6bd7a-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="6bd7a-118">L’ajout d’une résilience régionale pour la continuité des activités et la récupération d’urgence (BCDR)</span><span class="sxs-lookup"><span data-stu-id="6bd7a-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="6bd7a-119">Pour diffuser à faible latence tooend utilisateurs et il est recommandé de toodeploy à la fois hello application et que vous ajoutez se trouvent Cosmos base de données Azure dans des régions hello est correspondant aux utilisateurs de l’application toowhere hello.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="6bd7a-120">BCDR, il est recommandé de régions tooadd basées sur des paires de région de hello décrites dans hello [entreprise la continuité des activités et récupération d’urgence (BCDR) : les régions Azure associés] [ bcdr] l’article.</span><span class="sxs-lookup"><span data-stu-id="6bd7a-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
