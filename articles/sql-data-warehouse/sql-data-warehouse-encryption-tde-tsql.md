---
title: "aaaTransparent chiffrement des données dans l’entrepôt de données SQL (T-SQL) | Documents Microsoft"
description: "Chiffrement transparent des données (TDE) dans SQL Data Warehouse (T-SQL)"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="77ccc-103">Prise en main du chiffrement transparent des données (TDE)</span><span class="sxs-lookup"><span data-stu-id="77ccc-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77ccc-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="77ccc-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="77ccc-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="77ccc-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="77ccc-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="77ccc-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="77ccc-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="77ccc-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="77ccc-108">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="77ccc-108">Required Permssions</span></span>
<span data-ttu-id="77ccc-109">tooenable Transparent Data Encryption (TDE), vous devez être un administrateur ou un membre du rôle dbmanager de hello.</span><span class="sxs-lookup"><span data-stu-id="77ccc-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="77ccc-110">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="77ccc-110">Enabling Encryption</span></span>
<span data-ttu-id="77ccc-111">Suivez ces étapes de tooenable chiffrement transparent des données d’un entrepôt de données SQL :</span><span class="sxs-lookup"><span data-stu-id="77ccc-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="77ccc-112">Se connecter toohello *master* base de données serveur hello hébergeant hello de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="77ccc-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="77ccc-113">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="77ccc-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="77ccc-114">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="77ccc-114">Disabling Encryption</span></span>
<span data-ttu-id="77ccc-115">Suivez ces étapes de toodisable chiffrement transparent des données d’un entrepôt de données SQL :</span><span class="sxs-lookup"><span data-stu-id="77ccc-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="77ccc-116">Se connecter toohello *master* de la base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="77ccc-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="77ccc-117">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="77ccc-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="77ccc-118">Un entrepôt de données SQL en pause doit être repris avant d’apporter des modifications des paramètres de TDE toohello.</span><span class="sxs-lookup"><span data-stu-id="77ccc-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="77ccc-119">Vérification de chiffrement</span><span class="sxs-lookup"><span data-stu-id="77ccc-119">Verifying Encryption</span></span>
<span data-ttu-id="77ccc-120">état du chiffrement tooverify pour un entrepôt de données SQL, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="77ccc-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="77ccc-121">Se connecter toohello *master* ou instance de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="77ccc-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="77ccc-122">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="77ccc-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="77ccc-123">Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.</span><span class="sxs-lookup"><span data-stu-id="77ccc-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="77ccc-124">DMV de chiffrement</span><span class="sxs-lookup"><span data-stu-id="77ccc-124">Encryption DMVs</span></span>
* <span data-ttu-id="77ccc-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="77ccc-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="77ccc-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="77ccc-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
