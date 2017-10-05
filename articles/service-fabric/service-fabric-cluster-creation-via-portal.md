---
title: "Créer un cluster Service Fabric dans le portail Azure | Microsoft Docs"
description: "Cet article décrit comment configurer un cluster Service Fabric sécurisé dans Azure à l’aide du portail Azure et d’Azure Key Vault."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="29965-103">Création d’un cluster Service Fabric dans Azure à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="29965-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29965-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29965-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="29965-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="29965-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="29965-106">Ce guide vous mène pas à pas à travers les étapes de configuration d’un cluster Service Fabric sécurisé dans Azure à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29965-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="29965-107">Il vous permet de vous familiariser avec les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="29965-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="29965-108">configuration d’Azure Key Vault de manière à gérer des clés pour la sécurité des clusters ;</span><span class="sxs-lookup"><span data-stu-id="29965-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="29965-109">création d’un cluster sécurisé dans le portail Azure ;</span><span class="sxs-lookup"><span data-stu-id="29965-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="29965-110">authentification d’administrateurs à l’aide de certificat.</span><span class="sxs-lookup"><span data-stu-id="29965-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="29965-111">Pour accéder à des options de sécurité plus avancées, telles que l’authentification des utilisateurs avec Azure Active Directory et la configuration de certificats pour la sécurité des applications, [créez votre cluster à l’aide d’Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="29965-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="29965-112">Un cluster sécurisé est un cluster qui empêche tout accès non autorisé à des opérations de gestion, notamment le déploiement, la mise à niveau et la suppression d’applications, de services et des données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="29965-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="29965-113">Un cluster non sécurisé est un cluster auquel toute personne peut se connecter à tout moment pour effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="29965-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="29965-114">Bien qu’il soit possible de créer un cluster non sécurisé, il est **vivement recommandé de créer un cluster sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="29965-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="29965-115">Un cluster non sécurisé **ne peut pas être sécurisé ultérieurement** , ce qui implique la création d’un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="29965-116">Les concepts appliqués sont les mêmes pour la création de clusters sécurisés, qu’il s’agisse de clusters Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="29965-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="29965-117">Pour en savoir plus et pour accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="29965-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="29965-118">Les paramètres obtenus par le script d’assistance peuvent être saisis directement dans le portail, comme indiqué dans la section [Création d’un cluster dans le portail Azure](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="29965-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="29965-119">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="29965-119">Log in to Azure</span></span>
<span data-ttu-id="29965-120">Ce guide utilise [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="29965-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="29965-121">Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à votre compte Azure et sélectionnez votre abonnement avant d’exécuter des commandes Azure.</span><span class="sxs-lookup"><span data-stu-id="29965-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="29965-122">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="29965-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="29965-123">Sélectionnez votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="29965-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="29965-124">Configuration d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="29965-124">Set up Key Vault</span></span>
<span data-ttu-id="29965-125">Cette partie du guide vous présente la création d’un coffre de clés pour un cluster Service Fabric dans Azure et pour des applications Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29965-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="29965-126">Pour obtenir un guide complet sur Key Vault, consultez le [Guide pratique de Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="29965-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="29965-127">Service Fabric utilise des certificats X.509 pour sécuriser un cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="29965-128">Azure Key Vault permet de gérer des certificats pour des clusters Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="29965-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="29965-129">Lorsqu’un cluster est déployé dans Azure, le fournisseur de ressources Azure chargé de la création des clusters Service Fabric extrait les certificats de Key Vault et les installe sur les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="29965-130">Le diagramme suivant illustre la relation entre Key Vault, un cluster Service Fabric et le fournisseur de ressources Azure qui utilise des certificats stockés dans Key Vault lorsqu’il crée un cluster :</span><span class="sxs-lookup"><span data-stu-id="29965-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="29965-132">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="29965-132">Create a Resource Group</span></span>
<span data-ttu-id="29965-133">La première étape consiste à créer un nouveau groupe de ressources spécifiquement pour le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="29965-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="29965-134">Il est recommandé de placer le coffre de clés dans son propre groupe de ressources pour vous permettre de supprimer des groupes de ressources de calcul et de stockage (par exemple, le groupe de ressources qui contient votre cluster Service Fabric) sans perdre vos clés et vos secrets.</span><span class="sxs-lookup"><span data-stu-id="29965-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="29965-135">Le groupe de ressources qui contient votre coffre de clés doit se trouver dans la même région que le cluster qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="29965-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="29965-136">Création d'un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="29965-136">Create Key Vault</span></span>
<span data-ttu-id="29965-137">Créez un coffre de clés dans le nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="29965-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="29965-138">Le coffre de clés **doit être activé pour le déploiement** afin d’autoriser le fournisseur de ressources Service Fabric à obtenir des certificats à partir de ce coffre et à les installer sur les nœuds de cluster :</span><span class="sxs-lookup"><span data-stu-id="29965-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="29965-139">Si vous avez un coffre de clés existant, vous pouvez l’activer pour le déploiement à l’aide de l’interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="29965-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="29965-140">Ajout de certificats à Key Vault</span><span class="sxs-lookup"><span data-stu-id="29965-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="29965-141">Les certificats sont utilisés dans Service Fabric à des fins d’authentification et de chiffrement pour sécuriser les divers aspects d’un cluster et de ses applications.</span><span class="sxs-lookup"><span data-stu-id="29965-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="29965-142">Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="29965-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="29965-143">Certificat de cluster et de serveur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="29965-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="29965-144">Ce certificat est nécessaire pour sécuriser un cluster et empêcher un accès non autorisé à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="29965-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="29965-145">Il assure la sécurité du cluster de différentes manières :</span><span class="sxs-lookup"><span data-stu-id="29965-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="29965-146">**Authentification du cluster :** authentifie la communication nœud à nœud pour la fédération du cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="29965-147">Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajoutés au cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="29965-148">**Authentification du serveur :** authentifie les points de terminaison de gestion du cluster sur un client de gestion, afin que le client de gestion sache qu’il communique avec le véritable cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="29965-149">Ce certificat fournit également SSL pour l’API de gestion HTTPS et Service Fabric Explorer par le biais de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="29965-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="29965-150">Pour cela, le certificat doit répondre aux exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="29965-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="29965-151">Le certificat doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="29965-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="29965-152">Le certificat doit être créé pour l'échange de clés et pouvoir faire l'objet d'un export au format Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="29965-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="29965-153">Le nom d'objet du certificat doit correspondre au domaine servant à accéder au cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29965-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="29965-154">Cela est nécessaire pour la fourniture de SSL pour les points de terminaison de gestion HTTPS du cluster et Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="29965-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="29965-155">Vous ne pouvez pas obtenir de certificat SSL auprès d'une autorité de certification pour le domaine `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="29965-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="29965-156">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="29965-157">Lorsque vous demandez un certificat auprès d'une autorité de certification, le nom d'objet du certificat doit correspondre au nom de domaine personnalisé que vous utilisez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="29965-158">Authentification de certificat client</span><span class="sxs-lookup"><span data-stu-id="29965-158">Client authentication certificates</span></span>
<span data-ttu-id="29965-159">Les certificats client supplémentaires authentifient les administrateurs pour les tâches de gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="29965-160">Service Fabric dispose de deux niveaux d’accès : **admin** et **read-only user**.</span><span class="sxs-lookup"><span data-stu-id="29965-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="29965-161">Au minimum, un seul certificat pour un accès administrateur doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="29965-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="29965-162">Pour un accès de niveau utilisateur supplémentaire, un certificat distinct doit être fourni.</span><span class="sxs-lookup"><span data-stu-id="29965-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="29965-163">Pour en savoir plus sur les rôles d’accès, consultez la page [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="29965-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="29965-164">Vous n’avez pas besoin de charger les certificats d’authentification client dans le Key Vault pour pouvoir travailler avec Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29965-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="29965-165">Il suffit de fournir ces certificats aux utilisateurs qui sont autorisés à effectuer la gestion des clusters.</span><span class="sxs-lookup"><span data-stu-id="29965-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="29965-166">Azure Active Directory est la méthode recommandée pour authentifier les clients pour des opérations de gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="29965-167">Pour utiliser Azure Active Directory, vous devez [créer un cluster à l’aide d’Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="29965-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="29965-168">Certificats d’application (facultatif)</span><span class="sxs-lookup"><span data-stu-id="29965-168">Application certificates (optional)</span></span>
<span data-ttu-id="29965-169">Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application.</span><span class="sxs-lookup"><span data-stu-id="29965-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="29965-170">Avant de créer votre cluster, examinez les scénarios de sécurité d’application qui nécessitent l’installation d’un certificat sur les nœuds, notamment :</span><span class="sxs-lookup"><span data-stu-id="29965-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="29965-171">Le chiffrement et déchiffrement de valeurs de configuration d’applications.</span><span class="sxs-lookup"><span data-stu-id="29965-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="29965-172">Le chiffrement des données sur les nœuds lors de la réplication.</span><span class="sxs-lookup"><span data-stu-id="29965-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="29965-173">Les certificats d’application ne peuvent pas être configurés lors de la création d’un cluster par le biais du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29965-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="29965-174">Pour configurer les certificats d’application au moment de la configuration du cluster, vous devez [créer un cluster à l’aide d’Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="29965-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="29965-175">Vous pouvez également ajouter des certificats d’application au cluster après sa création.</span><span class="sxs-lookup"><span data-stu-id="29965-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="29965-176">Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="29965-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="29965-177">Des fichiers de clé privée (.pfx) peuvent être ajoutés et utilisés directement par le biais de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29965-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="29965-178">Toutefois, le fournisseur de ressources Azure nécessite que les clés soient stockées dans un format JSON spécial qui inclut le fichier .pfx en tant que chaîne encodée en base 64 et le mot de passe de clé privée.</span><span class="sxs-lookup"><span data-stu-id="29965-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="29965-179">Pour répondre à ces exigences, les clés doivent être placées dans une chaîne JSON, puis stockées en tant que *secrets* dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29965-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="29965-180">Pour faciliter ce processus, un module PowerShell est [disponible sur GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="29965-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="29965-181">Procédez comme suit pour utiliser le module :</span><span class="sxs-lookup"><span data-stu-id="29965-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="29965-182">Téléchargez le contenu complet du référentiel dans un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="29965-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="29965-183">Importez le module dans la fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="29965-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="29965-184">La commande `Invoke-AddCertToKeyVault` dans ce module PowerShell met automatiquement en forme une clé privée de certificat dans une chaîne JSON et la charge vers Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29965-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="29965-185">Il permet d’ajouter le certificat de cluster et tous les certificats d’application supplémentaires à Key Vault.</span><span class="sxs-lookup"><span data-stu-id="29965-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="29965-186">Répétez simplement cette étape pour tous les certificats supplémentaires à installer sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="29965-187">Il s’agit de toutes les conditions préalables de Key Vault pour la configuration d’un modèle Service Fabric Cluster Resource Manager qui installe des certificats pour l’authentification de nœud, la sécurité des points de terminaison d’administration et les fonctionnalités de sécurité d’application supplémentaires qui utilisent des certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="29965-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="29965-188">À ce stade, vous disposez à présent la configuration suivante dans Azure :</span><span class="sxs-lookup"><span data-stu-id="29965-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="29965-189">Groupe de ressources Key Vault</span><span class="sxs-lookup"><span data-stu-id="29965-189">Key Vault resource group</span></span>
  * <span data-ttu-id="29965-190">Key Vault</span><span class="sxs-lookup"><span data-stu-id="29965-190">Key Vault</span></span>
    * <span data-ttu-id="29965-191">Certificat d’authentification de serveur de clusters</span><span class="sxs-lookup"><span data-stu-id="29965-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="29965-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="29965-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="29965-193">Création d’un cluster dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="29965-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="29965-194">Rechercher la ressource de cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="29965-194">Search for the Service Fabric cluster resource</span></span>
![Rechercher le modèle de cluster Service Fabric sur le portail Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="29965-196">Connectez-vous au [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="29965-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="29965-197">Cliquez sur **Nouveau** pour ajouter un nouveau modèle de ressources.</span><span class="sxs-lookup"><span data-stu-id="29965-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="29965-198">Recherchez le modèle de cluster Service Fabric dans **Marketplace** sous **Tout**.</span><span class="sxs-lookup"><span data-stu-id="29965-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="29965-199">Sélectionnez **Cluster Service Fabric** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="29965-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="29965-200">Accédez au panneau **Cluster Service Fabric**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="29965-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="29965-201">Le panneau **Créer un cluster Service Fabric** inclut les quatre étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="29965-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="29965-202">1. Concepts de base</span><span class="sxs-lookup"><span data-stu-id="29965-202">1. Basics</span></span>
![Capture d’écran de la création d’un groupe de ressources.][CreateRG]

<span data-ttu-id="29965-204">Dans le volet De base, vous devez fournir les informations de base de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="29965-205">Entrez le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="29965-206">Choisissez un **Nom d’utilisateur** et un **Mot de passe** pour le bureau à distance pour les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="29965-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="29965-207">Veillez à sélectionner **l’Abonnement** sur lequel vous souhaitez que votre cluster soit déployé, surtout si vous avez plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="29965-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="29965-208">Créez un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="29965-208">Create a **new resource group**.</span></span> <span data-ttu-id="29965-209">Il est préférable de lui attribuer le même nom que le cluster, car cela vous permet de le retrouver plus facilement, surtout lorsque vous essayez d’apporter des modifications à votre déploiement ou de supprimer votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="29965-210">Bien que vous puissiez décider d’utiliser un groupe de ressources existant, nous vous conseillons de créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="29965-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="29965-211">Cela facilite la suppression des clusters dont vous n’avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="29965-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="29965-212">Sélectionnez la **région** dans laquelle vous souhaitez créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="29965-213">Vous devez utiliser la région de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="29965-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="29965-214">2. Configuration de clusters</span><span class="sxs-lookup"><span data-stu-id="29965-214">2. Cluster configuration</span></span>
![Création d’un type de nœud][CreateNodeType]

<span data-ttu-id="29965-216">Configurez vos nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-216">Configure your cluster nodes.</span></span> <span data-ttu-id="29965-217">Les types de nœuds définissent les tailles de machine virtuelle, le nombre de machines virtuelles et leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="29965-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="29965-218">Votre cluster peut avoir plusieurs types de nœud, mais le type de nœud principal (le premier que vous définissez sur le portail) doit avoir au moins cinq machines virtuelles, car il s’agit du type de nœud dans lequel les services du système Service Fabric sont placés.</span><span class="sxs-lookup"><span data-stu-id="29965-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="29965-219">Ne configurez pas la zone **Propriétés de sélection élective** , car une propriété de sélection élective par défaut de « NodeTypeName » est ajoutée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="29965-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="29965-220">Un scénario répandu si vous avez plusieurs types de nœuds est une application qui contient un service front-end et un service back-end.</span><span class="sxs-lookup"><span data-stu-id="29965-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="29965-221">Vous souhaitez placer le service front-end sur des machines virtuelles plus petites (tailles de machine virtuelle de type D2) avec leurs ports ouverts à Internet, mais vous souhaitez placer le service back-end sur des machines virtuelles de plus grandes tailles (dont les tailles sont de type D4, D6, D15, etc.) dont les ports ne sont pas accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="29965-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="29965-222">Choisissez un nom pour votre type de nœud (1 à 12 caractères contenant uniquement des lettres et des chiffres).</span><span class="sxs-lookup"><span data-stu-id="29965-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="29965-223">La **taille** minimale des machines virtuelles pour le type de nœud principal dépend de la couche de **durabilité** que vous choisissez pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="29965-224">La valeur par défaut du niveau de durabilité est Bronze.</span><span class="sxs-lookup"><span data-stu-id="29965-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="29965-225">Pour en savoir plus sur la durabilité, consultez la page [Comment choisir la fiabilité et la durabilité du cluster Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="29965-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="29965-226">Sélectionnez la taille de machine virtuelle et le niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="29965-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="29965-227">Les machines virtuelles de série D ont des lecteurs de disques SSD et sont vivement recommandées pour les applications avec état.</span><span class="sxs-lookup"><span data-stu-id="29965-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="29965-228">N’utilisez pas les références de machine virtuelle incluant des cœurs partiels ou présentant une capacité de disque disponible inférieure à 7 Go.</span><span class="sxs-lookup"><span data-stu-id="29965-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="29965-229">Le **nombre** minimum de machines virtuelles du type de nœud principal dépend du niveau de **fiabilité** que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="29965-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="29965-230">La valeur par défaut du niveau de fiabilité est Silver.</span><span class="sxs-lookup"><span data-stu-id="29965-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="29965-231">Pour en savoir plus sur la fiabilité, consultez la page [Comment choisir la fiabilité et la durabilité du cluster Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="29965-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="29965-232">Choisissez le nombre de machines virtuelles du type de nœud.</span><span class="sxs-lookup"><span data-stu-id="29965-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="29965-233">Vous pouvez augmenter ou réduire ultérieurement le nombre de machines virtuelles d’un type de nœud. Cependant, pour le type de nœud principal, le nombre de machines virtuelles minimum dépend du niveau de fiabilité que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="29965-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="29965-234">Les autres types de nœud peuvent avoir au moins 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="29965-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="29965-235">Configurez des points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="29965-235">Configure custom endpoints.</span></span> <span data-ttu-id="29965-236">Ce champ vous permet d’entrer une liste séparée par des virgules des ports que vous souhaitez exposer par le biais de l’Azure Load Balancer à l’Internet public pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="29965-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="29965-237">Par exemple, si vous envisagez de déployer une application web dans votre cluster, saisissez « 80 » pour autoriser le trafic sur le port 80 dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="29965-238">Pour en savoir plus sur les points de terminaison, consultez la page [Communiquer avec des applications][service-fabric-connect-and-communicate-with-services].</span><span class="sxs-lookup"><span data-stu-id="29965-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="29965-239">Configurez les **diagnostics**du cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="29965-240">Par défaut, les diagnostics sont activés sur votre cluster afin de faciliter la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="29965-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="29965-241">Si vous souhaitez désactiver les diagnostics, définissez **l’État** sur **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="29965-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="29965-242">Nous vous recommandons de **ne pas** désactiver les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="29965-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="29965-243">Sélectionnez le mode de mise à niveau Service Fabric que vous souhaitez associer à votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="29965-244">Sélectionnez **Automatique**si vous souhaitez que le système récupère automatiquement la dernière version disponible et essaye de mettre à niveau votre cluster vers cette version.</span><span class="sxs-lookup"><span data-stu-id="29965-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="29965-245">Définissez le mode sur **Manuel**si vous souhaitez choisir une version prise en charge.</span><span class="sxs-lookup"><span data-stu-id="29965-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="29965-246">Nous prenons uniquement en charge les clusters qui exécutent des versions prises en charge de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="29965-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="29965-247">Si vous sélectionnez le mode **Manuel** , vous êtes responsable de la mise à niveau de votre cluster vers une version prise en charge.</span><span class="sxs-lookup"><span data-stu-id="29965-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="29965-248">Pour en savoir plus sur le mode de mise à niveau de Service Fabric, consultez le document [Mettre à niveau un cluster Service Fabric][service-fabric-cluster-upgrade].</span><span class="sxs-lookup"><span data-stu-id="29965-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="29965-249">3. Sécurité</span><span class="sxs-lookup"><span data-stu-id="29965-249">3. Security</span></span>
![Capture d’écran des configurations de sécurité sur le portail Azure.][SecurityConfigs]

<span data-ttu-id="29965-251">L’étape finale consiste à fournir des informations de certificat pour sécuriser le cluster à l’aide de Key Vault et les informations de certificat créées précédemment.</span><span class="sxs-lookup"><span data-stu-id="29965-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="29965-252">Remplissez les champs de certificat principaux par la sortie obtenue du chargement du **certificat de cluster** dans Key Vault à l’aide de la commande PowerShell `Invoke-AddCertToKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="29965-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="29965-253">Activez la case **Configurer les paramètres avancés** pour saisir les certificats clients pour le **Client d’administration** et le **Client en lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="29965-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="29965-254">Dans ces champs, saisissez l’empreinte de votre certificat de client d’administration et l’empreinte de votre certificat de client en lecture seule, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="29965-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="29965-255">Lorsque les administrateurs tentent de se connecter au cluster, ils se voient attribuer l’accès uniquement s’ils disposent d’un certificat avec une empreinte qui correspond aux valeurs entrées ici.</span><span class="sxs-lookup"><span data-stu-id="29965-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="29965-256">4. Résumé</span><span class="sxs-lookup"><span data-stu-id="29965-256">4. Summary</span></span>
![<span data-ttu-id="29965-257">Capture d’écran du Tableau d’accueil affichant « Déploiement du cluster Service Fabric ».</span><span class="sxs-lookup"><span data-stu-id="29965-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="29965-258">Pour achever la création du cluster, cliquez sur **Résumé** de manière à afficher les configurations que vous avez fournies, ou téléchargez le modèle Azure Resource Manager utilisé pour déployer votre cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="29965-259">Lorsque vous avez fourni les paramètres obligatoires, le bouton **OK** s’affiche en vert. Vous pouvez cliquer dessus pour démarrer le processus de création du cluster.</span><span class="sxs-lookup"><span data-stu-id="29965-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="29965-260">Vous pouvez voir la progression de la création dans les notifications.</span><span class="sxs-lookup"><span data-stu-id="29965-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="29965-261">(Cliquez sur l’icône représentant une cloche près de la barre d’état dans l’angle supérieur droit de votre écran.) Si vous avez cliqué sur **Épingler au tableau d’accueil** pendant la création du cluster, **Déploiement du cluster Service Fabric** apparaît épinglé au **tableau d’accueil**.</span><span class="sxs-lookup"><span data-stu-id="29965-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="29965-262">Afficher l’état de votre cluster</span><span class="sxs-lookup"><span data-stu-id="29965-262">View your cluster status</span></span>
![Capture d’écran des détails du cluster dans le tableau de bord.][ClusterDashboard]

<span data-ttu-id="29965-264">Une fois votre cluster créé, vous pouvez l’inspecter dans le portail :</span><span class="sxs-lookup"><span data-stu-id="29965-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="29965-265">Accédez à **Parcourir**, puis cliquez sur **Clusters Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="29965-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="29965-266">Recherchez votre cluster et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="29965-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="29965-267">Vous pouvez maintenant voir les détails de votre cluster dans le tableau de bord, notamment le point de terminaison du cluster et un lien vers Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="29965-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="29965-268">La section **Surveillance des nœuds** du panneau du tableau de bord du cluster indique le nombre de machines virtuelles intègres et de machines virtuelles non intègres.</span><span class="sxs-lookup"><span data-stu-id="29965-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="29965-269">Pour plus d’informations sur l’intégrité du cluster, consultez [Présentation du contrôle d’intégrité de Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="29965-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="29965-270">Les clusters Service Fabric nécessitent un certain nombre de nœuds actifs en permanence pour maintenir la disponibilité et préserver l’état. Cette situation est appelée « conservation du quorum ».</span><span class="sxs-lookup"><span data-stu-id="29965-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="29965-271">Par conséquent, il est généralement déconseillé d’arrêter tous les ordinateurs du cluster, sauf si vous avez d’abord effectué une [sauvegarde complète de votre état][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="29965-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="29965-272">Connexion distante à une instance de jeu de mise à l’échelle de machine virtuelle ou à un nœud de cluster</span><span class="sxs-lookup"><span data-stu-id="29965-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="29965-273">Chacune des valeurs NodeTypes que vous spécifiez dans votre cluster entraîne la configuration d’un groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="29965-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="29965-274">Consultez [Connexion distante à une instance de jeu de mise à l’échelle de machine virtuelle][remote-connect-to-a-vm-scale-set] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="29965-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29965-275">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29965-275">Next steps</span></span>
<span data-ttu-id="29965-276">À ce stade, vous avez un cluster sécurisé à l’aide de certificats pour l’authentification de la gestion.</span><span class="sxs-lookup"><span data-stu-id="29965-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="29965-277">Ensuite, [connectez-vous à votre cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment [gérer les secrets d’application](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="29965-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="29965-278">Découvrez également les [options de support de Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="29965-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
