---
title: "Didacticiel : application web avec une base de données mutualisée à l’aide d‘Entity Framework et de la sécurité de niveau de ligne"
description: "Découvrez comment développer une application web d’ASP.NET MVC 5 avec une architecture mutualisée, base de données SQL principale, à l‘aide d’Entity Framework et une sécurité de niveau de ligne."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="1a996-103">Didacticiel : application web avec une base de données mutualisée à l’aide d‘Entity Framework et de la sécurité de niveau de ligne</span><span class="sxs-lookup"><span data-stu-id="1a996-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="1a996-104">Ce didacticiel montre comment créer une application web multi-locataire avec un modèle de location « [base de données partagée, schéma partagé](https://msdn.microsoft.com/library/aa479086.aspx) », à l’aide d’Entity Framework et de la [sécurité au niveau des lignes](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="1a996-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="1a996-105">Dans ce modèle, une base de données simple contient les données de nombreux clients, et chaque ligne de chaque table est associée à un « ID client »</span><span class="sxs-lookup"><span data-stu-id="1a996-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="1a996-106">La sécurité au niveau des lignes (RLS), nouvelle fonctionnalité de base de données SQL Azure est utilisée pour empêcher les autres clients d‘accéder aux données les uns des autres.</span><span class="sxs-lookup"><span data-stu-id="1a996-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="1a996-107">Cela nécessite juste une modification mineure de l‘application.</span><span class="sxs-lookup"><span data-stu-id="1a996-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="1a996-108">En centralisant la logique d‘accès client au sein de la base de données, RLS simplifie le code d‘application et réduit le risque de fuites accidentelles d’un utilisateur à l’autre.</span><span class="sxs-lookup"><span data-stu-id="1a996-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="1a996-109">Commençons par l‘application Gestionnaire de contact avec la section [Créer une application ASP.NET MVP avec l‘authentification et la base de données SQL et déployer le service d’application Azure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1a996-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="1a996-110">Actuellement, l’application permet à tous les utilisateurs (clients) d’afficher tous les contacts :</span><span class="sxs-lookup"><span data-stu-id="1a996-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="1a996-112">Avec simplement quelques modifications mineures, nous allons ajouter la prise en charge de l’architecture mutualisée, afin que les utilisateurs puissent voir uniquement les contacts qui leur appartiennent.</span><span class="sxs-lookup"><span data-stu-id="1a996-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="1a996-113">Étape 1 : Ajouter une classe d’intercepteur dans l’application pour définir la SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="1a996-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="1a996-114">Il faut apporter une modification à l’application.</span><span class="sxs-lookup"><span data-stu-id="1a996-114">There is one application change we need to make.</span></span> <span data-ttu-id="1a996-115">Tous les utilisateurs d‘applications se connectent à la base de données à l‘aide de la chaîne de connexion (c‘est-à-dire même connexion SQL), il n‘existe actuellement aucun moyen pour une stratégie RLS de savoir pour quel utilisateur il doit effectuer le filtrage.</span><span class="sxs-lookup"><span data-stu-id="1a996-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="1a996-116">Cette approche est très courante dans les applications web, car elle permet un regroupement de connexions efficace. Cependant, cela signifie que nous avons besoin d‘une autre façon d’identifier l’utilisateur actuel de l’application dans la base de données. </span><span class="sxs-lookup"><span data-stu-id="1a996-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="1a996-117">La solution consiste à utiliser l‘application pour définir une paire clé-valeur pour le UserId actuel dans le [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immédiatement après l’ouverture d’une connexion et avant l’exécution d’une requête.</span><span class="sxs-lookup"><span data-stu-id="1a996-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="1a996-118">SESSION_CONTEXT est un magasin clé-valeur session, et notre stratégie RLS utilise le nom d’utilisateur qu’il contient pour identifier l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="1a996-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="1a996-119">Nous allons ajouter un [intercepteur](https://msdn.microsoft.com/data/dn469464.aspx) (plus particulièrement, un intercepteur [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), nouvelle fonctionnalité dans Entity Framework (EF) 6, pour définir automatiquement le UserId actuel dans SESSION_CONTEXT en exécutant une instruction T-SQL à chaque fois qu’Entity Framework ouvre une connexion.</span><span class="sxs-lookup"><span data-stu-id="1a996-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="1a996-120">Ouvrez le projet ContactManager dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a996-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="1a996-121">Cliquez avec le bouton droit sur le dossier Modèles dans l’Explorateur de solutions, puis sélectionnez Ajouter > Classe.</span><span class="sxs-lookup"><span data-stu-id="1a996-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="1a996-122">Nommez la nouvelle classe « SessionContextInterceptor.cs », puis cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="1a996-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="1a996-123">Remplacez le contenu de SessionContextInterceptor.cs par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1a996-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="1a996-124">Il s’agit de la seule modification d’application requise.</span><span class="sxs-lookup"><span data-stu-id="1a996-124">That's the only application change required.</span></span> <span data-ttu-id="1a996-125">Continuez, réalisez et publiez l’application.</span><span class="sxs-lookup"><span data-stu-id="1a996-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="1a996-126">Étape 2 : Ajouter une colonne UserId au schéma de base de données</span><span class="sxs-lookup"><span data-stu-id="1a996-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="1a996-127">Ensuite, nous devons ajouter une colonne UserId à la table Contacts à associer à chaque ligne d’un utilisateur (client).</span><span class="sxs-lookup"><span data-stu-id="1a996-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="1a996-128">Il modifie le schéma directement dans la base de données, et nous n’avons donc pas à inclure ce champ dans notre modèle de données Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="1a996-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="1a996-129">Connectez-vous à la base de données directement en utilisant SQL Server Management Studio ou Visual Studio, puis exécutez l’instruction T-SQL suivante :</span><span class="sxs-lookup"><span data-stu-id="1a996-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="1a996-130">Cela ajoute une colonne UserId à la table Contacts.</span><span class="sxs-lookup"><span data-stu-id="1a996-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="1a996-131">Nous utilisons le type de données nvarchar (128) pour faire correspondre les ID utilisateur stockés dans la table AspNetUsers, puis nous créons une contrainte DEFAULT qui définira automatiquement le UserId des lignes nouvellement insérées au UserId actuellement stocké dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1a996-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="1a996-132">Maintenant, le tableau ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="1a996-132">Now the table looks like this:</span></span>

![Table de contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="1a996-134">Lors de la création de nouveaux contacts, ces derniers se verront affectés un ID d‘utilisateur correct.</span><span class="sxs-lookup"><span data-stu-id="1a996-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="1a996-135">À des fins de démonstration, toutefois, nous allons affecter quelques-uns de ces contacts existants à un utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="1a996-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="1a996-136">Si vous avez déjà créé quelques utilisateurs dans l‘application (par exemple, à l‘aide de comptes locaux Google ou Facebook), vous pouvez les voir dans la table AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="1a996-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="1a996-137">Dans la capture d‘écran ci-dessous, il n’y a jusqu‘ici qu‘un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a996-137">In the screenshot below, there is only one user so far.</span></span>

![Tableau AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="1a996-139">Copiez l’ID de user1@contoso.com et collez-le dans l’instruction T-SQL ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1a996-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="1a996-140">Exécutez cette instruction pour associer trois des Contacts à cet ID utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a996-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="1a996-141">Étape 3 : créer une stratégie de sécurité de niveau de ligne dans la base de données</span><span class="sxs-lookup"><span data-stu-id="1a996-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="1a996-142">L’étape finale consiste à créer une stratégie de sécurité qui utilise le nom d’utilisateur dans SESSION_CONTEXT pour filtrer automatiquement les résultats renvoyés par les requêtes.</span><span class="sxs-lookup"><span data-stu-id="1a996-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="1a996-143">Bien que toujours connecté à la base de données, exécutez le T-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="1a996-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="1a996-144">Ce code exécute trois opérations.</span><span class="sxs-lookup"><span data-stu-id="1a996-144">This code does three things.</span></span> <span data-ttu-id="1a996-145">Tout d‘abord, il crée un nouveau schéma en tant que meilleure pratique pour la centralisation et la limitation d’accès aux objets RLS.</span><span class="sxs-lookup"><span data-stu-id="1a996-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="1a996-146">Ensuite, il crée une fonction de prédicat qui renverra « 1 » lorsque le UserId d’une ligne correspond au UserId dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1a996-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="1a996-147">Enfin, il crée une stratégie de sécurité qui ajoute cette fonction en tant que prédicat de bloc et de filtre sur la table Contacts.</span><span class="sxs-lookup"><span data-stu-id="1a996-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="1a996-148">Le prédicat de filtre fait en sorte que les requêtes retournent uniquement des lignes appartenant à l’utilisateur actuel et le prédicat de bloc agit comme un dispositif de protection pour empêcher l‘application d‘insérer une ligne pour le mauvais utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a996-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="1a996-149">Maintenant, exécutez l’application puis connectez-vous en tant que user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1a996-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="1a996-150">Cet utilisateur voit à présent que les Contacts que nous avons attribués à ce UserId:</span><span class="sxs-lookup"><span data-stu-id="1a996-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="1a996-152">Pour valider cette opération, essayez d‘enregistrer un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a996-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="1a996-153">Ils ne verront aucun contact, car aucun ne leur a été affecté.</span><span class="sxs-lookup"><span data-stu-id="1a996-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="1a996-154">S’ils créent un nouveau contact, il leur sera affecté et ils seront les seuls à pouvoir le visualiser.</span><span class="sxs-lookup"><span data-stu-id="1a996-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a996-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a996-155">Next steps</span></span>
<span data-ttu-id="1a996-156">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="1a996-156">That's it!</span></span> <span data-ttu-id="1a996-157">L’application web Gestionnaire de contact a été transformée en application mutualisée où chaque utilisateur a sa propre liste de contacts.</span><span class="sxs-lookup"><span data-stu-id="1a996-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="1a996-158">En utilisant la sécurité de niveau ligne, nous avons évité la complexité liée à l’application de la logique d‘accès aux clients dans notre code d’application.</span><span class="sxs-lookup"><span data-stu-id="1a996-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="1a996-159">Cette transparence permet à l‘application de se concentrer sur les véritables problèmes de l’entreprise et elle réduit également le risque de fuite accidentelle des données au fur et à mesure que le code de base de l‘application augmente.</span><span class="sxs-lookup"><span data-stu-id="1a996-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="1a996-160">Ce didacticiel a seulement effleuré la surface de ce qui est possible avec RLS.</span><span class="sxs-lookup"><span data-stu-id="1a996-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="1a996-161">Par exemple, il est possible d‘avoir des logiques d’accès plus sophistiquées ou granulaires, et il est possible de stocker davantage que le simple UserId dans SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="1a996-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="1a996-162">Il est également possible d’ [intégrer RLS avec les bibliothèques client des outils de base de données élastique](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) pour prendre en charge des partitions mutualisées dans une couche de données mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="1a996-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="1a996-163">Au-delà de ces possibilités, nous nous efforçons d’améliorer encore RLS.</span><span class="sxs-lookup"><span data-stu-id="1a996-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="1a996-164">Si vous avez des questions, des idées ou des choses que vous aimeriez voir, faites-le nous savoir par le biais de vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="1a996-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="1a996-165">Nous apprécions vos commentaires !</span><span class="sxs-lookup"><span data-stu-id="1a996-165">We appreciate your feedback!</span></span>

