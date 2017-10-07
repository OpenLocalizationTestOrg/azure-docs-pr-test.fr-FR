---
title: "l’authentification non interactive aaaCreate applications .NET HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment les applications .NET HDInsight toocreate d’authentification non interactive."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 8e32430f-6404-498a-9fcd-f20338d964af
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 5367c160b0146e6b855486b95f363e8fe7f1c98f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a>Créer des applications .NET HDInsight d’authentification non interactives
Vous pouvez exécuter votre application .NET Azure HDInsight sous l’identité de l’application (non interactif) ou sous l’identité hello de hello utilisateur connecté de l’application hello (interactive). Pour voir un exemple d’application interactive de hello, [connecter tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight). Cet article vous montre comment toocreate l’authentification non interactive .NET application tooconnect tooAzure et gérer HDInsight.

À partir de votre application .NET non interactive, vous avez besoin des éléments suivants :

* Votre ID de locataire d’abonnement Azure (ou ID répertoire). Voir [Obtenir l’ID de locataire](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).
* ID client d’application Hello Azure Active Directory. Voir [Créer une application Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) et la rubrique [Obtenir un ID d’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)
* clé secrète Hello Azure Active Directory application. Voir la rubrique sur [l’obtention de la clé d’authentification de l’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

## <a name="prerequisites"></a>Composants requis
* Cluster HDInsight. Voir le [didacticiel de prise en main](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).



## <a name="assign-azure-ad-application-toorole"></a>Affecter des toorole d’application Azure AD
Vous devez attribuer hello application tooa [rôle](../active-directory/role-based-access-built-in-roles.md) toogrant il autorisations pour effectuer des actions. Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource. les autorisations de Hello sont toolower hérités des niveaux d’étendue (par exemple, ajout de qu'un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire le groupe de ressources hello et toutes les ressources qu’il contient). Dans ce didacticiel, vous allez définir la portée de hello au niveau de groupe de ressources hello. Pour plus d’informations, consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md)

**tooadd hello application toohello Azure AD de rôle propriétaire**

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **groupe de ressources** hello volet de gauche.
3. Cliquez sur le groupe de ressources hello qui contient le cluster HDInsight de hello où vous exécuterez votre requête Hive plus loin dans ce didacticiel. S’il existe trop de groupes de ressources, vous pouvez utiliser le filtre de hello.
4. Cliquez sur **(IAM) de contrôle d’accès** à partir du menu hello du groupe de ressources.
5. Cliquez sur **ajouter** de hello **utilisateurs** panneau.
6. Suivez hello de hello instruction tooadd **propriétaire** rôle toohello application Azure AD que vous avez créé dans la dernière procédure de hello. Lorsque vous terminez correctement, vous devez voir l’application hello répertoriée dans le panneau des utilisateurs hello avec le rôle de propriétaire hello.

## <a name="develop-hdinsight-client-application"></a>Développer une application cliente HDInsight

1. Création d’une application console C#.
2. Ajoutez hello suivant les packages Nuget :

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. Utilisez hello suivant l’exemple de code :

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Common.Authentication;
        using Microsoft.Azure.Common.Authentication.Factories;
        using Microsoft.Azure.Common.Authentication.Models;
        using Microsoft.Azure.Management.Resources;
        using Microsoft.Azure.Management.HDInsight;
        
        namespace CreateHDICluster
        {
            internal class Program
            {
                private static HDInsightManagementClient _hdiManagementClient;
        
                private static Guid SubscriptionId = new Guid("<Enter Your Azure Subscription ID>");
                private static string tenantID = "<Enter Your Tenant ID (A.K.A. Directory ID)>";
                private static string applicationID = "<Enter Your Application ID>";
                private static string secretKey = "<Enter hello Application Secret Key>";
        
                private static void Main(string[] args)
                {
                    var key = new SecureString();
                    foreach (char c in secretKey) { key.AppendChar(c); }

                    var tokenCreds = GetTokenCloudCredentials(tenantID, applicationID, key);
                    var subCloudCredentials = GetSubscriptionCloudCredentials(tokenCreds, SubscriptionId);
        
                    var resourceManagementClient = new ResourceManagementClient(subCloudCredentials);
                    resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        
                    _hdiManagementClient = new HDInsightManagementClient(subCloudCredentials);
        
                    var results = _hdiManagementClient.Clusters.List();
                    foreach (var name in results.Clusters)
                    {
                        Console.WriteLine("Cluster Name: " + name.Name);
                        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
                        Console.WriteLine("\t Cluster location: " + name.Location);
                        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
                    }
                    Console.WriteLine("Press Enter toocontinue");
                    Console.ReadLine();
                }

                /// Get hello access token for a service principal and provided key                
                public static TokenCloudCredentials GetTokenCloudCredentials(string tenantId, string clientId, SecureString secretKey)
                {
                    var authFactory = new AuthenticationFactory();
                    var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
                    var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
                    var accessToken =
                        authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
        
                    return new TokenCloudCredentials(accessToken);
                }
        
                public static SubscriptionCloudCredentials GetSubscriptionCloudCredentials(SubscriptionCloudCredentials creds, Guid subId)
                {
                    return new TokenCloudCredentials(subId.ToString(), ((TokenCloudCredentials)creds).Token);
                }
            }
        }

## <a name="next-steps"></a>Étapes suivantes
* [Création de l'application Azure Active Directory et du principal du service à l'aide du portail](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Authentifier un principal du service à l’aide d’Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Contrôle d’accès en fonction du rôle Azure](../active-directory/role-based-access-control-configure.md)
