## <a name="repeatability-during-copy"></a><span data-ttu-id="a0e19-101">Répétabilité pendant la copie</span><span class="sxs-lookup"><span data-stu-id="a0e19-101">Repeatability during Copy</span></span>
<span data-ttu-id="a0e19-102">Copie des données tooAzure SQL/SQL Server à partir d’autres données lorsque stocke une répétabilité de tookeep besoins dans l’esprit tooavoid des résultats inattendus.</span><span class="sxs-lookup"><span data-stu-id="a0e19-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="a0e19-103">Lors de la copie des données tooAzure base de données SQL/SQL Server, l’activité de copie sera par table récepteur des toohello de jeu de données par défaut APPEND hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="a0e19-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="a0e19-104">Par exemple, lors de la copie des données à partir d’une source de fichier CSV (valeurs de données séparées par des virgules) contenant deux enregistrements tooAzure base de données SQL/SQL Server, il s’agit quelle table hello ressemble à :</span><span class="sxs-lookup"><span data-stu-id="a0e19-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="a0e19-105">Supposons que vous a détecté des erreurs dans le fichier source et de la quantité de mise à jour hello de Tube vers le bas à partir de 2 too4 dans le fichier de source de hello.</span><span class="sxs-lookup"><span data-stu-id="a0e19-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="a0e19-106">Si vous réexécutez la tranche de données hello pour cette période, vous trouverez deux nouveaux enregistrements ajoutés tooAzure base de données SQL/SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a0e19-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="a0e19-107">Hello ci-dessous suppose que Hello des colonnes dans la table de hello ont de contrainte de clé primaire hello.</span><span class="sxs-lookup"><span data-stu-id="a0e19-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="a0e19-108">tooavoid, vous devez la sémantique UPSERT toospecify en tirant parti d’un des hello ci-dessous 2 mécanismes indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="a0e19-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="a0e19-109">Une tranche peut être réexécutée automatiquement dans Azure Data Factory en fonction de la stratégie de nouvelle tentative hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="a0e19-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="a0e19-110">Mécanisme 1</span><span class="sxs-lookup"><span data-stu-id="a0e19-110">Mechanism 1</span></span>
<span data-ttu-id="a0e19-111">Vous pouvez tirer parti de **sqlWriterCleanupScript** propriété toofirst effectuer l’action de nettoyage lors de l’exécution d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="a0e19-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="a0e19-112">Hello script de nettoyage sera exécuté à la première pendant la copie pour une tranche de donnée qui supprime les données de salutation à partir de la tranche de toothat hello Table SQL correspondante.</span><span class="sxs-lookup"><span data-stu-id="a0e19-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="a0e19-113">activité Hello est par la suite insérer des données de hello dans hello Table SQL.</span><span class="sxs-lookup"><span data-stu-id="a0e19-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="a0e19-114">Si la tranche de hello est maintenant exécuter à nouveau, puis vous trouverez quantité de hello est mise à jour comme vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="a0e19-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="a0e19-115">Supposons que hello enregistrement de laver plat est supprimé de volume partagé de cluster hello d’origine.</span><span class="sxs-lookup"><span data-stu-id="a0e19-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="a0e19-116">Puis réexécutez tranche de hello produirait hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="a0e19-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="a0e19-117">Rien de nouveau avait toobe terminé.</span><span class="sxs-lookup"><span data-stu-id="a0e19-117">Nothing new had toobe done.</span></span> <span data-ttu-id="a0e19-118">activité de copie Hello s’exécutaient hello nettoyage script toodelete hello données correspondantes pour ce secteur.</span><span class="sxs-lookup"><span data-stu-id="a0e19-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="a0e19-119">Puis il lire l’entrée de hello de csv hello (qui puis contenu uniquement 1 enregistrement) et inséré dans la Table de hello.</span><span class="sxs-lookup"><span data-stu-id="a0e19-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="a0e19-120">Mécanisme 2</span><span class="sxs-lookup"><span data-stu-id="a0e19-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0e19-121">Pour le moment, sliceIdentifierColumnName n’est pas pris en charge pour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a0e19-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="a0e19-122">Répétabilité de tooachieve un autre mécanisme consiste à avoir une colonne dédiée (**sliceIdentifierColumnName**) Bonjour cibler la Table.</span><span class="sxs-lookup"><span data-stu-id="a0e19-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="a0e19-123">Cette colonne peut être utilisée par Azure Data Factory tooensure hello source et destination reste synchronisé.</span><span class="sxs-lookup"><span data-stu-id="a0e19-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="a0e19-124">Cette approche fonctionne quand il existe une grande souplesse dans la modification ou la définition de schéma de Table SQL de destination hello.</span><span class="sxs-lookup"><span data-stu-id="a0e19-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="a0e19-125">Cette colonne devrait être utilisée par Azure Data Factory à des fins de répétabilité et de dans le processus de hello Azure Data Factory n’apporte aucun schéma change toohello Table.</span><span class="sxs-lookup"><span data-stu-id="a0e19-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="a0e19-126">Méthode toouse cette approche :</span><span class="sxs-lookup"><span data-stu-id="a0e19-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="a0e19-127">Définir une colonne de type binary (32) dans la destination de hello Table SQL.</span><span class="sxs-lookup"><span data-stu-id="a0e19-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="a0e19-128">Aucune contrainte ne doit exister sur cette colonne.</span><span class="sxs-lookup"><span data-stu-id="a0e19-128">There should be no constraints on this column.</span></span> <span data-ttu-id="a0e19-129">Pour cet exemple, nommons cette colonne « ColumnForADFuseOnly ».</span><span class="sxs-lookup"><span data-stu-id="a0e19-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="a0e19-130">Utiliser dans l’activité de copie hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0e19-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="a0e19-131">Azure Data Factory remplit cette colonne en fonction de son besoin tooensure hello source et destination restent synchronisés.</span><span class="sxs-lookup"><span data-stu-id="a0e19-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="a0e19-132">les valeurs Hello de cette colonne ne doivent pas être utilisées en dehors de ce contexte par utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a0e19-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="a0e19-133">Toomechanism similaires 1, est de l’activité de copie automatiquement première Nettoyez les données hello pour hello donné tranche à partir de destination hello Table SQL et puis exécutez l’activité de copie hello normalement données hello tooinsert toodestination source pour cette tranche.</span><span class="sxs-lookup"><span data-stu-id="a0e19-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

