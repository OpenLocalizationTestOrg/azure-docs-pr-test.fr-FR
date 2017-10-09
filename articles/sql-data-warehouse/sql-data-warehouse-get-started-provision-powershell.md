---
title: "aaaCreate SQL Data Warehouse à l’aide de PowerShell | Documents Microsoft"
description: "Création de SQL Data Warehouse à l’aide de PowerShell"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a><span data-ttu-id="4318a-103">Création de SQL Data Warehouse à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4318a-103">Create SQL Data Warehouse using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4318a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4318a-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="4318a-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="4318a-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="4318a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4318a-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="4318a-107">Cet article vous explique comment toocreate une SQL Data Warehouse à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4318a-107">This article shows you how toocreate a SQL Data Warehouse using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4318a-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4318a-108">Prerequisites</span></span>
<span data-ttu-id="4318a-109">tooget démarré, vous devez :</span><span class="sxs-lookup"><span data-stu-id="4318a-109">tooget started, you need:</span></span>

* <span data-ttu-id="4318a-110">**Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="4318a-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="4318a-111">**Serveur SQL Azure**: consultez [créer une base de données SQL Azure Bonjour Azure Portal] [ Create an Azure SQL database in hello Azure Portal] ou [créer une base de données SQL Azure avec PowerShell] [ Create an Azure SQL database with PowerShell] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4318a-111">**Azure SQL server**:  See [Create an Azure SQL database in hello Azure Portal][Create an Azure SQL database in hello Azure Portal] or [Create an Azure SQL database with PowerShell][Create an Azure SQL database with PowerShell] for more details.</span></span>
* <span data-ttu-id="4318a-112">**Groupe de ressources**: utilisez hello même ressource de groupe en tant que votre serveur SQL Azure, ou consultez [comment toocreate un groupe de ressources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4318a-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="4318a-113">**PowerShell version 1.0.3 ou supérieure** : vous pouvez vérifier la version en exécutant **Get-Module -ListAvailable -Name Azure**.</span><span class="sxs-lookup"><span data-stu-id="4318a-113">**PowerShell version 1.0.3 or greater**:  You can check your version by running **Get-Module -ListAvailable -Name Azure**.</span></span>  <span data-ttu-id="4318a-114">version la plus récente Hello peut être installée à partir de [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="4318a-114">hello latest version can be installed from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="4318a-115">Pour plus d’informations sur l’installation de version la plus récente hello, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="4318a-115">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

> [!NOTE]
> <span data-ttu-id="4318a-116">La création d’un entrepôt SQL Data Warehouse peut entraîner un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="4318a-116">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="4318a-117">Voir [Tarification de SQL Data Warehouse][SQL Data Warehouse pricing] pour plus d’informations sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="4318a-117">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="4318a-118">Créer un entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="4318a-118">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="4318a-119">Ouvrez Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4318a-119">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="4318a-120">Exécutez cette tooAzure de toologin d’applet de commande Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="4318a-120">Run this cmdlet toologin tooAzure Resource Manager.</span></span>

    ```Powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="4318a-121">Sélectionnez hello abonnement toouse pour votre session actuelle.</span><span class="sxs-lookup"><span data-stu-id="4318a-121">Select hello subscription you want toouse for your current session.</span></span>

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. <span data-ttu-id="4318a-122">Créez la base de données.</span><span class="sxs-lookup"><span data-stu-id="4318a-122">Create database.</span></span> <span data-ttu-id="4318a-123">Cet exemple crée une base de données nommée « mynewsqldw », avec un niveau objectif de service « DW400 », serveur toohello nommé « sqldwserver1 », qui se trouve dans le groupe de ressources hello nommé « mywesteuroperesgp1 ».</span><span class="sxs-lookup"><span data-stu-id="4318a-123">This example creates a database named "mynewsqldw", with service objective level "DW400", toohello server named "sqldwserver1", which is in hello resource group named "mywesteuroperesgp1".</span></span>

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

<span data-ttu-id="4318a-124">Les paramètres obligatoires sont :</span><span class="sxs-lookup"><span data-stu-id="4318a-124">Required Parameters are:</span></span>

* <span data-ttu-id="4318a-125">**RequestedServiceObjectiveName**: quantité de hello [DWU] [ DWU] vous demandez.</span><span class="sxs-lookup"><span data-stu-id="4318a-125">**RequestedServiceObjectiveName**: hello amount of [DWU][DWU] you are requesting.</span></span>  <span data-ttu-id="4318a-126">Les valeurs prises en charge sont les suivantes : DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 et DW6000.</span><span class="sxs-lookup"><span data-stu-id="4318a-126">Supported values are: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000, and DW6000.</span></span>
* <span data-ttu-id="4318a-127">**DatabaseName**: nom hello Hello SQL Data Warehouse que vous créez.</span><span class="sxs-lookup"><span data-stu-id="4318a-127">**DatabaseName**: hello name of hello SQL Data Warehouse that you are creating.</span></span>
* <span data-ttu-id="4318a-128">**Nom_serveur**: nom hello du serveur hello que vous utilisez pour la création (doit être le V12).</span><span class="sxs-lookup"><span data-stu-id="4318a-128">**ServerName**: hello name of hello server that you are using for creation (must be V12).</span></span>
* <span data-ttu-id="4318a-129">**ResourceGroupName**: groupe de ressources que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="4318a-129">**ResourceGroupName**: Resource group you are using.</span></span>  <span data-ttu-id="4318a-130">toofind des groupes de ressources disponibles dans votre abonnement utilisent Get-AzureResource.</span><span class="sxs-lookup"><span data-stu-id="4318a-130">toofind available resource groups in your subscription use Get-AzureResource.</span></span>
* <span data-ttu-id="4318a-131">**Édition**: doit être « Entrepôt de données » toocreate un entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="4318a-131">**Edition**: Must be "DataWarehouse" toocreate a SQL Data Warehouse.</span></span>

<span data-ttu-id="4318a-132">Les paramètres facultatifs sont :</span><span class="sxs-lookup"><span data-stu-id="4318a-132">Optional Parameters are:</span></span>

* <span data-ttu-id="4318a-133">**CollationName**: classement par défaut de hello si non spécifié est SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="4318a-133">**CollationName**: hello default collation if not specified is SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="4318a-134">Le classement ne peut pas être modifié sur une base de données.</span><span class="sxs-lookup"><span data-stu-id="4318a-134">Collation cannot be changed on a database.</span></span>
* <span data-ttu-id="4318a-135">**MaxSizeBytes**: taille maximale de hello par défaut d’une base de données est de 10 Go.</span><span class="sxs-lookup"><span data-stu-id="4318a-135">**MaxSizeBytes**: hello default max size of a database is 10 GB.</span></span>

<span data-ttu-id="4318a-136">Pour plus d’informations sur les options de paramètre hello, consultez [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] et [créer une base de données (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span><span class="sxs-lookup"><span data-stu-id="4318a-136">For more details on hello parameter options, see [New-AzureRmSqlDatabase][New-AzureRmSqlDatabase] and [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].</span></span>

## <a name="next-steps"></a><span data-ttu-id="4318a-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4318a-137">Next steps</span></span>
<span data-ttu-id="4318a-138">Une fois terminé votre entrepôt de données SQL de configuration vous souhaiterez peut-être tootry [le chargement des données d’exemple] [ loading sample data] ou extraire de façon trop[développer] [ develop] , [charger][load], ou [migrer][migrate].</span><span class="sxs-lookup"><span data-stu-id="4318a-138">After your SQL Data Warehouse has finished provisioning you may want tootry [loading sample data][loading sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<span data-ttu-id="4318a-139">Si vous êtes intéressé par plus d’informations sur la façon de toomanage SQL Data Warehouse par programme, consultez notre article sur la façon de toouse [applets de commande PowerShell et l’API REST][PowerShell cmdlets and REST APIs].</span><span class="sxs-lookup"><span data-stu-id="4318a-139">If you're interested in more on how toomanage SQL Data Warehouse programmatically, check out our article on how toouse [PowerShell cmdlets and REST APIs][PowerShell cmdlets and REST APIs].</span></span>

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
