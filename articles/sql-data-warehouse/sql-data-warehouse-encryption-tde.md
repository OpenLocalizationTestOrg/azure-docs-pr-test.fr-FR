---
title: "Chiffrement transparent des données dans SQL Data Warehouse (portail) | Microsoft Docs"
description: "Chiffrement transparent des données (TDE) dans SQL Data Warehouse"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: fabf75d3-9bbf-4e0d-9b31-8b5a8713f08d
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: b1db3bdfdfb54bda325c9b971cfcb4dd5efa333a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="ad324-103">Mise en route avec le chiffrement transparent des données (TDE) dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ad324-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ad324-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="ad324-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="ad324-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="ad324-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="ad324-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="ad324-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="ad324-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="ad324-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="ad324-108">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="ad324-108">Required Permssions</span></span>
<span data-ttu-id="ad324-109">Pour activer le chiffrement transparent des données (TDE), vous devez être un administrateur ou un membre du rôle dbmanager.</span><span class="sxs-lookup"><span data-stu-id="ad324-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ad324-110">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="ad324-110">Enabling Encryption</span></span>
<span data-ttu-id="ad324-111">Pour activer le chiffrement transparent des données pour SQL Data Warehouse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad324-111">To enable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="ad324-112">Ouvrez la base de données dans le [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ad324-112">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ad324-113">Dans le panneau de la base de données, cliquez sur le bouton **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="ad324-113">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="ad324-114">Sélectionnez l’option **Chiffrement transparent des données**![][1]</span><span class="sxs-lookup"><span data-stu-id="ad324-114">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="ad324-115">Sélectionnez le paramètre **Activé** ![][2]</span><span class="sxs-lookup"><span data-stu-id="ad324-115">Select the **On** setting ![][2]</span></span>
5. <span data-ttu-id="ad324-116">Sélectionnez **Enregistrer**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="ad324-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="ad324-117">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="ad324-117">Disabling Encryption</span></span>
<span data-ttu-id="ad324-118">Pour désactiver le chiffrement transparent des données pour SQL Data Warehouse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad324-118">To disable TDE for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="ad324-119">Ouvrez la base de données dans le [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ad324-119">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ad324-120">Dans le panneau de la base de données, cliquez sur le bouton **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="ad324-120">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="ad324-121">Sélectionnez l’option **Chiffrement transparent des données**![][1]</span><span class="sxs-lookup"><span data-stu-id="ad324-121">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="ad324-122">Sélectionnez le paramètre **Désactivé** ![][4]</span><span class="sxs-lookup"><span data-stu-id="ad324-122">Select the **Off** setting ![][4]</span></span>
5. <span data-ttu-id="ad324-123">Sélectionnez **Enregistrer**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="ad324-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="ad324-124">DMV de chiffrement</span><span class="sxs-lookup"><span data-stu-id="ad324-124">Encryption DMVs</span></span>
<span data-ttu-id="ad324-125">Le chiffrement peut être vérifié avec les vues DMV suivantes :</span><span class="sxs-lookup"><span data-stu-id="ad324-125">Encryption can be confirmed with the following DMVs:</span></span>

* <span data-ttu-id="ad324-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="ad324-126">[sys.databases]</span></span>
* <span data-ttu-id="ad324-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="ad324-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
<span data-ttu-id="ad324-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span><span class="sxs-lookup"><span data-stu-id="ad324-128">[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx</span></span>
<span data-ttu-id="ad324-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span><span class="sxs-lookup"><span data-stu-id="ad324-129">[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
