---
title: "Créer un cluster Azure Service Fabric à partir d’un modèle | Microsoft Docs"
description: "Cet article explique comment configurer un cluster Service Fabric sécurisé dans Azure à l’aide d’Azure Resource Manager, Azure Key Vault et Azure Active Directory (Azure AD) pour l’authentification des clients."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="1f6c1-103">Créer un cluster Service Fabric à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f6c1-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="1f6c1-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f6c1-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="1f6c1-106">Ce guide vous montre pas à pas comment configurer un cluster Azure Service Fabric sécurisé dans Azure à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="1f6c1-107">Nous reconnaissons que cet article est un peu long.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="1f6c1-108">Cependant, à moins que vous soyez déjà parfaitement familiarisés avec le contenu, veillez à suivre attentivement chaque étape.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="1f6c1-109">Ce guide couvre les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="1f6c1-110">Configuration d’un Azure Key Vault afin de charger des certificats pour la sécurité du cluster et des applications</span><span class="sxs-lookup"><span data-stu-id="1f6c1-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="1f6c1-111">Création d’un cluster sécurisé dans Azure à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="1f6c1-112">Authentification des utilisateurs à l’aide d’Azure Active Directory (Azure AD) pour la gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="1f6c1-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="1f6c1-113">Un cluster sécurisé est un cluster qui empêche tout accès non autorisé aux opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="1f6c1-114">Cela inclut le déploiement, la mise à niveau et la suppression des applications, des services et des données qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="1f6c1-115">Un cluster non sécurisé est un cluster auquel toute personne peut se connecter à tout moment pour effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="1f6c1-116">Bien qu’il soit possible de créer un cluster non sécurisé, nous vous recommandons vivement de créer dès le départ un cluster sécurisé.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="1f6c1-117">En effet, un cluster non sécurisé ne peut pas être sécurisé ultérieurement, ce qui implique la création d’un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="1f6c1-118">La méthode de création de clusters sécurisés est la même pour les clusters Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="1f6c1-119">Pour en savoir plus et accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="1f6c1-120">Connexion à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="1f6c1-120">Sign in to your Azure account</span></span>
<span data-ttu-id="1f6c1-121">Ce guide utilise [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="1f6c1-122">Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à votre compte Azure et sélectionnez votre abonnement avant d’exécuter des commandes Azure.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="1f6c1-123">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1f6c1-124">Sélectionnez votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="1f6c1-125">Configurer un Key Vault</span><span class="sxs-lookup"><span data-stu-id="1f6c1-125">Set up a key vault</span></span>
<span data-ttu-id="1f6c1-126">Cette section explique comment créer un Key Vault pour un cluster Service Fabric dans Azure et pour des applications Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="1f6c1-127">Pour obtenir un guide complet sur Azure Key Vault, reportez-vous à l’article [Prise en main de Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="1f6c1-128">Service Fabric utilise des certificats X.509 pour sécuriser un cluster et fournir des fonctionnalités de sécurité d’applications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="1f6c1-129">Key Vault sert à gérer des certificats pour des clusters Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="1f6c1-130">Lorsqu’un cluster est déployé dans Azure, le fournisseur de ressources Azure chargé de la création des clusters Service Fabric extrait les certificats de Key Vault et les installe sur les machines virtuelles du cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="1f6c1-131">Le diagramme suivant illustre la relation entre Azure Key Vault, un cluster Service Fabric et le fournisseur de ressources Azure qui utilise des certificats stockés dans un Key Vault lorsqu’il crée un cluster :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagramme de l’installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="1f6c1-133">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1f6c1-133">Create a resource group</span></span>
<span data-ttu-id="1f6c1-134">La première étape consiste à créer un groupe de ressources dédié à votre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="1f6c1-135">Nous vous recommandons de placer ce Key Vault dans son propre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="1f6c1-136">Vous pouvez ainsi supprimer les groupes de ressources de calcul et de stockage, y compris le groupe de ressources contenant votre cluster Service Fabric, sans risquer de perdre vos clés et secrets.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="1f6c1-137">Le groupe de ressources qui contient votre Key Vault _doit se trouver dans la même région_ que le cluster qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="1f6c1-138">Si vous prévoyez de déployer des clusters dans plusieurs régions, nous vous conseillons de nommer le groupe de ressources et le Key Vault de manière à indiquer la région à laquelle ils appartiennent.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="1f6c1-139">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="1f6c1-140">Créer un Key Vault dans le nouveau groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1f6c1-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="1f6c1-141">Le Key Vault _doit être activé pour le déploiement_ afin d’autoriser le fournisseur de ressources de calcul à obtenir des certificats à partir de ce Key Vault et à les installer sur les instances de machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="1f6c1-142">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-142">The output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="1f6c1-143">Utiliser un Key Vault existant</span><span class="sxs-lookup"><span data-stu-id="1f6c1-143">Use an existing key vault</span></span>

<span data-ttu-id="1f6c1-144">Pour utiliser un Key Vault existant, vous _devez l’activer pour le déploiement_ afin d’autoriser le fournisseur de ressources de calcul à obtenir des certificats à partir de ce Key Vault et à les installer sur les nœuds de cluster :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="1f6c1-145">Ajouter des certificats à votre Key Vault</span><span class="sxs-lookup"><span data-stu-id="1f6c1-145">Add certificates to your key vault</span></span>

<span data-ttu-id="1f6c1-146">Les certificats sont utilisés dans Service Fabric à des fins d’authentification et de chiffrement pour sécuriser les divers aspects d’un cluster et de ses applications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="1f6c1-147">Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="1f6c1-148">Certificat de cluster et de serveur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="1f6c1-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="1f6c1-149">Ce certificat est nécessaire pour sécuriser un cluster et empêcher un accès non autorisé à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="1f6c1-150">Il assure la sécurité du cluster de deux manières :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="1f6c1-151">Authentification du cluster : authentifie la communication nœud à nœud pour la fédération du cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="1f6c1-152">Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajoutés au cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="1f6c1-153">Authentification du serveur : authentifie les points de terminaison de gestion du cluster sur un client de gestion, afin que le client de gestion sache qu’il communique avec le véritable cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="1f6c1-154">Ce certificat fournit également un certificat SSL pour l’API de gestion HTTPS et Service Fabric Explorer par le biais de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="1f6c1-155">Pour cela, le certificat doit répondre aux exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="1f6c1-156">Le certificat doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="1f6c1-157">Le certificat doit être créé pour l’échange de clés, qui peut faire l’objet d’un export vers un fichier .pfx (Personal Information Exchange).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="1f6c1-158">Le nom de sujet du certificat doit correspondre au domaine utilisé pour accéder au cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="1f6c1-159">Cela est nécessaire pour la fourniture d’un certificat SSL pour les points de terminaison de gestion HTTPS du cluster et pour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="1f6c1-160">Vous ne pouvez pas obtenir de certificat SSL auprès d’une autorité de certification pour le domaine azure.com.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="1f6c1-161">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="1f6c1-162">Lorsque vous demandez un certificat auprès d’une autorité de certification, le nom de sujet du certificat doit correspondre au nom de domaine personnalisé utilisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="1f6c1-163">Certificats d’application (facultatif)</span><span class="sxs-lookup"><span data-stu-id="1f6c1-163">Application certificates (optional)</span></span>
<span data-ttu-id="1f6c1-164">Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="1f6c1-165">Avant de créer votre cluster, examinez les scénarios de sécurité d’application qui nécessitent l’installation d’un certificat sur les nœuds, notamment :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="1f6c1-166">Le chiffrement et déchiffrement de valeurs de configuration d’application.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="1f6c1-167">Le chiffrement des données sur les nœuds lors de la réplication.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="1f6c1-168">Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="1f6c1-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="1f6c1-169">Vous pouvez ajouter et utiliser les fichiers de clé privée (.pfx) directement via votre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="1f6c1-170">Cependant, le fournisseur de ressources de calcul Azure exige que les clés soient stockées dans un format JSON (JavaScript Objet Notation) spécial.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="1f6c1-171">Ce format inclut le fichier .pfx sous la forme d’une chaîne encodée en base 64, ainsi que le mot de passe de la clé privée.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="1f6c1-172">Pour répondre à ces exigences, les clés doivent être placées dans une chaîne JSON, puis stockées en tant que « secrets » dans le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="1f6c1-173">Un module PowerShell [disponible sur GitHub][service-fabric-rp-helpers] facilite ce processus.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="1f6c1-174">Pour utiliser ce module, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="1f6c1-175">Téléchargez le contenu complet du référentiel dans un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="1f6c1-176">Accédez au répertoire local.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-176">Go to the local directory.</span></span>
2. <span data-ttu-id="1f6c1-177">Importez le module ServiceFabricRPHelpers dans votre fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="1f6c1-178">La commande `Invoke-AddCertToKeyVault` dans ce module PowerShell met automatiquement en forme une clé privée de certificat dans une chaîne JSON et la charge dans le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="1f6c1-179">Utilisez cette commande pour ajouter le certificat de cluster et tous les certificats d’application supplémentaires dans le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="1f6c1-180">Répétez simplement cette étape pour tous les certificats supplémentaires à installer sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="1f6c1-181">Chargement d’un certificat existant</span><span class="sxs-lookup"><span data-stu-id="1f6c1-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="1f6c1-182">Si vous obtenez une erreur, comme celle illustrée ici, cela signifie généralement qu’il existe un conflit d’URL de ressource.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="1f6c1-183">Pour résoudre ce conflit, modifiez le nom du Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="1f6c1-184">Une fois le conflit résolu, la sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="1f6c1-185">Vous avez besoin des trois chaînes précédentes (CertificateThumbprint, SourceVault et CertificateURL) pour configurer un cluster Service Fabric sécurisé et obtenir les certificats d’application que vous utilisez peut-être pour la sécurité des applications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="1f6c1-186">Si vous n’enregistrez pas ces chaînes, il peut s’avérer difficile de les récupérer ultérieurement en interrogeant le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="1f6c1-187">Création d’un certificat auto-signé et chargement de ce certificat dans le Key Vault</span><span class="sxs-lookup"><span data-stu-id="1f6c1-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="1f6c1-188">Si vous avez déjà chargé vos certificats dans le Key Vault, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="1f6c1-189">Cette étape concerne la génération d’un nouveau certificat auto-signé et son chargement dans votre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="1f6c1-190">Après avoir modifié les paramètres dans le script suivant et exécuté ce dernier, vous devriez être invité à fournir un mot de passe de certificat.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="1f6c1-191">Si vous obtenez une erreur, comme celle illustrée ici, cela signifie généralement qu’il existe un conflit d’URL de ressource.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="1f6c1-192">Pour résoudre ce conflit, modifiez le nom du Key Vault, le nom du groupe de ressources et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="1f6c1-193">Une fois le conflit résolu, la sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="1f6c1-194">Vous avez besoin des trois chaînes précédentes (CertificateThumbprint, SourceVault et CertificateURL) pour configurer un cluster Service Fabric sécurisé et obtenir les certificats d’application que vous utilisez peut-être pour la sécurité des applications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="1f6c1-195">Si vous n’enregistrez pas ces chaînes, il peut s’avérer difficile de les récupérer ultérieurement en interrogeant le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="1f6c1-196">À ce stade, vous devriez avoir les éléments suivants en place :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="1f6c1-197">Le groupe de ressources du Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-197">The key vault resource group.</span></span>
* <span data-ttu-id="1f6c1-198">Le Key Vault (appelé SourceVault dans la sorite PowerShell précédente) et son URL.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="1f6c1-199">Le certificat d’authentification du serveur de cluster et son URL dans le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="1f6c1-200">Les certificats d’application et leurs URL dans le Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="1f6c1-201">Configuration d’Azure Active Directory pour l’authentification des clients</span><span class="sxs-lookup"><span data-stu-id="1f6c1-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="1f6c1-202">Azure AD permet aux organisation (appelées locataires) de gérer l’accès utilisateur aux applications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="1f6c1-203">Ces dernières se composent d’applications avec une interface utilisateur de connexion web et d’applications avec une expérience client natif.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="1f6c1-204">Dans cet article, nous partons du principe que vous avez déjà créé un locataire.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="1f6c1-205">Si ce n’est pas le cas, commencez par lire [Obtention d’un client Azure Active Directory][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="1f6c1-206">Un cluster Service Fabric offre différents points d’entrée pour leurs fonctionnalités de gestion, notamment les outils [Service Fabric Explorer][service-fabric-visualizing-your-cluster] et [Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="1f6c1-207">Par conséquent, vous allez créer deux applications Azure AD pour contrôler l’accès au cluster : une application web et une application native.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="1f6c1-208">Pour simplifier certaines des étapes impliquées dans la configuration d’Azure AD avec un cluster Service Fabric, nous avons créé un ensemble de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="1f6c1-209">Vous devez exécuter les étapes suivantes avant de créer le cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="1f6c1-210">Étant donné que les scripts attendent des noms de cluster et des points de terminaison, ces valeurs doivent être des valeurs planifiées et non celles que vous avez déjà créées.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="1f6c1-211">[Téléchargez les scripts][sf-aad-ps-script-download] sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="1f6c1-212">Cliquez avec le bouton sur le fichier zip, sélectionnez **Propriétés**, activez la case à cocher **Débloquer**, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="1f6c1-213">Extrayez le fichier zip.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-213">Extract the zip file.</span></span>
4. <span data-ttu-id="1f6c1-214">Exécutez `SetupApplications.ps1` et indiquez les valeurs de TenantId, ClusterName et WebApplicationReplyUrl en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="1f6c1-215">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="1f6c1-216">Vous pouvez trouver votre TenantId en exécutant la commande PowerShell `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="1f6c1-217">L’exécution de cette commande permet d’afficher le TenantId de chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="1f6c1-218">Le paramètre ClusterName est utilisé pour préfixer les applications Azure AD créées par le script.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="1f6c1-219">Il ne doit pas forcément correspondre précisément au nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="1f6c1-220">Il sert uniquement à simplifier le mappage des artefacts Azure AD au cluster Service Fabric avec lequel ils sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="1f6c1-221">Le paramètre WebApplicationReplyUrl est le point de terminaison par défaut renvoyé par Azure AD aux utilisateurs une fois qu’ils se sont connectés.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="1f6c1-222">Définissez ce point de terminaison en tant que point de terminaison Service Fabric Explorer pour votre cluster, qui est par défaut :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="1f6c1-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="1f6c1-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="1f6c1-224">Vous êtes invité à vous connecter à un compte qui dispose de privilèges d’administration pour le locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="1f6c1-225">Une fois que vous vous êtes connecté, le script crée les applications web et native pour représenter votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="1f6c1-226">Si vous examinez les applications du client dans le [Portail Azure Classic][azure-classic-portal], vous devez voir deux nouvelles entrées :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="1f6c1-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="1f6c1-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="1f6c1-228">*ClusterName*\_Client</span><span class="sxs-lookup"><span data-stu-id="1f6c1-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="1f6c1-229">Comme le script imprime le JSON exigé par le modèle Azure Resource Manager lorsque vous créez le cluster (dans la section suivante), il est judicieux de garder la fenêtre PowerShell ouverte.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="1f6c1-230">Création d’un modèle Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="1f6c1-231">Dans cette section, les sorties des commandes PowerShell précédentes sont utilisées dans un modèle Resource Manager de cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="1f6c1-232">Des exemples de modèles Resource Manager sont disponibles dans [la galerie de modèles de démarrage rapide Azure sur GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="1f6c1-233">Ces modèles peuvent être utilisés comme point de départ pour votre modèle de cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="1f6c1-234">Créer le modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-234">Create the Resource Manager template</span></span>
<span data-ttu-id="1f6c1-235">Ce guide utilise l’exemple de modèle [cluster sécurisé à 5 nœuds][service-fabric-secure-cluster-5-node-1-nodetype] et ses paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="1f6c1-236">Téléchargez `azuredeploy.json` et `azuredeploy.parameters.json` sur votre ordinateur et ouvrez les deux fichiers dans votre éditeur de texte préféré.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="1f6c1-237">Ajout de certificats</span><span class="sxs-lookup"><span data-stu-id="1f6c1-237">Add certificates</span></span>
<span data-ttu-id="1f6c1-238">Pour ajouter les certificats à un modèle Resource Manager de cluster, vous devez référencer le Key Vault qui contient les clés de certificat.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="1f6c1-239">Nous vous recommandons de placer les valeurs de Key Vault dans un fichier de paramètres de modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="1f6c1-240">Le fichier de modèle Resource Manager sera ainsi réutilisable et exempt de valeurs propres à un déploiement.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="1f6c1-241">Ajouter tous les certificats à l’osProfile du groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="1f6c1-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="1f6c1-242">Chaque certificat qui est installé dans le cluster doit être configuré dans la section osProfile de la ressource des groupes identiques (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="1f6c1-243">Cela permet d’indiquer au fournisseur de ressources d’installer le certificat sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="1f6c1-244">Cette installation inclut le certificat de cluster et tous les certificats de sécurité d’application que vous projetez d’utiliser pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="1f6c1-245">Configurer le certificat de cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1f6c1-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="1f6c1-246">Le certificat d’authentification de cluster doit être configuré à la fois dans la ressource de cluster Service Fabric (Microsoft.ServiceFabric/clusters) et dans l’extension de Service Fabric pour les groupes de machines virtuelles identiques dans la ressource associée à ces derniers.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="1f6c1-247">Cette disposition permet au fournisseur de ressources de Service Fabric de configurer le certificat pour l’authentification du cluster et l’authentification du serveur pour les points de terminaison de gestion.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="1f6c1-248">Ressource des groupes de machines virtuelles identiques :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="1f6c1-249">Ressource Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="1f6c1-250">Insérer la configuration Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f6c1-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="1f6c1-251">La configuration Azure AD que vous avez créée précédemment peut être insérée directement dans votre modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="1f6c1-252">Cependant, nous vous recommandons d’extraire d’abord les valeurs dans un fichier de paramètres pour que le modèle Resource Manager soit réutilisable et exempt de valeurs propres à un déploiement.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="1f6c1-253"><a "configure-arm" ></a>Configuration des paramètres de modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="1f6c1-254">Enfin, utilisez les valeurs de sortie des commandes PowerShell Azure AD et du Key Vault pour renseigner le fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="1f6c1-255">À ce stade, vous devriez avoir les éléments suivants en place :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="1f6c1-256">Groupe de ressources du Key Vault</span><span class="sxs-lookup"><span data-stu-id="1f6c1-256">Key vault resource group</span></span>
  * <span data-ttu-id="1f6c1-257">Coffre de clés</span><span class="sxs-lookup"><span data-stu-id="1f6c1-257">Key vault</span></span>
  * <span data-ttu-id="1f6c1-258">Certificat d’authentification de serveur de clusters</span><span class="sxs-lookup"><span data-stu-id="1f6c1-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="1f6c1-259">Certificat de chiffrement de données</span><span class="sxs-lookup"><span data-stu-id="1f6c1-259">Data encipherment certificate</span></span>
* <span data-ttu-id="1f6c1-260">Locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f6c1-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="1f6c1-261">Application Azure AD pour la gestion basée sur le web et Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1f6c1-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="1f6c1-262">Application Azure AD pour la gestion du client natif</span><span class="sxs-lookup"><span data-stu-id="1f6c1-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="1f6c1-263">Utilisateurs et rôles qui leur sont affectés</span><span class="sxs-lookup"><span data-stu-id="1f6c1-263">Users and their assigned roles</span></span>
* <span data-ttu-id="1f6c1-264">Modèle Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f6c1-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="1f6c1-265">Certificats configurés par le biais du Key Vault</span><span class="sxs-lookup"><span data-stu-id="1f6c1-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="1f6c1-266">Configuration d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f6c1-266">Azure Active Directory configured</span></span>

<span data-ttu-id="1f6c1-267">Le diagramme suivant montre comment votre Key Vault et la configuration Azure AD s’appliquent à votre modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mappage de dépendances de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="1f6c1-269">Création du cluster</span><span class="sxs-lookup"><span data-stu-id="1f6c1-269">Create the cluster</span></span>
<span data-ttu-id="1f6c1-270">Vous êtes maintenant prêt à créer le cluster en [déployant le modèle de ressource Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="1f6c1-271">Testez-le</span><span class="sxs-lookup"><span data-stu-id="1f6c1-271">Test it</span></span>
<span data-ttu-id="1f6c1-272">Pour tester votre modèle Resource Manager avec un fichier de paramètres, utilisez la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="1f6c1-273">Déployez-le</span><span class="sxs-lookup"><span data-stu-id="1f6c1-273">Deploy it</span></span>
<span data-ttu-id="1f6c1-274">Si le test du modèle Resource Manager réussit, utilisez la commande PowerShell suivante pour déployer votre modèle Resource Manager avec un fichier de paramètres  :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="1f6c1-275">Affecter des utilisateurs aux rôles</span><span class="sxs-lookup"><span data-stu-id="1f6c1-275">Assign users to roles</span></span>
<span data-ttu-id="1f6c1-276">Une fois que vous avez créé les applications pour représenter votre cluster, affectez les utilisateurs aux rôles pris en charge par Service Fabric : lecture seule et administrateur. Vous pouvez affecter ces rôles à l’aide du [portail Azure Classic][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="1f6c1-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="1f6c1-277">Dans le portail Azure, accédez à votre locataire, puis sélectionnez **Applications**.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="1f6c1-278">Sélectionnez l’application web, qui porte un nom similaire à `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="1f6c1-279">Cliquez sur l’onglet **Users** .</span><span class="sxs-lookup"><span data-stu-id="1f6c1-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="1f6c1-280">Sélectionnez un utilisateur à affecter, puis cliquez sur le bouton **Affecter** situé en bas de l’écran.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Bouton Assign users to roles (Affecter des utilisateurs aux rôles)][assign-users-to-roles-button]
5. <span data-ttu-id="1f6c1-282">Sélectionnez le rôle à affecter à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-282">Select the role to assign to the user.</span></span>

    ![Boîte de dialogue Affecter des utilisateurs][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="1f6c1-284">Pour plus d’informations sur les rôles dans Service Fabric, consultez [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="1f6c1-285">Créer des clusters sécurisés sur Linux</span><span class="sxs-lookup"><span data-stu-id="1f6c1-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="1f6c1-286">Pour faciliter le processus, nous avons mis à disposition un [script d’assistance](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="1f6c1-287">Avant d’utiliser ce script d’assistance, assurez-vous que l’interface de ligne de commande Azure (CLI) est déjà installée, et qu’il se trouve dans votre chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="1f6c1-288">Vérifiez que le script dispose des autorisations d’exécution en lançant la commande `chmod +x cert_helper.py` après l’avoir téléchargé.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="1f6c1-289">La première étape consiste à se connecter à votre compte Azure à l’aide de l’interface de ligne de commande avec la commande `azure login` .</span><span class="sxs-lookup"><span data-stu-id="1f6c1-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="1f6c1-290">Une fois connecté à votre compte Azure, utilisez le script d’assistance avec votre certificat signé par une autorité de certification, comme l’illustre la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="1f6c1-291">Le paramètre -ifile peut accepter un fichier .pfx ou .pem en entrée avec le type de certificat (pfx ou pem, ou ss s’il s’agit d’un certificat auto-signé).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="1f6c1-292">Le paramètre -h permet d’afficher le texte d’aide.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="1f6c1-293">La sortie de cette commande renvoie les trois chaînes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="1f6c1-294">SourceVaultID, qui correspond à l’ID du nouvel élément KeyVault ResourceGroup créé pour vous ;</span><span class="sxs-lookup"><span data-stu-id="1f6c1-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="1f6c1-295">CertificateUrl pour l’accès au certificat ;</span><span class="sxs-lookup"><span data-stu-id="1f6c1-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="1f6c1-296">CertificateThumbprint, qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="1f6c1-297">L’exemple suivant explique comment utiliser la commande :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="1f6c1-298">L’exécution de la commande précédente génère les trois chaînes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="1f6c1-299">Le nom de sujet du certificat doit correspondre au domaine utilisé pour accéder au cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="1f6c1-300">Cela est nécessaire pour la fourniture d’un certificat SSL pour les points de terminaison de gestion HTTPS du cluster et pour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="1f6c1-301">Vous ne pouvez pas obtenir de certificat SSL auprès d’une autorité de certification pour le domaine `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="1f6c1-302">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="1f6c1-303">Lorsque vous demandez un certificat auprès d’une autorité de certification, le nom de sujet du certificat doit correspondre au nom de domaine personnalisé utilisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="1f6c1-304">Ces noms de sujet sont les entrées dont vous avez besoin pour créer un cluster Service Fabric sécurisé (sans Azure AD), comme décrit dans la section [Configuration des paramètres de modèle Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="1f6c1-305">Vous pouvez vous connecter au cluster sécurisé en suivant les instructions permettant d’[authentifier l’accès client à un cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="1f6c1-306">Les clusters Linux en version préliminaire ne prennent pas en charge l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="1f6c1-307">Vous pouvez affecter des rôles d’administrateur et de client, comme décrit dans la section [Affecter des utilisateurs aux rôles](#assign-roles).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="1f6c1-308">Lorsque vous spécifiez des rôles d’administrateur et de client pour un cluster Linux en version préliminaire, vous devez fournir des empreintes de certificat pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="1f6c1-309">(Vous ne fournissez pas de nom de sujet, car aucune validation ou révocation de chaîne n’est effectuée dans cette version préliminaire.)</span><span class="sxs-lookup"><span data-stu-id="1f6c1-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="1f6c1-310">Si vous souhaitez utiliser un certificat auto-signé à des fins de test, vous pouvez utiliser le même script pour en générer un.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="1f6c1-311">Vous pouvez ensuite charger le certificat dans votre Key Vault en fournissant l’indicateur `ss` au lieu de spécifier le chemin d’accès et le nom du certificat.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="1f6c1-312">Par exemple, consultez la commande suivante pour créer et télécharger un certificat auto-signé :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="1f6c1-313">Cette commande renvoie les trois mêmes chaînes : SourceVault, CertificateUrl et CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="1f6c1-314">Vous pouvez ensuite utiliser les chaînes pour créer un cluster Linux sécurisé et un emplacement pour le certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="1f6c1-315">Vous avez besoin du certificat auto-signé pour vous connecter au cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="1f6c1-316">Vous pouvez vous connecter au cluster sécurisé en suivant les instructions permettant d’[authentifier l’accès client à un cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="1f6c1-317">Le nom de sujet du certificat doit correspondre au domaine utilisé pour accéder au cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="1f6c1-318">Cela est nécessaire pour la fourniture d’un certificat SSL pour les points de terminaison de gestion HTTPS du cluster et pour Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="1f6c1-319">Vous ne pouvez pas obtenir de certificat SSL auprès d’une autorité de certification pour le domaine `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="1f6c1-320">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="1f6c1-321">Lorsque vous demandez un certificat auprès d’une autorité de certification, le nom de sujet du certificat doit correspondre au nom de domaine personnalisé utilisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="1f6c1-322">Vous pouvez renseigner les paramètres fournis par le script d’assistance dans le portail, comme indiqué dans la section [Création d’un cluster dans le portail Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f6c1-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f6c1-323">Next steps</span></span>
<span data-ttu-id="1f6c1-324">À ce stade, vous avez un cluster sécurisé avec l’authentification de gestion fournie par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="1f6c1-325">Ensuite, [connectez-vous à votre cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment [gérer les secrets d’application](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="1f6c1-326">Résoudre les problèmes de configuration d’Azure Active Directory pour l’authentification des clients</span><span class="sxs-lookup"><span data-stu-id="1f6c1-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="1f6c1-327">Si vous rencontrez un problème pendant la configuration d’Azure AD pour l’authentification des clients, examinez les solutions potentielles présentées dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="1f6c1-328">Service Fabric Explorer vous demande de sélectionner un certificat</span><span class="sxs-lookup"><span data-stu-id="1f6c1-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="1f6c1-329">Problème</span><span class="sxs-lookup"><span data-stu-id="1f6c1-329">Problem</span></span>
<span data-ttu-id="1f6c1-330">Une fois que vous vous êtes connecté à Azure AD dans Service Fabric Explorer, le navigateur revient à la page d’accueil, mais un message vous invite à sélectionner un certificat.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![Boîte de dialogue SFX de sélection d’un certificat][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="1f6c1-332">Motif</span><span class="sxs-lookup"><span data-stu-id="1f6c1-332">Reason</span></span>
<span data-ttu-id="1f6c1-333">Aucun rôle n’a été affecté à l’utilisateur dans l’application Azure AD en cluster.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="1f6c1-334">Par conséquent, l’authentification Azure AD échoue sur le cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="1f6c1-335">Service Fabric Explorer revient à l’authentification par certificat.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="1f6c1-336">Solution</span><span class="sxs-lookup"><span data-stu-id="1f6c1-336">Solution</span></span>
<span data-ttu-id="1f6c1-337">Suivez les instructions de configuration d’Azure AD et affectez des rôles utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="1f6c1-338">Nous vous recommandons également d’activer l’option Affectation de l’utilisateur requise pour accéder à l’application, comme le fait `SetupApplications.ps1`.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="1f6c1-339">La connexion avec PowerShell échoue avec un message d’erreur : « Les informations d’identification spécifiées ne sont pas valides »</span><span class="sxs-lookup"><span data-stu-id="1f6c1-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="1f6c1-340">Problème</span><span class="sxs-lookup"><span data-stu-id="1f6c1-340">Problem</span></span>
<span data-ttu-id="1f6c1-341">Lorsque vous utilisez PowerShell pour vous connecter au cluster à l’aide du mode de sécurité « AzureActiveDirectory », une fois que vous vous êtes connecté à Azure AD, la connexion échoue avec un message d’erreur : « Les informations d’identification spécifiées ne sont pas valides. »</span><span class="sxs-lookup"><span data-stu-id="1f6c1-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="1f6c1-342">Solution</span><span class="sxs-lookup"><span data-stu-id="1f6c1-342">Solution</span></span>
<span data-ttu-id="1f6c1-343">La solution est la même que pour le problème précédent.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="1f6c1-344">Lorsque vous vous connectez, Service Fabric Explorer renvoie un message d’échec : « AADSTS50011 »</span><span class="sxs-lookup"><span data-stu-id="1f6c1-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="1f6c1-345">Problème</span><span class="sxs-lookup"><span data-stu-id="1f6c1-345">Problem</span></span>
<span data-ttu-id="1f6c1-346">Lorsque vous essayez de vous connecter à Azure AD dans Service Fabric Explorer, la page renvoie un message d’échec : « AADSTS50011 : l’adresse de réponse &lt;url&gt; ne correspond pas aux adresses de réponse configurées pour l’application : &lt;guid&gt;. »</span><span class="sxs-lookup"><span data-stu-id="1f6c1-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![L’adresse de réponse SFX ne correspond pas][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="1f6c1-348">Motif</span><span class="sxs-lookup"><span data-stu-id="1f6c1-348">Reason</span></span>
<span data-ttu-id="1f6c1-349">L’application en cluster (web) représentant Service Fabric Explorer tente de s’authentifier auprès d’Azure AD. Dans le cadre de cette demande, elle fournit l’URL de redirection.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="1f6c1-350">Cette dernière ne figure cependant pas dans la liste **URL DE RÉPONSE** de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="1f6c1-351">Solution</span><span class="sxs-lookup"><span data-stu-id="1f6c1-351">Solution</span></span>
<span data-ttu-id="1f6c1-352">Dans l’onglet **Configurer** de l’application en cluster (web), ajoutez l’URL de Service Fabric Explorer à la liste **URL de réponse** ou remplacez l’un des éléments de la liste.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="1f6c1-353">Lorsque vous avez terminé, enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-353">When you have finished, save your change.</span></span>

![URL de réponse d’application web][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="1f6c1-355">Connecter le cluster à l’aide de l’authentification Azure AD via PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f6c1-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="1f6c1-356">Pour connecter le cluster Service Fabric, utilisez l’exemple de commande PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="1f6c1-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="1f6c1-357">Pour en savoir plus sur l’applet de commande Connect-ServiceFabricCluster, consultez [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="1f6c1-358">Puis-je utiliser le même locataire Azure AD pour plusieurs clusters ?</span><span class="sxs-lookup"><span data-stu-id="1f6c1-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="1f6c1-359"> Oui.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-359">Yes.</span></span> <span data-ttu-id="1f6c1-360">Cependant, n’oubliez pas d’ajouter l’URL de Service Fabric Explorer à votre application en cluster (web).</span><span class="sxs-lookup"><span data-stu-id="1f6c1-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="1f6c1-361">Si vous ne le faites pas, Service Fabric Explorer ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="1f6c1-362">Pourquoi dois-je disposer d’un certificat de serveur lorsqu’Azure AD est activé ?</span><span class="sxs-lookup"><span data-stu-id="1f6c1-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="1f6c1-363">FabricClient et FabricGateway effectuent une authentification mutuelle.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="1f6c1-364">Pendant l’authentification Azure AD, l’intégration Azure AD fournit une identité de client au serveur et le certificat de serveur est utilisé pour vérifier l’identité du serveur.</span><span class="sxs-lookup"><span data-stu-id="1f6c1-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="1f6c1-365">Pour plus d’informations sur les certificats Service Fabric, consultez [Certificats X.509 et Service Fabric][x509-certificates-and-service-fabric]</span><span class="sxs-lookup"><span data-stu-id="1f6c1-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

