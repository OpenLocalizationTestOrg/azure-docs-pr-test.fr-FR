---
title: "aaaLoad - Azure Data Lake Store tooSQL l’entrepôt de données | Documents Microsoft"
description: "Découvrez comment toouse PolyBase externe tables données tooload à partir d’Azure Data Lake Store dans Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="ccaa3-103">Chargement de données Azure Data Lake Store dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ccaa3-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="ccaa3-104">Ce document vous donne toutes les étapes que vous avez besoin de tooload vos propres données à partir de Azure données Lake Store (ADLS) dans l’entrepôt de données SQL à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="ccaa3-105">Lorsque vous êtes en mesure de toorun des requêtes ad hoc sur les données de hello stockées dans ADLS à l’aide des Tables externes hello, comme une meilleure pratique nous vous suggérons l’importation des données de hello en hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="ccaa3-106">Durée estimée : 10 minutes, en supposant que vous avez conditions préalables de hello devez toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="ccaa3-107">Ce didacticiel vous apprendra à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ccaa3-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="ccaa3-108">Créer tooload des objets de base de données externe à partir d’Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="ccaa3-109">Se connecter tooan répertoire de magasin Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="ccaa3-110">Charger des données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ccaa3-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ccaa3-111">Before you begin</span></span>
<span data-ttu-id="ccaa3-112">toorun ce didacticiel, vous devez :</span><span class="sxs-lookup"><span data-stu-id="ccaa3-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="ccaa3-113">Toouse Active Directory Application Azure pour l’authentification de Service.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="ccaa3-114">toocreate, suivez [l’authentification Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="ccaa3-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="ccaa3-115">Vous devez hello client ID, clé et valeur de point de terminaison de jeton OAuth2.0 de votre tooyour de tooconnect d’Active Directory Application Azure Data Lake à partir de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="ccaa3-116">Détails de tooget comment ces valeurs sont dans le lien hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="ccaa3-117">Remarque pour l’inscription Azure Active Directory Application servir hello ID de l’Application hello ID Client.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="ccaa3-118">SQL Server Management Studio ou SQL Server Data Tools, toodownload SSMS et connecter voir [requête SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="ccaa3-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="ccaa3-119">Un entrepôt de données SQL Azure, suivez de toocreate un : https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="ccaa3-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="ccaa3-120">Un Azure Data Lake Store pour lequel le chiffrement est activé ou non.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="ccaa3-121">suivi d’un seul toocreate : https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="ccaa3-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="ccaa3-122">Configurer la source de données hello</span><span class="sxs-lookup"><span data-stu-id="ccaa3-122">Configure hello data source</span></span>
<span data-ttu-id="ccaa3-123">PolyBase utilise l’emplacement de T-SQL des objets externes toodefine hello et les attributs de données externes de hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="ccaa3-124">des objets externes Hello sont stockés dans la référence de l’entrepôt de données SQL et des données hello que th est stockées en externe.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="ccaa3-125">Créer des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="ccaa3-125">Create a credential</span></span>
<span data-ttu-id="ccaa3-126">Stocker de votre Azure Data Lake tooaccess, vous devez toocreate une clé principale de base de données de tooencrypt votre secret d’identification utilisé dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="ccaa3-127">Vous créez ensuite des informations d’identification d’une étendue de la base de données, ce qui stocke les hello principal des références de service définis dans AAD.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="ccaa3-128">Pour ceux qui ont utilisé PolyBase tooconnect tooWindows objets BLOB de stockage Azure, notez ces informations d’identification hello syntaxe est différente.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="ccaa3-129">tooconnect tooAzure Data Lake Store, vous devez **premier** créer une Application Active Directory de Azure, créer une clé d’accès et accordez hello application accès toohello Azure Data Lake ressource.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="ccaa3-130">Instrucitons tooperform ces étapes sont situés [ici](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="ccaa3-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="ccaa3-131">Créer la source de données externe hello</span><span class="sxs-lookup"><span data-stu-id="ccaa3-131">Create hello external data source</span></span>
<span data-ttu-id="ccaa3-132">Utilisez cette [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] emplacement de hello toostore des données de hello et type hello de données de commande.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="ccaa3-133">Vous trouverez hello ADL URI dans hello portail Azure et www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="ccaa3-134">Configurer le format des données</span><span class="sxs-lookup"><span data-stu-id="ccaa3-134">Configure data format</span></span>
<span data-ttu-id="ccaa3-135">les données de salutation tooimport de ADLS, vous devez format de fichier externe toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="ccaa3-136">Cette commande a les options spécifiques au format toodescribe vos données.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="ccaa3-137">Voici un exemple de format de fichier fréquemment utilisé, soit un fichier texte délimité par une barre verticale.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="ccaa3-138">Consultez notre documentation T-SQL pour obtenir une liste complète [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="ccaa3-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a><span data-ttu-id="ccaa3-139">Créer des tables externes hello</span><span class="sxs-lookup"><span data-stu-id="ccaa3-139">Create hello external tables</span></span>
<span data-ttu-id="ccaa3-140">Maintenant que vous avez spécifié hello données source et formats de fichier, vous êtes prêt toocreate des tables externes hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="ccaa3-141">Les tables externes vous permettent d’interagir avec des données externes.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="ccaa3-142">PolyBase utilise tooread de parcours de répertoire récursive tous les fichiers dans tous les sous-répertoires du répertoire hello spécifié dans le paramètre d’emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="ccaa3-143">En outre, hello l’exemple suivant montre comment toocreate hello objet.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="ccaa3-144">Vous devez toocustomize hello instruction toowork avec données hello dans ADLS.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="ccaa3-145">Considérations relatives aux tables externes</span><span class="sxs-lookup"><span data-stu-id="ccaa3-145">External Table Considerations</span></span>
<span data-ttu-id="ccaa3-146">Création d’une table externe est facile, mais il existe des nuances qui doivent toobe indiqué.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="ccaa3-147">Le chargement de données avec PolyBase est fortement typé.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="ccaa3-148">Cela signifie que chaque ligne de données hello en cours ingérées doit satisfaire la définition de schéma de table hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="ccaa3-149">Si une ligne donnée ne correspond pas à la définition de schéma hello, ligne de hello est rejetée à partir de la charge de hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="ccaa3-150">Hello REJECT_TYPE et REJECT_VALUE permettent de toodefine le nombre de lignes ou le pourcentage de données de salutation doit être présent dans la table finale de hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="ccaa3-151">Au cours du chargement, si la valeur de rejet hello est atteinte, le chargement de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="ccaa3-152">cause la plus courante de lignes rejetées Hello est une incompatibilité de définition de schéma.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="ccaa3-153">Par exemple, si une colonne reçoit correctement schéma hello int lorsque les données de salutation dans le fichier de hello sont une chaîne, chaque ligne ne fonctionnera pas tooload.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="ccaa3-154">Hello emplacement spécifie hello premier répertoire tooread des données à partir de.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="ccaa3-155">Dans ce cas, s’il y avait sous-répertoires /DimProduct/ PolyBase seraient importer toutes les données hello dans les sous-répertoires hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="ccaa3-156">Charger des données hello</span><span class="sxs-lookup"><span data-stu-id="ccaa3-156">Load hello data</span></span>
<span data-ttu-id="ccaa3-157">données tooload à partir d’Azure Data Lake Store utilisent hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instruction.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="ccaa3-158">Utilise hello chargement avec SACT fortement typé que vous avez créé une table externe.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="ccaa3-159">SACT crée une nouvelle table et le remplit avec des résultats d’une instruction select hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="ccaa3-160">SACT définit hello nouvelle table toohave hello les mêmes colonnes et types de données comme résultats hello Hello select (instruction).</span><span class="sxs-lookup"><span data-stu-id="ccaa3-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="ccaa3-161">Si vous sélectionnez toutes les colonnes hello à partir d’une table externe, hello nouvelle table est un réplica de colonnes de hello et les types de données dans une table externe hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="ccaa3-162">Dans cet exemple, nous créons une table de hachage distribuée appelée DimProduct à partir de notre table externe DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="ccaa3-163">Optimiser la compression columnstore</span><span class="sxs-lookup"><span data-stu-id="ccaa3-163">Optimize columnstore compression</span></span>
<span data-ttu-id="ccaa3-164">Par défaut, SQL Data Warehouse stocke la table de hello en tant qu’un index cluster columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="ccaa3-165">Après un chargement, certains hello lignes de données ne peuvent pas être compressé au hello columnstore.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="ccaa3-166">Cela peut être dû à diverses raisons.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="ccaa3-167">toolearn, voir [gérer les index columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="ccaa3-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="ccaa3-168">performances des requêtes toooptimize et la compression de columnstore après un chargement, reconstruire hello table tooforce hello columnstore index toocompress toutes les lignes hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="ccaa3-169">Pour plus d’informations sur la gestion des index columnstore, consultez hello [gérer les index columnstore] [ manage columnstore indexes] l’article.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="ccaa3-170">Optimiser les statistiques</span><span class="sxs-lookup"><span data-stu-id="ccaa3-170">Optimize statistics</span></span>
<span data-ttu-id="ccaa3-171">Il s’agit des statistiques de colonne unique toocreate meilleures immédiatement après un chargement.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="ccaa3-172">Les statistiques offrent plusieurs possibilités.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-172">There are some choices for statistics.</span></span> <span data-ttu-id="ccaa3-173">Par exemple, si vous créez des statistiques de colonnes uniques sur toutes les colonnes qu’il peut prendre un toorebuild beaucoup de temps toutes les statistiques de hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="ccaa3-174">Si vous savez que certaines colonnes ne vont pas toobe dans les prédicats de requête, vous pouvez ignorer la création des statistiques sur les colonnes.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="ccaa3-175">Si vous décidez de toocreate les statistiques de colonnes uniques sur chaque colonne de chaque table, vous pouvez utiliser les exemples de code de procédure stockée hello `prc_sqldw_create_stats` Bonjour [statistiques] [ statistics] l’article.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="ccaa3-176">Bonjour à l’exemple suivant est un bon point de départ pour la création de statistiques.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="ccaa3-177">Il crée des statistiques de colonnes uniques sur chaque colonne de table de dimension hello et sur chaque colonne de jointure dans des tables de faits hello.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="ccaa3-178">Vous pouvez toujours ajouter des colonnes de table de faits unique ou plusieurs colonnes de statistiques tooother ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="ccaa3-179">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="ccaa3-179">Achievement unlocked!</span></span>
<span data-ttu-id="ccaa3-180">Vous avez correctement chargé les données dans Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ccaa3-181">Bon travail !</span><span class="sxs-lookup"><span data-stu-id="ccaa3-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="ccaa3-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ccaa3-182">Next Steps</span></span>
<span data-ttu-id="ccaa3-183">Le chargement des données est hello première étape toodeveloping une solution d’entrepôt de données à l’aide de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ccaa3-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="ccaa3-184">Découvrez nos ressources de développement dans les sections [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) et [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="ccaa3-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
