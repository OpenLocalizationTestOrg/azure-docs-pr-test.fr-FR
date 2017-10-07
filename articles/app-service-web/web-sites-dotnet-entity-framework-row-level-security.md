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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Didacticiel : application web avec une base de données mutualisée à l’aide d‘Entity Framework et de la sécurité de niveau de ligne
Ce didacticiel montre comment toobuild mutualisée web application avec un «[base de données partagée, schéma partagé](https://msdn.microsoft.com/library/aa479086.aspx)« modèle d’architecture mutualisée, à l’aide d’Entity Framework et [sécurité de niveau ligne](https://msdn.microsoft.com/library/dn765131.aspx). Dans ce modèle, une base de données simple contient les données de nombreux clients, et chaque ligne de chaque table est associée à un « ID client » Sécurité au niveau des lignes (RLS), une nouvelle fonctionnalité de base de données SQL Azure est utilisé tooprevent des clients d’accéder aux données de l’autre. Cela nécessite uniquement une petite modification unique, application de toohello. Centralisation hello client accès logique au sein de la base de données hello elle-même, RLS simplifie le code de l’application hello et réduit les risques de fuites accidentelles de données entre les clients hello.

Commençons par l’application hello de gestionnaire de contacts simple à partir de [créer une application ASP.NET MVP avec l’authentification et de la base de données SQL et de déployer tooAzure du Service d’applications](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). À droite, application hello permet désormais tous les utilisateurs (clients) toosee tous les contacts :

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Avec seulement quelques modifications mineures, nous allons ajouter la prise en charge d’une architecture mutualisée, afin que les utilisateurs soient en mesure de toosee uniquement hello les contacts qui appartiennent toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Étape 1 : Ajouter une classe de l’intercepteur Bonjour de tooset application hello SESSION_CONTEXT
Il existe une modification d’application que nous devons toomake. Étant donné que tous les utilisateurs de l’application se connecteront à l’aide de base de données toohello hello même chaîne de connexion (c'est-à-dire même connexion SQL), il n’existe actuellement aucun moyen pour un tooknow de stratégie RLS utilisateur qui doit filtrer pour. Cette approche est très courante dans les applications web, car elle permet le regroupement de connexions efficace, mais cela signifie que nous avons besoin d’une autre façon tooidentify hello application utilisateur actuel au sein de la base de données hello. Hello solution est toohave hello application ensemble une paire clé-valeur pour hello actuel UserId Bonjour [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immédiatement après l’ouverture d’une connexion, avant qu’il exécute toutes les requêtes. SESSION_CONTEXT est un magasin clé-valeur étendue de session et notre stratégie RLS utilisera hello UserId stocké qu’il contient l’utilisateur actuel tooidentify hello.

Nous allons ajouter un [intercepteur](https://msdn.microsoft.com/data/dn469464.aspx) (en particulier, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), une fonctionnalité nouvelle dans Entity Framework (EF) 6, tooautomatically ensemble hello actuel UserId Bonjour SESSION_CONTEXT en exécutant un Instruction T-SQL chaque fois qu’EF ouvre une connexion.

1. Ouvrez le projet de ContactManager hello dans Visual Studio.
2. Avec le bouton droit sur le dossier de modèles hello Bonjour l’Explorateur de solutions, puis sélectionnez Ajouter > classe.
3. Nom de classe hello « SessionContextInterceptor.cs » et cliquez sur Ajouter.
4. Remplacez contenu hello de SessionContextInterceptor.cs hello suivant de code.

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

Qui hello application seule modification est requise. Continuez et générer et publier l’application hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Étape 2 : Ajouter un schéma de base de données UserId colonne toohello
Ensuite, nous devons tooadd un tooassociate de table UserId colonne toohello Contacts chaque ligne à un utilisateur (client). Nous modifient le schéma hello directement dans la base de données hello, afin que nous n’avons pas ce champ tooinclude dans notre modèle de données EF.

Se connecter toohello de base de données directement à l’aide de SQL Server Management Studio ou Visual Studio et puis exécutez hello T-SQL suivant :

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Cette opération ajoute une table de Contacts UserId colonne toohello. Nous utilisons hello toomatch hello nvarchar (128) données type Qu'userids stockées dans la table de AspNetUsers hello, et nous créons une contrainte par défaut qui définira automatiquement hello UserId pour les lignes nouvellement insérées toobe hello UserId actuellement stocké dans SESSION_CONTEXT.

Table de hello ressemble à ceci :

![Table de contacts SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Lors de la création de nouveaux contacts, leur automatiquement sont affectées hello corriger le nom d’utilisateur. À des fins de démonstration, cependant, nous allons attribuer des quelques exemples de ces tooan contacts existants existant utilisateur.

Si vous avez créé un petit nombre d’utilisateurs dans l’application hello déjà (par exemple, à l’aide locale, Google ou Facebook comptes), vous verrez les dans la table de AspNetUsers hello. Dans hello capture d’écran ci-dessous, il existe un seul utilisateur jusqu'à présent.

![Tableau AspNetUsers SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Hello de copie Id pour user1@contoso.comet le coller dans une instruction T-SQL de hello ci-dessous. Exécutez cette instruction de tooassociate trois contacts hello avec cet ID utilisateur.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Étape 3 : Créer une stratégie de sécurité au niveau de la ligne de base de données hello
étape finale de Hello est toocreate une stratégie de sécurité qui utilise hello UserId dans SESSION_CONTEXT tooautomatically filtre hello résultats renvoyés par les requêtes.

Lors de la base de données toohello toujours connecté, exécutez hello T-SQL suivant :

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

Ce code exécute trois opérations. Tout d’abord, il crée un nouveau schéma en tant que meilleure pratique pour centraliser et en limitant les objets RLS de toohello d’accès. Ensuite, il crée une fonction de prédicat qui retourne '1' lorsque hello UserId d’une ligne correspond à hello UserId dans SESSION_CONTEXT. Enfin, il crée une stratégie de sécurité qui ajoute cette fonction en tant que prédicat à la fois un filtre et block sur la table de Contacts hello. prédicat de filtre Hello provoque des requêtes tooreturn uniquement les lignes appartenant à l’utilisateur actuel toohello et prédicat block de hello agit comme une application hello tooprevent sauvegarde jamais accidentellement insertion d’une ligne pour les utilisateur incorrect hello.

Maintenant, exécutez l’application hello et connectez-vous en tant que user1@contoso.com. Maintenant, cet utilisateur voit uniquement les Contacts hello nous avons attribué toothis UserId :

![Application du Gestionnaire de contacts avant d‘activer la RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate cela est en outre, essayez d’inscrire un nouvel utilisateur. Ils ne verront aucun contact, car aucun n’a été attribué toothem. Si elles créent un contact, lui soit affecté toothem et uniquement, ils seront en mesure de toosee il.

## <a name="next-steps"></a>Étapes suivantes
Et voilà ! application web le Gestionnaire de contacts simple de Hello a été convertie en une architecture mutualisée une où chaque utilisateur possède sa propre liste de contacts. En utilisant la sécurité de niveau ligne, nous avons évité complexité hello d’appliquer la logique d’accès client dans notre code d’application. La transparence permet hello application toofocus sur hello réel problème de gestion, et il réduit également le risque de hello d’accidentellement une fuite de données comme code de base de l’application hello augmente.

Ce didacticiel a surface de hello rayé uniquement ce qui est possible avec les lignes. Par exemple, il est possible de toohave plus sophistiquée ou logique d’un accès granulaire et son possible toostore plus que hello actuel UserId Bonjour SESSION_CONTEXT. Il est également possible trop[intégrer RLS bibliothèques de client d’outils de base de données élastique hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport les partitions de plusieurs locataires dans une couche de données de la montée en puissance parallèle.

Au-delà de ces possibilités, nous nous efforçons également toomake RLS encore plus performants. Si vous avez des questions, idées ou autres éléments que vous aimeriez toosee, faites-nous savoir dans les commentaires de hello. Nous apprécions vos commentaires !

