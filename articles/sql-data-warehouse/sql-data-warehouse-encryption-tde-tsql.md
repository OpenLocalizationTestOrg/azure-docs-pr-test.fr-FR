---
title: Transparent Data Encryption dans SQL Data Warehouse (T-SQL)| Microsoft Docs
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="37e95-103">Prise en main du chiffrement transparent des données (TDE)</span><span class="sxs-lookup"><span data-stu-id="37e95-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37e95-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="37e95-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="37e95-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="37e95-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="37e95-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="37e95-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="37e95-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="37e95-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="37e95-108">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="37e95-108">Required Permssions</span></span>
<span data-ttu-id="37e95-109">Pour activer le chiffrement transparent des données (TDE), vous devez être un administrateur ou un membre du rôle dbmanager.</span><span class="sxs-lookup"><span data-stu-id="37e95-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="37e95-110">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="37e95-110">Enabling Encryption</span></span>
<span data-ttu-id="37e95-111">Pour activer le chiffrement transparent des données pour une instance SQL Data Warehouse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e95-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="37e95-112">Connectez-vous à la base de données *master* sur le serveur hébergeant la base de données à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="37e95-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="37e95-113">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="37e95-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="37e95-114">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="37e95-114">Disabling Encryption</span></span>
<span data-ttu-id="37e95-115">Pour désactiver le chiffrement transparent des données pour une instance SQL Data Warehouse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e95-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="37e95-116">Connectez-vous à la base de données *master* à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="37e95-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="37e95-117">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="37e95-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="37e95-118">Une instance SQL Data Warehouse suspendue doit reprendre avant que des modifications ne puissent être apportées aux paramètres de chiffrement transparent des données.</span><span class="sxs-lookup"><span data-stu-id="37e95-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="37e95-119">Vérification de chiffrement</span><span class="sxs-lookup"><span data-stu-id="37e95-119">Verifying Encryption</span></span>
<span data-ttu-id="37e95-120">Pour vérifier l’état du chiffrement pour SQL Data Warehouse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37e95-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="37e95-121">Connectez-vous à la base de données *master* ou d’instance à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="37e95-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="37e95-122">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="37e95-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="37e95-123">Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.</span><span class="sxs-lookup"><span data-stu-id="37e95-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="37e95-124">DMV de chiffrement</span><span class="sxs-lookup"><span data-stu-id="37e95-124">Encryption DMVs</span></span>
* <span data-ttu-id="37e95-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="37e95-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="37e95-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="37e95-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
