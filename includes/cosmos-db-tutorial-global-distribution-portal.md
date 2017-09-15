
<span data-ttu-id="8bff9-101">Vous pouvez découvrir la diffusion mondiale de Azure Cosmos DB dans cette vidéo Azure Friday avec Scott Hanselman et Karthik Raman, responsable principal de l’ingénierie.</span><span class="sxs-lookup"><span data-stu-id="8bff9-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="8bff9-102">Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8bff9-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="8bff9-103"><a id="addregion"></a>Ajouter des régions de bases de donnée mondiales à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8bff9-103"><a id="addregion"></a>Add global database regions using the Azure Portal</span></span>
<span data-ttu-id="8bff9-104">Azure Cosmos DB est disponible dans toutes les [régions Azure][azureregions] à travers le monde.</span><span class="sxs-lookup"><span data-stu-id="8bff9-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="8bff9-105">Après avoir sélectionné le niveau de cohérence par défaut pour votre compte de base de données, vous pouvez associer une ou plusieurs régions (en fonction de votre choix de niveau de cohérence par défaut et de vos besoins de distribution mondiale).</span><span class="sxs-lookup"><span data-stu-id="8bff9-105">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="8bff9-106">Dans la barre à gauche du [portail Azure](https://portal.azure.com/), cliquez sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8bff9-106">In the [Azure portal](https://portal.azure.com/), in the left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="8bff9-107">Dans le panneau **Azure Cosmos DB**, sélectionnez le compte de base de données à modifier.</span><span class="sxs-lookup"><span data-stu-id="8bff9-107">In the **Azure Cosmos DB** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="8bff9-108">Dans le panneau du compte, cliquez sur **Répliquer les données globalement** à partir du menu.</span><span class="sxs-lookup"><span data-stu-id="8bff9-108">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="8bff9-109">Dans le panneau **Répliquer les données globalement**, sélectionnez les régions à ajouter ou à supprimer en cliquant sur des régions sur la carte, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8bff9-109">In the **Replicate data globally** blade, select the regions to add or remove by clicking regions in the map, and then click **Save**.</span></span> <span data-ttu-id="8bff9-110">L’ajout de régions est payant. Pour plus d’informations, consultez la [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/) ou l’article [Distribution mondiale des données avec DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="8bff9-110">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Cliquez sur les régions dans la carte pour les ajouter ou les supprimer.][1]
    
<span data-ttu-id="8bff9-112">Une fois que vous ajoutez une deuxième région, l’option **basculement manuel** est activée sur le panneau **Répliquer les données localement** dans le portail.</span><span class="sxs-lookup"><span data-stu-id="8bff9-112">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data globally** blade in the portal.</span></span> <span data-ttu-id="8bff9-113">Vous pouvez utiliser cette option pour tester le processus de basculement ou modifier la région principale d’écriture.</span><span class="sxs-lookup"><span data-stu-id="8bff9-113">You can use this option to test the failover process or change the primary write region.</span></span> <span data-ttu-id="8bff9-114">Une fois que vous ajoutez une troisième région, l’option **Priorités de basculement** est activée sur le même panneau afin que vous puissiez modifier l’ordre de basculement pour les lectures.</span><span class="sxs-lookup"><span data-stu-id="8bff9-114">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="8bff9-115">Sélection de régions de base de données mondiale</span><span class="sxs-lookup"><span data-stu-id="8bff9-115">Selecting global database regions</span></span>
<span data-ttu-id="8bff9-116">Il existe deux scénarios courants pour la configuration de deux ou plusieurs régions :</span><span class="sxs-lookup"><span data-stu-id="8bff9-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="8bff9-117">La fourniture aux utilisateurs finaux d’un accès à faible latence aux données, où qu’ils se trouvent dans le monde</span><span class="sxs-lookup"><span data-stu-id="8bff9-117">Delivering low-latency access to data to end users no matter where they are located around the globe</span></span>
2. <span data-ttu-id="8bff9-118">L’ajout d’une résilience régionale pour la continuité des activités et la récupération d’urgence (BCDR)</span><span class="sxs-lookup"><span data-stu-id="8bff9-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="8bff9-119">Pour fournir une faible latence aux utilisateurs finaux, il est recommandé de déployer l’application et d’ajouter Azure Cosmos DB dans les régions correspondant à la localisation géographique des utilisateurs de l’application.</span><span class="sxs-lookup"><span data-stu-id="8bff9-119">For delivering low-latency to end-users, it is recommended to deploy both the application and add Azure Cosmos DB in the regions thats correspond to where the application's users are located.</span></span>

<span data-ttu-id="8bff9-120">Pour BCDR, nous vous recommandons d’ajouter les régions en fonction des paires de régions décrites dans l’article [Continuité des activités et récupération d’urgence (BCDR) : régions jumelées d’Azure][bcdr].</span><span class="sxs-lookup"><span data-stu-id="8bff9-120">For BCDR, it is recommended to add regions based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<!--

## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **Azure Cosmos DB** blade, select the database account to modify.
2. In the account blade, click **Replicate data globally** from the menu.
3. In the **Replicate data globally** blade, click **Manual Failover** from the top bar.
    ![Change the write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region to become the new write region, click the checkbox to confirm triggering a failover, and click OK
    ![Change the write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
