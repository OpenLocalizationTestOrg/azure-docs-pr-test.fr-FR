---
title: Activer Transparent Data Encryption pour Stretch Database TSQL - Azure | Microsoft Docs
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
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="4358d-103">Activer le chiffrement transparent des données (TDE) pour Stretch Database sur Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="4358d-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4358d-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4358d-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="4358d-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="4358d-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="4358d-106">Le chiffrement transparent des données (Transparent Data Encryption, TDE) protège le système contre toute menace d’activité malveillante, en effectuant un chiffrement et un déchiffrement en temps réel de la base de données, des sauvegardes associées et des fichiers journaux de transactions au repos, sans qu’il soit nécessaire de modifier l’application.</span><span class="sxs-lookup"><span data-stu-id="4358d-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="4358d-107">Le chiffrement transparent des données chiffre le stockage d’une base de données entière à l’aide d’une clé symétrique appelée clé de chiffrement de base de données.</span><span class="sxs-lookup"><span data-stu-id="4358d-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="4358d-108">La clé de chiffrement de base de données est protégée par un certificat de serveur intégré.</span><span class="sxs-lookup"><span data-stu-id="4358d-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="4358d-109">Le certificat de serveur intégré est unique pour chaque serveur Azure.</span><span class="sxs-lookup"><span data-stu-id="4358d-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="4358d-110">Microsoft alterne automatiquement ces certificats au moins tous les 90 jours.</span><span class="sxs-lookup"><span data-stu-id="4358d-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="4358d-111">Pour obtenir une description générale du chiffrement transparent des données, consultez [Chiffrement transparent des données (TDE)].</span><span class="sxs-lookup"><span data-stu-id="4358d-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="4358d-112">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="4358d-112">Enabling Encryption</span></span>
<span data-ttu-id="4358d-113">Pour activer le chiffrement transparent des données pour une base de données Azure qui stocke les données migrées à partir d’une base de données SQL Server compatible avec Stretch, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4358d-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="4358d-114">Connectez-vous à la base de données *master* sur le serveur Azure hébergeant la base de données à l’aide d’identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="4358d-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="4358d-115">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="4358d-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="4358d-116">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="4358d-116">Disabling Encryption</span></span>
<span data-ttu-id="4358d-117">Pour désactiver le chiffrement transparent des données pour une base de données Azure qui stocke les données migrées à partir d’une base de données SQL Server compatible avec Stretch, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4358d-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="4358d-118">Connectez-vous à la base de données *master* à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="4358d-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="4358d-119">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="4358d-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="4358d-120">Vérification de chiffrement</span><span class="sxs-lookup"><span data-stu-id="4358d-120">Verifying Encryption</span></span>
<span data-ttu-id="4358d-121">Pour vérifier l’état de chiffrement d’une base de données Azure qui stocke les données migrées à partir d’une base de données SQL Server compatible avec Stretch, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4358d-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="4358d-122">Connectez-vous à la base de données *master* ou d’instance à l'aide d'identifiants de connexion administrateurs ou membres du rôle **dbmanager** dans la base de données master</span><span class="sxs-lookup"><span data-stu-id="4358d-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="4358d-123">Exécutez l'instruction suivante pour chiffrer la base de données.</span><span class="sxs-lookup"><span data-stu-id="4358d-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="4358d-124">Un résultat de ```1``` indique une base de données chiffrée, ```0``` indique une base de données non chiffrée.</span><span class="sxs-lookup"><span data-stu-id="4358d-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="4358d-125">[Chiffrement transparent des données (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="4358d-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
