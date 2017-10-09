---
title: "applications client-aaaMulti avec les outils de base de données élastique et de sécurité de niveau ligne"
description: "Découvrez comment toouse les outils de base de données élastique au niveau des lignes toobuild de sécurité une application avec un niveau de données hautement évolutif sur la base de données SQL Azure qui prend en charge les partitions de l’architecture mutualisées."
metakeywords: azure sql database elastic tools multi tenant row level security rls
services: sql-database
documentationcenter: 
manager: jhubbard
author: tmullaney
ms.assetid: e72d3cfe-e9be-4326-b776-9c6d96c0a18e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: thmullan;torsteng
ms.openlocfilehash: e00076a8db4a295374993aedd49f2318bd4d701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="d0957-103">Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes</span><span class="sxs-lookup"><span data-stu-id="d0957-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="d0957-104">[Outils de base de données élastique](sql-database-elastic-scale-get-started.md) et [(RLS) de sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131) offrent de puissantes de fonctionnalités pour la couche de données hello d’une application mutualisée avec la base de données SQL Azure mise à l’échelle flexible et plus efficacement.</span><span class="sxs-lookup"><span data-stu-id="d0957-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling hello data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="d0957-105">Consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d0957-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="d0957-106">Cet article explique comment toouse ces toobuild ensemble de technologies une application avec un niveau de données hautement évolutive qui prend en charge plusieurs locataires de partitions, à l’aide de **ADO.NET SqlClient** et/ou **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="d0957-106">This article illustrates how toouse these technologies together toobuild an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="d0957-107">**Outils de base de données élastique** permet aux développeurs des tooscale à la couche de données hello d’une application via des pratiques de partitionnement de la norme à l’aide d’un ensemble de bibliothèques .NET et les modèles de service Azure.</span><span class="sxs-lookup"><span data-stu-id="d0957-107">**Elastic database tools** enables developers tooscale out hello data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="d0957-108">Gestion des partitions à l’aide de la bibliothèque cliente de base de données élastique de hello permet d’automatiser et de rationaliser le grand nombre de tâches apportée à l’infrastructure de hello est généralement associés partitionnement.</span><span class="sxs-lookup"><span data-stu-id="d0957-108">Managing shards with using hello Elastic Database Client Library helps automate and streamline many of hello infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="d0957-109">**Sécurité au niveau des lignes** permet de données de toostore les développeurs pour plusieurs clients Bonjour même base de données à l’aide de toofilter de stratégies de sécurité les lignes qui n’appartiennent pas locataire toohello l’exécution d’une requête.</span><span class="sxs-lookup"><span data-stu-id="d0957-109">**Row-level security** enables developers toostore data for multiple tenants in hello same database using security policies toofilter out rows that do not belong toohello tenant executing a query.</span></span> <span data-ttu-id="d0957-110">En centralisant la logique d’accès avec des lignes au sein de la base de données hello, plutôt que dans l’application hello, simplifie la maintenance et de réduire les risques de hello d’erreur comme code de base d’une application se développe.</span><span class="sxs-lookup"><span data-stu-id="d0957-110">Centralizing access logic with RLS inside hello database, rather than in hello application, simplifies maintenance and reduces hello risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="d0957-111">L’utilisation de ces fonctionnalités ensemble, une application peut bénéficier de gains d’économies et l’efficacité de coût en stockant les données pour plusieurs locataires dans hello même base de données de la partition.</span><span class="sxs-lookup"><span data-stu-id="d0957-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in hello same shard database.</span></span> <span data-ttu-id="d0957-112">À hello même temps, une application toujours a toooffer de flexibilité hello isolé, partitions locataire unique pour les clients de « premium » qui requièrent des garanties de performance plus strictes dans la mesure où les partitions de l’architecture mutualisées ne garantissent pas la distribution des ressources égale entre les clients.</span><span class="sxs-lookup"><span data-stu-id="d0957-112">At hello same time, an application still has hello flexibility toooffer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="d0957-113">En bref, hello la bibliothèque cliente de base de données élastique [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) API connectent automatiquement aux clients toohello partition appropriée de base de données contenant la clé de partitionnement (généralement un « TenantId »).</span><span class="sxs-lookup"><span data-stu-id="d0957-113">In short, hello elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants toohello correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="d0957-114">Une fois connecté, une stratégie de sécurité RLS au sein de la base de données hello garantit que les clients peuvent accéder uniquement les lignes qui contiennent leur TenantId.</span><span class="sxs-lookup"><span data-stu-id="d0957-114">Once connected, an RLS security policy within hello database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="d0957-115">Il est supposé que toutes les tables contiennent un tooindicate de colonne TenantId quelles lignes appartiennent tooeach client.</span><span class="sxs-lookup"><span data-stu-id="d0957-115">It is assumed that all tables contain a TenantId column tooindicate which rows belong tooeach tenant.</span></span> 

![Architecture d’application de création de blogs][1]

## <a name="download-hello-sample-project"></a><span data-ttu-id="d0957-117">Télécharger l’exemple de projet hello</span><span class="sxs-lookup"><span data-stu-id="d0957-117">Download hello sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="d0957-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d0957-118">Prerequisites</span></span>
* <span data-ttu-id="d0957-119">Exécuter Visual Studio version 2012 ou plus</span><span class="sxs-lookup"><span data-stu-id="d0957-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="d0957-120">Créer trois bases de données SQL Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0957-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="d0957-121">Télécharger un exemple de projet : [Outils de base de données pour base de données SQL Microsoft Azure - Partitions multi-locataires](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="d0957-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="d0957-122">Renseignez les informations de hello pour vos bases de données au début de hello de **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="d0957-122">Fill in hello information for your databases at hello beginning of **Program.cs**</span></span> 

<span data-ttu-id="d0957-123">Ce projet étend hello une décrites dans [élastique outils de base de données pour SQL Azure - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) en ajoutant la prise en charge des bases de données de partition de l’architecture mutualisée.</span><span class="sxs-lookup"><span data-stu-id="d0957-123">This project extends hello one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="d0957-124">Il crée une application console simple pour la création de blogs et publications, avec quatre locataires et deux bases de données de la partition de l’architecture mutualisée comme illustré dans hello diagramme ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="d0957-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in hello above diagram.</span></span> 

<span data-ttu-id="d0957-125">Générez et exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d0957-125">Build and run hello application.</span></span> <span data-ttu-id="d0957-126">Cela sera amorcer des outils de base de données élastique hello Gestionnaire de carte de partitions et exécution hello suite de tests :</span><span class="sxs-lookup"><span data-stu-id="d0957-126">This will bootstrap hello elastic database tools’ shard map manager and run hello following tests:</span></span> 

1. <span data-ttu-id="d0957-127">À l’aide d’Entity Framework et de LINQ, créez un blog et affichez tous les blogs pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="d0957-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="d0957-128">À l’aide de la fonction SqlClient ADO.NET, affichez tous les blogs d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="d0957-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="d0957-129">Essayez tooinsert un blog pour hello client incorrect tooverify levée par une erreur</span><span class="sxs-lookup"><span data-stu-id="d0957-129">Try tooinsert a blog for hello wrong tenant tooverify that an error is thrown</span></span>  

<span data-ttu-id="d0957-130">Notez qu’étant donné que la sécurité RLS n’a pas encore été activée dans les bases de données de partition hello, chacun de ces tests révèle un problème : les clients sont en mesure de toosee blogs qui n’appartiennent pas toothem, et application hello n’empêche pas d’insérer un blog de client incorrect de hello.</span><span class="sxs-lookup"><span data-stu-id="d0957-130">Notice that because RLS has not yet been enabled in hello shard databases, each of these tests reveals a problem: tenants are able toosee blogs that do not belong toothem, and hello application is not prevented from inserting a blog for hello wrong tenant.</span></span> <span data-ttu-id="d0957-131">Hello reste de cet article décrit comment tooresolve locataire ces problèmes en mettant en isolement avec des lignes.</span><span class="sxs-lookup"><span data-stu-id="d0957-131">hello remainder of this article describes how tooresolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="d0957-132">La procédure à suivre implique deux étapes :</span><span class="sxs-lookup"><span data-stu-id="d0957-132">There are two steps:</span></span> 

1. <span data-ttu-id="d0957-133">**Couche application**: modifier le code de l’application hello tooalways ensemble hello actuel TenantId Bonjour SESSION_CONTEXT après l’ouverture d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="d0957-133">**Application tier**: Modify hello application code tooalways set hello current TenantId in hello SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="d0957-134">exemple de projet Hello a déjà fait.</span><span class="sxs-lookup"><span data-stu-id="d0957-134">hello sample project has already done this.</span></span> 
2. <span data-ttu-id="d0957-135">**Couche données**: créer une stratégie de sécurité RLS dans chaque toofilter de base de données de partition en fonction de hello TenantId de lignes stockées dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d0957-135">**Data tier**: Create an RLS security policy in each shard database toofilter rows based on hello TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="d0957-136">Vous en aurez besoin toodo pour chacun de vos bases de données de partition, sinon les lignes dans des partitions de l’architecture mutualisées ne sont pas filtrés.</span><span class="sxs-lookup"><span data-stu-id="d0957-136">You will need toodo this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a><span data-ttu-id="d0957-137">Couche d’Application étape 1) : définissez le TenantId Bonjour SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="d0957-137">Step 1) Application tier: Set TenantId in hello SESSION_CONTEXT</span></span>
<span data-ttu-id="d0957-138">Une fois la connexion tooa partition base de données à l’aide des données de la bibliothèque cliente hello élastique de base de données que fixes de l’API de routage dépendant, application hello a besoin de base de données tootell hello le TenantId est à l’aide de cette connexion afin qu’une stratégie de sécurité RLS peut filtrer les lignes clients tooother appartenant.</span><span class="sxs-lookup"><span data-stu-id="d0957-138">After connecting tooa shard database using hello elastic database client library’s data dependent routing APIs, hello application still needs tootell hello database which TenantId is using that connection so that an RLS security policy can filter out rows belonging tooother tenants.</span></span> <span data-ttu-id="d0957-139">Hello toopass recommandée sont de ces informations toostore hello TenantId actuel pour cette connexion Bonjour [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0957-139">hello recommended way toopass this information is toostore hello current TenantId for that connection in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="d0957-140">(Remarque : vous pouvez également utiliser [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mais SESSION_CONTEXT constitue une meilleure option car il est plus facile toouse, renvoie la valeur NULL par défaut et prend en charge les paires clé-valeur.)</span><span class="sxs-lookup"><span data-stu-id="d0957-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier toouse, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="d0957-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="d0957-141">Entity Framework</span></span>
<span data-ttu-id="d0957-142">Pour les applications à l’aide d’Entity Framework, approche la plus simple hello est hello tooset SESSION_CONTEXT dans hello ElasticScaleContext remplacer décrit dans [routage dépendant des données à l’aide de DbContext EF](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="d0957-142">For applications using Entity Framework, hello easiest approach is tooset hello SESSION_CONTEXT within hello ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="d0957-143">Avant de retourner la connexion hello répartie via le routage dépendant des données, il vous suffit de créer et de l’exécuter de SqlCommand qui définit 'TenantId' dans hello SESSION_CONTEXT toohello shardingKey spécifié pour cette connexion.</span><span class="sxs-lookup"><span data-stu-id="d0957-143">Before returning hello connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in hello SESSION_CONTEXT toohello shardingKey specified for that connection.</span></span> <span data-ttu-id="d0957-144">De cette manière, vous ne devez toowrite code une fois tooset hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d0957-144">This way, you only need toowrite code once tooset hello SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed toohello proper 
// shard by hello shard map manager. Note that hello base class c'tor call will fail for an open connection 
// if migrations need toobe done and SQL credentials are used. This is hello reason for hello  
// separation of c'tors into hello DDR case (this c'tor) and hello internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map toobroker a validated connection for hello given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", shardingKey);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
} 
// ... 
```

<span data-ttu-id="d0957-145">Maintenant hello SESSION_CONTEXT est défini automatiquement avec hello spécifié TenantId chaque fois que ElasticScaleContext est appelé :</span><span class="sxs-lookup"><span data-stu-id="d0957-145">Now hello SESSION_CONTEXT is automatically set with hello specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

```
// Program.cs 
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))   
    {     
        var query = from b in db.Blogs
                    orderby b.Name
                    select b;

        Console.WriteLine("All blogs for TenantId {0}:", tenantId);     
        foreach (var item in query)     
        {       
            Console.WriteLine(item.Name);     
        }   
    } 
}); 
```

### <a name="adonet-sqlclient"></a><span data-ttu-id="d0957-146">SqlClient ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d0957-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="d0957-147">Pour les applications utilisant ADO.NET SqlClient, hello recommandé consiste toocreate une fonction wrapper autour de ShardMap.OpenConnectionForKey() qui définit automatiquement 'TenantId' hello SESSION_CONTEXT toohello corriger TenantId avant de retourner un connexion.</span><span class="sxs-lookup"><span data-stu-id="d0957-147">For applications using ADO.NET SqlClient, hello recommended approach is toocreate a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in hello SESSION_CONTEXT toohello correct TenantId before returning a connection.</span></span> <span data-ttu-id="d0957-148">tooensure qui SESSION_CONTEXT a toujours la valeur, vous devez ouvrir uniquement les connexions à l’aide de cette fonction wrapper.</span><span class="sxs-lookup"><span data-stu-id="d0957-148">tooensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with hello correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method tooensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map toobroker a validated connection for hello given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT tooshardingKey tooenable Row-Level Security filtering
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"exec sp_set_session_context @key=N'TenantId', @value=@shardingKey";
        cmd.Parameters.AddWithValue("@shardingKey", tenantId);
        cmd.ExecuteNonQuery();

        return conn;
    }
    catch (Exception)
    {
        if (conn != null)
        {
            conn.Dispose();
        }

        throw;
    }
}

// ...

// Example query via ADO.NET SqlClient
// If row-level security is enabled, only Tenant 4's blogs will be listed
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
{
    using (SqlConnection conn = OpenConnectionForTenant(sharding.ShardMap, tenantId4, connStrBldr.ConnectionString))
    {
        SqlCommand cmd = conn.CreateCommand();
        cmd.CommandText = @"SELECT * FROM Blogs";

        Console.WriteLine("--\nAll blogs for TenantId {0} (using ADO.NET SqlClient):", tenantId4);
        SqlDataReader reader = cmd.ExecuteReader();
        while (reader.Read())
        {
            Console.WriteLine("{0}", reader["Name"]);
        }
    }
});

```

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="d0957-149">Étape 2) Couche données : création d’une stratégie de sécurité au niveau des lignes</span><span class="sxs-lookup"><span data-stu-id="d0957-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a><span data-ttu-id="d0957-150">Créer des lignes de chaque client peut accéder à un Bonjour de toofilter de stratégie de sécurité</span><span class="sxs-lookup"><span data-stu-id="d0957-150">Create a security policy toofilter hello rows each tenant can access</span></span>
<span data-ttu-id="d0957-151">Maintenant que l’application hello est paramètre SESSION_CONTEXT avec hello TenantId actuelle avant d’interroger, une stratégie de sécurité RLS peut filtrer les requêtes et exclure les lignes qui ont un TenantId différent.</span><span class="sxs-lookup"><span data-stu-id="d0957-151">Now that hello application is setting SESSION_CONTEXT with hello current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="d0957-152">La sécurité RLS est implémentée dans T-SQL : une fonction définie par l’utilisateur définit la logique d’accès hello et une stratégie de sécurité lie ce nombre tooany de fonction de tables.</span><span class="sxs-lookup"><span data-stu-id="d0957-152">RLS is implemented in T-SQL: a user-defined function defines hello access logic, and a security policy binds this function tooany number of tables.</span></span> <span data-ttu-id="d0957-153">Pour ce projet, fonction hello vérifiera simplement que hello application (plutôt qu’un autre utilisateur SQL) est connecté toohello de base de données, et ce hello 'TenantId' stocké dans hello SESSION_CONTEXT correspond à hello tenantid fait partie d’une ligne donnée.</span><span class="sxs-lookup"><span data-stu-id="d0957-153">For this project, hello function will simply verify that hello application (rather than some other SQL user) is connected toohello database, and that hello 'TenantId' stored in hello SESSION_CONTEXT matches hello TenantId of a given row.</span></span> <span data-ttu-id="d0957-154">Un prédicat de filtre autorisera les lignes qui répondent à ces conditions toopass filtre hello pour les requêtes SELECT, UPDATE et DELETE ; et un prédicat block empêchera les lignes qui violent ces conditions d’être insérée ou mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d0957-154">A filter predicate will allow rows that meet these conditions toopass through hello filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="d0957-155">Si SESSION_CONTEXT n’a pas été définie, elle retournera que null et aucune ligne ne sera visible ou en mesure de toobe inséré.</span><span class="sxs-lookup"><span data-stu-id="d0957-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able toobe inserted.</span></span> 

<span data-ttu-id="d0957-156">tooenable RLS, exécutez hello T-SQL suivant sur toutes les partitions à l’aide soit Visual Studio (SSDT), SSMS, ou hello script PowerShell inclus dans le projet de hello (ou si vous utilisez [des travaux de base de données élastique](sql-database-elastic-jobs-overview.md), vous pouvez l’utiliser dans l’exécution de tooautomate Ce T-SQL sur toutes les partitions) :</span><span class="sxs-lookup"><span data-stu-id="d0957-156">tooenable RLS, execute hello following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or hello PowerShell script included in hello project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it tooautomate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema tooorganize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- hello user in your application’s connection string (dbo is only for demo purposes!)         
        AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
GO

CREATE SECURITY POLICY rls.tenantAccessPolicy
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Blogs,
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.Posts
GO 
```

> [!TIP]
> <span data-ttu-id="d0957-157">Pour les projets plus complexes nécessitant le prédicat de hello tooadd sur des centaines de tables, vous pouvez utiliser une procédure stockée d’assistance qui génère automatiquement une stratégie de sécurité ajoutant un prédicat sur toutes les tables dans un schéma.</span><span class="sxs-lookup"><span data-stu-id="d0957-157">For more complex projects that need tooadd hello predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="d0957-158">Consultez [les tables tooall appliquer la sécurité au niveau des lignes - le script d’assistance (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="d0957-158">See [Apply Row-Level Security tooall tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="d0957-159">Maintenant si vous exécutez à nouveau les application exemple hello, locataires seront en mesure de toosee uniquement les lignes qui appartiennent toothem.</span><span class="sxs-lookup"><span data-stu-id="d0957-159">Now if you run hello sample application again, tenants will able toosee only rows that belong toothem.</span></span> <span data-ttu-id="d0957-160">En outre, application hello ne peut pas insérer les lignes qui appartiennent tootenants que base de données hello toohello actuellement connecté une partition, et il ne peut pas mettre à jour des lignes visibles toohave un TenantId différent.</span><span class="sxs-lookup"><span data-stu-id="d0957-160">In addition, hello application cannot insert rows that belong tootenants other than hello one currently connected toohello shard database, and it cannot update visible rows toohave a different TenantId.</span></span> <span data-ttu-id="d0957-161">Si l’application hello tente toodo soit, une DbUpdateException est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="d0957-161">If hello application attempts toodo either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="d0957-162">Si vous ajoutez ultérieurement sur une nouvelle table, ALTER simplement hello de stratégie de sécurité et ajouter des prédicats de filtre et block sur la nouvelle table de hello :</span><span class="sxs-lookup"><span data-stu-id="d0957-162">If you add a new table later on, simply ALTER hello security policy and add filter and block predicates on hello new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a><span data-ttu-id="d0957-163">Ajouter la valeur par défaut des contraintes tooautomatically remplir TenantId pour les insertions</span><span class="sxs-lookup"><span data-stu-id="d0957-163">Add default constraints tooautomatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="d0957-164">Vous pouvez placer une valeur par défaut contrainte sur chaque tooautomatically table remplir hello TenantId par hello valeur actuellement stockée dans SESSION_CONTEXT lors de l’insertion de lignes.</span><span class="sxs-lookup"><span data-stu-id="d0957-164">You can put a default constraint on each table tooautomatically populate hello TenantId with hello value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="d0957-165">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d0957-165">For example:</span></span> 

```
-- Create default constraints tooauto-populate TenantId with hello value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="d0957-166">Maintenant application hello dispense toospecify un TenantId lors de l’insertion de lignes :</span><span class="sxs-lookup"><span data-stu-id="d0957-166">Now hello application does not need toospecify a TenantId when inserting rows:</span></span> 

```
SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
{   
    using (var db = new ElasticScaleContext<int>(sharding.ShardMap, tenantId, connStrBldr.ConnectionString))
    {
        var blog = new Blog { Name = name }; // default constraint sets TenantId automatically     
        db.Blogs.Add(blog);     
        db.SaveChanges();   
    } 
}); 
```

> [!NOTE]
> <span data-ttu-id="d0957-167">Si vous utilisez des contraintes par défaut pour un projet Entity Framework, il est recommandé que vous n’incluez pas de colonne de TenantId hello dans votre modèle de données EF.</span><span class="sxs-lookup"><span data-stu-id="d0957-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include hello TenantId column in your EF data model.</span></span> <span data-ttu-id="d0957-168">Il s’agit, car les requêtes Entity Framework fournissent automatiquement les valeurs par défaut qui remplaceront les contraintes de valeur par défaut hello créés dans T-SQL qui utilisent SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d0957-168">This is because Entity Framework queries automatically supply default values which will override hello default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="d0957-169">contraintes de valeur par défaut toouse Bonjour exemple de projet, par exemple, vous devez supprimer les TenantId de DataClasses.cs (et exécution Add-Migration dans la Console du Gestionnaire de Package de hello) et tooensure utilisez T-SQL qui hello champ existe uniquement dans les tables de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d0957-169">toouse default constraints in hello sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in hello Package Manager Console) and use T-SQL tooensure that hello field only exists in hello database tables.</span></span> <span data-ttu-id="d0957-170">De cette façon, vous vous assurez qu’Entity Framework ne fournit pas automatiquement des valeurs par défaut incorrectes lors de l’insertion de données.</span><span class="sxs-lookup"><span data-stu-id="d0957-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a><span data-ttu-id="d0957-171">(Facultatif) Activer un tooaccess « superutilisateur » de toutes les lignes</span><span class="sxs-lookup"><span data-stu-id="d0957-171">(Optional) Enable a "superuser" tooaccess all rows</span></span>
<span data-ttu-id="d0957-172">Certaines applications veulent toocreate « superutilisateur » qui peut accéder à toutes les lignes, par exemple, dans tooenable d’ordre des rapports sur tous les locataires sur toutes les partitions ou les opérations de fractionnement/fusion tooperform sur les partitions qui impliquent le déplacement de lignes client entre les bases de données.</span><span class="sxs-lookup"><span data-stu-id="d0957-172">Some applications may want toocreate a "superuser" who can access all rows, for instance, in order tooenable reporting across all tenants on all shards, or tooperform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="d0957-173">tooenable, vous devez créer un nouvel utilisateur SQL (« superutilisateur » dans cet exemple) dans chaque base de données de partition.</span><span class="sxs-lookup"><span data-stu-id="d0957-173">tooenable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="d0957-174">Puis changez de stratégie de sécurité hello avec une nouvelle fonction de prédicat qui permet cette tooaccess utilisateur toutes les lignes :</span><span class="sxs-lookup"><span data-stu-id="d0957-174">Then alter hello security policy with a new predicate function that allows this user tooaccess all rows:</span></span>

```
-- New predicate function that adds superuser logic
CREATE FUNCTION rls.fn_tenantAccessPredicateWithSuperUser(@TenantId int)
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult 
        WHERE 
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- note, should not be dbo!
            AND CAST(SESSION_CONTEXT(N'TenantId') AS int) = @TenantId
        ) 
        OR
        (
            DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('superuser')
        )
GO

-- Atomically swap in hello new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="d0957-175">Maintenance </span><span class="sxs-lookup"><span data-stu-id="d0957-175">Maintenance</span></span>
* <span data-ttu-id="d0957-176">**Ajout de nouvelles partitions**: vous devez exécuter hello T-SQL script tooenable RLS sur toutes les nouvelles partitions, sinon les requêtes sur ces partitions ne sont pas filtrés.</span><span class="sxs-lookup"><span data-stu-id="d0957-176">**Adding new shards**: You must execute hello T-SQL script tooenable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="d0957-177">**Ajout de nouvelles tables**: vous devez ajouter un filtre et bloquer la stratégie de sécurité de prédicat toohello sur toutes les partitions chaque fois qu’une nouvelle table est créée, sinon les requêtes sur la nouvelle table de hello ne sont pas filtrés.</span><span class="sxs-lookup"><span data-stu-id="d0957-177">**Adding new tables**: You must add a filter and block predicate toohello security policy on all shards whenever a new table is created, otherwise queries on hello new table will not be filtered.</span></span> <span data-ttu-id="d0957-178">Cette opération peut être automatisée à l’aide d’un déclencheur DDL, comme décrit dans [appliquer la sécurité au niveau des lignes toonewly créé automatiquement les tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0957-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically toonewly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="d0957-179">Résumé</span><span class="sxs-lookup"><span data-stu-id="d0957-179">Summary</span></span>
<span data-ttu-id="d0957-180">Outils de base de données élastique et la sécurité de niveau ligne peuvent être utilisé tooscale ensemble à la couche de données d’une application prenant en charge des partitions mutualisées et locataire unique.</span><span class="sxs-lookup"><span data-stu-id="d0957-180">Elastic database tools and row-level security can be used together tooscale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="d0957-181">Partitions de l’architecture mutualisées peuvent être utilisé toostore données plus efficacement (en particulier dans les cas où un grand nombre de clients ont uniquement quelques lignes de données), lors de locataire unique partitions peuvent être des clients de premium toosupport utilisé avec l’isolation et de performances plus strictes configuration requise.</span><span class="sxs-lookup"><span data-stu-id="d0957-181">Multi-tenant shards can be used toostore data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used toosupport premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="d0957-182">Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="d0957-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d0957-183">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d0957-183">Additional resources</span></span>
* [<span data-ttu-id="d0957-184">Qu’est-ce qu’un pool élastique Azure ?</span><span class="sxs-lookup"><span data-stu-id="d0957-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="d0957-185">Montée en charge avec Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d0957-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="d0957-186">Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d0957-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="d0957-187">Authentification sur les applications mutualisées, avec Azure AD et OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="d0957-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="d0957-188">Application Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="d0957-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="d0957-189">Questions et demandes de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="d0957-189">Questions and Feature Requests</span></span>
<span data-ttu-id="d0957-190">Pour toute question, veuillez contacter toous sur hello [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et pour les demandes de fonctionnalités, ajoutez-les toohello [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="d0957-190">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


