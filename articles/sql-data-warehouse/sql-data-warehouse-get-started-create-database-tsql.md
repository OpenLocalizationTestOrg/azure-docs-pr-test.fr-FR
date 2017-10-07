---
title: "aaaCreate un entrepôt de données SQL avec TSQL | Documents Microsoft"
description: "Découvrez comment toocreate une données SQL Azure de l’entrepôt de TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="e5ff2-103">Créer une base de données SQL Data Warehouse à l’aide de Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="e5ff2-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5ff2-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e5ff2-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="e5ff2-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="e5ff2-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="e5ff2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5ff2-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="e5ff2-107">Cet article vous explique comment toocreate une SQL Data Warehouse à l’aide de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5ff2-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e5ff2-108">Prerequisites</span></span>
<span data-ttu-id="e5ff2-109">tooget démarré, vous devez :</span><span class="sxs-lookup"><span data-stu-id="e5ff2-109">tooget started, you need:</span></span>

* <span data-ttu-id="e5ff2-110">**Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="e5ff2-111">**Serveur SQL Azure**: consultez [créer un serveur logique de la base de données SQL Azure avec hello Azure Portal] [créer un serveur logique de base de données SQL Azure avec hello Azure Portal] ou [créer un serveur logique de base de données SQL Azure avec PowerShell] [créer SQL Azure Serveur logique de la base de données avec PowerShell] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="e5ff2-112">**Groupe de ressources**: utilisez hello même ressource de groupe en tant que votre serveur SQL Azure, ou consultez [comment toocreate un groupe de ressources][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="e5ff2-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="e5ff2-113">**Environnement tooexecute T-SQL**: vous pouvez utiliser [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], ou [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="e5ff2-114">La création d’un entrepôt SQL Data Warehouse peut entraîner un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="e5ff2-115">Voir [Tarification de SQL Data Warehouse][SQL Data Warehouse pricing] pour plus d’informations sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="e5ff2-116">Créer une base de données avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e5ff2-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="e5ff2-117">Si vous êtes de nouveau tooVisual Studio, voir l’article hello [requête Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="e5ff2-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="e5ff2-118">toostart, ouvrez l’Explorateur d’objets SQL Server dans Visual Studio et connectez toohello serveur qui hébergera la base de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="e5ff2-119">Une fois connecté, vous pouvez créer un entrepôt de données SQL en exécutant hello suivant de commande SQL hello **master** base de données.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="e5ff2-120">Cette commande crée la base de données de hello MySqlDwDb avec un objectif de Service de DW400 et autoriser hello de base de données toogrow tooa taille maximale de 10 To.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="e5ff2-121">Créer une base de données avec sqlcmd</span><span class="sxs-lookup"><span data-stu-id="e5ff2-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="e5ff2-122">Vous pouvez également exécuter hello même commande avec sqlcmd en exécutant hello suite à une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="e5ff2-123">classement par défaut de Hello lorsque ne pas spécifié est SQL_Latin1_General_CP1_CI_AS de COLLATE.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="e5ff2-124">Hello `MAXSIZE` entre 250 Go et to 240.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="e5ff2-125">Hello `SERVICE_OBJECTIVE` peut être comprise entre DW100 et DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="e5ff2-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="e5ff2-126">Pour obtenir la liste de toutes les valeurs valides, consultez la documentation MSDN pour hello [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="e5ff2-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="e5ff2-127">Hello MAXSIZE et peut SERVICE_OBJECTIVE être modifié avec un [ALTER DATABASE] [ ALTER DATABASE] commande T-SQL.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="e5ff2-128">classement de Hello d’une base de données ne peut pas être modifié après sa création.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="e5ff2-129">Soyez vigilant lors de la modification hello SERVICE_OBJECTIVE modification DWU provoque un redémarrage des services, ce qui annule toutes les requêtes en vol.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="e5ff2-130">La modification du paramètre MAXSIZE ne redémarre pas les services car il s’agit d’une simple opération de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="e5ff2-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5ff2-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5ff2-131">Next steps</span></span>
<span data-ttu-id="e5ff2-132">Une fois votre entrepôt de données SQL a terminé, vous pouvez l’approvisionnement [charger les données d’exemple] [ load sample data] ou extraire de façon trop[développer][develop], [charger][load], ou [migrer][migrate].</span><span class="sxs-lookup"><span data-stu-id="e5ff2-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
