---
title: "Créer des applications .NET HDInsight d’authentification non interactives - Azure | Microsoft Docs"
description: "Apprenez à créer des applications .NET HDInsight d’authentification non interactives."
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
ms.openlocfilehash: 7821a9e60e60ff01cff06db2a6f216a260c1c41a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="155b3-103">Créer des applications .NET HDInsight d’authentification non interactives</span><span class="sxs-lookup"><span data-stu-id="155b3-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="155b3-104">Vous pouvez exécuter votre application .NET Azure HDInsight sous l’identité de l’application (non interactive) ou sous l’identité de l’utilisateur connecté à l’application (interactive).</span><span class="sxs-lookup"><span data-stu-id="155b3-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under the identity of the signed-in user of the application (interactive).</span></span> <span data-ttu-id="155b3-105">Pour voir un exemple de l’application interactive, consultez [Se connecter à Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="155b3-105">For a sample of the interactive application, see [Connect to Azure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="155b3-106">Cet article vous présente la création d’une application .NET d’authentification non interactive pour se connecter à Azure et gérer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="155b3-106">This article shows you how to create non-interactive authentication .NET application to connect to Azure and manage HDInsight.</span></span>

<span data-ttu-id="155b3-107">À partir de votre application .NET non interactive, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="155b3-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="155b3-108">Votre ID de locataire d’abonnement Azure (ou ID répertoire).</span><span class="sxs-lookup"><span data-stu-id="155b3-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="155b3-109">Voir [Obtenir l’ID de locataire](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="155b3-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="155b3-110">L’ID client d’application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="155b3-110">The Azure Active Directory application client ID.</span></span> <span data-ttu-id="155b3-111">Voir [Créer une application Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) et la rubrique [Obtenir un ID d’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="155b3-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="155b3-112">La clé secrète de l’application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="155b3-112">The Azure Active Directory application secret key.</span></span> <span data-ttu-id="155b3-113">Voir la rubrique sur [l’obtention de la clé d’authentification de l’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="155b3-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="155b3-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="155b3-114">Prerequisites</span></span>
* <span data-ttu-id="155b3-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="155b3-115">HDInsight cluster.</span></span> <span data-ttu-id="155b3-116">Voir le [didacticiel de prise en main](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="155b3-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-to-role"></a><span data-ttu-id="155b3-117">Affecter l’application Azure AD à un rôle</span><span class="sxs-lookup"><span data-stu-id="155b3-117">Assign Azure AD application to role</span></span>
<span data-ttu-id="155b3-118">Vous devez affecter l’application à un [rôle](../active-directory/role-based-access-built-in-roles.md) pour lui accorder les autorisations lui permettant de réaliser des opérations.</span><span class="sxs-lookup"><span data-stu-id="155b3-118">You must assign the application to a [role](../active-directory/role-based-access-built-in-roles.md) to grant it permissions for performing actions.</span></span> <span data-ttu-id="155b3-119">Vous pouvez définir l’étendue au niveau de l’abonnement, du groupe de ressources ou de la ressource.</span><span class="sxs-lookup"><span data-stu-id="155b3-119">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="155b3-120">Les autorisations sont héritées des niveaux inférieurs de l’étendue (par exemple, l’ajout d’une application au rôle Lecteur pour un groupe de ressources signifie qu’elle peut lire le groupe de ressources et toutes les ressources qu’il contient).</span><span class="sxs-lookup"><span data-stu-id="155b3-120">The permissions are inherited to lower levels of scope (for example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains).</span></span> <span data-ttu-id="155b3-121">Dans ce didacticiel, vous allez définir la portée au niveau du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="155b3-121">In this tutorial, you will set the scope at the resource group level.</span></span> <span data-ttu-id="155b3-122">Pour en savoir plus, consultez [Utiliser les attributions de rôle pour gérer l’accès à vos ressources d’abonnement Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="155b3-122">For more information, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="155b3-123">**Pour ajouter le rôle propriétaire à l’application Azure AD**</span><span class="sxs-lookup"><span data-stu-id="155b3-123">**To add the Owner role to the Azure AD application**</span></span>

1. <span data-ttu-id="155b3-124">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="155b3-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="155b3-125">Cliquez sur **Groupe de ressources** dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="155b3-125">Click **Resource Group** from the left pane.</span></span>
3. <span data-ttu-id="155b3-126">Cliquez sur le groupe de ressources qui contient le cluster HDInsight sur lequel vous exécuterez votre requête Hive plus tard dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="155b3-126">Click the resource group that contains the HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="155b3-127">S’il y a trop de groupes de ressources, vous pouvez utiliser le filtre.</span><span class="sxs-lookup"><span data-stu-id="155b3-127">If there are too many resource groups, you can use the filter.</span></span>
4. <span data-ttu-id="155b3-128">Dans le panneau du groupe de ressources, cliquez sur **Contrôle d’accès (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="155b3-128">Click **Access control (IAM)** from the resource group menu.</span></span>
5. <span data-ttu-id="155b3-129">Dans le panneau **Utilisateurs**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="155b3-129">Click **Add** from the **Users** blade.</span></span>
6. <span data-ttu-id="155b3-130">Suivez les instructions pour ajouter le rôle **Propriétaire** à l’application Azure AD que vous avez créée dans la dernière procédure.</span><span class="sxs-lookup"><span data-stu-id="155b3-130">Follow the instruction to add the **Owner** role to the Azure AD application you created in the last procedure.</span></span> <span data-ttu-id="155b3-131">Lorsque la procédure se termine correctement, vous devez voir l’application répertoriée dans le panneau des utilisateurs, avec le rôle de propriétaire.</span><span class="sxs-lookup"><span data-stu-id="155b3-131">When you complete it successfully, you shall see the application listed in the Users blade with the Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="155b3-132">Développer une application cliente HDInsight</span><span class="sxs-lookup"><span data-stu-id="155b3-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="155b3-133">Création d’une application console C#.</span><span class="sxs-lookup"><span data-stu-id="155b3-133">Create a C# console application.</span></span>
2. <span data-ttu-id="155b3-134">Ajouter les packages Nuget suivants :</span><span class="sxs-lookup"><span data-stu-id="155b3-134">Add the following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="155b3-135">Utiliser l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="155b3-135">Use the following code sample:</span></span>

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
                private static string secretKey = "<Enter the Application Secret Key>";
        
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
                    Console.WriteLine("Press Enter to continue");
                    Console.ReadLine();
                }

                /// Get the access token for a service principal and provided key                
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

## <a name="next-steps"></a><span data-ttu-id="155b3-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="155b3-136">Next steps</span></span>
* [<span data-ttu-id="155b3-137">Création de l'application Azure Active Directory et du principal du service à l'aide du portail</span><span class="sxs-lookup"><span data-stu-id="155b3-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="155b3-138">Authentifier un principal du service à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="155b3-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="155b3-139">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="155b3-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
