---
title: "aaaImport un fichier BACPAC fichier toocreate une base de données SQL Azure | Documents Microsoft"
description: "Créez une base de données SQL Azure en important un fichier BACPAC."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: cf9a9631-56aa-4985-a565-1cacc297871d
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/26/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 0d5fc93acf27b79502969fcd6199d11161915b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-a-bacpac-file-tooa-new-azure-sql-database"></a><span data-ttu-id="a0c4b-103">Importer un tooa de fichier BACPAC nouvelle base de données de SQL Azure</span><span class="sxs-lookup"><span data-stu-id="a0c4b-103">Import a BACPAC file tooa new Azure SQL Database</span></span>

<span data-ttu-id="a0c4b-104">Lorsque vous avez besoin d’une base de données à partir d’une archive de tooimport ou lors de la migration à partir d’une autre plateforme, vous pouvez importer des schémas hello et les données à partir d’un [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) fichier.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-104">When you need tooimport a database from an archive or when migrating from another platform, you can import hello database schema and data from a [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) file.</span></span> <span data-ttu-id="a0c4b-105">Un fichier BACPAC est un fichier ZIP avec une extension de fichier BACPAC qui contient les métadonnées de hello et les données à partir d’une base de données SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-105">A BACPAC file is a ZIP file with an extension of BACPAC containing hello metadata and data from a SQL Server database.</span></span> <span data-ttu-id="a0c4b-106">Il peut être importé à partir du Stockage Blob Azure (stockage standard uniquement) ou à partir du stockage local dans un emplacement local.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-106">A BACPAC file can be imported from Azure blob storage (standard storage only) or from local storage in an on-premises location.</span></span> <span data-ttu-id="a0c4b-107">vitesse d’importation toomaximize hello, nous recommandons que vous spécifiez des performances et le niveau de niveau de service, par exemple un P6 et puis mettre à l’échelle toodown selon une fois l’importation de hello réussie.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-107">toomaximize hello import speed, we recommend that you specify a higher service tier and performance level, such as a P6, and then scale toodown as appropriate after hello import is successful.</span></span> <span data-ttu-id="a0c4b-108">En outre, le niveau de compatibilité de base de données hello après l’importation de hello est basé sur le niveau de compatibilité hello de base de données source hello.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-108">Also, hello database compatibility level after hello import is based on hello compatibility level of hello source database.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="a0c4b-109">Après avoir migré votre tooAzure de base de données de la base de données SQL, vous pouvez choisir la base de données toooperate hello à son niveau de compatibilité actuel (niveau 100 pour la base de données AdventureWorks2008R2 hello) ou à un niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-109">After you migrate your database tooAzure SQL Database, you can choose toooperate hello database at its current compatibility level (level 100 for hello AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="a0c4b-110">Pour plus d’informations sur les implications en matière de hello et les options pour l’exploitation d’une base de données à un niveau de compatibilité spécifiques, consultez [niveau de compatibilité ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-110">For more information on hello implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="a0c4b-111">Voir aussi [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) pour plus d’informations sur les paramètres de niveau de base de données supplémentaires liées toocompatibility niveaux.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-111">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related toocompatibility levels.</span></span>   >

> [!NOTE]
> <span data-ttu-id="a0c4b-112">tooimport un BACPAC tooa nouvelle base de données, vous devez d’abord créer un serveur logique de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-112">tooimport a BACPAC tooa new database, you must first create an Azure SQL Database logical server.</span></span> <span data-ttu-id="a0c4b-113">Pour obtenir un didacticiel montrant comment toomigrate un serveur SQL Server de base de données tooAzure base de données SQL à l’aide de SQLPackage, consultez [migrer une base de données SQL Server](sql-database-migrate-your-sql-server-database.md)</span><span class="sxs-lookup"><span data-stu-id="a0c4b-113">For a tutorial showing you how toomigrate a SQL Server database tooAzure SQL Database using SQLPackage, see [Migrate a SQL Server Database](sql-database-migrate-your-sql-server-database.md)</span></span>
>

## <a name="import-from-a-bacpac-file-using-azure-portal"></a><span data-ttu-id="a0c4b-114">Importation à partir d’un fichier BACPAC à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="a0c4b-114">Import from a BACPAC file using Azure portal</span></span>

<span data-ttu-id="a0c4b-115">Cet article fournit des instructions pour la création d’une base de données SQL Azure à partir d’un fichier BACPAC stocké dans le stockage blob Azure à l’aide de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-115">This article provides directions for creating an Azure SQL database from a BACPAC file stored in Azure blob storage using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a0c4b-116">Importation à l’aide de hello uniquement le portail Azure prend en charge l’importation d’un fichier BACPAC à partir du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-116">Import using hello Azure portal only supports importing a BACPAC file from Azure blob storage.</span></span>

<span data-ttu-id="a0c4b-117">une base de données à l’aide de tooimport hello portail Azure, page hello ouvert pour votre base de données cliquez sur **importation** sur la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-117">tooimport a database using hello Azure portal, open hello page for your database and click **Import** on hello toolbar.</span></span> <span data-ttu-id="a0c4b-118">Spécifiez le compte de stockage hello et un conteneur et sélectionnez hello BACPAC fichier tooimport.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-118">Specify hello storage account and container, and select hello BACPAC file you want tooimport.</span></span> <span data-ttu-id="a0c4b-119">Sélectionnez la taille de base de données hello hello (généralement hello même origine) et fournissent des informations d’identification de SQL Server de destination hello.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-119">Select hello size of hello new database (usually hello same as origin) and provide hello destination SQL Server credentials.</span></span>  

   ![Importation de base de données](./media/sql-database-import/import.png)

<span data-ttu-id="a0c4b-121">progression de hello toomonitor Hello l’opération d’importation, ouvrez une page hello pour hello serveur logique contenant hello de base de données en cours d’importation.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-121">toomonitor hello progress of hello import operation, open hello page for hello logical server containing hello database being imported.</span></span> <span data-ttu-id="a0c4b-122">Faites défiler la liste trop**Operations** puis cliquez sur **Import/Export** l’historique.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-122">Scroll down too**Operations** and then click **Import/Export** history.</span></span>

### <a name="monitor-hello-progress-of-an-import-operation"></a><span data-ttu-id="a0c4b-123">Surveiller la progression d’une opération d’importation hello</span><span class="sxs-lookup"><span data-stu-id="a0c4b-123">Monitor hello progress of an import operation</span></span>

<span data-ttu-id="a0c4b-124">progression de hello toomonitor Hello l’opération d’importation, ouvrez une page hello pour hello serveur logique dans le hello base de données est en cours d’importation importé.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-124">toomonitor hello progress of hello import operation, open hello page for hello logical server into which hello database is being imported imported.</span></span> <span data-ttu-id="a0c4b-125">Faites défiler la liste trop**Operations** puis cliquez sur **Import/Export** l’historique.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-125">Scroll down too**Operations** and then click **Import/Export** history.</span></span>
   
   <span data-ttu-id="a0c4b-126">![importer](./media/sql-database-import/import-history.png)![état d’importation](./media/sql-database-import/import-status.png)</span><span class="sxs-lookup"><span data-stu-id="a0c4b-126">![import](./media/sql-database-import/import-history.png) ![import status](./media/sql-database-import/import-status.png)</span></span>

<span data-ttu-id="a0c4b-127">base de données tooverify hello est actif sur le serveur de hello, cliquez sur **bases de données SQL** et vérifiez que la nouvelle base de données hello **Online**.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-127">tooverify hello database is live on hello server, click **SQL databases** and verify hello new database is **Online**.</span></span>

## <a name="import-from-a-bacpac-file-using-sqlpackage"></a><span data-ttu-id="a0c4b-128">Importer à partir d’un fichier BACPAC à l’aide de SQLPackage</span><span class="sxs-lookup"><span data-stu-id="a0c4b-128">Import from a BACPAC file using SQLPackage</span></span>

<span data-ttu-id="a0c4b-129">tooimport SQL de base de données à l’aide de hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) utilitaire de ligne de commande, consultez [importer les paramètres et les propriétés](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-129">tooimport a SQL database using hello [SqlPackage](https://msdn.microsoft.com/library/hh550080.aspx) command-line utility, see [Import parameters and properties](https://msdn.microsoft.com/library/hh550080.aspx#Import Parameters and Properties).</span></span> <span data-ttu-id="a0c4b-130">Hello SQLPackage utilitaire est fourni avec les versions les plus récentes de hello [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) et [SQL Server Data Tools pour Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), ou vous pouvez télécharger la version la plus récente de hello [ SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directement hello Microsoft Centre de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-130">hello SQLPackage utility ships with hello latest versions of [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) and [SQL Server Data Tools for Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx), or you can download hello latest version of [SqlPackage](https://www.microsoft.com/download/details.aspx?id=53876) directly from hello Microsoft download center.</span></span>

<span data-ttu-id="a0c4b-131">Nous vous recommandons d’utiliser hello Hello SQLPackage utilitaire pour l’évolutivité et de performances dans la plupart des environnements de production.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-131">We recommend hello use of hello SQLPackage utility for scale and performance in most production environments.</span></span> <span data-ttu-id="a0c4b-132">Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-132">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

<span data-ttu-id="a0c4b-133">Consultez hello commande SQLPackage pour un exemple de script de la façon suivante tooimport hello **AdventureWorks2008R2** base de données à partir du stockage local tooan base de données SQL Azure serveur logique, appelée **mynewserver20170403** dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-133">See hello following SQLPackage command for a script example for how tooimport hello **AdventureWorks2008R2** database from local storage tooan Azure SQL Database logical server, called **mynewserver20170403** in this example.</span></span> <span data-ttu-id="a0c4b-134">Ce script illustre la création d’une base de données appelée hello **myMigratedDatabase**, avec un niveau de service de **Premium**et un objectif de Service de **P6**.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-134">This script shows hello creation of a new database called **myMigratedDatabase**, with a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="a0c4b-135">Modifiez ces valeurs comme environnement de tooyour appropriée.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-135">Change these values as appropriate tooyour environment.</span></span>

```cmd
SqlPackage.exe /a:import /tcs:"Data Source=mynewserver20170403.database.windows.net;Initial Catalog=myMigratedDatabase;User Id=ServerAdmin;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
```

   ![importer sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="a0c4b-137">Un serveur logique Azure SQL Database écoute sur le port 1433.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-137">An Azure SQL Database logical server listens on port 1433.</span></span> <span data-ttu-id="a0c4b-138">Si vous essayez de tooconnect tooan base de données SQL Azure serveur logique au sein d’un pare-feu d’entreprise, ce port doit être ouvert dans le pare-feu d’entreprise hello pour toosuccessfully de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-138">If you are attempting tooconnect tooan Azure SQL Database logical server from within a corporate firewall, this port must be open in hello corporate firewall for you toosuccessfully connect.</span></span>
>

<span data-ttu-id="a0c4b-139">Cet exemple montre comment tooimport une base de données à l’aide de SqlPackage.exe avec l’authentification universelle Active Directory :</span><span class="sxs-lookup"><span data-stu-id="a0c4b-139">This example shows how tooimport a database using SqlPackage.exe with Active Directory Universal Authentication:</span></span>

```cmd
SqlPackage.exe /a:Import /sf:testExport.bacpac /tdn:NewDacFX /tsn:apptestserver.database.windows.net /ua:True /tid:"apptest.onmicrosoft.com"
```

## <a name="import-from-a-bacpac-file-using-powershell"></a><span data-ttu-id="a0c4b-140">Importer à partir d’un fichier BACPAC à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0c4b-140">Import from a BACPAC file using PowerShell</span></span>

<span data-ttu-id="a0c4b-141">Hello d’utilisation [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) toosubmit de l’applet de commande un toohello de requête de base de données importation service de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-141">Use hello [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) cmdlet toosubmit an import database request toohello Azure SQL Database service.</span></span> <span data-ttu-id="a0c4b-142">Selon la taille de hello de votre base de données, opération d’importation hello peut prendre quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-142">Depending on hello size of your database, hello import operation may take some time toocomplete.</span></span>

 ```powershell
 $importRequest = New-AzureRmSqlDatabaseImport -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "MyImportSample" `
    -DatabaseMaxSizeBytes "262144000" `
    -StorageKeyType "StorageAccessKey" `
    -StorageKey $(Get-AzureRmStorageAccountKey -ResourceGroupName "myResourceGroup" -StorageAccountName $storageaccountname).Value[0] `
    -StorageUri "http://$storageaccountname.blob.core.windows.net/importsample/sample.bacpac" `
    -Edition "Standard" `
    -ServiceObjectiveName "P6" `
    -AdministratorLogin "ServerAdmin" `
    -AdministratorLoginPassword $(ConvertTo-SecureString -String "ASecureP@assw0rd" -AsPlainText -Force)

 ```

<span data-ttu-id="a0c4b-143">état de hello toocheck Hello la demande d’importation, utilisez hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-143">toocheck hello status of hello import request, use hello [Get-AzureRmSqlDatabaseImportExportStatus](/powershell/module/azurerm.sql/get-azurermsqldatabaseimportexportstatus) cmdlet.</span></span> <span data-ttu-id="a0c4b-144">Cela exécute immédiatement après hello demande généralement retourne **état : InProgress**.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-144">Running this immediately after hello request usually returns **Status: InProgress**.</span></span> <span data-ttu-id="a0c4b-145">Lorsque vous consultez **état : a réussi** hello l’importation est terminée.</span><span class="sxs-lookup"><span data-stu-id="a0c4b-145">When you see **Status: Succeeded** hello import is complete.</span></span>

```powershell
$importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
[Console]::Write("Importing")
while ($importStatus.Status -eq "InProgress")
{
    $importStatus = Get-AzureRmSqlDatabaseImportExportStatus -OperationStatusLink $importRequest.OperationStatusLink
    [Console]::Write(".")
    Start-Sleep -s 10
}
[Console]::WriteLine("")
$importStatus
```

> [!TIP]
<span data-ttu-id="a0c4b-146">Pour un autre exemple de script, consultez [Importation d’une base de données à partir d’un fichier BACPAC](scripts/sql-database-import-from-bacpac-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-146">For another script example, see [Import a database from a BACPAC file](scripts/sql-database-import-from-bacpac-powershell.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0c4b-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0c4b-147">Next steps</span></span>
* <span data-ttu-id="a0c4b-148">toolearn tooconnect tooand interroger une base de données SQL importée, voir [connecter tooSQL de base de données avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-148">toolearn how tooconnect tooand query an imported SQL Database, see [Connect tooSQL Database with SQL Server Management Studio and perform a sample T-SQL query](sql-database-connect-query-ssms.md).</span></span>
* <span data-ttu-id="a0c4b-149">Pour une équipe de consultants clients SQL Server à l’aide des fichiers BACPAC, consultez le blog sur la migration [migration à partir de SQL Server tooAzure de la base de données SQL à l’aide des fichiers BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-149">For a SQL Server Customer Advisory Team blog about migrating using BACPAC files, see [Migrating from SQL Server tooAzure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>
* <span data-ttu-id="a0c4b-150">Pour en savoir plus sur hello entière SQL Server de base de données du processus de migration, y compris les recommandations relatives aux performances, consultez [migrer un tooAzure de base de données SQL Server de la base de données SQL](sql-database-cloud-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="a0c4b-150">For a discussion of hello entire SQL Server database migration process, including performance recommendations, see [Migrate a SQL Server database tooAzure SQL Database](sql-database-cloud-migrate.md).</span></span>



