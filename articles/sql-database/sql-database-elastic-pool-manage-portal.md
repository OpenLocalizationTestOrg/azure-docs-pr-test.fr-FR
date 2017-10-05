---
title: "Portail Azure : Créer et gérer un pool élastique SQL Database | Microsoft Docs"
description: "Découvrez comment utiliser le Portail Azure et l’intelligence intégrée de la base de données SQL pour gérer, surveiller et redimensionner un pool élastique évolutif pour optimiser les performances de la base de données et gérer les coûts."
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="cce52-103">Créer et gérer un pool élastique avec le Portail Azure</span><span class="sxs-lookup"><span data-stu-id="cce52-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="cce52-104">Cette rubrique montre comment créer et gérer des [pools élastiques](sql-database-elastic-pool.md) évolutifs avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cce52-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="cce52-105">Vous pouvez également créer et gérer un pool élastique Azure avec [PowerShell](sql-database-elastic-pool-manage-powershell.md), l’API REST ou [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="cce52-106">Vous pouvez également créer et déplacer des bases de données vers et depuis des pools élastiques à l’aide de [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="cce52-107">Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-107">Create an elastic pool</span></span> 

<span data-ttu-id="cce52-108">Vous pouvez créer un pool élastique de deux façons.</span><span class="sxs-lookup"><span data-stu-id="cce52-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="cce52-109">Vous pouvez le faire à partir de zéro si vous connaissez la configuration de pool souhaitée ou si vous commencez par une recommandation issue du service.</span><span class="sxs-lookup"><span data-stu-id="cce52-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="cce52-110">La base de données SQL est dotée d’une intelligence intégrée qui recommande une configuration de pool élastique si cela semble plus économique pour vous en fonction de la dernière télémétrie d’utilisation de vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="cce52-111">Vous pouvez créer plusieurs pools sur un serveur, mais il est impossible d’ajouter des bases de données de différents serveurs dans le même pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="cce52-112">Les pools élastiques sont mis à la disposition générale dans toutes les régions Azure, à l’exception de l’Inde de l’Ouest, où ils sont actuellement en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="cce52-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="cce52-113">Les pools élastiques seront en disposition générale dès que possible dans cette région.</span><span class="sxs-lookup"><span data-stu-id="cce52-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="cce52-114">Étape 1 : Créer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="cce52-115">Créer un pool élastique à partir d’un panneau **serveur** existant dans le portail est le moyen le plus simple pour déplacer des bases de données existantes dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="cce52-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="cce52-116">Vous pouvez également créer un pool élastique en recherchant **pool élastique SQL** sur le **Marketplace** ou en cliquant sur **+Ajouter** dans le panneau de recherche **Pools élastiques SQL**.</span><span class="sxs-lookup"><span data-stu-id="cce52-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="cce52-117">Ce workflow d’approvisionnement de pool vous permet d’indiquer un nouveau serveur ou un serveur existant.</span><span class="sxs-lookup"><span data-stu-id="cce52-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="cce52-118">Dans le [portail Azure](http://portal.azure.com/), cliquez sur **Plus de services** **>** **Serveurs SQL**, puis sur le serveur qui contient les bases de données que vous souhaitez ajouter à un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="cce52-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="cce52-119">Cliquez sur **Nouveau pool**.</span><span class="sxs-lookup"><span data-stu-id="cce52-119">Click **New pool**.</span></span>

    ![Ajouter un pool à un serveur](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="cce52-121">**OU**</span><span class="sxs-lookup"><span data-stu-id="cce52-121">**-OR-**</span></span>

    <span data-ttu-id="cce52-122">Il se peut qu’un message indiquant que des pools élastiques recommandés sont disponibles pour le serveur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cce52-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="cce52-123">Cliquez sur le message pour afficher les pools recommandés en fonction de la télémétrie de l’historique d’utilisation de base de données, puis cliquez sur le niveau pour afficher plus de détails et personnaliser le pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="cce52-124">Consultez la section [Comprendre les recommandations relatives au pool](#understand-elastic-pool-recommendations) plus loin dans cette rubrique pour savoir sur quoi repose la recommandation.</span><span class="sxs-lookup"><span data-stu-id="cce52-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="cce52-126">Le panneau **Pool élastique** s’affiche pour vous permettre de spécifier les paramètres de votre pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="cce52-127">Si vous avez cliqué sur **Nouveau pool** à l’étape précédente, le niveau tarifaire par défaut est **Standard** et aucune base de données n’est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="cce52-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="cce52-128">Vous pouvez créer un pool vide ou spécifier un ensemble de bases de données existantes à partir de ce serveur, pour les déplacer vers le pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="cce52-129">Si vous créez un pool recommandé, le niveau tarifaire recommandé, les paramètres de performances et la liste des bases de données sont préremplis, mais vous pouvez toujours les modifier.</span><span class="sxs-lookup"><span data-stu-id="cce52-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="cce52-131">Entrez un nom pour le pool élastique, ou conservez la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="cce52-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="cce52-132">Étape 2 : sélectionner un niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="cce52-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="cce52-133">Le niveau de tarification du pool détermine les fonctionnalités disponibles pour les bases de données élastiques dans le pool, ainsi que le nombre maximal d'eDTU (eDTU MAX) et le stockage (Go) disponibles pour chaque base de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="cce52-134">Pour plus d’informations, voir Niveaux de service.</span><span class="sxs-lookup"><span data-stu-id="cce52-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="cce52-135">Pour modifier le niveau tarifaire du pool, cliquez sur **Niveau tarifaire**, sur le niveau tarifaire de votre choix, puis sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="cce52-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cce52-136">Une fois que vous avez choisi le niveau tarifaire et validé vos modifications en cliquant sur **OK** à la dernière étape, vous ne pouvez plus modifier le niveau tarifaire du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="cce52-137">Pour modifier le niveau de tarification d’un pool élastique existant, créez un pool élastique dans le niveau de tarification souhaité et migrez les bases de données vers ce nouveau pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![Sélectionner un niveau de tarification](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="cce52-139">Étape 3 : configurer le pool</span><span class="sxs-lookup"><span data-stu-id="cce52-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="cce52-140">Après avoir défini le niveau de tarification, cliquez sur Configurer le pool à l’endroit où vous ajoutez des bases de données, définissez la quantité d’eDTU et de stockage (Go de pool), et définissez les nombres minimum et maximum d’eDTU des bases de données élastiques dans le pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="cce52-141">Cliquez sur **Configurer le pool**</span><span class="sxs-lookup"><span data-stu-id="cce52-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="cce52-142">Sélectionnez les bases de données que vous souhaitez ajouter au pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="cce52-143">Cette étape est facultative lors de la création du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="cce52-144">Les bases de données peuvent être ajoutées après la création du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="cce52-145">Pour ajouter des bases de données, cliquez sur **Ajouter une base de données** et sur les bases de données que vous voulez ajouter, puis sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="cce52-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Ajouter des bases de données](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="cce52-147">Si les bases de données que vous utilisez contiennent suffisamment de données de télémétrie d’historique d’utilisation, le graphique **Utilisation estimée des eDTU et des Go** et le graphique à barres **Utilisation effective des eDTU** sont mis à jour pour vous aider à prendre des décisions en termes de configuration.</span><span class="sxs-lookup"><span data-stu-id="cce52-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="cce52-148">Le service peut également vous envoyer un message de recommandation pour vous aider à rectifier la taille du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="cce52-149">Voir [Recommandations dynamiques](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="cce52-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="cce52-150">Utilisez les contrôles de la page **Configurer le pool** pour explorer les paramètres et configurer votre pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="cce52-151">Pour plus d’informations sur les limites de chaque niveau de service, consultez l’article décrivant les [limites des pools élastiques](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools). Pour obtenir des conseils détaillés sur le dimensionnement approprié d’un pool, consultez l’article fournissant des [considérations sur les prix et performances pour un pool élastique](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="cce52-152">Pour plus d’informations sur les paramètres du pool, consultez [Propriétés du pool élastique](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="cce52-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Configurer un pool élastique](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="cce52-154">Cliquez sur **Sélectionner** in the **Configure Pool** après avoir modifié des paramètres.</span><span class="sxs-lookup"><span data-stu-id="cce52-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="cce52-155">Cliquez sur **OK** pour créer le pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="cce52-156">Comprendre les recommandations relatives au pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="cce52-157">Le service SQL Database évalue l’historique d’utilisation et recommande un ou plusieurs pools lorsque cela est plus rentable que d’utiliser des bases de données uniques.</span><span class="sxs-lookup"><span data-stu-id="cce52-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="cce52-158">Chaque recommandation est configurée avec un sous-ensemble unique de bases de données du serveur qui correspond le mieux au pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![pool recommandé](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="cce52-160">La recommandation relative au pool comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cce52-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="cce52-161">Niveau tarifaire du pool (De base, Standard, Premium ou Premium RS)</span><span class="sxs-lookup"><span data-stu-id="cce52-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="cce52-162">Valeur **eDTU du pool** appropriée (également appelée eDTU max par pool)</span><span class="sxs-lookup"><span data-stu-id="cce52-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="cce52-163">Paramètres **eDTU max** et **eDTU min** par base de données</span><span class="sxs-lookup"><span data-stu-id="cce52-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="cce52-164">Liste des bases de données recommandées pour le pool</span><span class="sxs-lookup"><span data-stu-id="cce52-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cce52-165">Le service prend en compte les 30 derniers jours de télémétrie lors de la recommandation de pools.</span><span class="sxs-lookup"><span data-stu-id="cce52-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="cce52-166">Pour qu’une base de données soit considérée comme candidate à un pool élastique, elle doit exister depuis au moins 7 jours.</span><span class="sxs-lookup"><span data-stu-id="cce52-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="cce52-167">Les bases de données qui figurent déjà dans un pool élastique ne sont pas considérées comme candidates pour les recommandations de pool élastique.</span><span class="sxs-lookup"><span data-stu-id="cce52-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="cce52-168">Le service évalue les besoins en ressources et la rentabilité du déplacement des bases de données uniques dans chaque niveau de service vers des pools du même niveau.</span><span class="sxs-lookup"><span data-stu-id="cce52-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="cce52-169">Par exemple, toutes les bases de données Standard d’un serveur sont évaluées pour leur compatibilité avec un pool élastique Standard.</span><span class="sxs-lookup"><span data-stu-id="cce52-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="cce52-170">Cela signifie que le service n'effectue aucune recommandation multiniveau telle que le déplacement d'une base de données Standard dans un pool Premium.</span><span class="sxs-lookup"><span data-stu-id="cce52-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="cce52-171">Après avoir ajouté des bases de données au pool, des recommandations sont générées de façon dynamique en fonction de l’historique d’utilisation des bases de données que vous avez sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="cce52-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="cce52-172">Ces recommandations sont affichées dans le graphique d’utilisation d’eDTU et de Go ainsi que dans la bannière de recommandation en haut du panneau **Configurer le pool**.</span><span class="sxs-lookup"><span data-stu-id="cce52-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="cce52-173">Ces recommandations sont destinées à vous aider à créer un pool élastique optimisé pour vos bases de données spécifiques.</span><span class="sxs-lookup"><span data-stu-id="cce52-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![Recommandations dynamiques](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="cce52-175">Gérer et surveiller un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="cce52-176">Vous pouvez utiliser le portail Azure pour surveiller et gérer un pool élastique et les bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="cce52-177">Depuis le portail, vous pouvez surveiller l’utilisation d’un pool élastique et des bases de données que contient ce pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="cce52-178">Vous pouvez également apporter un ensemble de modifications à votre pool élastique et soumettre toutes les modifications en même temps.</span><span class="sxs-lookup"><span data-stu-id="cce52-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="cce52-179">Ces modifications incluent l’ajout ou la suppression de bases de données, ainsi que le changement des paramètres du pool élastique ou des bases de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="cce52-180">Le graphique suivant montre un exemple de pool élastique.</span><span class="sxs-lookup"><span data-stu-id="cce52-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="cce52-181">L’affichage inclut :</span><span class="sxs-lookup"><span data-stu-id="cce52-181">The view includes:</span></span>

*  <span data-ttu-id="cce52-182">Des graphiques pour la surveillance de l’utilisation des ressources du pool élastique et des bases de données que contient ce pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="cce52-183">Le bouton **Configurer le pool** pour apporter des modifications au pool élastique.</span><span class="sxs-lookup"><span data-stu-id="cce52-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="cce52-184">Le bouton **Créer une base de données**, qui crée une base de données et l’ajoute au pool élastique actuel.</span><span class="sxs-lookup"><span data-stu-id="cce52-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="cce52-185">Des tâches élastiques, qui vous aident à gérer un grand nombre de bases de données en exécutant des scripts Transact SQL sur toutes les bases de données d’une liste.</span><span class="sxs-lookup"><span data-stu-id="cce52-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Affichage du pool][2]

<span data-ttu-id="cce52-187">Vous pouvez accéder à un pool particulier pour consulter l’utilisation des ressources de ce dernier.</span><span class="sxs-lookup"><span data-stu-id="cce52-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="cce52-188">Par défaut, le pool est configuré pour afficher l’utilisation du stockage et des eDTU au cours de la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="cce52-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="cce52-189">Le graphique peut être configuré pour afficher d’autres métriques sur différentes plages de temps.</span><span class="sxs-lookup"><span data-stu-id="cce52-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="cce52-190">Sélectionnez un pool élastique à utiliser.</span><span class="sxs-lookup"><span data-stu-id="cce52-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="cce52-191">Sous **Surveillance du pool élastique**, vous trouverez un graphique intitulé **Utilisation des ressources**.</span><span class="sxs-lookup"><span data-stu-id="cce52-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="cce52-192">Cliquez sur ce graphique.</span><span class="sxs-lookup"><span data-stu-id="cce52-192">Click the chart.</span></span>

    ![Surveillance du pool élastique][3]

    <span data-ttu-id="cce52-194">Le panneau **Métrique** s’ouvre. Celui-ci affiche une vue détaillée des métriques spécifiées sur la plage de temps définie.</span><span class="sxs-lookup"><span data-stu-id="cce52-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Volet Metric][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="cce52-196">Pour personnaliser l’affichage du graphique</span><span class="sxs-lookup"><span data-stu-id="cce52-196">To customize the chart display</span></span>

<span data-ttu-id="cce52-197">Vous pouvez modifier le graphique et le panneau Métrique pour afficher d’autres métriques, telles que le pourcentage d’UC, le pourcentage d’E/S des données et le pourcentage d’E/S des fichiers journaux utilisés.</span><span class="sxs-lookup"><span data-stu-id="cce52-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="cce52-198">Dans le panneau Métrique, cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="cce52-198">On the metric blade, click **Edit**.</span></span>

    ![Cliquez sur Modifier][6]

2. <span data-ttu-id="cce52-200">Dans le panneau **Modifier le graphique**, sélectionnez une plage de temps (dernière heure, aujourd’hui ou semaine dernière) ou cliquez sur **Personnalisé** pour sélectionner la plage de temps de votre choix au cours des deux dernières semaines.</span><span class="sxs-lookup"><span data-stu-id="cce52-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="cce52-201">Sélectionnez le type de graphique (bâtons ou linéaire), puis sélectionnez les ressources à surveiller.</span><span class="sxs-lookup"><span data-stu-id="cce52-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="cce52-202">Seules les mesures présentant la même unité peuvent figurer simultanément dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="cce52-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="cce52-203">Par exemple, si vous sélectionnez « Pourcentage eDTU », vous pouvez sélectionner d’autres mesures de pourcentage.</span><span class="sxs-lookup"><span data-stu-id="cce52-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Cliquez sur Modifier](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="cce52-205">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cce52-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="cce52-206">Gérer et surveiller des bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="cce52-207">Il est également possible de surveiller des bases de données individuelles pour identifier des problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="cce52-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="cce52-208">Sous **Surveillance de la base de données élastique**, vous trouverez un graphique qui affiche les métriques de cinq bases de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="cce52-209">Par défaut, le graphique affiche les 5 premières bases de données du pool en termes d’utilisation moyenne des eDTU au cours de la dernière heure.</span><span class="sxs-lookup"><span data-stu-id="cce52-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="cce52-210">Cliquez sur ce graphique.</span><span class="sxs-lookup"><span data-stu-id="cce52-210">Click the chart.</span></span>

    ![Surveillance du pool élastique][4]

2. <span data-ttu-id="cce52-212">Le panneau **Database resource utilization** (Utilisation des ressources des bases de données) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="cce52-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="cce52-213">Celui-ci fournit une vue détaillée de l’utilisation des bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="cce52-214">À l’aide de la grille dans la partie inférieure du panneau, vous pouvez sélectionner les bases de données du pool de votre choix (jusqu’à 5 bases de données) pour afficher leur utilisation dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="cce52-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="cce52-215">Vous pouvez également personnaliser les métriques et la plage de temps affichées dans le graphique en cliquant sur **Modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="cce52-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Panneau Database Resource Utilization (Utilisation des ressources des bases de données)][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="cce52-217">Pour personnaliser l’affichage</span><span class="sxs-lookup"><span data-stu-id="cce52-217">To customize the view</span></span>

1. <span data-ttu-id="cce52-218">Dans le panneau **Database Resource Utilization** (Utilisation des ressources des bases de données), cliquez sur **Modifier le graphique**.</span><span class="sxs-lookup"><span data-stu-id="cce52-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Cliquez sur Modifier le graphique](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="cce52-220">Dans le panneau **Modifier le graphique**, sélectionnez une plage de temps (dernière heure ou dernières 24 heures) ou cliquez sur **Personnalisé** pour sélectionner un autre jour au cours des 2 dernières semaines.</span><span class="sxs-lookup"><span data-stu-id="cce52-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Cliquez sur Personnalisé](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="cce52-222">Cliquez sur la liste déroulante **Compare databases by** (Comparer les bases de données par) pour modifier la métrique à utiliser lors de la comparaison des bases de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![Modifiez le graphique](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="cce52-224">Pour sélectionner les bases de données à surveiller</span><span class="sxs-lookup"><span data-stu-id="cce52-224">To select databases to monitor</span></span>

<span data-ttu-id="cce52-225">Dans la liste de base de données du panneau **Database Resource Utilization** (Utilisation des ressources des bases de données), vous pouvez rechercher des bases de données spécifiques en parcourant les différentes pages ou en tapant leur nom.</span><span class="sxs-lookup"><span data-stu-id="cce52-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="cce52-226">Activez la case à cocher pour sélectionner la base de données.</span><span class="sxs-lookup"><span data-stu-id="cce52-226">Use the checkbox to select the database.</span></span>

![Recherchez les bases de données à surveiller][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="cce52-228">Ajouter une alerte à une ressource de pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="cce52-229">Vous pouvez ajouter des règles à un pool élastique qui envoient des messages électroniques à des personnes ou des chaînes d’alertes à des points de terminaison d’URL quand le pool élastique atteint un seuil d’utilisation que vous configurez.</span><span class="sxs-lookup"><span data-stu-id="cce52-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="cce52-230">**Pour ajouter une alerte à une ressource :**</span><span class="sxs-lookup"><span data-stu-id="cce52-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="cce52-231">Cliquez sur le graphique **Utilisation des ressources** pour ouvrir le panneau **Métrique**. Cliquez sur **Ajouter une alerte**, puis renseignez les informations dans le panneau **Ajouter une règle d’alerte** (la valeur **Ressource** est automatiquement définie comme étant le pool que vous utilisez).</span><span class="sxs-lookup"><span data-stu-id="cce52-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="cce52-232">Saisissez un **nom** et une **description** qui identifient l’alerte pour vous et les destinataires.</span><span class="sxs-lookup"><span data-stu-id="cce52-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="cce52-233">Choisissez une **métrique** pour l’alerte dans la liste.</span><span class="sxs-lookup"><span data-stu-id="cce52-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="cce52-234">Le graphique affiche dynamiquement l’utilisation des ressources pour cette métrique pour vous aider à choisir un seuil.</span><span class="sxs-lookup"><span data-stu-id="cce52-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="cce52-235">Choisissez une **condition** (supérieur à, inférieur à, etc.) et un **seuil**.</span><span class="sxs-lookup"><span data-stu-id="cce52-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="cce52-236">Choisissez une **Période** de temps pendant laquelle la règle de métrique doit être satisfaite pour que l’alerte se déclenche.</span><span class="sxs-lookup"><span data-stu-id="cce52-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="cce52-237">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cce52-237">Click **OK**.</span></span>

<span data-ttu-id="cce52-238">Pour plus d'informations, voir [Créer des alertes SQL Database dans le portail Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="cce52-239">Déplacer une base de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="cce52-240">Vous pouvez ajouter ou supprimer des bases de données dans un pool existant.</span><span class="sxs-lookup"><span data-stu-id="cce52-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="cce52-241">Les bases de données peuvent se trouver dans d’autres pools.</span><span class="sxs-lookup"><span data-stu-id="cce52-241">The databases can be in other pools.</span></span> <span data-ttu-id="cce52-242">Toutefois, vous pouvez uniquement ajouter des bases de données qui se trouvent sur le même serveur logique.</span><span class="sxs-lookup"><span data-stu-id="cce52-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="cce52-243">Dans le panneau du pool, sous **Bases de données élastiques**, cliquez sur **Configurer le pool**.</span><span class="sxs-lookup"><span data-stu-id="cce52-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Cliquez sur Configurer le pool][1]

2. <span data-ttu-id="cce52-245">Dans le panneau **Configurer le pool**, cliquez sur **Ajouter au pool**.</span><span class="sxs-lookup"><span data-stu-id="cce52-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Cliquez sur Ajouter au pool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="cce52-247">Dans le panneau **Ajouter des bases de données** , sélectionnez les bases de données à ajouter au pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="cce52-248">Puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="cce52-248">Then click **Select**.</span></span>

    ![Sélectionnez les bases de données à ajouter](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="cce52-250">Le panneau **Configurer le pool** répertorie maintenant les bases de données sélectionnées à ajouter, avec leur état défini sur **En attente**.</span><span class="sxs-lookup"><span data-stu-id="cce52-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![Ajouts de pool en attente](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="cce52-252">Dans le panneau **Configurer le pool**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cce52-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="cce52-254">Déplacer une base de données hors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="cce52-255">Dans le panneau **Configurer le pool** , sélectionnez les bases de données à supprimer.</span><span class="sxs-lookup"><span data-stu-id="cce52-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="cce52-257">Cliquez sur **Supprimer du pool**.</span><span class="sxs-lookup"><span data-stu-id="cce52-257">Click **Remove from pool**.</span></span>

    ![liste des bases de données](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="cce52-259">Le panneau **Configurer le pool** répertorie maintenant les bases de données sélectionnées à supprimer, avec leur état défini sur **En attente**.</span><span class="sxs-lookup"><span data-stu-id="cce52-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![Afficher l’aperçu d’ajout et de suppression de base de données](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="cce52-261">Dans le panneau **Configurer le pool**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cce52-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![Cliquez sur Enregistrer.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="cce52-263">Modifier les paramètres de performances d'un pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="cce52-264">Lorsque vous surveillez l’utilisation des ressources d’un pool élastique, vous pouvez constater que certains ajustements sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="cce52-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="cce52-265">Les limites de performances ou de stockage du pool ont peut-être besoin d’être modifiées.</span><span class="sxs-lookup"><span data-stu-id="cce52-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="cce52-266">Vous pouvez aussi vouloir modifier les paramètres des bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="cce52-267">Vous pouvez modifier la configuration du pool à tout moment pour obtenir le meilleur compromis entre les performances et le coût.</span><span class="sxs-lookup"><span data-stu-id="cce52-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="cce52-268">Pour plus d’informations, consultez l’article [Quand utiliser un pool élastique ?](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="cce52-269">Pour modifier les eDTU ou les limites par pool et les eDTU par base de données :</span><span class="sxs-lookup"><span data-stu-id="cce52-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="cce52-270">Ouvrez le panneau **Configurer le pool** .</span><span class="sxs-lookup"><span data-stu-id="cce52-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="cce52-271">Dans les **paramètres du pool élastique**, utilisez l’un ou l’autre des curseurs pour modifier les paramètres du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Utilisation des ressources du pool élastique](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="cce52-273">Lorsque le paramètre change, l’affichage indique le coût mensuel estimé de la modification.</span><span class="sxs-lookup"><span data-stu-id="cce52-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Mise à jour d’un pool élastique et nouveau coût mensuel](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="cce52-275">Latence des opérations du pool élastique</span><span class="sxs-lookup"><span data-stu-id="cce52-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="cce52-276">En général, le processus de modification du nombre minimal d’eDTU par base de données ou du nombre maximal d’eDTU par base de données prend 5 minutes au maximum.</span><span class="sxs-lookup"><span data-stu-id="cce52-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="cce52-277">Le processus de modification du nombre d’eDTU par pool dépend quant à lui de la quantité totale d’espace utilisé par toutes les bases de données du pool.</span><span class="sxs-lookup"><span data-stu-id="cce52-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="cce52-278">Ce processus prend en moyenne 90 minutes au maximum, pour chaque tranche de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="cce52-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="cce52-279">Par exemple, si l’espace total utilisé par toutes les bases de données du pool est égal à 200 Go, une opération de modification du nombre d’eDTU par pool prend 3 heures au maximum.</span><span class="sxs-lookup"><span data-stu-id="cce52-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cce52-280">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cce52-280">Next steps</span></span>

- <span data-ttu-id="cce52-281">Pour comprendre ce que représente un pool élastique, consultez [Pool élastique de bases de données SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="cce52-282">Pour obtenir de l’aide sur l’utilisation des pools élastiques, consultez [Considérations sur les prix et performances pour les pools élastiques](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="cce52-283">Pour utiliser des tâches élastiques afin d'exécuter des scripts Transact-SQL, quel que soit le nombre de bases de données dans le pool, consultez [Vue d’ensemble des tâches de base de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="cce52-284">Pour interroger les bases de données du pool, quel que soit leur nombre, consultez [Vue d’ensemble de l’interrogation d’un pool élastique](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="cce52-285">Pour interroger les transactions de bases de données, quel que soit leur nombre, consultez [Transactions élastiques](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cce52-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
