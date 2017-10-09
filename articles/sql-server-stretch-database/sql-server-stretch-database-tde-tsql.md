---
title: "aaaEnable chiffrement Transparent des données pour Stretch TSQL de base de données - Azure | Documents Microsoft"
description: "Activer le chiffrement transparent des données (TDE) pour SQL Server Stretch Database sur Azure TSQL"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="3ce8b-103">Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="3ce8b-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ce8b-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="3ce8b-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="3ce8b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="3ce8b-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="3ce8b-106">Chiffrement transparent des données (TDE) vous aide à protéger contre les menaces hello d’activités malveillantes en effectuant le chiffrement en temps réel et le déchiffrement de la base de données de hello, les sauvegardes associées et les fichiers journaux des transactions au repos sans nécessiter de modifications toohello application.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="3ce8b-107">Stockage hello d’une base de données entière est chiffré à l’aide d’une clé de chiffrement de base de données hello appelée de clé symétrique.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="3ce8b-108">clé de chiffrement de base de données Hello est protégé par un certificat de serveur intégré.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="3ce8b-109">certificat de serveur intégré Hello est unique pour chaque serveur Azure.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="3ce8b-110">Microsoft alterne automatiquement ces certificats au moins tous les 90 jours.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="3ce8b-111">Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].</span><span class="sxs-lookup"><span data-stu-id="3ce8b-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="3ce8b-112">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="3ce8b-112">Enabling Encryption</span></span>
<span data-ttu-id="3ce8b-113">tooenable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="3ce8b-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="3ce8b-114">Se connecter toohello *master* base de données sur hello serveur Azure hébergement hello de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="3ce8b-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="3ce8b-115">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="3ce8b-116">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="3ce8b-116">Disabling Encryption</span></span>
<span data-ttu-id="3ce8b-117">toodisable chiffrement transparent des données pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="3ce8b-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="3ce8b-118">Se connecter toohello *master* de la base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="3ce8b-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="3ce8b-119">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="3ce8b-120">Vérification de chiffrement</span><span class="sxs-lookup"><span data-stu-id="3ce8b-120">Verifying Encryption</span></span>
<span data-ttu-id="3ce8b-121">état du chiffrement tooverify pour une base de données Azure stocke hello les données migrées à partir d’une base de données SQL Server compatible Stretch, hello suivant choses :</span><span class="sxs-lookup"><span data-stu-id="3ce8b-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="3ce8b-122">Se connecter toohello *master* ou instance de base de données à l’aide d’une connexion qui est un administrateur ou un membre de hello **dbmanager** rôle dans la base de données master hello</span><span class="sxs-lookup"><span data-stu-id="3ce8b-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="3ce8b-123">Exécutez hello suivant de base de données instruction tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="3ce8b-124">Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.</span><span class="sxs-lookup"><span data-stu-id="3ce8b-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
