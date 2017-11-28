---
title: "Didacticiel : application web avec une base de données mutualisée à l’aide d‘Entity Framework et de la sécurité de niveau de ligne"
description: "Découvrez comment toodevelop un ASP.NET MVC 5 web application avec une architecture mutualisée de base de données SQL backent, à l’aide d’Entity Framework et sécurité de niveau ligne."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="d9e56-103">Didacticiel : application web avec une base de données mutualisée à l’aide d‘Entity Framework et de la sécurité de niveau de ligne</span><span class="sxs-lookup"><span data-stu-id="d9e56-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="d9e56-104">Ce didacticiel montre comment toobuild mutualisée web application avec un «[base de données partagée, schéma partagé](https://msdn.microsoft.com/library/aa479086.aspx)« modèle d’architecture mutualisée, à l’aide d’Entity Framework et [sécurité de niveau ligne](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9e56-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="d9e56-105">Dans ce modèle, une base de données simple contient les données de nombreux clients, et chaque ligne de chaque table est associée à un « ID client »</span><span class="sxs-lookup"><span data-stu-id="d9e56-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="d9e56-106">Sécurité au niveau des lignes (RLS), une nouvelle fonctionnalité de base de données SQL Azure est utilisé tooprevent des clients d’accéder aux données de l’autre.</span><span class="sxs-lookup"><span data-stu-id="d9e56-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="d9e56-107">Cela nécessite uniquement une petite modification unique, application de toohello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="d9e56-108">Centralisation hello client accès logique au sein de la base de données hello elle-même, RLS simplifie le code de l’application hello et réduit les risques de fuites accidentelles de données entre les clients hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="d9e56-109">Commençons par l’application hello de gestionnaire de contacts simple à partir de [créer une application ASP.NET MVP avec l’authentification et de la base de données SQL et de déployer tooAzure du Service d’applications](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d9e56-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="d9e56-110">À droite, application hello permet désormais tous les utilisateurs (clients) toosee tous les contacts :</span><span class="sxs-lookup"><span data-stu-id="d9e56-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="d9e56-112">Avec seulement quelques modifications mineures, nous allons ajouter la prise en charge d’une architecture mutualisée, afin que les utilisateurs soient en mesure de toosee uniquement hello les contacts qui appartiennent toothem.</span><span class="sxs-lookup"><span data-stu-id="d9e56-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="d9e56-113">Étape 1 : Ajouter une classe de l’intercepteur Bonjour de tooset application hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="d9e56-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="d9e56-114">Il existe une modification d’application que nous devons toomake.</span><span class="sxs-lookup"><span data-stu-id="d9e56-114">There is one application change we need toomake.</span></span> <span data-ttu-id="d9e56-115">Étant donné que tous les utilisateurs de l’application se connecteront à l’aide de base de données toohello hello même chaîne de connexion (c'est-à-dire même connexion SQL), il n’existe actuellement aucun moyen pour un tooknow de stratégie RLS utilisateur qui doit filtrer pour.</span><span class="sxs-lookup"><span data-stu-id="d9e56-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="d9e56-116">Cette approche est très courante dans les applications web, car elle permet le regroupement de connexions efficace, mais cela signifie que nous avons besoin d’une autre façon tooidentify hello application utilisateur actuel au sein de la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="d9e56-117">Hello solution est toohave hello application ensemble une paire clé-valeur pour hello actuel UserId Bonjour [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immédiatement après l’ouverture d’une connexion, avant qu’il exécute toutes les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d9e56-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="d9e56-118">SESSION_CONTEXT est un magasin clé-valeur étendue de session et notre stratégie RLS utilisera hello UserId stocké qu’il contient l’utilisateur actuel tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="d9e56-119">Nous allons ajouter un [intercepteur](https://msdn.microsoft.com/data/dn469464.aspx) (en particulier, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), une fonctionnalité nouvelle dans Entity Framework (EF) 6, tooautomatically ensemble hello actuel UserId Bonjour SESSION_CONTEXT en exécutant un Instruction T-SQL chaque fois qu’EF ouvre une connexion.</span><span class="sxs-lookup"><span data-stu-id="d9e56-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="d9e56-120">Ouvrez le projet de ContactManager hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9e56-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="d9e56-121">Avec le bouton droit sur le dossier de modèles hello Bonjour l’Explorateur de solutions, puis sélectionnez Ajouter > classe.</span><span class="sxs-lookup"><span data-stu-id="d9e56-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="d9e56-122">Nom de classe hello « SessionContextInterceptor.cs » et cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="d9e56-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="d9e56-123">Remplacez contenu hello de SessionContextInterceptor.cs hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="d9e56-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="d9e56-124">Qui hello application seule modification est requise.</span><span class="sxs-lookup"><span data-stu-id="d9e56-124">That's hello only application change required.</span></span> <span data-ttu-id="d9e56-125">Continuez et générer et publier l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="d9e56-126">Étape 2 : Ajouter un schéma de base de données UserId colonne toohello</span><span class="sxs-lookup"><span data-stu-id="d9e56-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="d9e56-127">Ensuite, nous devons tooadd un tooassociate de table UserId colonne toohello Contacts chaque ligne à un utilisateur (client).</span><span class="sxs-lookup"><span data-stu-id="d9e56-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="d9e56-128">Nous modifient le schéma hello directement dans la base de données hello, afin que nous n’avons pas ce champ tooinclude dans notre modèle de données EF.</span><span class="sxs-lookup"><span data-stu-id="d9e56-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="d9e56-129">Se connecter toohello de base de données directement à l’aide de SQL Server Management Studio ou Visual Studio et puis exécutez hello T-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="d9e56-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="d9e56-130">Cette opération ajoute une table de Contacts UserId colonne toohello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="d9e56-131">Nous utilisons hello toomatch hello nvarchar (128) données type Qu'userids stockées dans la table de AspNetUsers hello, et nous créons une contrainte par défaut qui définira automatiquement hello UserId pour les lignes nouvellement insérées toobe hello UserId actuellement stocké dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d9e56-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="d9e56-132">Table de hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="d9e56-132">Now hello table looks like this:</span></span>

![Table de contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="d9e56-134">Lors de la création de nouveaux contacts, leur automatiquement sont affectées hello corriger le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9e56-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="d9e56-135">À des fins de démonstration, cependant, nous allons attribuer des quelques exemples de ces tooan contacts existants existant utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9e56-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="d9e56-136">Si vous avez créé un petit nombre d’utilisateurs dans l’application hello déjà (par exemple, à l’aide locale, Google ou Facebook comptes), vous verrez les dans la table de AspNetUsers hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="d9e56-137">Dans hello capture d’écran ci-dessous, il existe un seul utilisateur jusqu'à présent.</span><span class="sxs-lookup"><span data-stu-id="d9e56-137">In hello screenshot below, there is only one user so far.</span></span>

![Tableau AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="d9e56-139">Hello de copie Id pour user1@contoso.comet le coller dans une instruction T-SQL de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d9e56-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="d9e56-140">Exécutez cette instruction de tooassociate trois contacts hello avec cet ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9e56-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="d9e56-141">Étape 3 : Créer une stratégie de sécurité au niveau de la ligne de base de données hello</span><span class="sxs-lookup"><span data-stu-id="d9e56-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="d9e56-142">étape finale de Hello est toocreate une stratégie de sécurité qui utilise hello UserId dans SESSION_CONTEXT tooautomatically filtre hello résultats renvoyés par les requêtes.</span><span class="sxs-lookup"><span data-stu-id="d9e56-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="d9e56-143">Lors de la base de données toohello toujours connecté, exécutez hello T-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="d9e56-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="d9e56-144">Ce code exécute trois opérations.</span><span class="sxs-lookup"><span data-stu-id="d9e56-144">This code does three things.</span></span> <span data-ttu-id="d9e56-145">Tout d’abord, il crée un nouveau schéma en tant que meilleure pratique pour centraliser et en limitant les objets RLS de toohello d’accès.</span><span class="sxs-lookup"><span data-stu-id="d9e56-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="d9e56-146">Ensuite, il crée une fonction de prédicat qui retourne '1' lorsque hello UserId d’une ligne correspond à hello UserId dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d9e56-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="d9e56-147">Enfin, il crée une stratégie de sécurité qui ajoute cette fonction en tant que prédicat à la fois un filtre et block sur la table de Contacts hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="d9e56-148">prédicat de filtre Hello provoque des requêtes tooreturn uniquement les lignes appartenant à l’utilisateur actuel toohello et prédicat block de hello agit comme une application hello tooprevent sauvegarde jamais accidentellement insertion d’une ligne pour les utilisateur incorrect hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="d9e56-149">Maintenant, exécutez l’application hello et connectez-vous en tant que user1@contoso.com. Maintenant, cet utilisateur voit uniquement les Contacts hello nous avons attribué toothis UserId :</span><span class="sxs-lookup"><span data-stu-id="d9e56-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="d9e56-151">toovalidate cela est en outre, essayez d’inscrire un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d9e56-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="d9e56-152">Ils ne verront aucun contact, car aucun n’a été attribué toothem.</span><span class="sxs-lookup"><span data-stu-id="d9e56-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="d9e56-153">Si elles créent un contact, lui soit affecté toothem et uniquement, ils seront en mesure de toosee il.</span><span class="sxs-lookup"><span data-stu-id="d9e56-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9e56-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9e56-154">Next steps</span></span>
<span data-ttu-id="d9e56-155">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="d9e56-155">That's it!</span></span> <span data-ttu-id="d9e56-156">application web le Gestionnaire de contacts simple de Hello a été convertie en une architecture mutualisée une où chaque utilisateur possède sa propre liste de contacts.</span><span class="sxs-lookup"><span data-stu-id="d9e56-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="d9e56-157">En utilisant la sécurité de niveau ligne, nous avons évité complexité hello d’appliquer la logique d’accès client dans notre code d’application.</span><span class="sxs-lookup"><span data-stu-id="d9e56-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="d9e56-158">La transparence permet hello application toofocus sur hello réel problème de gestion, et il réduit également le risque de hello d’accidentellement une fuite de données comme code de base de l’application hello augmente.</span><span class="sxs-lookup"><span data-stu-id="d9e56-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="d9e56-159">Ce didacticiel a surface de hello rayé uniquement ce qui est possible avec les lignes.</span><span class="sxs-lookup"><span data-stu-id="d9e56-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="d9e56-160">Par exemple, il est possible de toohave plus sophistiquée ou logique d’un accès granulaire et son possible toostore plus que hello actuel UserId Bonjour SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="d9e56-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="d9e56-161">Il est également possible trop[intégrer RLS bibliothèques de client d’outils de base de données élastique hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport les partitions de plusieurs locataires dans une couche de données de la montée en puissance parallèle.</span><span class="sxs-lookup"><span data-stu-id="d9e56-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="d9e56-162">Au-delà de ces possibilités, nous nous efforçons également toomake RLS encore plus performants.</span><span class="sxs-lookup"><span data-stu-id="d9e56-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="d9e56-163">Si vous avez des questions, idées ou autres éléments que vous aimeriez toosee, faites-nous savoir dans les commentaires de hello.</span><span class="sxs-lookup"><span data-stu-id="d9e56-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="d9e56-164">Nous apprécions vos commentaires !</span><span class="sxs-lookup"><span data-stu-id="d9e56-164">We appreciate your feedback!</span></span>

