---
title: "Portail Azure : Créer et gérer un pool élastique SQL Database | Microsoft Docs"
description: "Découvrez comment toouse hello portail Azure et toomanage intelligence intégrée de la base de données SQL, analyse et redimensionner un performances de base de données évolutive pool élastique toooptimize et gérer les coûts."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="9afb3-103">Créer et gérer un pool élastique hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9afb3-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="9afb3-104">Cette rubrique vous montre comment toocreate et gérer évolutive [pools élastiques](sql-database-elastic-pool.md) avec hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9afb3-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="9afb3-105">Vous pouvez également créer et gérer un pool élastique Azure [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello API REST, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="9afb3-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="9afb3-107">Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-107">Create an elastic pool</span></span> 

<span data-ttu-id="9afb3-108">Vous pouvez créer un pool élastique de deux façons.</span><span class="sxs-lookup"><span data-stu-id="9afb3-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="9afb3-109">Vous pouvez le faire à partir de zéro si vous savez que le programme d’installation de hello pool que vous voulez, ou commencer par la recommandation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="9afb3-110">Base de données SQL a une intelligence intégrée qui recommande une configuration de pool élastique, s’il est plus économique en fonction de hello au-delà de télémétrie d’utilisation pour vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="9afb3-111">Vous pouvez créer plusieurs pools sur un serveur, mais vous ne pouvez ajouter des bases de données à partir de différents serveurs dans hello même pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="9afb3-112">Les pools élastiques sont mis à la disposition générale dans toutes les régions Azure, à l’exception de l’Inde de l’Ouest, où ils sont actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="9afb3-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="9afb3-113">Les pools élastiques seront en disposition générale dès que possible dans cette région.</span><span class="sxs-lookup"><span data-stu-id="9afb3-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="9afb3-114">Étape 1 : Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="9afb3-115">Création d’un pool élastique d’un existant **server** panneau dans le portail de hello est hello plus simple façon toomove bases de données existantes dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="9afb3-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="9afb3-116">Vous pouvez également créer un pool élastique en recherchant **pool élastique SQL** Bonjour **Marketplace** ou en cliquant sur **+ ajouter** Bonjour **pools élastiques de SQL**parcourir le panneau.</span><span class="sxs-lookup"><span data-stu-id="9afb3-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="9afb3-117">Vous êtes en mesure de toospecify un serveur nouveau ou existant à ce pool de mise en service de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9afb3-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="9afb3-118">Bonjour [portail Azure](http://portal.azure.com/), cliquez sur **davantage de services**  **>**  **serveurs SQL**, puis cliquez sur serveur hello contenant hello bases de données pool élastique de tooadd tooan.</span><span class="sxs-lookup"><span data-stu-id="9afb3-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="9afb3-119">Cliquez sur **Nouveau pool**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-119">Click **New pool**.</span></span>

    ![Ajouter le serveur de tooa pool](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="9afb3-121">**OU**</span><span class="sxs-lookup"><span data-stu-id="9afb3-121">**-OR-**</span></span>

    <span data-ttu-id="9afb3-122">Vous pouvez voir un message indiquant qu’il est recommandé de pools élastiques pour serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="9afb3-123">Cliquez sur hello de toosee message hello recommandé en fonction de la télémétrie d’utilisation de base de données historiques, puis sur hello couche toosee plus de détails et personnaliser le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="9afb3-124">Consultez [comprendre les recommandations de pool](#understand-elastic-pool-recommendations) plus loin dans cette rubrique pour la recommandation de hello est effectuée.</span><span class="sxs-lookup"><span data-stu-id="9afb3-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="9afb3-126">Hello **pool élastique** panneau s’affiche, qui est de spécifier les paramètres de hello pour le pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="9afb3-127">Si vous avez cliqué sur **nouveau pool** à l’étape précédente de hello, hello niveau tarifaire est **Standard** par défaut et aucune base de données est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="9afb3-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="9afb3-128">Vous pouvez créer un pool vide, ou spécifier un ensemble de bases de données existantes à partir de cette toomove serveur dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="9afb3-129">Si vous créez un pool recommandé, hello recommandé de tarification, les paramètres de performances et la liste des bases de données sont préremplies, mais vous pouvez toujours modifier les.</span><span class="sxs-lookup"><span data-stu-id="9afb3-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="9afb3-131">Spécifiez un nom pour le pool élastique de hello, ou laissez-le comme valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="9afb3-132">Étape 2 : sélectionner un niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="9afb3-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="9afb3-133">Hello niveau de tarification du pool détermine hello fonctionnalités ELASTIQUES toohello disponibles dans le pool de hello et hello le nombre maximal d’Edtu (eDTU MAX) et de base de données de stockage (Go) disponible tooeach.</span><span class="sxs-lookup"><span data-stu-id="9afb3-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="9afb3-134">Pour plus d’informations, voir Niveaux de service.</span><span class="sxs-lookup"><span data-stu-id="9afb3-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="9afb3-135">Cliquez sur le niveau de tarification hello toochange de pool de hello **niveau tarifaire**, cliquez sur hello tarification de votre choix, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9afb3-136">Une fois que vous choisissez hello tarification et valider vos modifications en cliquant sur **OK** dans la dernière étape de hello, vous ne serez pas hello toochange en mesure de tarification du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="9afb3-137">toochange hello niveau tarifaire pour un pool élastique existant, créez un pool élastique dans le niveau de tarification souhaité hello et migrez hello bases de données toothis nouveau pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Sélectionner un niveau de tarification](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="9afb3-139">Étape 3 : Configurer le pool de hello</span><span class="sxs-lookup"><span data-stu-id="9afb3-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="9afb3-140">Après avoir hello niveau tarifaire, cliquez sur Configurer pool lorsque vous ajoutez des bases de données, Edtu de pool de jeu et du stockage (pool Go), où vous avez défini des Edtu de hello min et max pour ELASTIQUES de hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="9afb3-141">Cliquez sur **Configurer le pool**</span><span class="sxs-lookup"><span data-stu-id="9afb3-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="9afb3-142">Sélectionnez hello bases de données tooadd toohello pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="9afb3-143">Cette étape est facultative lors de la création du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="9afb3-144">Bases de données peuvent être ajoutés qu’après que hello pool a été créé.</span><span class="sxs-lookup"><span data-stu-id="9afb3-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="9afb3-145">tooadd de bases de données, cliquez sur **Add database**, cliquez sur les bases de données hello que vous souhaitez tooadd, puis cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="9afb3-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Ajouter des bases de données](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="9afb3-147">Si les bases de données hello avec lequel vous travaillez ont suffisamment de télémétrie d’utilisation historiques, hello **estimée des eDTU et l’utilisation de Go** graphique et hello **réel eDTU utilisation** toohelp de mise à jour de graphique à barres vous vérifiez la configuration décisions.</span><span class="sxs-lookup"><span data-stu-id="9afb3-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="9afb3-148">En outre, les service hello peut donner un toohelp de message de recommandation vous redimensionner hello pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="9afb3-149">Voir [Recommandations dynamiques](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="9afb3-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="9afb3-150">Utilisez les contrôles de hello dans hello **configurer le pool** tooexplore paramètres de page et de configurer le pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="9afb3-151">Pour plus d’informations sur les limites de chaque niveau de service, consultez l’article décrivant les [limites des pools élastiques](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools). Pour obtenir des conseils détaillés sur le dimensionnement approprié d’un pool, consultez l’article fournissant des [considérations sur les prix et performances pour un pool élastique](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="9afb3-152">Pour plus d’informations sur les paramètres du pool, consultez [Propriétés du pool élastique](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="9afb3-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="9afb3-154">Cliquez sur **sélectionnez** Bonjour **configurer un Pool** panneau après modification des paramètres.</span><span class="sxs-lookup"><span data-stu-id="9afb3-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="9afb3-155">Cliquez sur **OK** pool de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="9afb3-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="9afb3-156">Comprendre les recommandations relatives au pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="9afb3-157">Hello service de base de données SQL évalue l’historique d’utilisation et recommande un ou plusieurs pools lorsqu’il est plus économique que l’utilisation de bases de données uniques.</span><span class="sxs-lookup"><span data-stu-id="9afb3-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="9afb3-158">Chaque recommandation est configurée avec un sous-ensemble unique de bases de données du serveur hello ajuster le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="9afb3-160">recommandation de pool Hello comprend :</span><span class="sxs-lookup"><span data-stu-id="9afb3-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="9afb3-161">Un niveau de tarification pour le pool hello (Basic, Standard, Premium ou Premium RS)</span><span class="sxs-lookup"><span data-stu-id="9afb3-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="9afb3-162">Valeur **eDTU du pool** appropriée (également appelée eDTU max par pool)</span><span class="sxs-lookup"><span data-stu-id="9afb3-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="9afb3-163">Hello **eDTU MAX** et **eDTU Min** par base de données</span><span class="sxs-lookup"><span data-stu-id="9afb3-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="9afb3-164">liste Hello des bases de données recommandés pour le pool de hello</span><span class="sxs-lookup"><span data-stu-id="9afb3-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9afb3-165">service de Hello prend hello 30 derniers jours de données de télémétrie en compte lorsque vous recommander des pools.</span><span class="sxs-lookup"><span data-stu-id="9afb3-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="9afb3-166">Pour une base de données toobe considéré comme un candidat pour un pool élastique, il doit exister au moins 7 jours.</span><span class="sxs-lookup"><span data-stu-id="9afb3-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="9afb3-167">Les bases de données qui figurent déjà dans un pool élastique ne sont pas considérées comme candidates pour les recommandations de pool élastique.</span><span class="sxs-lookup"><span data-stu-id="9afb3-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="9afb3-168">Hello évalue les besoins en ressources et rentabilité de déplacement hello unique bases de données dans chaque niveau de service dans des pools de hello même couche.</span><span class="sxs-lookup"><span data-stu-id="9afb3-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="9afb3-169">Par exemple, toutes les bases de données Standard d’un serveur sont évaluées pour leur compatibilité avec un pool élastique Standard.</span><span class="sxs-lookup"><span data-stu-id="9afb3-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="9afb3-170">Cela signifie que le service de hello ne fait pas de recommandations entre les couches tels que le déplacement d’une base de données Standard dans un pool Premium.</span><span class="sxs-lookup"><span data-stu-id="9afb3-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="9afb3-171">Après avoir ajouté un pool toohello de bases de données, les recommandations sont générées dynamiquement selon hello historique de l’utilisation des bases de données hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9afb3-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="9afb3-172">Ces recommandations sont affichées dans hello eDTU et graphique d’utilisation Go et une bannière de recommandation haut hello hello **configurer pool** panneau.</span><span class="sxs-lookup"><span data-stu-id="9afb3-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="9afb3-173">Ces recommandations sont tooassist prévue dans la création d’un pool élastique optimisé pour vos bases de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9afb3-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![Recommandations dynamiques](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="9afb3-175">Gérer et surveiller un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="9afb3-176">Vous pouvez utiliser hello toomonitor portail Azure et gérer un pool élastique et hello bases de données hello pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="9afb3-177">À partir du portail de hello, vous pouvez surveiller l’utilisation de hello un pool élastique et bases de données hello dans ce pool.</span><span class="sxs-lookup"><span data-stu-id="9afb3-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="9afb3-178">Vous pouvez également effectuer un ensemble de modifications pool élastique de tooyour et envoyer toutes les modifications apportées à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="9afb3-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="9afb3-179">Ces modifications incluent l’ajout ou la suppression de bases de données, ainsi que le changement des paramètres du pool élastique ou des bases de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="9afb3-180">Hello graphique suivant montre un pool élastique exemple.</span><span class="sxs-lookup"><span data-stu-id="9afb3-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="9afb3-181">affichage de Hello inclut :</span><span class="sxs-lookup"><span data-stu-id="9afb3-181">hello view includes:</span></span>

*  <span data-ttu-id="9afb3-182">Graphiques de surveillance de l’utilisation des ressources de pool élastique de hello et bases de données hello contenus dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="9afb3-183">Hello **configurer** pool bouton toomake modifie le pool élastique de toohello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="9afb3-184">Hello **créer la base de données** bouton qui crée une base de données et l’ajoute toohello pool élastique en cours.</span><span class="sxs-lookup"><span data-stu-id="9afb3-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="9afb3-185">Des tâches élastiques, qui vous aident à gérer un grand nombre de bases de données en exécutant des scripts Transact SQL sur toutes les bases de données d’une liste.</span><span class="sxs-lookup"><span data-stu-id="9afb3-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Affichage du pool][2]

<span data-ttu-id="9afb3-187">Vous pouvez accéder tooa pool particulier toosee son utilisation des ressources.</span><span class="sxs-lookup"><span data-stu-id="9afb3-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="9afb3-188">Par défaut, le pool de hello est l’utilisation de stockage et d’eDTU tooshow configuré pour hello dernière heure.</span><span class="sxs-lookup"><span data-stu-id="9afb3-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="9afb3-189">graphique de Hello peut être configuré tooshow différentes métriques sur différentes périodes.</span><span class="sxs-lookup"><span data-stu-id="9afb3-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="9afb3-190">Sélectionnez un toowork pool élastique avec.</span><span class="sxs-lookup"><span data-stu-id="9afb3-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="9afb3-191">Sous **Surveillance du pool élastique**, vous trouverez un graphique intitulé **Utilisation des ressources**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="9afb3-192">Cliquez sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-192">Click hello chart.</span></span>

    ![Surveillance du pool élastique][3]

    <span data-ttu-id="9afb3-194">Hello **métrique** panneau s’ouvre, affichant une vue détaillée de hello spécifié métriques sur la fenêtre de temps spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Volet Metric][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="9afb3-196">affichage du graphique hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="9afb3-196">toocustomize hello chart display</span></span>

<span data-ttu-id="9afb3-197">Vous pouvez modifier les graphique hello et hello métriques toodisplay autres métriques telles que le pourcentage du processeur, pourcentage de données e/s et pourcentage d’e/s de journal utilisé.</span><span class="sxs-lookup"><span data-stu-id="9afb3-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="9afb3-198">Dans le panneau de métrique hello, cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-198">On hello metric blade, click **Edit**.</span></span>

    ![Cliquez sur Modifier][6]

2. <span data-ttu-id="9afb3-200">Bonjour **modifier le graphique** panneau, sélectionnez une plage de temps (heure, l’heure actuelle, ou semaine), ou cliquez sur **personnalisé** tooselect toute plage de dates hello deux dernières semaines.</span><span class="sxs-lookup"><span data-stu-id="9afb3-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="9afb3-201">Sélectionner le type de graphique hello (barre ou ligne), puis sélectionnez hello ressources toomonitor.</span><span class="sxs-lookup"><span data-stu-id="9afb3-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="9afb3-202">Seul graphique des métriques avec hello même unité de mesure peut être affichée dans hello en hello même temps.</span><span class="sxs-lookup"><span data-stu-id="9afb3-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="9afb3-203">Par exemple, si vous sélectionnez « pourcentage d’eDTU » puis vous pouvez uniquement sélectionner d’autres mesures avec pourcentage en tant qu’unité hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Cliquez sur Modifier](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="9afb3-205">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="9afb3-206">Gérer et surveiller des bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="9afb3-207">Il est également possible de surveiller des bases de données individuelles pour identifier des problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="9afb3-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="9afb3-208">Sous **Surveillance de la base de données élastique**, vous trouverez un graphique qui affiche les métriques de cinq bases de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="9afb3-209">Par défaut, hello graphique affiche hello 5 bases de données dans le pool de hello par utilisation moyenne eDTU Bonjour dernière heure.</span><span class="sxs-lookup"><span data-stu-id="9afb3-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="9afb3-210">Cliquez sur le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-210">Click hello chart.</span></span>

    ![Surveillance du pool élastique][4]

2. <span data-ttu-id="9afb3-212">Hello **l’utilisation des ressources de base de données** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="9afb3-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="9afb3-213">Cela fournit une vue détaillée de l’utilisation de base de données hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="9afb3-214">À l’aide de la grille hello dans la partie inférieure de hello du Panneau de hello, vous pouvez sélectionner des bases de données dans hello pool toodisplay son utilisation dans le graphique de hello (des bases de données too5).</span><span class="sxs-lookup"><span data-stu-id="9afb3-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="9afb3-215">Vous pouvez également personnaliser la fenêtre hello métriques et l’heure affichée dans le graphique de hello en cliquant sur **modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Panneau Database Resource Utilization (Utilisation des ressources des bases de données)][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="9afb3-217">affichage de hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="9afb3-217">toocustomize hello view</span></span>

1. <span data-ttu-id="9afb3-218">Bonjour **l’utilisation des ressources de base de données** panneau, cliquez sur **modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Cliquez sur Modifier le graphique](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="9afb3-220">Bonjour **modifier** panneau du graphique, sélectionnez une plage de temps (après les heures ou dernières 24 heures) ou cliquez sur **personnalisé** tooselect un autre jour Bonjour au-delà de 2 semaines toodisplay.</span><span class="sxs-lookup"><span data-stu-id="9afb3-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Cliquez sur Personnalisé](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="9afb3-222">Cliquez sur hello **comparer les bases de données par** tooselect de liste déroulante un toouse métrique différents lors de la comparaison des bases de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Modifier le graphique de hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="9afb3-224">toomonitor de bases de données tooselect</span><span class="sxs-lookup"><span data-stu-id="9afb3-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="9afb3-225">Dans la liste base de données hello hello **l’utilisation des ressources de base de données** panneau, vous pouvez trouver des bases de données particulières en consultant les pages hello dans la liste de hello ou en tapant dans nom hello d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="9afb3-226">Utilisez hello case à cocher tooselect hello base de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-226">Use hello checkbox tooselect hello database.</span></span>

![Recherchez des bases de données toomonitor][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="9afb3-228">Ajouter une ressource de pool élastique tooan alerte</span><span class="sxs-lookup"><span data-stu-id="9afb3-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="9afb3-229">Vous pouvez ajouter des règles tooan élastique pool d’envoyer un courrier électronique toopeople alerte chaînes tooURL points de terminaison ou lorsque le pool élastique de hello atteint un seuil d’utilisation que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="9afb3-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="9afb3-230">**tooadd une ressource tooany alerte :**</span><span class="sxs-lookup"><span data-stu-id="9afb3-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="9afb3-231">Cliquez sur hello **l’utilisation des ressources** hello de tooopen graphique **métrique** panneau, cliquez sur **ajouter une alerte**, puis remplissez les informations de hello Bonjour **ajouter une alerte règle** blade (**ressource** est configuré automatiquement de pool de hello toobe avec lequel vous travaillez).</span><span class="sxs-lookup"><span data-stu-id="9afb3-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="9afb3-232">Tapez un **nom** et **Description** qui identifie les tooyou alerte hello et les destinataires de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="9afb3-233">Choisissez un **métrique** que vous souhaitez tooalert à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="9afb3-234">graphique de Hello affiche dynamiquement l’utilisation des ressources pour cette métrique toohelp que vous choisissez un seuil.</span><span class="sxs-lookup"><span data-stu-id="9afb3-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="9afb3-235">Choisissez une **condition** (supérieur à, inférieur à, etc.) et un **seuil**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="9afb3-236">Choisissez un **période** de temps qui hello métrique règle doit être satisfaite avant de déclencheurs d’alerte hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="9afb3-237">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-237">Click **OK**.</span></span>

<span data-ttu-id="9afb3-238">Pour plus d'informations, voir [Créer des alertes SQL Database dans le portail Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="9afb3-239">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="9afb3-240">Vous pouvez ajouter ou supprimer des bases de données dans un pool existant.</span><span class="sxs-lookup"><span data-stu-id="9afb3-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="9afb3-241">bases de données Hello peuvent être dans d’autres pools.</span><span class="sxs-lookup"><span data-stu-id="9afb3-241">hello databases can be in other pools.</span></span> <span data-ttu-id="9afb3-242">Toutefois, vous pouvez uniquement ajouter des bases de données qui sont sur hello même serveur logique.</span><span class="sxs-lookup"><span data-stu-id="9afb3-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="9afb3-243">Dans le panneau hello pour le pool de hello, sous **des bases de données élastiques** cliquez sur **configurer pool**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Cliquez sur Configurer le pool][1]

2. <span data-ttu-id="9afb3-245">Bonjour **configurer pool** panneau, cliquez sur **ajouter toopool**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Cliquez sur Ajouter toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="9afb3-247">Bonjour **ajouter des bases de données** panneau, base de données Sélectionnez hello ou pool de bases de données tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="9afb3-248">Puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-248">Then click **Select**.</span></span>

    ![Sélectionnez les bases de données tooadd](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="9afb3-250">Hello **configurer pool** panneau maintenant listes hello de base de données sélectionnée toobe ajouté, avec son état défini trop**en attente**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Ajouts de pool en attente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="9afb3-252">Bonjour **Panneau de pool configurer**, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="9afb3-254">Déplacer une base de données hors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="9afb3-255">Bonjour **configurer pool** panneau, base de données Sélectionnez hello ou tooremove de bases de données.</span><span class="sxs-lookup"><span data-stu-id="9afb3-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="9afb3-257">Cliquez sur **Supprimer du pool**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-257">Click **Remove from pool**.</span></span>

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="9afb3-259">Hello **configurer pool** panneau maintenant listes hello de base de données sélectionnée toobe supprimée avec son état défini trop**en attente**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![Afficher l’aperçu d’ajout et de suppression de base de données](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="9afb3-261">Bonjour **Panneau de pool configurer**, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9afb3-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="9afb3-263">Modifier les paramètres de performances d'un pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="9afb3-264">Lorsque vous analysez l’utilisation des ressources d’un pool élastique hello, vous pouvez constater que quelques ajustements sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="9afb3-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="9afb3-265">Peut-être pool de hello doit être modifiée dans les limites de performances ou le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="9afb3-266">Éventuellement, vous souhaitez que les paramètres de base de données toochange hello dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="9afb3-267">Vous pouvez modifier le programme d’installation de hello du pool hello à n’importe quel moment tooget hello meilleur compromis entre les performances et le coût.</span><span class="sxs-lookup"><span data-stu-id="9afb3-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="9afb3-268">Pour plus d’informations, consultez l’article [Quand utiliser un pool élastique ?](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="9afb3-269">toochange hello Edtu limites ou de stockage par pool et Edtu par base de données :</span><span class="sxs-lookup"><span data-stu-id="9afb3-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="9afb3-270">Ouvrez hello **configurer pool** panneau.</span><span class="sxs-lookup"><span data-stu-id="9afb3-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="9afb3-271">Sous **les paramètres de pool élastique**, utilisez les deux paramètres de pool de curseur toochange hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Utilisation des ressources du pool élastique](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="9afb3-273">Lorsque le paramètre de hello change, hello affiche hello mensuel coût estimé de modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Mise à jour d’un pool élastique et nouveau coût mensuel](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="9afb3-275">Latence des opérations du pool élastique</span><span class="sxs-lookup"><span data-stu-id="9afb3-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="9afb3-276">La modification d’Edtu de min hello par base de données ou max Edtu par base de données généralement se termine dans 5 minutes ou moins.</span><span class="sxs-lookup"><span data-stu-id="9afb3-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="9afb3-277">Modification des Edtu hello par pool dépend hello total de l’espace utilisé par toutes les bases de données dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="9afb3-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="9afb3-278">Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="9afb3-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="9afb3-279">Par exemple, si hello l’espace total utilisé par toutes les bases de données dans le pool de hello est 200 Go, puis hello attendu de latence de modification hello eDTU du pool par pool est de 3 heures au maximum.</span><span class="sxs-lookup"><span data-stu-id="9afb3-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9afb3-280">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9afb3-280">Next steps</span></span>

- <span data-ttu-id="9afb3-281">toounderstand quelles un pool élastique, consultez [pool élastique de base de données SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="9afb3-282">Pour obtenir de l’aide sur l’utilisation des pools élastiques, consultez [Considérations sur les prix et performances pour les pools élastiques](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="9afb3-283">scripts de toorun Transact-SQL de travaux élastique toouse par rapport à n’importe quel nombre de bases de données dans le pool de hello, voir [vue d’ensemble de travaux élastique](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="9afb3-284">tooquery sur n’importe quel nombre de bases de données dans le pool de hello, consultez [vue d’ensemble de la requête élastique](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="9afb3-285">Pour les transactions de n’importe quel nombre de bases de données dans le pool de hello, consultez [transactions élastiques](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9afb3-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
