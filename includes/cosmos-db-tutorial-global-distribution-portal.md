
Vous pouvez découvrir la diffusion mondiale de Azure Cosmos DB dans cette vidéo Azure Friday avec Scott Hanselman et Karthik Raman, responsable principal de l’ingénierie.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Pour plus d’informations sur le fonctionnement de la réplication de base de données à l’échelle mondiale dans Cosmos DB, voir [Diffuser des données à l’échelle mondiale avec Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Ajouter des zones globales de la base de données à l’aide de hello portail Azure
Azure Cosmos DB est disponible dans toutes les [régions Azure][azureregions] à travers le monde. Après avoir sélectionné le niveau de cohérence hello par défaut pour votre compte de base de données, vous pouvez associer une ou plusieurs régions (selon le choix de vos besoins en matière de distribution globale et au niveau de cohérence par défaut).

1. Bonjour [portail Azure](https://portal.azure.com/)hello barre gauche, cliquez sur dans **base de données Azure Cosmos**.
2. Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello de base de données compte toomodify.
3. Dans le panneau de compte hello, cliquez sur **répliquer des données globalement** à partir du menu de hello.
4. Bonjour **répliquer des données globalement** panneau, sélectionnez hello régions tooadd ou supprimer en cliquant sur les régions de carte de hello, puis cliquez sur **enregistrer**. Il existe un régions tooadding de coût, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/documentdb/) ou hello [distribuer des données globalement avec DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article pour plus d’informations.
   
    ![Cliquez sur les zones hello dans hello carte tooadd ou les supprimer][1]
    
Une fois que vous ajoutez une autre zone, hello **basculement manuel** option est activée sur hello **répliquer des données globalement** panneau dans le portail de hello. Vous pouvez utiliser ce processus de basculement option tootest hello ou modifier la région primaire écriture hello. Une fois que vous ajoutez une région de tiers, hello **basculement priorités** option est activée sur hello même panneau afin que vous puissiez modifier ordre de basculement hello pour les lectures.  

### <a name="selecting-global-database-regions"></a>Sélection de régions de base de données mondiale
Il existe deux scénarios courants pour la configuration de deux ou plusieurs régions :

1. Fournir l’accès à faible latence aux utilisateurs de tooend toodata, quel que soit leur emplacement monde hello
2. L’ajout d’une résilience régionale pour la continuité des activités et la récupération d’urgence (BCDR)

Pour diffuser à faible latence tooend utilisateurs et il est recommandé de toodeploy à la fois hello application et que vous ajoutez se trouvent Cosmos base de données Azure dans des régions hello est correspondant aux utilisateurs de l’application toowhere hello.

BCDR, il est recommandé de régions tooadd basées sur des paires de région de hello décrites dans hello [entreprise la continuité des activités et récupération d’urgence (BCDR) : les régions Azure associés] [ bcdr] l’article.

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
