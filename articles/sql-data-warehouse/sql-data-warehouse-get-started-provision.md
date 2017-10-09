---
title: "aaaCreate un entrepôt de données SQL dans hello portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate un entrepôt de données SQL Azure dans hello portail Azure"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="7eb09-103">Créer un Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7eb09-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7eb09-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="7eb09-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="7eb09-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="7eb09-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="7eb09-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7eb09-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="7eb09-107">Ce didacticiel utilise hello toocreate portail Azure SQL Data Warehouse qui contient une base de données exemple AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7eb09-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7eb09-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7eb09-108">Prerequisites</span></span>
<span data-ttu-id="7eb09-109">tooget démarré, vous devez :</span><span class="sxs-lookup"><span data-stu-id="7eb09-109">tooget started, you need:</span></span>

* <span data-ttu-id="7eb09-110">**Compte Azure**: visitez [d’évaluation gratuite Azure] [ Azure Free Trial] ou [des crédits Azure MSDN] [ MSDN Azure Credits] toocreate un compte.</span><span class="sxs-lookup"><span data-stu-id="7eb09-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="7eb09-111">**Serveur SQL Azure**: consultez [créer une base de données SQL Azure avec hello portail Azure] [ Create an Azure SQL database in hello Azure portal] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7eb09-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="7eb09-112">La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="7eb09-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="7eb09-113">Pour plus d’informations sur la tarification, consultez la page [SQL Data Warehouse Tarification][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="7eb09-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="7eb09-114">Créer un entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="7eb09-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="7eb09-115">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7eb09-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7eb09-116">Cliquez sur **+Nouveau** > **Bases de données** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="7eb09-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Créer](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="7eb09-118">Bonjour **SQL Data Warehouse** panneau, renseignez les informations de hello nécessaires, puis appuyez sur 'Create' toocreate.</span><span class="sxs-lookup"><span data-stu-id="7eb09-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Création d’une base de données](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="7eb09-120">**Serveur**: nous vous recommandons de commencer par sélectionner votre serveur.</span><span class="sxs-lookup"><span data-stu-id="7eb09-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="7eb09-121">**Nom de la base de données**: nom de hello est utilisé tooreference hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7eb09-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="7eb09-122">Il doit être unique toohello server.</span><span class="sxs-lookup"><span data-stu-id="7eb09-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="7eb09-123">**Performances** : nous vous recommandons de commencer par 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="7eb09-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="7eb09-124">Vous pouvez déplacer hello toohello de curseur gauche ou avec le bouton droit tooadjust les performances de hello de votre entrepôt de données, ou de mise à l’échelle vers le haut ou vers le bas après sa création.</span><span class="sxs-lookup"><span data-stu-id="7eb09-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="7eb09-125">toolearn en savoir plus sur les Dwu, reportez-vous à notre documentation sur [mise à l’échelle](sql-data-warehouse-manage-compute-overview.md) ou notre [page de tarification][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="7eb09-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="7eb09-126">**Abonnement**: hello sélectionnez [abonnement] qui sera facturation cet entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7eb09-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="7eb09-127">**Groupe de ressources**: [groupes de ressources] [ Resource group] sont toohelp conteneurs conçues vous gérez une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb09-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="7eb09-128">En savoir plus sur les [groupes de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7eb09-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="7eb09-129">**Sélectionner une source** : cliquez sur **Sélectionner une source** > **Exemple**.</span><span class="sxs-lookup"><span data-stu-id="7eb09-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="7eb09-130">Azure remplit automatiquement hello **sélectionnez exemple** option avec AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="7eb09-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7eb09-131">classement par défaut de Hello pour un entrepôt de données SQL est SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="7eb09-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="7eb09-132">Si un classement différent est nécessaire, [T-SQL] [ T-SQL] peuvent être utilisés toocreate hello avec un classement différent.</span><span class="sxs-lookup"><span data-stu-id="7eb09-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="7eb09-133">Cliquez sur **créer** toocreate votre SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7eb09-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="7eb09-134">Patientez quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7eb09-134">Wait for a few minutes.</span></span> <span data-ttu-id="7eb09-135">Lorsque votre entrepôt de données est prête, vous devez être retournée toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7eb09-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7eb09-136">Vous pouvez trouver votre entrepôt de données SQL sur votre tableau de bord, conformément à vos bases de données SQL, ou dans la ressource de hello groupe que vous avez utilisé toocreate il.</span><span class="sxs-lookup"><span data-stu-id="7eb09-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![vue du portail](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="7eb09-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7eb09-138">Next steps</span></span>
<span data-ttu-id="7eb09-139">Maintenant que vous avez créé un entrepôt de données SQL, vous êtes prêt trop[Connect](sql-data-warehouse-connect-overview.md) et procéder à l’interrogation.</span><span class="sxs-lookup"><span data-stu-id="7eb09-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="7eb09-140">données tooload dans l’entrepôt de données SQL, consultez hello [vue d’ensemble de chargement](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="7eb09-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="7eb09-141">Si vous essayez de toomigrate un tooSQL existant de la base de données l’entrepôt de données, consultez hello [présentation de la Migration](sql-data-warehouse-overview-migrate.md) ou utilisez [l’utilitaire de Migration](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="7eb09-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="7eb09-142">Les règles de pare-feu peuvent également être configurées à l’aide de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="7eb09-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="7eb09-143">Pour plus d’informations, consultez [sp_set_firewall_rule][sp_set_firewall_rule] et [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="7eb09-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="7eb09-144">Il est également un toolook idée à hello [meilleures pratiques][Best practices].</span><span class="sxs-lookup"><span data-stu-id="7eb09-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[abonnement]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
