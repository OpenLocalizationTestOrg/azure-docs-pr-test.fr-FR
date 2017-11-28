---
title: "Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes"
description: "Découvrez comment utiliser les outils de base de données élastique avec la fonction de sécurité au niveau des lignes (RLS) pour générer une application présentant une couche Données hautement évolutive sur la base de données SQL Microsoft Azure qui prend en charge les partitions multi-locataires."
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
ms.openlocfilehash: 73f1210b8d1f5ceca8fac9534d498bdc23d96d48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a><span data-ttu-id="6cbe1-103">Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes</span><span class="sxs-lookup"><span data-stu-id="6cbe1-103">Multi-tenant applications with elastic database tools and row-level security</span></span>
<span data-ttu-id="6cbe1-104">Les [outils de base de données élastique](sql-database-elastic-scale-get-started.md) et la fonction de [sécurité au niveau des lignes (RLS)](https://msdn.microsoft.com/library/dn765131) offrent un ensemble de puissants outils, qui permettent d’étendre la couche Données d’une application multi-locataires de manière souple et efficace au moyen d’Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-104">[Elastic database tools](sql-database-elastic-scale-get-started.md) and [row-level security (RLS)](https://msdn.microsoft.com/library/dn765131) offer a powerful set of capabilities for flexibly and efficiently scaling the data tier of a multi-tenant application with Azure SQL Database.</span></span> <span data-ttu-id="6cbe1-105">Consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-105">See [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) for more information.</span></span> 

<span data-ttu-id="6cbe1-106">Cet article explique comment utiliser ces technologies conjointement, afin de créer une application proposant une couche Données hautement évolutive, capable de prendre en charge des partitions multi-locataires, en utilisant **SqlClient ADO.NET** et/ou **Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-106">This article illustrates how to use these technologies together to build an application with a highly scalable data tier that supports multi-tenant shards, using **ADO.NET SqlClient** and/or **Entity Framework**.</span></span>  

* <span data-ttu-id="6cbe1-107">**outils de base de données élastique** permettent aux développeurs de monter en charge la couche Données d’une application via des pratiques de partitionnement normalisées, reposant sur un ensemble de bibliothèques .NET et des modèles de service Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-107">**Elastic database tools** enables developers to scale out the data tier of an application via industry-standard sharding practices using a set of .NET libraries and Azure service templates.</span></span> <span data-ttu-id="6cbe1-108">En gérant les partitions via la bibliothèque cliente de base de données élastique, vous rationalisez et automatisez nombre des tâches de l’infrastructure portant généralement sur le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-108">Managing shards with using the Elastic Database Client Library helps automate and streamline many of the infrastructural tasks typically associated with sharding.</span></span> 
* <span data-ttu-id="6cbe1-109">**sécurité au niveau des lignes** permet aux développeurs de stocker les données de plusieurs locataires dans la même base de données, à l’aide de stratégies de sécurité permettant de filtrer les lignes qui n’appartiennent pas au locataire exécutant une requête.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-109">**Row-level security** enables developers to store data for multiple tenants in the same database using security policies to filter out rows that do not belong to the tenant executing a query.</span></span> <span data-ttu-id="6cbe1-110">Grâce à la centralisation de la logique d’accès avec RLS dans la base de données plutôt que dans l’application, vous simplifiez la maintenance et réduisez le risque d’erreurs lorsque la codebase d’une application s’agrandit.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-110">Centralizing access logic with RLS inside the database, rather than in the application, simplifies maintenance and reduces the risk of error as an application’s codebase grows.</span></span> 

<span data-ttu-id="6cbe1-111">Grâce à l’utilisation conjointe de ces fonctionnalités, une application peut bénéficier d’une réduction des coûts et d’une optimisation de l’efficacité, via le stockage des données de plusieurs locataires au sein de la base de données d’une seule et même partition.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-111">Using these features together, an application can benefit from cost savings and efficiency gains by storing data for multiple tenants in the same shard database.</span></span> <span data-ttu-id="6cbe1-112">Parallèlement à cela, elle a toujours la possibilité de proposer des partitions isolées, incluant un seul locataire, aux locataires « premium » qui doivent respecter des exigences plus élevées en termes de performances. En effet, les partitions multi-locataires ne garantissent pas la distribution équitable des ressources entre les locataires.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-112">At the same time, an application still has the flexibility to offer isolated, single-tenant shards for “premium” tenants who require stricter performance guarantees since multi-tenant shards do not guarantee equal resource distribution among tenants.</span></span>  

<span data-ttu-id="6cbe1-113">En bref, la bibliothèque cliente de la base de données élastique offre des API de [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) , qui connectent automatiquement les locataires à la base de données de partition qui contient leur clé de partitionnement (il s’agit généralement d’un« ID de locataire »).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-113">In short, the elastic database client library’s [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) APIs automatically connect tenants to the correct shard database containing their sharding key (generally a “TenantId”).</span></span> <span data-ttu-id="6cbe1-114">Une fois la connexion établie, une stratégie de sécurité RLS appliquée au sein de la base de données s’assure que les locataires peuvent uniquement accéder aux lignes qui contiennent leur ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-114">Once connected, an RLS security policy within the database ensures that tenants can only access rows that contain their TenantId.</span></span> <span data-ttu-id="6cbe1-115">Le système part du principe que l’ensemble des tables contient une colonne « ID de locataire », qui indique à quel locataire appartiennent les lignes.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-115">It is assumed that all tables contain a TenantId column to indicate which rows belong to each tenant.</span></span> 

![Architecture d’application de création de blogs][1]

## <a name="download-the-sample-project"></a><span data-ttu-id="6cbe1-117">Téléchargement de l’exemple de projet</span><span class="sxs-lookup"><span data-stu-id="6cbe1-117">Download the sample project</span></span>
### <a name="prerequisites"></a><span data-ttu-id="6cbe1-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6cbe1-118">Prerequisites</span></span>
* <span data-ttu-id="6cbe1-119">Exécuter Visual Studio version 2012 ou plus</span><span class="sxs-lookup"><span data-stu-id="6cbe1-119">Use Visual Studio (2012 or higher)</span></span> 
* <span data-ttu-id="6cbe1-120">Créer trois bases de données SQL Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6cbe1-120">Create three Azure SQL Databases</span></span> 
* <span data-ttu-id="6cbe1-121">Télécharger un exemple de projet : [Outils de base de données pour base de données SQL Microsoft Azure - Partitions multi-locataires](http://go.microsoft.com/?linkid=9888163)</span><span class="sxs-lookup"><span data-stu-id="6cbe1-121">Download sample project: [Elastic DB Tools for Azure SQL - Multi-Tenant Shards](http://go.microsoft.com/?linkid=9888163)</span></span>
  * <span data-ttu-id="6cbe1-122">Saisissez les informations sur vos bases de données au début du fichier **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="6cbe1-122">Fill in the information for your databases at the beginning of **Program.cs**</span></span> 

<span data-ttu-id="6cbe1-123">Ce projet étend celui que décrit la section [Outils de base de données pour base de données SQL Microsoft Azure - Intégration d’Entity Framework](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) , en ajoutant la prise en charge des bases de données de partition multi-locataires.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-123">This project extends the one described in [Elastic DB Tools for Azure SQL - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) by adding support for multi-tenant shard databases.</span></span> <span data-ttu-id="6cbe1-124">Il permet de créer une application console simple afin de créer des blogs et des publications, avec quatre locataires et deux bases de données de partition multi-locataires (comme illustré dans le diagramme ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-124">It builds a simple console application for creating blogs and posts, with four tenants and two multi-tenant shard databases as illustrated in the above diagram.</span></span> 

<span data-ttu-id="6cbe1-125">Générez et exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-125">Build and run the application.</span></span> <span data-ttu-id="6cbe1-126">Cette opération démarre le gestionnaire de mappage de la partition dédiée aux outils de base de données élastique. Exécutez les tests suivants :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-126">This will bootstrap the elastic database tools’ shard map manager and run the following tests:</span></span> 

1. <span data-ttu-id="6cbe1-127">À l’aide d’Entity Framework et de LINQ, créez un blog et affichez tous les blogs pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-127">Using Entity Framework and LINQ, create a new blog and then display all blogs for each tenant</span></span>
2. <span data-ttu-id="6cbe1-128">À l’aide de la fonction SqlClient ADO.NET, affichez tous les blogs d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-128">Using ADO.NET SqlClient, display all blogs for a tenant</span></span>
3. <span data-ttu-id="6cbe1-129">Essayez d’insérer un blog associé à un locataire incorrect, afin de vérifier qu’une erreur est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-129">Try to insert a blog for the wrong tenant to verify that an error is thrown</span></span>  

<span data-ttu-id="6cbe1-130">Comme la fonction RLS n’a pas encore été activée sur les bases de données de la partition, vous pouvez voir que chacun de ces tests met en lumière un problème : les locataires peuvent afficher des blogs qui ne leur appartiennent pas et l’application est autorisée à insérer un blog associé à un locataire incorrect.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-130">Notice that because RLS has not yet been enabled in the shard databases, each of these tests reveals a problem: tenants are able to see blogs that do not belong to them, and the application is not prevented from inserting a blog for the wrong tenant.</span></span> <span data-ttu-id="6cbe1-131">Le reste de cet article explique comment résoudre ces problèmes en appliquant l’isolation des locataires avec la fonction RLS.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-131">The remainder of this article describes how to resolve these problems by enforcing tenant isolation with RLS.</span></span> <span data-ttu-id="6cbe1-132">La procédure à suivre implique deux étapes :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-132">There are two steps:</span></span> 

1. <span data-ttu-id="6cbe1-133">**Couche Application** : modifiez le code de l’application en définissant toujours l’élément SESSION_CONTEXT sur l’ID de locataire (TenantId)actuel après l’ouverture d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-133">**Application tier**: Modify the application code to always set the current TenantId in the SESSION_CONTEXT after opening a connection.</span></span> <span data-ttu-id="6cbe1-134">Cet exemple de projet a déjà effectué cette opération.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-134">The sample project has already done this.</span></span> 
2. <span data-ttu-id="6cbe1-135">**Couche Données** : créez une stratégie de sécurité RLS dans chaque base de données de partition, afin de filtrer les lignes selon l’ID de locataire (TenantId) stocké dans l’élément SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-135">**Data tier**: Create an RLS security policy in each shard database to filter rows based on the TenantId stored in SESSION_CONTEXT.</span></span> <span data-ttu-id="6cbe1-136">Vous devez procéder ainsi pour chaque base de données de partition. Dans le cas contraire, les lignes de partitions multi-locataires ne seront pas filtrées.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-136">You will need to do this for each of your shard databases, otherwise rows in multi-tenant shards will not be filtered.</span></span> 

## <a name="step-1-application-tier-set-tenantid-in-the-sessioncontext"></a><span data-ttu-id="6cbe1-137">Étape 1) Couche application : définissez l’identifiant de locataire dans l’élément SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="6cbe1-137">Step 1) Application tier: Set TenantId in the SESSION_CONTEXT</span></span>
<span data-ttu-id="6cbe1-138">Une fois la connexion à la base de données de partition établie, via les API de routage dépendant des données de la bibliothèque de base de données élastique, vous devez faire en sorte que l’application indique à la base de données quel ID de locataire utilise cette connexion, afin que la stratégie de sécurité RLS puisse filtrer les lignes appartenant aux autres locataires.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-138">After connecting to a shard database using the elastic database client library’s data dependent routing APIs, the application still needs to tell the database which TenantId is using that connection so that an RLS security policy can filter out rows belonging to other tenants.</span></span> <span data-ttu-id="6cbe1-139">Pour transmettre ces informations, la méthode recommandée consiste à stocker l’ID de locataire (TenantId) en cours pour cette connexion dans l’élément [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-139">The recommended way to pass this information is to store the current TenantId for that connection in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx).</span></span> <span data-ttu-id="6cbe1-140">(Remarque : vous pouvez également utiliser [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mais SESSION_CONTEXT offre une meilleure option, car cet élément, plus facile à utiliser, renvoie la valeur NULL par défaut et prend en charge les paires clé-valeur.)</span><span class="sxs-lookup"><span data-stu-id="6cbe1-140">(Note: You could alternatively use [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), but SESSION_CONTEXT is a better option because it is easier to use, returns NULL by default, and supports key-value pairs.)</span></span>

### <a name="entity-framework"></a><span data-ttu-id="6cbe1-141">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="6cbe1-141">Entity Framework</span></span>
<span data-ttu-id="6cbe1-142">Pour les applications utilisant Entity Framework, l’approche la plus simple consiste à définir l’élément SESSION_CONTEXT dans la substitution ElasticScaleContext décrite dans la section [Routage dépendant des données à l'aide de DbContext EF](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-142">For applications using Entity Framework, the easiest approach is to set the SESSION_CONTEXT within the ElasticScaleContext override described in [Data Dependent Routing using EF DbContext](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext).</span></span> <span data-ttu-id="6cbe1-143">Avant de retourner la connexion répartie via le routage dépendant des données, vous devez simplement créer et exécuter une commande SqlCommand qui définit l’élément SESSION_CONTEXT sur la valeur shardingKey spécifiée pour cette connexion.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-143">Before returning the connection brokered through data dependent routing, simply create and execute a SqlCommand that sets 'TenantId' in the SESSION_CONTEXT to the shardingKey specified for that connection.</span></span> <span data-ttu-id="6cbe1-144">De cette façon, il vous suffit d’écrire le code une seule fois pour définir l’élément SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-144">This way, you only need to write code once to set the SESSION_CONTEXT.</span></span> 

```
// ElasticScaleContext.cs 
// ... 
// C'tor for data dependent routing. This call will open a validated connection routed to the proper 
// shard by the shard map manager. Note that the base class c'tor call will fail for an open connection 
// if migrations need to be done and SQL credentials are used. This is the reason for the  
// separation of c'tors into the DDR case (this c'tor) and the internal c'tor for new shards. 
public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
    : base(OpenDDRConnection(shardMap, shardingKey, connectionStr), true /* contextOwnsConnection */)
{
}

public static SqlConnection OpenDDRConnection(ShardMap shardMap, T shardingKey, string connectionStr)
{
    // No initialization
    Database.SetInitializer<ElasticScaleContext<T>>(null);

    // Ask shard map to broker a validated connection for the given key
    SqlConnection conn = null;
    try
    {
        conn = shardMap.OpenConnectionForKey(shardingKey, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

<span data-ttu-id="6cbe1-145">Désormais, l’élément SESSION_CONTEXT est automatiquement défini avec l’ID de locataire spécifié chaque fois que le paramètre ElasticScaleContext est appelé :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-145">Now the SESSION_CONTEXT is automatically set with the specified TenantId whenever ElasticScaleContext is invoked:</span></span> 

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

### <a name="adonet-sqlclient"></a><span data-ttu-id="6cbe1-146">SqlClient ADO.NET</span><span class="sxs-lookup"><span data-stu-id="6cbe1-146">ADO.NET SqlClient</span></span>
<span data-ttu-id="6cbe1-147">Pour les applications utilisant SqlClient ADO.NET, il est recommandé d’opter pour la création d’une fonction wrapper autour de ShardMap.OpenConnectionForKey() qui définit automatiquement SESSION_CONTEXT sur l’ID de locataire correct avant de renvoyer une connexion.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-147">For applications using ADO.NET SqlClient, the recommended approach is to create a wrapper function around ShardMap.OpenConnectionForKey() that automatically sets 'TenantId' in the SESSION_CONTEXT to the correct TenantId before returning a connection.</span></span> <span data-ttu-id="6cbe1-148">Pour garantir que SESSION_CONTEXT est toujours défini, vous ne devez ouvrir des connexions qu’à l’aide de cette fonction wrapper.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-148">To ensure that SESSION_CONTEXT is always set, you should only open connections using this wrapper function.</span></span>

```
// Program.cs
// ...

// Wrapper function for ShardMap.OpenConnectionForKey() that automatically sets SESSION_CONTEXT with the correct
// tenantId before returning a connection. As a best practice, you should only open connections using this 
// method to ensure that SESSION_CONTEXT is always set before executing a query.
public static SqlConnection OpenConnectionForTenant(ShardMap shardMap, int tenantId, string connectionStr)
{
    SqlConnection conn = null;
    try
    {
        // Ask shard map to broker a validated connection for the given key
        conn = shardMap.OpenConnectionForKey(tenantId, connectionStr, ConnectionOptions.Validate);

        // Set TenantId in SESSION_CONTEXT to shardingKey to enable Row-Level Security filtering
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

## <a name="step-2-data-tier-create-row-level-security-policy"></a><span data-ttu-id="6cbe1-149">Étape 2) Couche données : création d’une stratégie de sécurité au niveau des lignes</span><span class="sxs-lookup"><span data-stu-id="6cbe1-149">Step 2) Data tier: Create row-level security policy</span></span>
### <a name="create-a-security-policy-to-filter-the-rows-each-tenant-can-access"></a><span data-ttu-id="6cbe1-150">Créez une stratégie de sécurité pour filtrer les lignes accessibles à chaque client.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-150">Create a security policy to filter the rows each tenant can access</span></span>
<span data-ttu-id="6cbe1-151">Comme l’application définit désormais l’élément SESSION_CONTEXT avec l’ID de locataire en cours avant d’envoyer des requêtes, une stratégie de sécurité RLS peut filtrer les requêtes et exclure les lignes associées à un ID de locataire différent.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-151">Now that the application is setting SESSION_CONTEXT with the current TenantId before querying, an RLS security policy can filter queries and exclude rows that have a different TenantId.</span></span>  

<span data-ttu-id="6cbe1-152">La fonction RLS est implémentée dans T-SQL : une fonction définie par l’utilisateur détermine la logique d’accès, et une stratégie de sécurité lie cette fonction à un nombre de tables quelconque.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-152">RLS is implemented in T-SQL: a user-defined function defines the access logic, and a security policy binds this function to any number of tables.</span></span> <span data-ttu-id="6cbe1-153">Pour les besoins de ce projet, la fonction vérifie simplement que l’application (plutôt qu’un autre utilisateur SQL) est connectée à la base de données, et que l’ID de locataire stocké dans l’élément SESSION_CONTEXT correspond à l’ID de locataire d’une ligne donnée.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-153">For this project, the function will simply verify that the application (rather than some other SQL user) is connected to the database, and that the 'TenantId' stored in the SESSION_CONTEXT matches the TenantId of a given row.</span></span> <span data-ttu-id="6cbe1-154">Un prédicat de filtrage permet de filtrer les lignes satisfaisant à ces conditions pour les requêtes SELECT, UPDATE et DELETE ; un prédicat de blocage empêche l’insertion ou la mise à jour des lignes qui violent ces conditions.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-154">A filter predicate will allow rows that meet these conditions to pass through the filter for SELECT, UPDATE, and DELETE queries; and a block predicate will prevent rows that violate these conditions from being INSERTed or UPDATEd.</span></span> <span data-ttu-id="6cbe1-155">Si l’élément SESSION_CONTEXT n’a pas été défini, il retournera la valeur NULL et aucune ligne ne sera visible ou ne pourra être insérée.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-155">If SESSION_CONTEXT has not been set, it will return NULL and no rows will be visible or able to be inserted.</span></span> 

<span data-ttu-id="6cbe1-156">Pour activer la fonction RLS, exécutez la commande T-SQL suivante sur toutes les partitions, à l’aide de Visual Studio (SSDT), de SSMS ou du script PowerShell inclus dans le projet (le cas échéant, si vous avez recours aux [tâches de la base de données élastique](sql-database-elastic-jobs-overview.md), vous pouvez les utiliser pour automatiser l’exécution de cette commande T-SQL sur toutes les partitions) :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-156">To enable RLS, execute the following T-SQL on all shards using either Visual Studio (SSDT), SSMS, or the PowerShell script included in the project (or if you are using [Elastic Database Jobs](sql-database-elastic-jobs-overview.md), you can use it to automate execution of this T-SQL on all shards):</span></span> 

```
CREATE SCHEMA rls -- separate schema to organize RLS objects 
GO

CREATE FUNCTION rls.fn_tenantAccessPredicate(@TenantId int)     
    RETURNS TABLE     
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS fn_accessResult          
        WHERE DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('dbo') -- the user in your application’s connection string (dbo is only for demo purposes!)         
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
> <span data-ttu-id="6cbe1-157">Pour les projets plus complexes qui nécessitent l’ajout du prédicat à des centaines de tables, vous pouvez utiliser une procédure stockée d’assistance, qui génère automatiquement une stratégie de sécurité en ajoutant un prédicat sur toutes les tables dans un schéma.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-157">For more complex projects that need to add the predicate on hundreds of tables, you can use a helper stored procedure that automatically generates a security policy adding a predicate on all tables in a schema.</span></span> <span data-ttu-id="6cbe1-158">Consultez le [blog Apply Row-Level Security to all tables - helper script (Appliquer la sécurité au niveau des lignes à toutes les tables - Script d’assistance)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-158">See [Apply Row-Level Security to all tables - helper script (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).</span></span>  
> 
> 

<span data-ttu-id="6cbe1-159">À présent, si vous exécutez l’exemple d’application une nouvelle fois, les locataires ne seront en mesure de voir que les lignes qui leur appartiennent.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-159">Now if you run the sample application again, tenants will able to see only rows that belong to them.</span></span> <span data-ttu-id="6cbe1-160">Par ailleurs, l’application ne peut pas insérer des lignes qui appartiennent à un locataire autre que celui qui est actuellement connecté à la base de données de partition, de même qu’elle ne peut pas mettre à jour les lignes visibles pour leur affecter un autre ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-160">In addition, the application cannot insert rows that belong to tenants other than the one currently connected to the shard database, and it cannot update visible rows to have a different TenantId.</span></span> <span data-ttu-id="6cbe1-161">Si elle tente d’effectuer l’une ou l’autre de ces opérations, une exception DbUpdateException est déclenchée.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-161">If the application attempts to do either, a DbUpdateException will be raised.</span></span>

<span data-ttu-id="6cbe1-162">Si vous ajoutez une nouvelle table par la suite, il vous suffit de MODIFIER la stratégie de sécurité et d’ajouter des prédicats de filtrage et de blocage sur la nouvelle table :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-162">If you add a new table later on, simply ALTER the security policy and add filter and block predicates on the new table:</span></span> 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-to-automatically-populate-tenantid-for-inserts"></a><span data-ttu-id="6cbe1-163">Ajouter des contraintes par défaut afin d’indiquer automatiquement les ID de locataire pour les opérations INSERT</span><span class="sxs-lookup"><span data-stu-id="6cbe1-163">Add default constraints to automatically populate TenantId for INSERTs</span></span>
<span data-ttu-id="6cbe1-164">Vous pouvez placer une contrainte par défaut sur chaque table pour renseigner automatiquement l’ID de locataire avec la valeur actuellement stockée dans l’élément SESSION_CONTEXT lors de l’insertion de lignes.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-164">You can put a default constraint on each table to automatically populate the TenantId with the value currently stored in SESSION_CONTEXT when inserting rows.</span></span> <span data-ttu-id="6cbe1-165">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-165">For example:</span></span> 

```
-- Create default constraints to auto-populate TenantId with the value of SESSION_CONTEXT for inserts 
ALTER TABLE Blogs     
    ADD CONSTRAINT df_TenantId_Blogs      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO

ALTER TABLE Posts     
    ADD CONSTRAINT df_TenantId_Posts      
    DEFAULT CAST(SESSION_CONTEXT(N'TenantId') AS int) FOR TenantId 
GO 
```

<span data-ttu-id="6cbe1-166">À présent, l’application n’a pas besoin de spécifier un ID de locataire lors de l’insertion de lignes :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-166">Now the application does not need to specify a TenantId when inserting rows:</span></span> 

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
> <span data-ttu-id="6cbe1-167">Si vous utilisez des contraintes par défaut pour un projet Entity Framework, il est recommandé de ne PAS inclure la colonne « ID de locataire » dans votre modèle de données Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-167">If you use default constraints for an Entity Framework project, it is recommended that you do NOT include the TenantId column in your EF data model.</span></span> <span data-ttu-id="6cbe1-168">En effet, les requêtes Entity Framework fournissent automatiquement des valeurs par défaut, qui remplacent les contraintes par défaut créées dans T-SQL et qui utilisent l’élément SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-168">This is because Entity Framework queries automatically supply default values which will override the default constraints created in T-SQL that use SESSION_CONTEXT.</span></span> <span data-ttu-id="6cbe1-169">Pour utiliser les contraintes par défaut dans l’exemple de projet, par exemple, vous devez supprimer l’ID de locataire dans le fichier DataClasses.cs (et exécuter l’élément Add-Migration dans la Console du gestionnaire de package), puis utiliser T-SQL pour vérifier que le champ existe uniquement dans les tables de base de données.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-169">To use default constraints in the sample project, for instance, you should remove TenantId from DataClasses.cs (and run Add-Migration in the Package Manager Console) and use T-SQL to ensure that the field only exists in the database tables.</span></span> <span data-ttu-id="6cbe1-170">De cette façon, vous vous assurez qu’Entity Framework ne fournit pas automatiquement des valeurs par défaut incorrectes lors de l’insertion de données.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-170">This way, EF will not automatically supply incorrect default values when inserting data.</span></span> 
> 
> 

### <a name="optional-enable-a-superuser-to-access-all-rows"></a><span data-ttu-id="6cbe1-171">(Facultatif) Activer un « superutilisateur » pour accéder à toutes les lignes</span><span class="sxs-lookup"><span data-stu-id="6cbe1-171">(Optional) Enable a "superuser" to access all rows</span></span>
<span data-ttu-id="6cbe1-172">Certaines applications peuvent nécessiter la création d’un « superutilisateur » pouvant accéder à toutes les lignes. Cela permet par exemple d’activer la création de rapports pour tous les locataires de toutes les partitions, ou d’exécuter des opérations de fractionnement et de fusion sur des partitions impliquant le déplacement de lignes de locataires entre les bases de données.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-172">Some applications may want to create a "superuser" who can access all rows, for instance, in order to enable reporting across all tenants on all shards, or to perform Split/Merge operations on shards that involve moving tenant rows between databases.</span></span> <span data-ttu-id="6cbe1-173">Pour ce faire, vous devez créer un nouvel utilisateur SQL (un « superutilisateur » dans cet exemple) dans chaque base de données de partition.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-173">To enable this, you should create a new SQL user ("superuser" in this example) in each shard database.</span></span> <span data-ttu-id="6cbe1-174">Vous devez ensuite modifier la stratégie de sécurité en ajoutant une nouvelle fonction de prédicat permettant à cet utilisateur d’accéder à toutes les lignes :</span><span class="sxs-lookup"><span data-stu-id="6cbe1-174">Then alter the security policy with a new predicate function that allows this user to access all rows:</span></span>

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

-- Atomically swap in the new predicate function on each table
ALTER SECURITY POLICY rls.tenantAccessPolicy
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Blogs,
    ALTER FILTER PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts,
    ALTER BLOCK PREDICATE rls.fn_tenantAccessPredicateWithSuperUser(TenantId) ON dbo.Posts
GO
```


### <a name="maintenance"></a><span data-ttu-id="6cbe1-175">Maintenance</span><span class="sxs-lookup"><span data-stu-id="6cbe1-175">Maintenance</span></span>
* <span data-ttu-id="6cbe1-176">**Ajout de nouvelles partitions** : vous devez exécuter le script T-SQL pour activer la fonction RLS sur les nouvelles partitions. Dans le cas contraire, les requêtes portant sur ces partitions ne seront pas filtrées.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-176">**Adding new shards**: You must execute the T-SQL script to enable RLS on any new shards, otherwise queries on these shards will not be filtered.</span></span>
* <span data-ttu-id="6cbe1-177">**Ajout de nouvelles tables** : vous devez ajouter un prédicat de filtrage et de blocage à la stratégie de sécurité sur toutes les partitions chaque fois qu’une table est créée. Dans le cas contraire, les requêtes portant sur la nouvelle table ne seront pas filtrées.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-177">**Adding new tables**: You must add a filter and block predicate to the security policy on all shards whenever a new table is created, otherwise queries on the new table will not be filtered.</span></span> <span data-ttu-id="6cbe1-178">Vous pouvez automatiser ce processus par le biais d’un déclencheur DDL, comme décrit dans l’article [Apply Row-Level Security automatically to newly created tables (Appliquer automatiquement la sécurité au niveau des lignes aux nouvelles tables) (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-178">This can be automated using a DDL trigger, as described in [Apply Row-Level Security automatically to newly created tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).</span></span>

## <a name="summary"></a><span data-ttu-id="6cbe1-179">Résumé</span><span class="sxs-lookup"><span data-stu-id="6cbe1-179">Summary</span></span>
<span data-ttu-id="6cbe1-180">Les outils de base de données élastique et la fonction de sécurité au niveau des lignes (RLS) peuvent être utilisés ensemble pour faire monter en charge la couche Données d’une application prenant en charge les partitions multi-locataires ou à un seul locataire.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-180">Elastic database tools and row-level security can be used together to scale out an application’s data tier with support for both multi-tenant and single-tenant shards.</span></span> <span data-ttu-id="6cbe1-181">Les partitions multi-locataires peuvent être utilisées pour stocker des données de manière plus efficace (notamment dans les cas où un grand nombre de locataires présente quelques lignes de données seulement). Les partitions à un seul locataire peuvent quant à elles servir à prendre en charge les locataires « premium » qui doivent respecter des exigences plus élevées en termes de performances et d’isolation.</span><span class="sxs-lookup"><span data-stu-id="6cbe1-181">Multi-tenant shards can be used to store data more efficiently (particularly in cases where a large number of tenants have only a few rows of data), while single-tenant shards can be used to support premium tenants with stricter performance and isolation requirements.</span></span>  <span data-ttu-id="6cbe1-182">Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-182">For more information, see [Row-Level Security reference](https://msdn.microsoft.com/library/dn765131).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6cbe1-183">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6cbe1-183">Additional resources</span></span>
* [<span data-ttu-id="6cbe1-184">Qu’est-ce qu’un pool élastique Azure ?</span><span class="sxs-lookup"><span data-stu-id="6cbe1-184">What is an Azure elastic pool?</span></span>](sql-database-elastic-pool.md)
* [<span data-ttu-id="6cbe1-185">Montée en charge avec Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6cbe1-185">Scaling out with Azure SQL Database</span></span>](sql-database-elastic-scale-introduction.md)
* [<span data-ttu-id="6cbe1-186">Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6cbe1-186">Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database</span></span>](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [<span data-ttu-id="6cbe1-187">Authentification sur les applications mutualisées, avec Azure AD et OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="6cbe1-187">Authentication in multitenant apps, using Azure AD and OpenID Connect</span></span>](../guidance/guidance-multitenant-identity-authenticate.md)
* [<span data-ttu-id="6cbe1-188">Application Tailspin Surveys</span><span class="sxs-lookup"><span data-stu-id="6cbe1-188">Tailspin Surveys application</span></span>](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a><span data-ttu-id="6cbe1-189">Questions et demandes de fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="6cbe1-189">Questions and Feature Requests</span></span>
<span data-ttu-id="6cbe1-190">Pour toute question, contactez-nous sur le [forum SQL Database](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et formulez vos demandes de fonctionnalités éventuelles sur le [forum de commentaires SQL Database](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="6cbe1-190">For questions, please reach out to us on the [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them to the [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


