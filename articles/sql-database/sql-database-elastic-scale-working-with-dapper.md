---
title: "bibliothèque cliente de base de données élastique aaaUsing avec Dapper | Documents Microsoft"
description: "Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a><span data-ttu-id="0823f-103">Utilisation de la bibliothèque cliente de la base de données élastique avec Dapper</span><span class="sxs-lookup"><span data-stu-id="0823f-103">Using elastic database client library with Dapper</span></span>
<span data-ttu-id="0823f-104">Ce document est destiné aux développeurs qui s’appuient sur les applications toobuild Dapper, mais aussi tooembrace [outils de base de données élastique](sql-database-elastic-scale-introduction.md) toocreate applications qui implémentent partitionnement tooscale-hors de leur couche données.</span><span class="sxs-lookup"><span data-stu-id="0823f-104">This document is for developers that rely on Dapper toobuild applications, but also want tooembrace [elastic database tooling](sql-database-elastic-scale-introduction.md) toocreate applications that implement sharding tooscale-out their data tier.</span></span>  <span data-ttu-id="0823f-105">Ce document illustre les modifications hello dans les applications Dapper qui sont nécessaire toointegrate avec les outils de base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="0823f-105">This document illustrates hello changes in Dapper-based applications that are necessary toointegrate with elastic database tools.</span></span> <span data-ttu-id="0823f-106">Notre le focus est sur la composition de gestion de partition de base de données élastique hello et dépendant des données de l’acheminement avec Dapper.</span><span class="sxs-lookup"><span data-stu-id="0823f-106">Our focus is on composing hello elastic database shard management and data dependent routing with Dapper.</span></span> 

<span data-ttu-id="0823f-107">**Exemple de code**: [outils de base de données élastique pour l’intégration de la base de données SQL Azure avec Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span><span class="sxs-lookup"><span data-stu-id="0823f-107">**Sample Code**: [Elastic database tools for Azure SQL Database - Dapper integration](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).</span></span>

<span data-ttu-id="0823f-108">Intégration **Dapper** et **DapperExtensions** avec hello bibliothèque cliente de base de données élastique pour base de données SQL Azure est facile.</span><span class="sxs-lookup"><span data-stu-id="0823f-108">Integrating **Dapper** and **DapperExtensions** with hello elastic database client library for Azure SQL Database is easy.</span></span> <span data-ttu-id="0823f-109">Les applications peuvent utiliser les données dépendantes de routage par la modification de la création de hello et l’ouverture des nouveaux [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello de toouse objets [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appeler à partir de hello [client bibliothèque](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span><span class="sxs-lookup"><span data-stu-id="0823f-109">Your applications can use data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call from hello [client library](http://msdn.microsoft.com/library/azure/dn765902.aspx).</span></span> <span data-ttu-id="0823f-110">Cela limite les modifications dans votre tooonly application où les nouvelles connexions sont créées et ouvert.</span><span class="sxs-lookup"><span data-stu-id="0823f-110">This limits changes in your application tooonly where new connections are created and opened.</span></span> 

## <a name="dapper-overview"></a><span data-ttu-id="0823f-111">Vue d’ensemble de Dapper</span><span class="sxs-lookup"><span data-stu-id="0823f-111">Dapper overview</span></span>
<span data-ttu-id="0823f-112">**Dapper** est un mappeur relationnel objet.</span><span class="sxs-lookup"><span data-stu-id="0823f-112">**Dapper** is an object-relational mapper.</span></span> <span data-ttu-id="0823f-113">Il mappe des objets .NET à partir de votre base de données relationnelle tooa application (et vice versa).</span><span class="sxs-lookup"><span data-stu-id="0823f-113">It maps .NET objects from your application tooa relational database (and vice versa).</span></span> <span data-ttu-id="0823f-114">première partie de Hello hello exemple de code illustre comment vous pouvez intégrer la bibliothèque cliente de base de données élastique hello avec les applications Dapper.</span><span class="sxs-lookup"><span data-stu-id="0823f-114">hello first part of hello sample code illustrates how you can integrate hello elastic database client library with Dapper-based applications.</span></span> <span data-ttu-id="0823f-115">deuxième partie de Hello hello exemple de code illustre comment toointegrate lorsque vous utilisez Dapper et DapperExtensions.</span><span class="sxs-lookup"><span data-stu-id="0823f-115">hello second part of hello sample code illustrates how toointegrate when using both Dapper and DapperExtensions.</span></span>  

<span data-ttu-id="0823f-116">fonctionnalité du Mappeur Hello dans Dapper fournit des méthodes d’extension sur les connexions de base de données qui simplifient l’envoi instructions T-SQL pour l’exécution ou l’interrogation de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-116">hello mapper functionality in Dapper provides extension methods on database connections that simplify submitting T-SQL statements for execution or querying hello database.</span></span> <span data-ttu-id="0823f-117">Par exemple, Dapper permet de facilement toomap entre vos objets .NET et les paramètres hello des instructions SQL pour **Execute** appels ou résultats de hello tooconsume de vos requêtes SQL en objets .NET à l’aide de **requête**appels à partir de Dapper.</span><span class="sxs-lookup"><span data-stu-id="0823f-117">For instance, Dapper makes it easy toomap between your .NET objects and hello parameters of SQL statements for **Execute** calls, or tooconsume hello results of your SQL queries into .NET objects using **Query** calls from Dapper.</span></span> 

<span data-ttu-id="0823f-118">Lorsque vous utilisez DapperExtensions, vous n’avez plus besoin des instructions SQL tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-118">When using DapperExtensions, you no longer need tooprovide hello SQL statements.</span></span> <span data-ttu-id="0823f-119">Méthodes d’extension comme **GetList** ou **insérer** via une connexion de base de données hello créer hello instructions SQL coulisses hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-119">Extensions methods such as **GetList** or **Insert** over hello database connection create hello SQL statements behind hello scenes.</span></span>

<span data-ttu-id="0823f-120">Un autre avantage de Dapper et DapperExtensions est que les contrôles de l’application hello hello la création d’une connexion de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-120">Another benefit of Dapper and also DapperExtensions is that hello application controls hello creation of hello database connection.</span></span> <span data-ttu-id="0823f-121">Cela permet d’interagir avec la bibliothèque cliente de base de données élastique hello qui courtiers selon le mappage hello de shardlets toodatabases de connexions de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-121">This helps interact with hello elastic database client library which brokers database connections based on hello mapping of shardlets toodatabases.</span></span>

<span data-ttu-id="0823f-122">assemblys de Dapper hello tooget, consultez [Dapper point net](http://www.nuget.org/packages/Dapper/).</span><span class="sxs-lookup"><span data-stu-id="0823f-122">tooget hello Dapper assemblies, see [Dapper dot net](http://www.nuget.org/packages/Dapper/).</span></span> <span data-ttu-id="0823f-123">Pour les extensions Dapper hello, consultez [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span><span class="sxs-lookup"><span data-stu-id="0823f-123">For hello Dapper extensions, see [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).</span></span>

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a><span data-ttu-id="0823f-124">Un coup de œil rapide à la bibliothèque cliente de base de données élastique hello</span><span class="sxs-lookup"><span data-stu-id="0823f-124">A quick Look at hello elastic database client library</span></span>
<span data-ttu-id="0823f-125">Avec la bibliothèque cliente de base de données élastique hello, définissez les partitions de vos données d’application appelées *shardlets* , mapper les toodatabases et les identifier par *clés de partitionnement*.</span><span class="sxs-lookup"><span data-stu-id="0823f-125">With hello elastic database client library, you define partitions of your application data called *shardlets* , map them toodatabases, and identify them by *sharding keys*.</span></span> <span data-ttu-id="0823f-126">Vous pouvez avoir autant de bases de données que nécessaire et distribuer vos shardlets sur ces bases de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-126">You can have as many databases as you need and distribute your shardlets across these databases.</span></span> <span data-ttu-id="0823f-127">mappage Hello des bases de données de partitionnement les valeurs de clé toohello est stockée par une carte de partitions fournie par l’API de la bibliothèque hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-127">hello mapping of sharding key values toohello databases is stored by a shard map provided by hello library’s APIs.</span></span> <span data-ttu-id="0823f-128">Cette fonctionnalité s’appelle la **gestion des cartes de partitions**.</span><span class="sxs-lookup"><span data-stu-id="0823f-128">This capability is called **shard map management**.</span></span> <span data-ttu-id="0823f-129">carte de partitions Hello sert également de broker hello de connexions de base de données pour les requêtes qui comportent une clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="0823f-129">hello shard map also serves as hello broker of database connections for requests that carry a sharding key.</span></span> <span data-ttu-id="0823f-130">Cette fonctionnalité est désignée tooas **routage dépendant des données**.</span><span class="sxs-lookup"><span data-stu-id="0823f-130">This capability is referred tooas **data dependent routing**.</span></span>

![Cartes de partitions et routage dépendant des données][1]

<span data-ttu-id="0823f-132">Gestionnaire de cartes de partitions Hello protège les utilisateurs à partir des vues incohérentes dans les données de shardlet qui peuvent se produire lorsque les opérations de gestion de shardlet simultanées sont produisent sur les bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-132">hello shard map manager protects users from inconsistent views into shardlet data that can occur when concurrent shardlet management operations are happening on hello databases.</span></span> <span data-ttu-id="0823f-133">toodo hello par conséquent, les connexions de base de données partition maps broker hello pour une application générée avec la bibliothèque de hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-133">toodo so, hello shard maps broker hello database connections for an application built with hello library.</span></span> <span data-ttu-id="0823f-134">Lorsque les opérations de gestion de partitions peut affecter les shardlets hello, ainsi, kill de hello partition carte fonctionnalité tooautomatically une connexion de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-134">When shard management operations could impact hello shardlet, this allows hello shard map functionality tooautomatically kill a database connection.</span></span> 

<span data-ttu-id="0823f-135">Au lieu d’utiliser des connexions de toocreate méthode traditionnelle hello pour Dapper, nous devons toouse hello [OpenConnectionForKey méthode](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span><span class="sxs-lookup"><span data-stu-id="0823f-135">Instead of using hello traditional way toocreate connections for Dapper, we need toouse hello [OpenConnectionForKey method](http://msdn.microsoft.com/library/azure/dn824099.aspx).</span></span> <span data-ttu-id="0823f-136">Cela garantit que tous les hello la validation a lieu et les connexions sont gérées correctement quand les données sont déplacées entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="0823f-136">This ensures that all hello validation takes place and connections are managed properly when any data moves between shards.</span></span>

### <a name="requirements-for-dapper-integration"></a><span data-ttu-id="0823f-137">Configuration requise pour l’intégration Dapper</span><span class="sxs-lookup"><span data-stu-id="0823f-137">Requirements for Dapper integration</span></span>
<span data-ttu-id="0823f-138">Lorsque vous travaillez avec la bibliothèque cliente de base de données élastique hello et hello API Dapper, nous souhaitons hello tooretain propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="0823f-138">When working with both hello elastic database client library and hello Dapper APIs, we want tooretain hello following properties:</span></span>

* <span data-ttu-id="0823f-139">**Montée en puissance parallèle**: nous souhaitez tooadd ou supprimer des bases de données de la couche de données hello d’application partitionnée hello en fonction des besoins de capacité hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-139">**Scaleout**: We want tooadd or remove databases from hello data tier of hello sharded application as necessary for hello capacity demands of hello application.</span></span> 
* <span data-ttu-id="0823f-140">**Cohérence**: notre application est à l’échelle à l’aide de partitionnement, nous avons besoin de routage dépendant des données tooperform.</span><span class="sxs-lookup"><span data-stu-id="0823f-140">**Consistency**: Since our application is scaled out using sharding, we need tooperform data dependent routing.</span></span> <span data-ttu-id="0823f-141">Par conséquent, nous souhaitons toouse hello données dépendantes capacités de routage de hello bibliothèque toodo.</span><span class="sxs-lookup"><span data-stu-id="0823f-141">We want toouse hello Data dependent routing capabilities of hello library toodo so.</span></span> <span data-ttu-id="0823f-142">En particulier, nous la validation tooretain hello et cohérence garantie fournie par les connexions qui sont réparties via le Gestionnaire de carte de partitions hello altération de tooavoid de commande ou les résultats de requête incorrect.</span><span class="sxs-lookup"><span data-stu-id="0823f-142">In particular, we want tooretain hello validation and consistency guarantees provided by connections that are brokered through hello shard map manager in order tooavoid corruption or wrong query results.</span></span> <span data-ttu-id="0823f-143">Cela garantit que tooa connexions étant donné les shardlets sont rejetés ou arrêtée si (par exemple) hello shardlet tooa actuellement déplacé d’une autre partition à l’aide des API de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="0823f-143">This ensures that connections tooa given shardlet are rejected or stopped if (for instance) hello shardlet is currently moved tooa different shard using Split/Merge APIs.</span></span>
* <span data-ttu-id="0823f-144">**Mappage d’objet**: nous souhaitons tooretain hello offerts par les mappages hello fournie par Dapper tootranslate entre les classes dans l’application hello et hello sous-jacent des structures de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-144">**Object Mapping**: We want tooretain hello convenience of hello mappings provided by Dapper tootranslate between classes in hello application and hello underlying database structures.</span></span> 

<span data-ttu-id="0823f-145">Hello section suivante fournit des conseils pour cette configuration requise pour les applications basées sur **Dapper** et **DapperExtensions**.</span><span class="sxs-lookup"><span data-stu-id="0823f-145">hello following section provides guidance for these requirements for applications based on **Dapper** and **DapperExtensions**.</span></span>

## <a name="technical-guidance"></a><span data-ttu-id="0823f-146">Conseils techniques</span><span class="sxs-lookup"><span data-stu-id="0823f-146">Technical Guidance</span></span>
### <a name="data-dependent-routing-with-dapper"></a><span data-ttu-id="0823f-147">Routage dépendant des données avec Dapper</span><span class="sxs-lookup"><span data-stu-id="0823f-147">Data dependent routing with Dapper</span></span>
<span data-ttu-id="0823f-148">Avec Dapper, l’application hello est généralement responsable de la création et l’ouverture toohello de connexions hello sous-jacent de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-148">With Dapper, hello application is typically responsible for creating and opening hello connections toohello underlying database.</span></span> <span data-ttu-id="0823f-149">Étant donné un type T à l’application hello, Dapper renvoie les résultats de la requête en collections .NET de type T. Dapper effectue le mappage de hello de hello T-SQL résultat lignes toohello objets de type T. De même, Dapper mappe des objets .NET en valeurs SQL ou des paramètres pour les instructions data manipulation language (DML).</span><span class="sxs-lookup"><span data-stu-id="0823f-149">Given a type T by hello application, Dapper returns query results as .NET collections of type T. Dapper performs hello mapping from hello T-SQL result rows toohello objects of type T. Similarly, Dapper maps .NET objects into SQL values or parameters for data manipulation language (DML) statements.</span></span> <span data-ttu-id="0823f-150">Dapper offre cette fonctionnalité via les méthodes d’extension sur hello régulière [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objet à partir de bibliothèques de ADO .NET SQL Client hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-150">Dapper offers this functionality via extension methods on hello regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) object from hello ADO .NET SQL Client libraries.</span></span> <span data-ttu-id="0823f-151">Hello connexion SQL retournée par hello API infrastructure élastique pour DDR sont également régulière [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objets.</span><span class="sxs-lookup"><span data-stu-id="0823f-151">hello SQL connection returned by hello Elastic Scale APIs for DDR are also regular [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects.</span></span> <span data-ttu-id="0823f-152">Cela nous permet toodirectly utilisent des extensions de Dapper sur le type hello retourné par DDR API la bibliothèque cliente de hello, car il s’agit également d’une connexion SQL Client simple.</span><span class="sxs-lookup"><span data-stu-id="0823f-152">This allows us toodirectly use Dapper extensions over hello type returned by hello client library’s DDR API, as it is also a simple SQL Client connection.</span></span>

<span data-ttu-id="0823f-153">Ces observations rendent connexions toouse simple demandées par la bibliothèque cliente de base de données élastique hello pour Dapper.</span><span class="sxs-lookup"><span data-stu-id="0823f-153">These observations make it straightforward toouse connections brokered by hello elastic database client library for Dapper.</span></span>

<span data-ttu-id="0823f-154">Cet exemple de code (à partir de hello exemple d’accompagnement) illustre l’approche hello où clé de partitionnement hello est fournie par hello application toohello bibliothèque toobroker hello connexion toohello droite partitions.</span><span class="sxs-lookup"><span data-stu-id="0823f-154">This code example (from hello accompanying sample) illustrates hello approach where hello sharding key is provided by hello application toohello library toobroker hello connection toohello right shard.</span></span>   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

<span data-ttu-id="0823f-155">Hello appel toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API remplace la création par défaut de hello et à l’ouverture d’une connexion SQL Client.</span><span class="sxs-lookup"><span data-stu-id="0823f-155">hello call toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API replaces hello default creation and opening of a SQL Client connection.</span></span> <span data-ttu-id="0823f-156">Hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appel prend des arguments de hello qui sont requis pour le routage dépendant des données :</span><span class="sxs-lookup"><span data-stu-id="0823f-156">hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call takes hello arguments that are required for data dependent routing:</span></span> 

* <span data-ttu-id="0823f-157">tooaccess de carte de partitions Hello hello interfaces de routage dépendant de données</span><span class="sxs-lookup"><span data-stu-id="0823f-157">hello shard map tooaccess hello data dependent routing interfaces</span></span>
* <span data-ttu-id="0823f-158">Hello partitionnement tooidentify clé hello shardlet</span><span class="sxs-lookup"><span data-stu-id="0823f-158">hello sharding key tooidentify hello shardlet</span></span>
* <span data-ttu-id="0823f-159">partition de toohello tooconnect Hello les informations d’identification (nom d’utilisateur et mot de passe)</span><span class="sxs-lookup"><span data-stu-id="0823f-159">hello credentials (user name and password) tooconnect toohello shard</span></span>

<span data-ttu-id="0823f-160">objet de mappage de partitions Hello crée une partition de toohello de connexion qui contient le shardlet hello pour hello étant donné la clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="0823f-160">hello shard map object creates a connection toohello shard that holds hello shardlet for hello given sharding key.</span></span> <span data-ttu-id="0823f-161">API du client de base de données élastique Hello également baliser hello tooimplement de connexion sa cohérence garantit.</span><span class="sxs-lookup"><span data-stu-id="0823f-161">hello elastic database client APIs also tag hello connection tooimplement its consistency guarantees.</span></span> <span data-ttu-id="0823f-162">Depuis hello appeler trop[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) retourne un objet de connexion SQL Client normal, les hello appeler toohello **Execute** méthode d’extension à partir de Dapper suit hello Dapper standard pratique.</span><span class="sxs-lookup"><span data-stu-id="0823f-162">Since hello call too[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) returns a regular SQL Client connection object, hello subsequent call toohello **Execute** extension method from Dapper follows hello standard Dapper practice.</span></span>

<span data-ttu-id="0823f-163">Requêtes travail hello très même façon - vous ouvrez d’abord à l’aide de connexion hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) à partir de l’API du client hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-163">Queries work very much hello same way - you first open hello connection using [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) from hello client API.</span></span> <span data-ttu-id="0823f-164">Puis vous utilisez hello régulière extension Dapper méthodes toomap hello résultats de votre requête SQL en objets .NET :</span><span class="sxs-lookup"><span data-stu-id="0823f-164">Then you use hello regular Dapper extension methods toomap hello results of your SQL query into .NET objects:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

<span data-ttu-id="0823f-165">Notez que hello **à l’aide de** bloquer des étendues de connexion hello DDR toutes les opérations de base de données dans une seule partition hello bloc toohello où tenantId1 est conservé.</span><span class="sxs-lookup"><span data-stu-id="0823f-165">Note that hello **using** block with hello DDR connection scopes all database operations within hello block toohello one shard where tenantId1 is kept.</span></span> <span data-ttu-id="0823f-166">requête de Hello retourne uniquement les blogs stockés sur la partition actuelle de hello, mais pas hello ceux qui sont stockés sur toutes les autres partitions.</span><span class="sxs-lookup"><span data-stu-id="0823f-166">hello query only returns blogs stored on hello current shard, but not hello ones stored on any other shards.</span></span> 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a><span data-ttu-id="0823f-167">Routage dépendant des données avec Dapper et DapperExtensions</span><span class="sxs-lookup"><span data-stu-id="0823f-167">Data dependent routing with Dapper and DapperExtensions</span></span>
<span data-ttu-id="0823f-168">Dapper est fourni avec un écosystème d’extensions supplémentaires qui peut fournir plus de commodité et d’abstraction de base de données hello lors du développement d’applications de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-168">Dapper comes with an ecosystem of additional extensions that can provide further convenience and abstraction from hello database when developing database applications.</span></span> <span data-ttu-id="0823f-169">DapperExtensions est un exemple.</span><span class="sxs-lookup"><span data-stu-id="0823f-169">DapperExtensions is an example.</span></span> 

<span data-ttu-id="0823f-170">L’utilisation de DapperExtensions dans votre application ne change pas la gestion ni la création des connexions de base de données.</span><span class="sxs-lookup"><span data-stu-id="0823f-170">Using DapperExtensions in your application does not change how database connections are created and managed.</span></span> <span data-ttu-id="0823f-171">Il est toujours responsabilité tooopen connexions l’application hello et les objets de connexion SQL Client régulières sont attendus par les méthodes d’extension hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-171">It is still hello application’s responsibility tooopen connections, and regular SQL Client connection objects are expected by hello extension methods.</span></span> <span data-ttu-id="0823f-172">Nous pouvons s’appuient sur hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0823f-172">We can rely on hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) as outlined above.</span></span> <span data-ttu-id="0823f-173">En tant que hello exemples de code suivants affichent, hello seule différence est que les instructions T-SQL de hello toowrite ne ne plus avoir :</span><span class="sxs-lookup"><span data-stu-id="0823f-173">As hello following code samples show, hello only change is that we do no longer have toowrite hello T-SQL statements:</span></span>

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

<span data-ttu-id="0823f-174">Et Voici des exemples de code hello pour la requête de hello :</span><span class="sxs-lookup"><span data-stu-id="0823f-174">And here is hello code sample for hello query:</span></span> 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a><span data-ttu-id="0823f-175">Gestion des erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="0823f-175">Handling transient faults</span></span>
<span data-ttu-id="0823f-176">Hello Microsoft Patterns & Practices équipe hello publiée [bloc applicatif de pannes gestion](http://msdn.microsoft.com/library/hh680934.aspx) les développeurs d’applications toohelp atténuer les conditions courantes d’erreurs transitoires rencontrées lors de l’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-176">hello Microsoft Patterns & Practices team published hello [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) toohelp application developers mitigate common transient fault conditions encountered when running in hello cloud.</span></span> <span data-ttu-id="0823f-177">Pour plus d’informations, consultez [Perseverance, le Secret de toutes les luttes : à l’aide de hello bloc applicatif de pannes gestion](http://msdn.microsoft.com/library/dn440719.aspx).</span><span class="sxs-lookup"><span data-stu-id="0823f-177">For more information, see [Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block](http://msdn.microsoft.com/library/dn440719.aspx).</span></span>

<span data-ttu-id="0823f-178">exemple de code Hello s’appuie sur hello erreurs transitoires bibliothèque tooprotect contre les erreurs transitoires.</span><span class="sxs-lookup"><span data-stu-id="0823f-178">hello code sample relies on hello transient fault library tooprotect against transient faults.</span></span> 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

<span data-ttu-id="0823f-179">**SqlDatabaseUtils.SqlRetryPolicy** Bonjour code ci-dessus est défini comme un **SqlDatabaseTransientErrorDetectionStrategy** avec un nombre de tentatives de 10 et 5 secondes délai entre deux tentatives.</span><span class="sxs-lookup"><span data-stu-id="0823f-179">**SqlDatabaseUtils.SqlRetryPolicy** in hello code above is defined as a **SqlDatabaseTransientErrorDetectionStrategy** with a retry count of 10, and 5 seconds wait time between retries.</span></span> <span data-ttu-id="0823f-180">Si vous utilisez des transactions, assurez-vous que vos objectifs de nouvelle tentative repasse toohello début de la transaction hello dans les cas de hello d’une erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="0823f-180">If you are using transactions, make sure that your retry scope goes back toohello beginning of hello transaction in hello case of a transient fault.</span></span>

## <a name="limitations"></a><span data-ttu-id="0823f-181">Limites</span><span class="sxs-lookup"><span data-stu-id="0823f-181">Limitations</span></span>
<span data-ttu-id="0823f-182">les approches Hello décrites dans ce document entraînent quelques limitations :</span><span class="sxs-lookup"><span data-stu-id="0823f-182">hello approaches outlined in this document entail a couple of limitations:</span></span>

* <span data-ttu-id="0823f-183">exemple de code Hello pour ce document ne montre pas comment schéma toomanage entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="0823f-183">hello sample code for this document does not demonstrate how toomanage schema across shards.</span></span>
* <span data-ttu-id="0823f-184">Étant donné une demande, nous partons du principe que tous les traitements de sa base de données sont contenue dans une même partition identifiée par la clé de partitionnement hello fournie par la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-184">Given a request, we assume that all its database processing is contained within a single shard as identified by hello sharding key provided by hello request.</span></span> <span data-ttu-id="0823f-185">Toutefois, cette hypothèse ne pas toujours maintenir, par exemple, lorsqu’il n’est pas possible de toomake une clé de partitionnement disponible.</span><span class="sxs-lookup"><span data-stu-id="0823f-185">However, this assumption does not always hold, for example, when it is not possible toomake a sharding key available.</span></span> <span data-ttu-id="0823f-186">tooaddress, hello bibliothèque cliente de base de données élastique inclut hello [MultiShardQuery classe](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span><span class="sxs-lookup"><span data-stu-id="0823f-186">tooaddress this, hello elastic database client library includes hello [MultiShardQuery class](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx).</span></span> <span data-ttu-id="0823f-187">classe Hello implémente une abstraction de la connexion pour l’interrogation sur plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="0823f-187">hello class implements a connection abstraction for querying over several shards.</span></span> <span data-ttu-id="0823f-188">L’utilisation de MultiShardQuery en association avec Dapper est abordée dans ce document hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-188">Using MultiShardQuery in combination with Dapper is beyond hello scope of this document.</span></span>

## <a name="conclusion"></a><span data-ttu-id="0823f-189">Conclusion</span><span class="sxs-lookup"><span data-stu-id="0823f-189">Conclusion</span></span>
<span data-ttu-id="0823f-190">Les applications utilisant Dapper et DapperExtensions peuvent facilement tirer parti des outils de la base de données élastique pour la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0823f-190">Applications using Dapper and DapperExtensions can easily benefit from elastic database tools for Azure SQL Database.</span></span> <span data-ttu-id="0823f-191">Hello les étapes décrites dans ce document, ces applications peuvent utiliser la fonctionnalité de l’outil hello pour les données dépendantes de routage par la modification de la création de hello et l’ouverture des nouveaux [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello de toouse objets [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) appel d’une bibliothèque cliente de base de données élastique hello.</span><span class="sxs-lookup"><span data-stu-id="0823f-191">Through hello steps outlined in this document, those applications can use hello tool's capability for data dependent routing by changing hello creation and opening of new [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) objects toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) call of hello elastic database client library.</span></span> <span data-ttu-id="0823f-192">Cela limite les emplacements de toothose requis de modifications hello application où les nouvelles connexions sont créées et ouvert.</span><span class="sxs-lookup"><span data-stu-id="0823f-192">This limits hello application changes required toothose places where new connections are created and opened.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png