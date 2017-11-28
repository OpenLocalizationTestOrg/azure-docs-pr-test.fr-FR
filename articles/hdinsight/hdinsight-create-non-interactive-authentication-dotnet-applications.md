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
# <a name="create-non-interactive-authentication-net-hdinsight-applications"></a><span data-ttu-id="4e45e-103">Créer des applications .NET HDInsight d’authentification non interactives</span><span class="sxs-lookup"><span data-stu-id="4e45e-103">Create non-interactive authentication .NET HDInsight applications</span></span>
<span data-ttu-id="4e45e-104">Vous pouvez exécuter votre application .NET Azure HDInsight sous l’identité de l’application (non interactif) ou sous l’identité hello de hello utilisateur connecté de l’application hello (interactive).</span><span class="sxs-lookup"><span data-stu-id="4e45e-104">You can run your .NET Azure HDInsight application either under application's own identity (non-interactive) or under hello identity of hello signed-in user of hello application (interactive).</span></span> <span data-ttu-id="4e45e-105">Pour voir un exemple d’application interactive de hello, [connecter tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="4e45e-105">For a sample of hello interactive application, see [Connect tooAzure HDInsight](hdinsight-administer-use-dotnet-sdk.md#connect-to-azure-hdinsight).</span></span> <span data-ttu-id="4e45e-106">Cet article vous montre comment toocreate l’authentification non interactive .NET application tooconnect tooAzure et gérer HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e45e-106">This article shows you how toocreate non-interactive authentication .NET application tooconnect tooAzure and manage HDInsight.</span></span>

<span data-ttu-id="4e45e-107">À partir de votre application .NET non interactive, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4e45e-107">From your non-interactive .NET application, you need:</span></span>

* <span data-ttu-id="4e45e-108">Votre ID de locataire d’abonnement Azure (ou ID répertoire).</span><span class="sxs-lookup"><span data-stu-id="4e45e-108">Your Azure subscription tenant ID (A.K.A directory ID).</span></span> <span data-ttu-id="4e45e-109">Voir [Obtenir l’ID de locataire](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="4e45e-109">See [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
* <span data-ttu-id="4e45e-110">ID client d’application Hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4e45e-110">hello Azure Active Directory application client ID.</span></span> <span data-ttu-id="4e45e-111">Voir [Créer une application Azure Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) et la rubrique [Obtenir un ID d’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span><span class="sxs-lookup"><span data-stu-id="4e45e-111">See [Create an Azure Active Directory application](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), and [Get an application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>
* <span data-ttu-id="4e45e-112">clé secrète Hello Azure Active Directory application.</span><span class="sxs-lookup"><span data-stu-id="4e45e-112">hello Azure Active Directory application secret key.</span></span> <span data-ttu-id="4e45e-113">Voir la rubrique sur [l’obtention de la clé d’authentification de l’application](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="4e45e-113">See [Get application authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e45e-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4e45e-114">Prerequisites</span></span>
* <span data-ttu-id="4e45e-115">Cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4e45e-115">HDInsight cluster.</span></span> <span data-ttu-id="4e45e-116">Voir le [didacticiel de prise en main](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="4e45e-116">See [getting started tutorial](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span>



## <a name="assign-azure-ad-application-toorole"></a><span data-ttu-id="4e45e-117">Affecter des toorole d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="4e45e-117">Assign Azure AD application toorole</span></span>
<span data-ttu-id="4e45e-118">Vous devez attribuer hello application tooa [rôle](../active-directory/role-based-access-built-in-roles.md) toogrant il autorisations pour effectuer des actions.</span><span class="sxs-lookup"><span data-stu-id="4e45e-118">You must assign hello application tooa [role](../active-directory/role-based-access-built-in-roles.md) toogrant it permissions for performing actions.</span></span> <span data-ttu-id="4e45e-119">Vous pouvez définir l’étendue de hello au niveau hello d’abonnement de hello, groupe de ressources ou ressource.</span><span class="sxs-lookup"><span data-stu-id="4e45e-119">You can set hello scope at hello level of hello subscription, resource group, or resource.</span></span> <span data-ttu-id="4e45e-120">les autorisations de Hello sont toolower hérités des niveaux d’étendue (par exemple, ajout de qu'un rôle de lecteur application toohello pour un groupe de ressources signifie qu’il peut lire le groupe de ressources hello et toutes les ressources qu’il contient).</span><span class="sxs-lookup"><span data-stu-id="4e45e-120">hello permissions are inherited toolower levels of scope (for example, adding an application toohello Reader role for a resource group means it can read hello resource group and any resources it contains).</span></span> <span data-ttu-id="4e45e-121">Dans ce didacticiel, vous allez définir la portée de hello au niveau de groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="4e45e-121">In this tutorial, you will set hello scope at hello resource group level.</span></span> <span data-ttu-id="4e45e-122">Pour plus d’informations, consultez [utiliser les ressources de rôle affectations toomanage accès tooyour abonnement Azure](../active-directory/role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="4e45e-122">For more information, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md)</span></span>

<span data-ttu-id="4e45e-123">**tooadd hello application toohello Azure AD de rôle propriétaire**</span><span class="sxs-lookup"><span data-stu-id="4e45e-123">**tooadd hello Owner role toohello Azure AD application**</span></span>

1. <span data-ttu-id="4e45e-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e45e-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4e45e-125">Cliquez sur **groupe de ressources** hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="4e45e-125">Click **Resource Group** from hello left pane.</span></span>
3. <span data-ttu-id="4e45e-126">Cliquez sur le groupe de ressources hello qui contient le cluster HDInsight de hello où vous exécuterez votre requête Hive plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4e45e-126">Click hello resource group that contains hello HDInsight cluster where you will run your Hive query later in this tutorial.</span></span> <span data-ttu-id="4e45e-127">S’il existe trop de groupes de ressources, vous pouvez utiliser le filtre de hello.</span><span class="sxs-lookup"><span data-stu-id="4e45e-127">If there are too many resource groups, you can use hello filter.</span></span>
4. <span data-ttu-id="4e45e-128">Cliquez sur **(IAM) de contrôle d’accès** à partir du menu hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4e45e-128">Click **Access control (IAM)** from hello resource group menu.</span></span>
5. <span data-ttu-id="4e45e-129">Cliquez sur **ajouter** de hello **utilisateurs** panneau.</span><span class="sxs-lookup"><span data-stu-id="4e45e-129">Click **Add** from hello **Users** blade.</span></span>
6. <span data-ttu-id="4e45e-130">Suivez hello de hello instruction tooadd **propriétaire** rôle toohello application Azure AD que vous avez créé dans la dernière procédure de hello.</span><span class="sxs-lookup"><span data-stu-id="4e45e-130">Follow hello instruction tooadd hello **Owner** role toohello Azure AD application you created in hello last procedure.</span></span> <span data-ttu-id="4e45e-131">Lorsque vous terminez correctement, vous devez voir l’application hello répertoriée dans le panneau des utilisateurs hello avec le rôle de propriétaire hello.</span><span class="sxs-lookup"><span data-stu-id="4e45e-131">When you complete it successfully, you shall see hello application listed in hello Users blade with hello Owner role.</span></span>

## <a name="develop-hdinsight-client-application"></a><span data-ttu-id="4e45e-132">Développer une application cliente HDInsight</span><span class="sxs-lookup"><span data-stu-id="4e45e-132">Develop HDInsight client application</span></span>

1. <span data-ttu-id="4e45e-133">Création d’une application console C#.</span><span class="sxs-lookup"><span data-stu-id="4e45e-133">Create a C# console application.</span></span>
2. <span data-ttu-id="4e45e-134">Ajoutez hello suivant les packages Nuget :</span><span class="sxs-lookup"><span data-stu-id="4e45e-134">Add hello following Nuget packages:</span></span>

        Install-Package Microsoft.Azure.Common.Authentication -Pre
        Install-Package Microsoft.Azure.Management.HDInsight -Pre
        Install-Package Microsoft.Azure.Management.Resources -Pre

3. <span data-ttu-id="4e45e-135">Utilisez hello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="4e45e-135">Use hello following code sample:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4e45e-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e45e-136">Next steps</span></span>
* [<span data-ttu-id="4e45e-137">Création de l'application Azure Active Directory et du principal du service à l'aide du portail</span><span class="sxs-lookup"><span data-stu-id="4e45e-137">Create Azure Active Directory application and service principal using portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="4e45e-138">Authentifier un principal du service à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e45e-138">Authenticate service principal with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="4e45e-139">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="4e45e-139">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
