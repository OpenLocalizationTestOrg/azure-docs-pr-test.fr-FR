---
title: "aaaManage de calcul power dans l’entrepôt de données SQL Azure (PowerShell) | Documents Microsoft"
description: "PowerShell tâches toomanage une puissance de calcul. Mettez à l’échelle les ressources de calcul en ajustant les unités DWU. Ou bien, suspendre et reprendre des coûts toosave des ressources de calcul."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 8354a3c1-4e04-4809-933f-db414a8c74dc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 8b379d4cf89570649767f6896d2c630d4f1111d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="8b81b-105">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="8b81b-105">Manage compute power in Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b81b-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8b81b-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="8b81b-107">Portail</span><span class="sxs-lookup"><span data-stu-id="8b81b-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="8b81b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b81b-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="8b81b-109">REST</span><span class="sxs-lookup"><span data-stu-id="8b81b-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="8b81b-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="8b81b-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

## <a name="before-you-begin"></a><span data-ttu-id="8b81b-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8b81b-111">Before you begin</span></span>
### <a name="install-hello-latest-version-of-azure-powershell"></a><span data-ttu-id="8b81b-112">Installer la version la plus récente d’Azure PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="8b81b-112">Install hello latest version of Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="8b81b-113">toouse Azure PowerShell avec l’entrepôt de données SQL, vous avez besoin d’Azure PowerShell version 1.0.3 ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="8b81b-113">toouse Azure PowerShell with SQL Data Warehouse, you need Azure PowerShell version 1.0.3 or greater.</span></span>  <span data-ttu-id="8b81b-114">exécution de votre version actuelle de tooverify commande hello **Get-Module - ListAvailable-nom Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b81b-114">tooverify your current version run hello command **Get-Module -ListAvailable -Name Azure**.</span></span> <span data-ttu-id="8b81b-115">Vous pouvez installer la version la plus récente à partir de hello [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="8b81b-115">You can install hello latest version from [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="8b81b-116">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="8b81b-116">For more information, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>
>
> 

### <a name="get-started-with-azure-powershell-cmdlets"></a><span data-ttu-id="8b81b-117">Prise en main des applets de commande Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b81b-117">Get started with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="8b81b-118">tooget démarré :</span><span class="sxs-lookup"><span data-stu-id="8b81b-118">tooget started:</span></span>

1. <span data-ttu-id="8b81b-119">Ouvrez Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b81b-119">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="8b81b-120">À l’invite de PowerShell hello, exécutez toosign de ces commandes dans toohello Azure Resource Manager et sélectionnez votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b81b-120">At hello PowerShell prompt, run these commands toosign in toohello Azure Resource Manager and select your subscription.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="8b81b-121">Mise à l’échelle de la puissance de calcul</span><span class="sxs-lookup"><span data-stu-id="8b81b-121">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="8b81b-122">toochange hello Dwu, utilisez hello [Set-AzureRmSqlDatabase] [ Set-AzureRmSqlDatabase] applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8b81b-122">toochange hello DWUs, use hello [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase] PowerShell cmdlet.</span></span> <span data-ttu-id="8b81b-123">Hello exemple suivant définit hello service niveau objectif tooDW1000 pour la base de données de hello MySQLDW qui est hébergé sur le serveur monserveur.</span><span class="sxs-lookup"><span data-stu-id="8b81b-123">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span>

```Powershell
Set-AzureRmSqlDatabase -DatabaseName "MySQLDW" -ServerName "MyServer" -RequestedServiceObjectiveName "DW1000"
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="8b81b-124">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="8b81b-124">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="8b81b-125">toopause une base de données, utilisez hello [Suspend-AzureRmSqlDatabase] [ Suspend-AzureRmSqlDatabase] applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8b81b-125">toopause a database, use hello [Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8b81b-126">Hello exemple suivant suspend une base de données appelé base de données02 hébergé sur un serveur nommé Server01.</span><span class="sxs-lookup"><span data-stu-id="8b81b-126">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8b81b-127">serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="8b81b-127">hello server is in an Azure resource group named ResourceGroup1.</span></span>

> [!NOTE]
> <span data-ttu-id="8b81b-128">Notez que si votre serveur est foo.database.windows.net, utilisez « foo » comme hello - nom du serveur dans les applets de commande PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8b81b-128">Note that if your server is foo.database.windows.net, use "foo" as hello -ServerName in hello PowerShell cmdlets.</span></span>
>
> 

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
```
<span data-ttu-id="8b81b-129">Une variation, l’exemple suivant récupère la base de données hello en objet de hello $database.</span><span class="sxs-lookup"><span data-stu-id="8b81b-129">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8b81b-130">Elle redirige ensuite les objets hello trop[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span><span class="sxs-lookup"><span data-stu-id="8b81b-130">It then pipes hello object too[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].</span></span> <span data-ttu-id="8b81b-131">résultats de Hello sont stockés dans resultDatabase d’objet hello.</span><span class="sxs-lookup"><span data-stu-id="8b81b-131">hello results are stored in hello object resultDatabase.</span></span> <span data-ttu-id="8b81b-132">commande finale Hello montre les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="8b81b-132">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="8b81b-133">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="8b81b-133">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="8b81b-134">toostart une base de données, utilisez hello [Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] applet de commande.</span><span class="sxs-lookup"><span data-stu-id="8b81b-134">toostart a database, use hello [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] cmdlet.</span></span> <span data-ttu-id="8b81b-135">Hello exemple suivant démarre une base de données appelé base de données02 hébergé sur un serveur nommé Server01.</span><span class="sxs-lookup"><span data-stu-id="8b81b-135">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="8b81b-136">serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="8b81b-136">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" -DatabaseName "Database02"
```

<span data-ttu-id="8b81b-137">Une variation, l’exemple suivant récupère la base de données hello en objet de hello $database.</span><span class="sxs-lookup"><span data-stu-id="8b81b-137">A variation, this next example retrieves hello database into hello $database object.</span></span> <span data-ttu-id="8b81b-138">Elle redirige ensuite les objets hello trop[Resume-AzureRmSqlDatabase] [ Resume-AzureRmSqlDatabase] et stocke les résultats de hello dans $resultDatabase.</span><span class="sxs-lookup"><span data-stu-id="8b81b-138">It then pipes hello object too[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase] and stores hello results in $resultDatabase.</span></span> <span data-ttu-id="8b81b-139">commande finale Hello montre les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="8b81b-139">hello final command shows hello results.</span></span>

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" `
–ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
$resultDatabase
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state"></a><span data-ttu-id="8b81b-140">Vérifier l’état de base de données</span><span class="sxs-lookup"><span data-stu-id="8b81b-140">Check database state</span></span>

<span data-ttu-id="8b81b-141">Comme indiqué dans hello exemples ci-dessus, un utilisateur peut employer [Get-AzureRmSqlDatabase] [ Get-AzureRmSqlDatabase] applet de commande tooget plus d’informations sur une base de données, ainsi la vérification hello l’état, mais également toouse en tant qu’argument.</span><span class="sxs-lookup"><span data-stu-id="8b81b-141">As shown in hello above examples, one can use [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase] cmdlet tooget information on a database, thereby checking hello status, but also toouse as an argument.</span></span> 

```powershell
Get-AzureRmSqlDatabase [-ResourceGroupName] <String> [-ServerName] <String> [[-DatabaseName] <String>]
 [-InformationAction <ActionPreference>] [-InformationVariable <String>] [-Confirm] [-WhatIf]
 [<CommonParameters>]
```

<span data-ttu-id="8b81b-142">De qui donnera quelque chose comme ceci</span><span class="sxs-lookup"><span data-stu-id="8b81b-142">Which will result in something like</span></span> 

```powershell   
ResourceGroupName             : nytrg
ServerName                    : nytsvr
DatabaseName                  : nytdb
Location                      : West US
DatabaseId                    : 86461aae-8e3d-4ded-9389-ac9d4bc69bbb
Edition                       : DataWarehouse
CollationName                 : SQL_Latin1General_CP1CI_AS
CatalogCollation              :
MaxSizeBytes                  : 32212254720
Status                        : Online
CreationDate                  : 10/26/2016 4:33:14 PM
CurrentServiceObjectiveId     : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
CurrentServiceObjectiveName   : System2
RequestedServiceObjectiveId   : 620323bf-2879-4807-b30d-c2e6d7b3b3aa
RequestedServiceObjectiveName :
ElasticPoolName               :
EarliestRestoreDate           : 1/1/0001 12:00:00 AM
```

<span data-ttu-id="8b81b-143">Où vous pouvez ensuite vérifier toosee hello *état* de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="8b81b-143">Where you can then check toosee hello *Status* of hello database.</span></span> <span data-ttu-id="8b81b-144">Dans ce cas, vous pouvez voir que la base de données est en ligne.</span><span class="sxs-lookup"><span data-stu-id="8b81b-144">In this case, you can see that this database is online.</span></span> 

<span data-ttu-id="8b81b-145">Lorsque vous exécutez cette commande, vous devriez recevoir une valeur d’état En ligne, Suspension, Reprise, Mise à l’échelle ou Suspendu.</span><span class="sxs-lookup"><span data-stu-id="8b81b-145">When you run this command, you should receive a Status value of either Online, Pausing, Resuming, Scaling, and Paused.</span></span>

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="8b81b-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b81b-146">Next steps</span></span>
<span data-ttu-id="8b81b-147">Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="8b81b-147">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Get-AzureRmSqlDatabase]: /powershell/servicemanagement/azure.sqldatabase/v1.6.1/get-azuresqldatabase

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[Azure portal]: http://portal.azure.com/
