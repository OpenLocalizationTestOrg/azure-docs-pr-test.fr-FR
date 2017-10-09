---
title: "aaaTransparent chiffrement des données dans l’entrepôt de données SQL (portail) | Documents Microsoft"
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
ms.openlocfilehash: 8233886ecf170844104e0d1459e2a829cafa9b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde-in-sql-data-warehouse"></a><span data-ttu-id="160ba-103">Mise en route avec le chiffrement transparent des données (TDE) dans SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="160ba-103">Get started with Transparent Data Encryption (TDE) in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="160ba-104">Présentation de la sécurité</span><span class="sxs-lookup"><span data-stu-id="160ba-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="160ba-105">Authentification</span><span class="sxs-lookup"><span data-stu-id="160ba-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="160ba-106">Chiffrement (portail)</span><span class="sxs-lookup"><span data-stu-id="160ba-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="160ba-107">Chiffrement (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="160ba-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="160ba-108">Autorisations requises</span><span class="sxs-lookup"><span data-stu-id="160ba-108">Required Permssions</span></span>
<span data-ttu-id="160ba-109">tooenable Transparent Data Encryption (TDE), vous devez être un administrateur ou un membre du rôle dbmanager de hello.</span><span class="sxs-lookup"><span data-stu-id="160ba-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="160ba-110">Activation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="160ba-110">Enabling Encryption</span></span>
<span data-ttu-id="160ba-111">tooenable chiffrement transparent des données d’un entrepôt de données SQL, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="160ba-111">tooenable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="160ba-112">Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="160ba-112">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="160ba-113">Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton</span><span class="sxs-lookup"><span data-stu-id="160ba-113">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="160ba-114">Sélectionnez hello **chiffrement Transparent des données** option![][1]</span><span class="sxs-lookup"><span data-stu-id="160ba-114">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="160ba-115">Sélectionnez hello **sur** paramètre![][2]</span><span class="sxs-lookup"><span data-stu-id="160ba-115">Select hello **On** setting ![][2]</span></span>
5. <span data-ttu-id="160ba-116">Sélectionnez **Enregistrer**
   ![][3]</span><span class="sxs-lookup"><span data-stu-id="160ba-116">Select **Save**
![][3]</span></span>  

## <a name="disabling-encryption"></a><span data-ttu-id="160ba-117">Désactivation du chiffrement</span><span class="sxs-lookup"><span data-stu-id="160ba-117">Disabling Encryption</span></span>
<span data-ttu-id="160ba-118">toodisable chiffrement transparent des données d’un entrepôt de données SQL, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="160ba-118">toodisable TDE for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="160ba-119">Base de données ouverte hello Bonjour [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="160ba-119">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="160ba-120">Dans le panneau de la base de données hello, cliquez sur hello **paramètres** bouton</span><span class="sxs-lookup"><span data-stu-id="160ba-120">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="160ba-121">Sélectionnez hello **chiffrement Transparent des données** option![][1]</span><span class="sxs-lookup"><span data-stu-id="160ba-121">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="160ba-122">Sélectionnez hello **hors** paramètre![][4]</span><span class="sxs-lookup"><span data-stu-id="160ba-122">Select hello **Off** setting ![][4]</span></span>
5. <span data-ttu-id="160ba-123">Sélectionnez **Enregistrer**
   ![][5]</span><span class="sxs-lookup"><span data-stu-id="160ba-123">Select **Save**
![][5]</span></span>  

## <a name="encryption-dmvs"></a><span data-ttu-id="160ba-124">DMV de chiffrement</span><span class="sxs-lookup"><span data-stu-id="160ba-124">Encryption DMVs</span></span>
<span data-ttu-id="160ba-125">Le chiffrement peut être confirmé par hello suivant des vues de gestion dynamique :</span><span class="sxs-lookup"><span data-stu-id="160ba-125">Encryption can be confirmed with hello following DMVs:</span></span>

* <span data-ttu-id="160ba-126">[sys.databases]</span><span class="sxs-lookup"><span data-stu-id="160ba-126">[sys.databases]</span></span>
* <span data-ttu-id="160ba-127">[sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="160ba-127">[sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--MSDN references-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings.png
[2]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-on.png
[3]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save.png
[4]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-off.png
[5]: ./media/sql-data-warehouse-security-tde/sql-data-warehouse-security-tde-portal-settings-save2.png

<!--Link references-->
