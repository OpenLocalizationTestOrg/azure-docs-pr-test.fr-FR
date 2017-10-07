---
title: "aaaPause, reprendre, mettre à l’échelle avec reste dans l’entrepôt de données SQL Azure | Documents Microsoft"
description: "Gérez la puissance de calcul dans SQL Data Warehouse via REST, T-SQL et PowerShell."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="d31d8-103">Gestion de la puissance de calcul dans Azure SQL Data Warehouse (REST)</span><span class="sxs-lookup"><span data-stu-id="d31d8-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d31d8-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d31d8-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="d31d8-105">Portail</span><span class="sxs-lookup"><span data-stu-id="d31d8-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="d31d8-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d31d8-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="d31d8-107">REST</span><span class="sxs-lookup"><span data-stu-id="d31d8-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="d31d8-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="d31d8-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="d31d8-109">Mise à l’échelle de la puissance de calcul</span><span class="sxs-lookup"><span data-stu-id="d31d8-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="d31d8-110">toochange hello Dwu, utilisez hello [créer ou mettre à jour la base de données] [ Create or Update Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="d31d8-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="d31d8-111">Hello exemple suivant définit hello service niveau objectif tooDW1000 pour la base de données de hello MySQLDW qui est hébergé sur le serveur monserveur.</span><span class="sxs-lookup"><span data-stu-id="d31d8-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="d31d8-112">serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="d31d8-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="d31d8-113">Suspension du calcul</span><span class="sxs-lookup"><span data-stu-id="d31d8-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="d31d8-114">toopause une base de données, utilisez hello [base de données de la Pause] [ Pause Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="d31d8-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="d31d8-115">Hello exemple suivant suspend une base de données appelé base de données02 hébergé sur un serveur nommé Server01.</span><span class="sxs-lookup"><span data-stu-id="d31d8-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="d31d8-116">serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="d31d8-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="d31d8-117">Reprise du calcul</span><span class="sxs-lookup"><span data-stu-id="d31d8-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="d31d8-118">toostart une base de données, utilisez hello [reprendre la base de données] [ Resume Database] API REST.</span><span class="sxs-lookup"><span data-stu-id="d31d8-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="d31d8-119">Hello exemple suivant démarre une base de données appelé base de données02 hébergé sur un serveur nommé Server01.</span><span class="sxs-lookup"><span data-stu-id="d31d8-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="d31d8-120">serveur de Hello est dans un groupe de ressources Azure nommé ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="d31d8-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="d31d8-121">Vérifier l’état de base de données</span><span class="sxs-lookup"><span data-stu-id="d31d8-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="d31d8-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d31d8-122">Next steps</span></span>
<span data-ttu-id="d31d8-123">Pour d’autres tâches de gestion, consultez la rubrique [Vue d’ensemble du système de gestion][Management overview].</span><span class="sxs-lookup"><span data-stu-id="d31d8-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/