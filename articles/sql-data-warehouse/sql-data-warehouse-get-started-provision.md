---
title: "Création d’un entrepôt SQL Data Warehouse dans le portail Azure | Microsoft Docs"
description: "Découvrez comment créer un entrepôt de données Azure SQL Data Warehouse dans le portail Azure"
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
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="9fbc1-103">Créer un Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9fbc1-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fbc1-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9fbc1-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="9fbc1-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="9fbc1-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="9fbc1-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fbc1-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="9fbc1-107">Ce didacticiel fait appel au portail Azure pour créer un entrepôt de données SQL Data Warehouse qui contient un exemple de base de données AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fbc1-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9fbc1-108">Prerequisites</span></span>
<span data-ttu-id="9fbc1-109">Pour commencer, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9fbc1-109">To get started, you need:</span></span>

* <span data-ttu-id="9fbc1-110">**Compte Azure** : consultez [Évaluation gratuite d’Azure][Azure Free Trial] ou [Crédits Azure MSDN][MSDN Azure Credits] pour créer un compte.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="9fbc1-111">**Serveur SQL Azure** : pour en savoir plus, consultez [Create and query a single Azure SQL database in the Azure portal][Create an Azure SQL database in the Azure portal] (Créer et interroger une base de données SQL Azure unique dans le portail Azure).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="9fbc1-112">La création d’un entrepôt de données SQL Data Warehouse peut donner lieu à un nouveau service facturable.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="9fbc1-113">Pour plus d’informations sur la tarification, consultez la page [SQL Data Warehouse Tarification][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="9fbc1-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="9fbc1-114">Créer un entrepôt de données SQL</span><span class="sxs-lookup"><span data-stu-id="9fbc1-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="9fbc1-115">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9fbc1-116">Cliquez sur **+Nouveau** > **Bases de données** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Créer](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="9fbc1-118">Dans le panneau **SQL Data Warehouse** , fournissez les informations nécessaires, puis appuyez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="9fbc1-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Création d’une base de données](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="9fbc1-120">**Serveur**: nous vous recommandons de commencer par sélectionner votre serveur.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="9fbc1-121">**Nom de la base de données**: nom servant à référencer l’entrepôt de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="9fbc1-122">Le nom doit être unique sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="9fbc1-123">**Performances** : nous vous recommandons de commencer par 400 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="9fbc1-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="9fbc1-124">Vous pouvez déplacer le curseur vers la gauche ou la droite pour ajuster les performances de votre entrepôt de données, ou le faire monter ou descendre en puissance suivant la création.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="9fbc1-125">Pour en savoir plus sur les DWU, consultez notre documentation sur la [montée en charge](sql-data-warehouse-manage-compute-overview.md) ou notre [page de tarification][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="9fbc1-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="9fbc1-126">**Abonnement**: sélectionnez [l’abonnement] à utiliser pour la facturation de cet entrepôt de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="9fbc1-127">**Groupe de ressources** : un [groupe de ressources][Resource group] est un conteneur conçu pour vous aider à gérer une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="9fbc1-128">En savoir plus sur les [groupes de ressources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="9fbc1-129">**Sélectionner une source** : cliquez sur **Sélectionner une source** > **Exemple**.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="9fbc1-130">Azure renseigne automatiquement AdventureWorksDW dans l’option **Sélectionner un exemple** .</span><span class="sxs-lookup"><span data-stu-id="9fbc1-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9fbc1-131">Le classement par défaut pour un entrepôt SQL Data Warehouse est SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="9fbc1-132">Si vous avez besoin d’un classement différent, [T-SQL][T-SQL] permet de créer la base de données avec un autre classement.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="9fbc1-133">Cliquez sur **Créer** pour créer votre entrepôt de données SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="9fbc1-134">Patientez quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-134">Wait for a few minutes.</span></span> <span data-ttu-id="9fbc1-135">Une fois que votre entrepôt de données est prêt, vous devriez être redirigé vers le [Portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9fbc1-136">Vous pouvez trouver votre SQL Data Warehouse sur votre tableau de bord, répertorié sous vos bases de données SQL, ou dans le groupe de ressources que vous avez utilisé pour le créer.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![vue du portail](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="9fbc1-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9fbc1-138">Next steps</span></span>
<span data-ttu-id="9fbc1-139">Maintenant que vous avez créé un entrepôt de données SQL Data Warehouse, vous êtes prêt à vous [connecter](sql-data-warehouse-connect-overview.md) et à lancer des requêtes.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="9fbc1-140">Pour consulter une vue d’ensemble sur le chargement, accédez à la rubrique [Chargement de données dans SQL Data Warehouse](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="9fbc1-141">Si vous tentez de migrer une base de données existante vers SQL Data Warehouse, consultez la [vue d’ensemble de la migration](sql-data-warehouse-overview-migrate.md) ou utilisez [l’utilitaire de migration](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="9fbc1-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="9fbc1-142">Les règles de pare-feu peuvent également être configurées à l’aide de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="9fbc1-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="9fbc1-143">Pour plus d’informations, consultez [sp_set_firewall_rule][sp_set_firewall_rule] et [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="9fbc1-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="9fbc1-144">Nous vous recommandons également de prendre connaissance des [bonnes pratiques][Best practices].</span><span class="sxs-lookup"><span data-stu-id="9fbc1-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="9fbc1-145">[l’abonnement]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="9fbc1-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
