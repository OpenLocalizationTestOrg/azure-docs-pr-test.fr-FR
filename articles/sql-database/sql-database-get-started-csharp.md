---
title: "C# : Prise en main d’Azure SQL Database | Microsoft Docs"
description: "Essayez de base de données SQL pour le développement d’applications SQL et c# et créer une base de données SQL Azure avec c# à l’aide de la bibliothèque de base de données SQL de hello pour .NET."
keywords: essayer sql, sql c#
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: cfff2299-a474-4054-8d99-759af1ae5188
ms.service: sql-database
ms.custom: develop apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: csharp
ms.workload: data-management
ms.date: 10/04/2016
ms.author: sstein
ms.openlocfilehash: e880ebabd53546bea37a13186b0f1a13db35b684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-toocreate-a-sql-database-with-hello-sql-database-library-for-net"></a>Utilisez c# toocreate une base de données SQL avec hello bibliothèque de base de données SQL pour .NET

Découvrez comment toouse c# toocreate SQL Azure de base de données avec hello [bibliothèque de gestion SQL Microsoft Azure pour .NET](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql). Cet article décrit comment toocreate une seule base de données SQL et c#. les pools élastiques toocreate, consultez [créer un pool élastique](sql-database-elastic-pool-manage-csharp.md).

Hello bibliothèque de gestion de base de données SQL Azure pour .NET fournit un [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-en fonction des API qui encapsule hello [API REST de base de données SQL de gestionnaire de ressources](https://docs.microsoft.com/rest/api/sql/).

> [!NOTE]
> Plusieurs nouvelles fonctionnalités de base de données SQL seulement sont pris en charge que lorsque vous utilisez hello [modèle de déploiement Azure Resource Manager](../azure-resource-manager/resource-group-overview.md), donc vous devez toujours utiliser hello dernières **bibliothèque de gestion de base de données SQL Azure pour .NET ([documents](https://docs.microsoft.com/dotnet/api/overview/azure/sql?view=azure-dotnet) | [NuGet Package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql))**. Hello plus anciens [bibliothèques basés sur des modèles de déploiement classique](https://www.nuget.org/packages/Microsoft.WindowsAzure.Management.Sql) sont pris en charge pour la compatibilité ascendante, donc nous vous recommandons d’utiliser les bibliothèques en fonction de gestionnaire de ressources plus récentes hello.
> 
> 

toocomplete hello étapes décrites dans cet article, hello éléments suivants sont nécessaires :

* Un abonnement Azure. Si vous avez simplement besoin d’abonnement Azure cliquez sur **compte gratuit** en haut hello de cette page, puis revenir toofinish cet article.
* Visual Studio. Pour obtenir une copie gratuite de Visual Studio, consultez hello [téléchargements Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs) page.

> [!NOTE]
> Cet article permet de créer une base de données SQL vide. Modifier hello *CreateOrUpdateDatabase(...)*  méthode Bonjour suivant toocopy bases de données, l’échelle de bases de données, créer une base de données dans un pool.  
> 

## <a name="create-a-console-app-and-install-hello-required-libraries"></a>Créer une application console et installer les bibliothèques hello requis
1. Démarrez Visual Studio.
2. Cliquez sur **Fichier** > **Nouveau** > **Projet**.
3. Créez une **application de console** C# et nommez-la *SqlDbConsoleApp*

toocreate une base de données SQL avec c#, charge hello requise des bibliothèques de gestion (à l’aide de hello [console du Gestionnaire de package](http://docs.nuget.org/Consume/Package-Manager-Console)) :

1. Cliquez sur **Outils** > **Gestionnaire de package NuGet** > **Console du gestionnaire de package**.
2. Type `Install-Package Microsoft.Azure.Management.Sql -Pre` hello tooinstall dernière [bibliothèque de gestion Microsoft Azure SQL](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql).
3. Type `Install-Package Microsoft.Azure.Management.ResourceManager -Pre` tooinstall hello [bibliothèque du Gestionnaire de ressources Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager).
4. Type `Install-Package Microsoft.Azure.Common.Authentication -Pre` tooinstall hello [bibliothèque d’authentification commune Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.Common.Authentication). 

> [!NOTE]
> Hello exemples dans cet article utilisent une forme synchrone de chaque demande d’API et un bloc jusqu'à la fin de l’appel REST hello sur hello service sous-jacent. Des méthodes asynchrones sont disponibles.
> 
> 

## <a name="create-a-sql-database-server-firewall-rule-and-sql-database---c-example"></a>Créer un serveur SQL Database, une règle de pare-feu et une base de données SQL : exemple de code C#
Hello suivant l’exemple crée un groupe de ressources, de serveur, de règle de pare-feu et d’une base de données SQL. Consultez, [créer un tooaccess de principal du service des ressources](#create-a-service-principal-to-access-resources) tooget hello `_subscriptionId, _tenantId, _applicationId, and _applicationSecret` variables.

Remplacer le contenu hello de **Program.cs** avec hello suivant et mise à jour hello `{variables}` avec des valeurs de votre application (n’incluez pas hello `{}`).

    using Microsoft.Azure;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.Azure.Management.Sql;
    using Microsoft.Azure.Management.Sql.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;

    namespace SqlDbConsoleApp
    {
    class Program
       {
        // For details about these four (4) values, see
        // https://azure.microsoft.com/documentation/articles/resource-group-authenticate-service-principal/
        static string _subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _tenantId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}";
        static string _applicationSecret = "{your-password}";

        // Create management clients for hello Azure resources your app needs toowork with.
        // This app works with Resource Groups, and Azure SQL Database.
        static ResourceManagementClient _resourceMgmtClient;
        static SqlManagementClient _sqlMgmtClient;

        // Authentication token
        static AuthenticationResult _token;

        // Azure resource variables
        static string _resourceGroupName = "{resource-group-name}";
        static string _resourceGrouplocation = "{Azure-region}";

        static string _serverlocation = _resourceGrouplocation;
        static string _serverName = "{server-name}";
        static string _serverAdmin = "{server-admin-login}";
        static string _serverAdminPassword = "{server-admin-password}";

        static string _firewallRuleName = "{firewall-rule-name}";
        static string _startIpAddress = "{0.0.0.0}";
        static string _endIpAddress = "{255.255.255.255}";

        static string _databaseName = "{dbfromcsarticle}";
        static string _databaseEdition = DatabaseEditions.Basic;
        static string _databasePerfLevel = ""; // "S0", "S1", and so on here for other tiers


        static void Main(string[] args)
        {
            // Authenticate:
            _token = GetToken(_tenantId, _applicationId, _applicationSecret);
            Console.WriteLine("Token acquired. Expires on:" + _token.ExpiresOn);

            // Instantiate management clients:
            _resourceMgmtClient = new ResourceManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken));
            _sqlMgmtClient = new SqlManagementClient(new Microsoft.Rest.TokenCredentials(_token.AccessToken)) { SubscriptionId = _subscriptionId };

            Console.WriteLine("Resource group...");
            ResourceGroup rg = CreateOrUpdateResourceGroup(_resourceMgmtClient, _subscriptionId, _resourceGroupName, _resourceGrouplocation);
            Console.WriteLine("Resource group: " + rg.Id);


            Console.WriteLine("Server...");
            Server sgr = CreateOrUpdateServer(_sqlMgmtClient, _resourceGroupName, _serverlocation, _serverName, _serverAdmin, _serverAdminPassword);
            Console.WriteLine("Server: " + sgr.Id);

            Console.WriteLine("Server firewall...");
            FirewallRule fwr = CreateOrUpdateFirewallRule(_sqlMgmtClient, _resourceGroupName, _serverName, _firewallRuleName, _startIpAddress, _endIpAddress);
            Console.WriteLine("Server firewall: " + fwr.Id);

            Console.WriteLine("Database...");
            Database dbr = CreateOrUpdateDatabase(_sqlMgmtClient, _resourceGroupName, _serverName, _databaseName, _databaseEdition, _databasePerfLevel);
            Console.WriteLine("Database: " + dbr.Id);


            Console.WriteLine("Press any key toocontinue...");
            Console.ReadKey();
        }

        static ResourceGroup CreateOrUpdateResourceGroup(ResourceManagementClient resourceMgmtClient, string subscriptionId, string resourceGroupName, string resourceGroupLocation)
        {
            ResourceGroup resourceGroupParameters = new ResourceGroup()
            {
                Location = resourceGroupLocation,
            };
            resourceMgmtClient.SubscriptionId = subscriptionId;
            ResourceGroup resourceGroupResult = resourceMgmtClient.ResourceGroups.CreateOrUpdate(resourceGroupName, resourceGroupParameters);
            return resourceGroupResult;
        }

        static Server CreateOrUpdateServer(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverLocation, string serverName, string serverAdmin, string serverAdminPassword)
        {
            Server serverParameters = new Server()
            {
                Location = serverLocation,
                AdministratorLogin = serverAdmin,
                AdministratorLoginPassword = serverAdminPassword,
                Version = "12.0"
            };
            Server serverResult = sqlMgmtClient.Servers.CreateOrUpdate(resourceGroupName, serverName, serverParameters);
            return serverResult;
        }

        static FirewallRule CreateOrUpdateFirewallRule(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string firewallRuleName, string startIpAddress, string endIpAddress)
        {
            FirewallRule firewallParameters = new FirewallRule()
            {
                StartIpAddress = startIpAddress,
                EndIpAddress = endIpAddress
            };
            FirewallRule firewallResult = sqlMgmtClient.FirewallRules.CreateOrUpdate(resourceGroupName, serverName, firewallRuleName, firewallParameters);
            return firewallResult;
        }

        static Database CreateOrUpdateDatabase(SqlManagementClient sqlMgmtClient, string resourceGroupName, string serverName, string databaseName, string databaseEdition, string databasePerfLevel)
        {
            // Retrieve hello server that will host this database
            Server currentServer = sqlMgmtClient.Servers.Get(resourceGroupName, serverName);

            // Create a database: configure create or update parameters and properties explicitly
            Database newDatabaseParameters = new Database()
            {
                Location = currentServer.Location,
                CreateMode = CreateMode.Default,
                Edition = databaseEdition,
                RequestedServiceObjectiveName = databasePerfLevel

            };
            Database dbResponse = sqlMgmtClient.Databases.CreateOrUpdate(resourceGroupName, serverName, databaseName, newDatabaseParameters);
            return dbResponse;
        }



        private static AuthenticationResult GetToken(string tenantId, string applicationId, string applicationSecret)
        {
            AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/" + tenantId);
            _token = authContext.AcquireToken("https://management.core.windows.net/", new ClientCredential(applicationId, applicationSecret));
            return _token;
        }
      }
    }





## <a name="create-a-service-principal-tooaccess-resources"></a>Créer un tooaccess de principal du service des ressources
Hello script PowerShell suivant crée application d’Active Directory (AD) hello et service de hello principal que nous devons tooauthenticate notre application c#. script de Hello génère des valeurs, que nous devons pour hello précédant c# les exemples. Pour plus d’informations, consultez [utiliser Azure PowerShell toocreate un principal de service tooaccess ressources](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    # Sign in tooAzure.
    Add-AzureRmAccount

    # If you have multiple subscriptions, uncomment and set toohello subscription you want toowork with.
    #$subscriptionId = "{xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}"
    #Set-AzureRmContext -SubscriptionId $subscriptionId

    # Provide these values for your new AAD app.
    # $appName is hello display name for your app, must be unique in your directory.
    # $uri does not need toobe a real uri.
    # $secret is a password you create.

    $appName = "{app-name}"
    $uri = "http://{app-name}"
    $secret = "{app-password}"

    # Create a AAD app
    $azureAdApplication = New-AzureRmADApplication -DisplayName $appName -HomePage $Uri -IdentifierUris $Uri -Password $secret

    # Create a Service Principal for hello app
    $svcprincipal = New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

    # tooavoid a PrincipalNotFound error, I pause here for 15 seconds.
    Start-Sleep -s 15

    # If you still get a PrincipalNotFound error, then rerun hello following until successful. 
    $roleassignment = New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $azureAdApplication.ApplicationId.Guid


    # Output hello values we need for our C# application toosuccessfully authenticate

    Write-Output "Copy these values into hello C# sample app"

    Write-Output "_subscriptionId:" (Get-AzureRmContext).Subscription.SubscriptionId
    Write-Output "_tenantId:" (Get-AzureRmContext).Tenant.TenantId
    Write-Output "_applicationId:" $azureAdApplication.ApplicationId.Guid
    Write-Output "_applicationSecret:" $secret



## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez essayé de base de données SQL et configurer une base de données avec c#, vous êtes prêt pour hello suivant des articles :

* [Se connecter tooSQL de base de données avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md)

## <a name="additional-resources"></a>Ressources supplémentaires
* [Base de données SQL](https://azure.microsoft.com/documentation/services/sql-database/)
* [Classe de base de données](https://msdn.microsoft.com/library/azure/microsoft.azure.management.sql.models.database.aspx)

<!--Image references-->
[1]: ./media/sql-database-get-started-csharp/aad.png
[2]: ./media/sql-database-get-started-csharp/permissions.png
[3]: ./media/sql-database-get-started-csharp/getdomain.png
[4]: ./media/sql-database-get-started-csharp/aad2.png
[5]: ./media/sql-database-get-started-csharp/aad-applications.png
[6]: ./media/sql-database-get-started-csharp/add.png
[7]: ./media/sql-database-get-started-csharp/add-application.png
[8]: ./media/sql-database-get-started-csharp/add-application2.png
[9]: ./media/sql-database-get-started-csharp/clientid.png
