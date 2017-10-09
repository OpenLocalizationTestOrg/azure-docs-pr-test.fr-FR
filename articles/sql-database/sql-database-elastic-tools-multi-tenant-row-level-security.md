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
# <a name="multi-tenant-applications-with-elastic-database-tools-and-row-level-security"></a>Applications multi-locataires avec des outils de base de données élastique et la sécurité au niveau des lignes
[Outils de base de données élastique](sql-database-elastic-scale-get-started.md) et [(RLS) de sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131) offrent de puissantes de fonctionnalités pour la couche de données hello d’une application mutualisée avec la base de données SQL Azure mise à l’échelle flexible et plus efficacement. Consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md) pour plus d’informations. 

Cet article explique comment toouse ces toobuild ensemble de technologies une application avec un niveau de données hautement évolutive qui prend en charge plusieurs locataires de partitions, à l’aide de **ADO.NET SqlClient** et/ou **Entity Framework**.  

* **Outils de base de données élastique** permet aux développeurs des tooscale à la couche de données hello d’une application via des pratiques de partitionnement de la norme à l’aide d’un ensemble de bibliothèques .NET et les modèles de service Azure. Gestion des partitions à l’aide de la bibliothèque cliente de base de données élastique de hello permet d’automatiser et de rationaliser le grand nombre de tâches apportée à l’infrastructure de hello est généralement associés partitionnement. 
* **Sécurité au niveau des lignes** permet de données de toostore les développeurs pour plusieurs clients Bonjour même base de données à l’aide de toofilter de stratégies de sécurité les lignes qui n’appartiennent pas locataire toohello l’exécution d’une requête. En centralisant la logique d’accès avec des lignes au sein de la base de données hello, plutôt que dans l’application hello, simplifie la maintenance et de réduire les risques de hello d’erreur comme code de base d’une application se développe. 

L’utilisation de ces fonctionnalités ensemble, une application peut bénéficier de gains d’économies et l’efficacité de coût en stockant les données pour plusieurs locataires dans hello même base de données de la partition. À hello même temps, une application toujours a toooffer de flexibilité hello isolé, partitions locataire unique pour les clients de « premium » qui requièrent des garanties de performance plus strictes dans la mesure où les partitions de l’architecture mutualisées ne garantissent pas la distribution des ressources égale entre les clients.  

En bref, hello la bibliothèque cliente de base de données élastique [routage dépendant des données](sql-database-elastic-scale-data-dependent-routing.md) API connectent automatiquement aux clients toohello partition appropriée de base de données contenant la clé de partitionnement (généralement un « TenantId »). Une fois connecté, une stratégie de sécurité RLS au sein de la base de données hello garantit que les clients peuvent accéder uniquement les lignes qui contiennent leur TenantId. Il est supposé que toutes les tables contiennent un tooindicate de colonne TenantId quelles lignes appartiennent tooeach client. 

![Architecture d’application de création de blogs][1]

## <a name="download-hello-sample-project"></a>Télécharger l’exemple de projet hello
### <a name="prerequisites"></a>Composants requis
* Exécuter Visual Studio version 2012 ou plus 
* Créer trois bases de données SQL Microsoft Azure 
* Télécharger un exemple de projet : [Outils de base de données pour base de données SQL Microsoft Azure - Partitions multi-locataires](http://go.microsoft.com/?linkid=9888163)
  * Renseignez les informations de hello pour vos bases de données au début de hello de **Program.cs** 

Ce projet étend hello une décrites dans [élastique outils de base de données pour SQL Azure - Entity Framework Integration](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md) en ajoutant la prise en charge des bases de données de partition de l’architecture mutualisée. Il crée une application console simple pour la création de blogs et publications, avec quatre locataires et deux bases de données de la partition de l’architecture mutualisée comme illustré dans hello diagramme ci-dessus. 

Générez et exécutez l’application hello. Cela sera amorcer des outils de base de données élastique hello Gestionnaire de carte de partitions et exécution hello suite de tests : 

1. À l’aide d’Entity Framework et de LINQ, créez un blog et affichez tous les blogs pour chaque client.
2. À l’aide de la fonction SqlClient ADO.NET, affichez tous les blogs d’un locataire.
3. Essayez tooinsert un blog pour hello client incorrect tooverify levée par une erreur  

Notez qu’étant donné que la sécurité RLS n’a pas encore été activée dans les bases de données de partition hello, chacun de ces tests révèle un problème : les clients sont en mesure de toosee blogs qui n’appartiennent pas toothem, et application hello n’empêche pas d’insérer un blog de client incorrect de hello. Hello reste de cet article décrit comment tooresolve locataire ces problèmes en mettant en isolement avec des lignes. La procédure à suivre implique deux étapes : 

1. **Couche application**: modifier le code de l’application hello tooalways ensemble hello actuel TenantId Bonjour SESSION_CONTEXT après l’ouverture d’une connexion. exemple de projet Hello a déjà fait. 
2. **Couche données**: créer une stratégie de sécurité RLS dans chaque toofilter de base de données de partition en fonction de hello TenantId de lignes stockées dans SESSION_CONTEXT. Vous en aurez besoin toodo pour chacun de vos bases de données de partition, sinon les lignes dans des partitions de l’architecture mutualisées ne sont pas filtrés. 

## <a name="step-1-application-tier-set-tenantid-in-hello-sessioncontext"></a>Couche d’Application étape 1) : définissez le TenantId Bonjour SESSION_CONTEXT
Une fois la connexion tooa partition base de données à l’aide des données de la bibliothèque cliente hello élastique de base de données que fixes de l’API de routage dépendant, application hello a besoin de base de données tootell hello le TenantId est à l’aide de cette connexion afin qu’une stratégie de sécurité RLS peut filtrer les lignes clients tooother appartenant. Hello toopass recommandée sont de ces informations toostore hello TenantId actuel pour cette connexion Bonjour [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806.aspx). (Remarque : vous pouvez également utiliser [CONTEXT_INFO](https://msdn.microsoft.com/library/ms180125.aspx), mais SESSION_CONTEXT constitue une meilleure option car il est plus facile toouse, renvoie la valeur NULL par défaut et prend en charge les paires clé-valeur.)

### <a name="entity-framework"></a>Entity Framework
Pour les applications à l’aide d’Entity Framework, approche la plus simple hello est hello tooset SESSION_CONTEXT dans hello ElasticScaleContext remplacer décrit dans [routage dépendant des données à l’aide de DbContext EF](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md#data-dependent-routing-using-ef-dbcontext). Avant de retourner la connexion hello répartie via le routage dépendant des données, il vous suffit de créer et de l’exécuter de SqlCommand qui définit 'TenantId' dans hello SESSION_CONTEXT toohello shardingKey spécifié pour cette connexion. De cette manière, vous ne devez toowrite code une fois tooset hello SESSION_CONTEXT. 

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

Maintenant hello SESSION_CONTEXT est défini automatiquement avec hello spécifié TenantId chaque fois que ElasticScaleContext est appelé : 

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

### <a name="adonet-sqlclient"></a>SqlClient ADO.NET
Pour les applications utilisant ADO.NET SqlClient, hello recommandé consiste toocreate une fonction wrapper autour de ShardMap.OpenConnectionForKey() qui définit automatiquement 'TenantId' hello SESSION_CONTEXT toohello corriger TenantId avant de retourner un connexion. tooensure qui SESSION_CONTEXT a toujours la valeur, vous devez ouvrir uniquement les connexions à l’aide de cette fonction wrapper.

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

## <a name="step-2-data-tier-create-row-level-security-policy"></a>Étape 2) Couche données : création d’une stratégie de sécurité au niveau des lignes
### <a name="create-a-security-policy-toofilter-hello-rows-each-tenant-can-access"></a>Créer des lignes de chaque client peut accéder à un Bonjour de toofilter de stratégie de sécurité
Maintenant que l’application hello est paramètre SESSION_CONTEXT avec hello TenantId actuelle avant d’interroger, une stratégie de sécurité RLS peut filtrer les requêtes et exclure les lignes qui ont un TenantId différent.  

La sécurité RLS est implémentée dans T-SQL : une fonction définie par l’utilisateur définit la logique d’accès hello et une stratégie de sécurité lie ce nombre tooany de fonction de tables. Pour ce projet, fonction hello vérifiera simplement que hello application (plutôt qu’un autre utilisateur SQL) est connecté toohello de base de données, et ce hello 'TenantId' stocké dans hello SESSION_CONTEXT correspond à hello tenantid fait partie d’une ligne donnée. Un prédicat de filtre autorisera les lignes qui répondent à ces conditions toopass filtre hello pour les requêtes SELECT, UPDATE et DELETE ; et un prédicat block empêchera les lignes qui violent ces conditions d’être insérée ou mise à jour. Si SESSION_CONTEXT n’a pas été définie, elle retournera que null et aucune ligne ne sera visible ou en mesure de toobe inséré. 

tooenable RLS, exécutez hello T-SQL suivant sur toutes les partitions à l’aide soit Visual Studio (SSDT), SSMS, ou hello script PowerShell inclus dans le projet de hello (ou si vous utilisez [des travaux de base de données élastique](sql-database-elastic-jobs-overview.md), vous pouvez l’utiliser dans l’exécution de tooautomate Ce T-SQL sur toutes les partitions) : 

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
> Pour les projets plus complexes nécessitant le prédicat de hello tooadd sur des centaines de tables, vous pouvez utiliser une procédure stockée d’assistance qui génère automatiquement une stratégie de sécurité ajoutant un prédicat sur toutes les tables dans un schéma. Consultez [les tables tooall appliquer la sécurité au niveau des lignes - le script d’assistance (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/03/31/apply-row-level-security-to-all-tables-helper-script).  
> 
> 

Maintenant si vous exécutez à nouveau les application exemple hello, locataires seront en mesure de toosee uniquement les lignes qui appartiennent toothem. En outre, application hello ne peut pas insérer les lignes qui appartiennent tootenants que base de données hello toohello actuellement connecté une partition, et il ne peut pas mettre à jour des lignes visibles toohave un TenantId différent. Si l’application hello tente toodo soit, une DbUpdateException est déclenchée.

Si vous ajoutez ultérieurement sur une nouvelle table, ALTER simplement hello de stratégie de sécurité et ajouter des prédicats de filtre et block sur la nouvelle table de hello : 

```
ALTER SECURITY POLICY rls.tenantAccessPolicy     
    ADD FILTER PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable,
    ADD BLOCK PREDICATE rls.fn_tenantAccessPredicate(TenantId) ON dbo.MyNewTable
GO 
```

### <a name="add-default-constraints-tooautomatically-populate-tenantid-for-inserts"></a>Ajouter la valeur par défaut des contraintes tooautomatically remplir TenantId pour les insertions
Vous pouvez placer une valeur par défaut contrainte sur chaque tooautomatically table remplir hello TenantId par hello valeur actuellement stockée dans SESSION_CONTEXT lors de l’insertion de lignes. Par exemple : 

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

Maintenant application hello dispense toospecify un TenantId lors de l’insertion de lignes : 

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
> Si vous utilisez des contraintes par défaut pour un projet Entity Framework, il est recommandé que vous n’incluez pas de colonne de TenantId hello dans votre modèle de données EF. Il s’agit, car les requêtes Entity Framework fournissent automatiquement les valeurs par défaut qui remplaceront les contraintes de valeur par défaut hello créés dans T-SQL qui utilisent SESSION_CONTEXT. contraintes de valeur par défaut toouse Bonjour exemple de projet, par exemple, vous devez supprimer les TenantId de DataClasses.cs (et exécution Add-Migration dans la Console du Gestionnaire de Package de hello) et tooensure utilisez T-SQL qui hello champ existe uniquement dans les tables de base de données hello. De cette façon, vous vous assurez qu’Entity Framework ne fournit pas automatiquement des valeurs par défaut incorrectes lors de l’insertion de données. 
> 
> 

### <a name="optional-enable-a-superuser-tooaccess-all-rows"></a>(Facultatif) Activer un tooaccess « superutilisateur » de toutes les lignes
Certaines applications veulent toocreate « superutilisateur » qui peut accéder à toutes les lignes, par exemple, dans tooenable d’ordre des rapports sur tous les locataires sur toutes les partitions ou les opérations de fractionnement/fusion tooperform sur les partitions qui impliquent le déplacement de lignes client entre les bases de données. tooenable, vous devez créer un nouvel utilisateur SQL (« superutilisateur » dans cet exemple) dans chaque base de données de partition. Puis changez de stratégie de sécurité hello avec une nouvelle fonction de prédicat qui permet cette tooaccess utilisateur toutes les lignes :

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


### <a name="maintenance"></a>Maintenance 
* **Ajout de nouvelles partitions**: vous devez exécuter hello T-SQL script tooenable RLS sur toutes les nouvelles partitions, sinon les requêtes sur ces partitions ne sont pas filtrés.
* **Ajout de nouvelles tables**: vous devez ajouter un filtre et bloquer la stratégie de sécurité de prédicat toohello sur toutes les partitions chaque fois qu’une nouvelle table est créée, sinon les requêtes sur la nouvelle table de hello ne sont pas filtrés. Cette opération peut être automatisée à l’aide d’un déclencheur DDL, comme décrit dans [appliquer la sécurité au niveau des lignes toonewly créé automatiquement les tables (blog)](http://blogs.msdn.com/b/sqlsecurity/archive/2015/05/22/apply-row-level-security-automatically-to-newly-created-tables.aspx).

## <a name="summary"></a>Résumé
Outils de base de données élastique et la sécurité de niveau ligne peuvent être utilisé tooscale ensemble à la couche de données d’une application prenant en charge des partitions mutualisées et locataire unique. Partitions de l’architecture mutualisées peuvent être utilisé toostore données plus efficacement (en particulier dans les cas où un grand nombre de clients ont uniquement quelques lignes de données), lors de locataire unique partitions peuvent être des clients de premium toosupport utilisé avec l’isolation et de performances plus strictes configuration requise.  Pour plus d’informations, consultez [Sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131). 

## <a name="additional-resources"></a>Ressources supplémentaires
* [Qu’est-ce qu’un pool élastique Azure ?](sql-database-elastic-pool.md)
* [Montée en charge avec Base de données SQL Azure](sql-database-elastic-scale-introduction.md)
* [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [Authentification sur les applications mutualisées, avec Azure AD et OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Application Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)

## <a name="questions-and-feature-requests"></a>Questions et demandes de fonctionnalités
Pour toute question, veuillez contacter toous sur hello [Forum sur la base de données SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) et pour les demandes de fonctionnalités, ajoutez-les toohello [forum de commentaires de la base de données SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-tools-multi-tenant-row-level-security/blogging-app.png
<!--anchors-->


