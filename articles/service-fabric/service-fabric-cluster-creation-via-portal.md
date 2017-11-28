---
title: "aaaCreate l’infrastructure de Service de cluster Bonjour portail Azure | Documents Microsoft"
description: "Cet article décrit comment tooset configuration d’un cluster Service Fabric sécurisé à l’aide d’Azure hello portail Azure et Azure Key Vault."
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
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="d91d3-103">Créer un cluster Service Fabric dans Azure à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d91d3-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d91d3-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d91d3-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="d91d3-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d91d3-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="d91d3-106">Il s’agit d’un guide pas à pas qui vous guide tout au long des étapes de hello de configuration d’un cluster Service Fabric sécurisé dans Azure à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d91d3-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="d91d3-107">Ce guide vous guide tout au long de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d91d3-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="d91d3-108">Configurer les clés de toomanage de coffre de clés pour la sécurité du cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="d91d3-109">Créez un cluster sécurisé dans Azure via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d91d3-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="d91d3-110">authentification d’administrateurs à l’aide de certificat.</span><span class="sxs-lookup"><span data-stu-id="d91d3-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="d91d3-111">Pour accéder à des options de sécurité plus avancées, telles que l’authentification des utilisateurs avec Azure Active Directory et la configuration de certificats pour la sécurité des applications, [créez votre cluster à l’aide d’Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d91d3-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="d91d3-112">Un cluster sécurisé est un cluster qui empêche les opérations de toomanagement tout accès non autorisé, qui inclut le déploiement, la mise à niveau et la suppression des applications, services et données hello qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="d91d3-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="d91d3-113">Un cluster non sécurisé est un cluster que toute personne peut se connecter tooat à tout moment et effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="d91d3-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="d91d3-114">Bien qu’il soit possible de toocreate un cluster non sécurisé, il est **hautement recommandé toocreate un cluster sécurisé**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="d91d3-115">Un cluster non sécurisé **ne peut pas être sécurisé ultérieurement** , ce qui implique la création d’un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="d91d3-116">concepts de Hello sont hello même pour la création de clusters sécurisés, si les clusters hello sont des clusters Linux ou des clusters Windows.</span><span class="sxs-lookup"><span data-stu-id="d91d3-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="d91d3-117">Pour en savoir plus et pour accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="d91d3-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="d91d3-118">Hello paramètres obtenus par le script du programme d’assistance hello fourni peuvent être entrés directement dans le portail de hello comme décrit dans la section de hello [créer un cluster Bonjour Azure portal](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="d91d3-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="d91d3-119">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="d91d3-119">Log in tooAzure</span></span>
<span data-ttu-id="d91d3-120">Ce guide utilise [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="d91d3-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="d91d3-121">Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous tooyour compte Azure et sélectionnez votre abonnement avant l’exécution de commandes Azure.</span><span class="sxs-lookup"><span data-stu-id="d91d3-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="d91d3-122">Ouvrez une session dans le compte de tooyour azure :</span><span class="sxs-lookup"><span data-stu-id="d91d3-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d91d3-123">Sélectionnez votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="d91d3-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="d91d3-124">Configuration d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d91d3-124">Set up Key Vault</span></span>
<span data-ttu-id="d91d3-125">Cette partie du guide de hello vous guide tout au long de la création d’un coffre de clés pour un cluster Service Fabric dans Azure et les applications de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d91d3-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="d91d3-126">Pour obtenir un guide complet sur le coffre de clés, consultez hello [le coffre de clés mise en route][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="d91d3-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="d91d3-127">Service Fabric utilise toosecure de certificats X.509 un cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="d91d3-128">Coffre de clés Azure est toomanage utilisé des certificats pour les clusters Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d91d3-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="d91d3-129">Lorsqu’un cluster est déployé dans Azure, le fournisseur de ressources Azure hello chargé de créer des clusters Service Fabric extrait les certificats de coffre de clés et les installe sur les machines virtuelles du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="d91d3-130">Hello diagramme suivant illustre les relations hello entre le coffre de clés, un cluster Service Fabric et le fournisseur de ressources Azure hello qui utilise les certificats stockés dans le coffre de clés lorsqu’il crée un cluster :</span><span class="sxs-lookup"><span data-stu-id="d91d3-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="d91d3-132">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d91d3-132">Create a Resource Group</span></span>
<span data-ttu-id="d91d3-133">première étape de Hello est toocreate un nouveau groupe de ressources spécifiquement pour le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d91d3-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="d91d3-134">Placement de coffre de clés dans son propre groupe de ressources est recommandé afin que vous pouvez supprimer des groupes de ressources de calcul et de stockage - telles que le groupe de ressources hello qui a votre cluster Service Fabric - sans perdre vos clés et les clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="d91d3-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="d91d3-135">groupe de ressources Hello a votre coffre de clés doit être Bonjour même région que le cluster hello qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="d91d3-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="d91d3-136">Création d'un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d91d3-136">Create Key Vault</span></span>
<span data-ttu-id="d91d3-137">Créer un coffre de clés dans le nouveau groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="d91d3-138">Hello coffre de clés **doit être activée pour le déploiement** tooallow hello certificats de tooget de fournisseur de ressources de l’infrastructure de Service à partir de celui-ci et l’installer sur les nœuds de cluster :</span><span class="sxs-lookup"><span data-stu-id="d91d3-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

<span data-ttu-id="d91d3-139">Si vous avez un coffre de clés existant, vous pouvez l’activer pour le déploiement à l’aide de l’interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="d91d3-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="d91d3-140">Ajouter des certificats tooKey coffre</span><span class="sxs-lookup"><span data-stu-id="d91d3-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="d91d3-141">Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications.</span><span class="sxs-lookup"><span data-stu-id="d91d3-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="d91d3-142">Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="d91d3-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="d91d3-143">Certificat de cluster et de serveur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="d91d3-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="d91d3-144">Ce certificat est requis toosecure un cluster et empêcher tout accès non autorisé tooit.</span><span class="sxs-lookup"><span data-stu-id="d91d3-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="d91d3-145">Il assure la sécurité du cluster de différentes manières :</span><span class="sxs-lookup"><span data-stu-id="d91d3-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="d91d3-146">**Authentification du cluster :** authentifie la communication nœud à nœud pour la fédération du cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="d91d3-147">Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajouté hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="d91d3-148">**L’authentification du serveur :** authentifie hello gestion des points de terminaison tooa gestion client de cluster, afin que hello gestion client sait qu’il communique avec le véritable toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="d91d3-149">Ce certificat fournit également SSL pour hello API de gestion HTTPS et pour le Service Fabric Explorer via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d91d3-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="d91d3-150">tooserve ces fins, les certificats de hello doit respecter hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="d91d3-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="d91d3-151">certificat de Hello doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="d91d3-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="d91d3-152">certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).</span><span class="sxs-lookup"><span data-stu-id="d91d3-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d91d3-153">Hello nom du sujet du certificat doit correspondre au cluster Service Fabric de hello domaine utilisé tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="d91d3-154">Cela est requis tooprovide SSL pour la gestion de points de terminaison HTTPS et le Service Fabric Explorer du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d91d3-155">Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification (CA) pour hello `.cloudapp.azure.com` domaine.</span><span class="sxs-lookup"><span data-stu-id="d91d3-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d91d3-156">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="d91d3-157">Lorsque vous demandez un certificat à partir du nom du sujet du certificat de hello une autorité de certification doit correspondre au nom de domaine personnalisé hello utilisée pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="d91d3-158">Authentification de certificat client</span><span class="sxs-lookup"><span data-stu-id="d91d3-158">Client authentication certificates</span></span>
<span data-ttu-id="d91d3-159">Les certificats client supplémentaires authentifient les administrateurs pour les tâches de gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="d91d3-160">Service Fabric dispose de deux niveaux d’accès : **admin** et **read-only user**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="d91d3-161">Au minimum, un seul certificat pour un accès administrateur doit être utilisé.</span><span class="sxs-lookup"><span data-stu-id="d91d3-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="d91d3-162">Pour un accès de niveau utilisateur supplémentaire, un certificat distinct doit être fourni.</span><span class="sxs-lookup"><span data-stu-id="d91d3-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="d91d3-163">Pour en savoir plus sur les rôles d’accès, consultez la page [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="d91d3-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="d91d3-164">Vous n’avez pas besoin de coffre tooupload Client d’authentification des certificats tooKey toowork avec Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d91d3-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="d91d3-165">Ces certificats doivent uniquement toobe fourni toousers qui sont autorisés pour la gestion de cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="d91d3-166">Azure Active Directory est hello recommandé clients tooauthenticate de façon pour cluster des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="d91d3-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="d91d3-167">toouse Azure Active Directory, vous devez [créer un cluster à l’aide du Gestionnaire de ressources Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d91d3-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="d91d3-168">Certificats d’application (facultatif)</span><span class="sxs-lookup"><span data-stu-id="d91d3-168">Application certificates (optional)</span></span>
<span data-ttu-id="d91d3-169">Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application.</span><span class="sxs-lookup"><span data-stu-id="d91d3-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="d91d3-170">Avant de créer votre cluster, tenez compte des scénarios de sécurité hello qui nécessitent un toobe certificat installé sur les nœuds de hello, tel que :</span><span class="sxs-lookup"><span data-stu-id="d91d3-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="d91d3-171">Le chiffrement et déchiffrement de valeurs de configuration d’applications.</span><span class="sxs-lookup"><span data-stu-id="d91d3-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="d91d3-172">Le chiffrement des données sur les nœuds lors de la réplication.</span><span class="sxs-lookup"><span data-stu-id="d91d3-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="d91d3-173">Certificats d’application ne peut pas être configurés lors de la création d’un cluster via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d91d3-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="d91d3-174">certificats d’application tooconfigure au moment le programme d’installation de cluster, vous devez [créer un cluster à l’aide du Gestionnaire de ressources Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="d91d3-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="d91d3-175">Vous pouvez également ajouter le cluster de toohello certificats application après que qu’elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="d91d3-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="d91d3-176">Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="d91d3-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="d91d3-177">Des fichiers de clé privée (.pfx) peuvent être ajoutés et utilisés directement par le biais de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d91d3-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="d91d3-178">Toutefois, le fournisseur de ressources Azure hello nécessite toobe clés stockée dans un format JSON spécial qui inclut .pfx hello comme base-64 codé en chaîne et hello privée clé mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d91d3-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="d91d3-179">tooaccommodate ces exigences, les clés doivent être placés dans une chaîne JSON et ensuite stockées en tant que *secrets* dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d91d3-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="d91d3-180">est de toomake ce processus plus simple, un module PowerShell [disponible sur GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="d91d3-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="d91d3-181">Suivez ces module hello de toouse comme suit :</span><span class="sxs-lookup"><span data-stu-id="d91d3-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="d91d3-182">Téléchargez hello intégralité du contenu du référentiel de hello dans un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="d91d3-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="d91d3-183">Importez le module hello dans la fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="d91d3-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="d91d3-184">Hello `Invoke-AddCertToKeyVault` commande dans ce module PowerShell met en forme une clé privée du certificat en une chaîne JSON et télécharge automatiquement les il tooKey coffre.</span><span class="sxs-lookup"><span data-stu-id="d91d3-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="d91d3-185">Utiliser certificat de cluster tooadd hello et n’importe quel tooKey de certificats d’application supplémentaires coffre.</span><span class="sxs-lookup"><span data-stu-id="d91d3-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="d91d3-186">Répétez cette étape pour tous les certificats supplémentaires que vous souhaitez tooinstall dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="d91d3-187">Il s’agit de toutes les conditions préalables requises de coffre de clés hello pour la configuration d’un modèle de gestionnaire de ressources de cluster Service Fabric qui installe les certificats pour l’authentification de nœud, sécurité de point de terminaison de gestion et d’authentification et toute sécurité des applications supplémentaires fonctionnalités qui utilisent des certificats X.509.</span><span class="sxs-lookup"><span data-stu-id="d91d3-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="d91d3-188">À ce stade, vous devez maintenant avoir hello après l’installation dans Azure :</span><span class="sxs-lookup"><span data-stu-id="d91d3-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="d91d3-189">Groupe de ressources Key Vault</span><span class="sxs-lookup"><span data-stu-id="d91d3-189">Key Vault resource group</span></span>
  * <span data-ttu-id="d91d3-190">Key Vault</span><span class="sxs-lookup"><span data-stu-id="d91d3-190">Key Vault</span></span>
    * <span data-ttu-id="d91d3-191">Certificat d’authentification de serveur de clusters</span><span class="sxs-lookup"><span data-stu-id="d91d3-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="d91d3-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="d91d3-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="d91d3-193">Créer un cluster Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="d91d3-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="d91d3-194">Rechercher des ressources de cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d91d3-194">Search for hello Service Fabric cluster resource</span></span>
![Recherchez le modèle de cluster Service Fabric sur hello portail Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="d91d3-196">Connectez-vous à toohello [portail Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="d91d3-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="d91d3-197">Cliquez sur **nouveau** tooadd un nouveau modèle de ressource.</span><span class="sxs-lookup"><span data-stu-id="d91d3-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="d91d3-198">Recherchez le modèle de Cluster Service Fabric hello Bonjour **Marketplace** sous **tout**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="d91d3-199">Sélectionnez **Cluster Service Fabric** à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="d91d3-200">Accédez toohello **Cluster Service Fabric** panneau, cliquez sur **créer**,</span><span class="sxs-lookup"><span data-stu-id="d91d3-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="d91d3-201">Hello **cluster créer Service Fabric** panneau a hello suivant quatre étapes.</span><span class="sxs-lookup"><span data-stu-id="d91d3-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="d91d3-202">1. Concepts de base</span><span class="sxs-lookup"><span data-stu-id="d91d3-202">1. Basics</span></span>
![Capture d’écran de la création d’un groupe de ressources.][CreateRG]

<span data-ttu-id="d91d3-204">Dans le panneau des principes de base hello, vous devez les détails de base de hello tooprovide pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="d91d3-205">Entrez le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="d91d3-206">Entrez un **nom d’utilisateur** et **mot de passe** Bureau à distance pour hello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d91d3-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="d91d3-207">Assurez-vous que tooselect hello **abonnement** que vous souhaitez votre toobe cluster déployé, surtout si vous avez plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="d91d3-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="d91d3-208">Créez un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-208">Create a **new resource group**.</span></span> <span data-ttu-id="d91d3-209">Il s’agit des meilleures toogive il hello même nom que le cluster de hello, dans la mesure où il vous aide à trouver une version ultérieure, en particulier lorsque vous essayez toomake modifications tooyour déploiement ou de supprimer votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d91d3-210">Vous pouvez décider toouse un groupe de ressources existant, mais il est une bonne approche en matière de toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d91d3-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="d91d3-211">Il est ainsi facile toodelete clusters que vous n’avez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="d91d3-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="d91d3-212">Sélectionnez hello **région** dans lequel vous souhaitez le cluster de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d91d3-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="d91d3-213">Vous devez utiliser hello même région que votre clé de coffre est dans.</span><span class="sxs-lookup"><span data-stu-id="d91d3-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="d91d3-214">2. Configuration de clusters</span><span class="sxs-lookup"><span data-stu-id="d91d3-214">2. Cluster configuration</span></span>
![Création d’un type de nœud][CreateNodeType]

<span data-ttu-id="d91d3-216">Configurez vos nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-216">Configure your cluster nodes.</span></span> <span data-ttu-id="d91d3-217">Les types de nœud définissent les tailles de machine virtuelle hello, hello nombre de machines virtuelles et leurs propriétés.</span><span class="sxs-lookup"><span data-stu-id="d91d3-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="d91d3-218">Votre cluster peut avoir plus d’un type de nœud, mais type de nœud principal hello (hello un premier que vous définissez sur le portail hello) doit avoir au moins cinq de machines virtuelles, car il s’agit de type de nœud hello où sont placés les services de système de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d91d3-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="d91d3-219">Ne configurez pas la zone **Propriétés de sélection élective** , car une propriété de sélection élective par défaut de « NodeTypeName » est ajoutée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d91d3-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="d91d3-220">Un scénario répandu si vous avez plusieurs types de nœuds est une application qui contient un service front-end et un service back-end.</span><span class="sxs-lookup"><span data-stu-id="d91d3-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="d91d3-221">Vous souhaitez que service frontal de hello tooput sur des machines virtuelles la plus petites (tailles de machine virtuelle comme D2) avec toohello ouvrir de ports Internet, mais vous service de serveur principal tooput hello sur des machines virtuelles plus volumineux (avec des tailles de machine virtuelle, D4, D6, D15 et ainsi de suite) sans ouvrir de ports exposés à Internet.</span><span class="sxs-lookup"><span data-stu-id="d91d3-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="d91d3-222">Choisissez un nom pour votre type de nœud (1 too12 caractères contenant uniquement des lettres et chiffres).</span><span class="sxs-lookup"><span data-stu-id="d91d3-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="d91d3-223">Hello minimale **taille** de machines virtuelles de nœud principal de hello type est piloté par hello **durabilité** couche que vous choisissez pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="d91d3-224">valeur par défaut de Hello pour le niveau de durabilité hello est bronze.</span><span class="sxs-lookup"><span data-stu-id="d91d3-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="d91d3-225">Pour plus d’informations sur la durabilité, consultez [comment toochoose hello l’infrastructure de Service de cluster la fiabilité et durabilité][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="d91d3-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="d91d3-226">Sélectionnez la taille de machine virtuelle hello et le niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="d91d3-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="d91d3-227">Les machines virtuelles de série D ont des lecteurs de disques SSD et sont vivement recommandées pour les applications avec état.</span><span class="sxs-lookup"><span data-stu-id="d91d3-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="d91d3-228">N’utilisez pas les références de machine virtuelle incluant des cœurs partiels ou présentant une capacité de disque disponible inférieure à 7 Go.</span><span class="sxs-lookup"><span data-stu-id="d91d3-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="d91d3-229">Hello minimale **nombre** de machines virtuelles de nœud principal de hello type est piloté par hello **fiabilité** couche que vous choisissez.</span><span class="sxs-lookup"><span data-stu-id="d91d3-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="d91d3-230">valeur par défaut de Hello pour le niveau de fiabilité hello est argent.</span><span class="sxs-lookup"><span data-stu-id="d91d3-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="d91d3-231">Pour plus d’informations sur la fiabilité, consultez [comment toochoose hello l’infrastructure de Service de cluster la fiabilité et durabilité][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="d91d3-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="d91d3-232">Choisissez un nombre hello d’ordinateurs virtuels pour le type de nœud hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="d91d3-233">Vous pouvez augmenter ou diminuer nombre hello d’ordinateurs virtuels dans un type de nœud, ultérieurement, mais sur le type de nœud principal hello, hello minimale est pilotée par niveau de fiabilité hello que vous avez choisi.</span><span class="sxs-lookup"><span data-stu-id="d91d3-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="d91d3-234">Les autres types de nœud peuvent avoir au moins 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d91d3-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="d91d3-235">Configurez des points de terminaison personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d91d3-235">Configure custom endpoints.</span></span> <span data-ttu-id="d91d3-236">Ce champ vous permet de tooenter une liste séparée par des virgules des ports que vous souhaitez tooexpose via toohello d’équilibrage de charge Azure hello Internet public pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="d91d3-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="d91d3-237">Par exemple, si vous envisagez de toodeploy un cluster tooyour d’application web, entrez « 80 » ici trafic tooallow sur le port 80 dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="d91d3-238">Pour en savoir plus sur les points de terminaison, consultez la page [Communiquer avec des applications][service-fabric-connect-and-communicate-with-services].</span><span class="sxs-lookup"><span data-stu-id="d91d3-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="d91d3-239">Configurez les **diagnostics**du cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="d91d3-240">Par défaut, les diagnostics sont activés sur votre tooassist cluster avec la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="d91d3-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="d91d3-241">Si vous souhaitez que les diagnostics de toodisable modifier hello **état** basculer trop**hors**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="d91d3-242">Nous vous recommandons de **ne pas** désactiver les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d91d3-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="d91d3-243">Sélectionnez hello mode que vous souhaitez que votre cluster de la valeur mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="d91d3-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="d91d3-244">Sélectionnez **automatique**, si vous souhaitez hello système tooautomatically récupère hello version la plus récente et que vous essayez de tooupgrade tooit de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="d91d3-245">Définir le mode hello trop**manuel**, si vous souhaitez toochoose une version prise en charge.</span><span class="sxs-lookup"><span data-stu-id="d91d3-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="d91d3-246">Nous prenons uniquement en charge les clusters qui exécutent des versions prises en charge de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d91d3-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="d91d3-247">En sélectionnant hello **manuel** mode, vous tirez sur hello responsabilité tooupgrade version tooa pris en charge de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="d91d3-248">Pour plus d’informations sur le mode de mise à niveau de Fabric hello consultez hello [document de service fabric-cluster-mise à niveau.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="d91d3-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="d91d3-249">3. Sécurité</span><span class="sxs-lookup"><span data-stu-id="d91d3-249">3. Security</span></span>
![Capture d’écran des configurations de sécurité sur le portail Azure.][SecurityConfigs]

<span data-ttu-id="d91d3-251">étape finale de Hello est cluster hello tooprovide certificat informations toosecure à l’aide de hello coffre de clés et certificats informations créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d91d3-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="d91d3-252">Remplir les champs de certificat principal hello avec sortie hello obtenu à partir de téléchargement hello **certificat de cluster** à l’aide du coffre tooKey hello `Invoke-AddCertToKeyVault` commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d91d3-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="d91d3-253">Vérifiez hello **configurer des paramètres avancés** zone tooenter les certificats clients pour **administrateur client** et **client en lecture seule**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="d91d3-254">Dans ces champs, entrez l’empreinte numérique hello de votre certificat de client d’administration et l’empreinte numérique hello de votre certificat client utilisateur en lecture seule, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="d91d3-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="d91d3-255">Lorsque les administrateurs tentent tooconnect toohello cluster, elles sont accordées accès uniquement si elles ont un certificat avec une empreinte numérique qui correspond aux valeurs de l’empreinte numérique hello entré ici.</span><span class="sxs-lookup"><span data-stu-id="d91d3-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="d91d3-256">4. Résumé</span><span class="sxs-lookup"><span data-stu-id="d91d3-256">4. Summary</span></span>
![<span data-ttu-id="d91d3-257">Capture d’écran du tableau de démarrage hello affichage « Déploiement de Service Fabric Cluster ».</span><span class="sxs-lookup"><span data-stu-id="d91d3-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="d91d3-258">la création du cluster toocomplete hello, cliquez sur **Résumé** des configurations de hello toosee que vous avez fournies, ou téléchargez hello modèle Azure Resource Manager que qui utilisé toodeploy votre cluster.</span><span class="sxs-lookup"><span data-stu-id="d91d3-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="d91d3-259">Après avoir fourni les paramètres obligatoires hello, hello **OK** bouton devienne vert, et vous pouvez démarrer le processus de création de cluster hello en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="d91d3-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="d91d3-260">Vous pouvez voir la progression de la création de hello dans les notifications de hello.</span><span class="sxs-lookup"><span data-stu-id="d91d3-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="d91d3-261">(Cliquez sur l’icône de hello « cloche » près de barre d’état hello au niveau supérieur de hello à droite de votre écran.) Si vous avez cliqué sur **code confidentiel tooStartboard** lors de la création de cluster de hello, vous verrez **déploiement d’un Cluster Service Fabric** épinglé toohello **Démarrer** carte.</span><span class="sxs-lookup"><span data-stu-id="d91d3-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="d91d3-262">Afficher l’état de votre cluster</span><span class="sxs-lookup"><span data-stu-id="d91d3-262">View your cluster status</span></span>
![Capture d’écran de détails du cluster dans le tableau de bord hello.][ClusterDashboard]

<span data-ttu-id="d91d3-264">Une fois que votre cluster est créé, vous pouvez inspecter votre cluster dans le portail de hello :</span><span class="sxs-lookup"><span data-stu-id="d91d3-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="d91d3-265">Accédez trop**Parcourir** et cliquez sur **Service Fabric Clusters**.</span><span class="sxs-lookup"><span data-stu-id="d91d3-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="d91d3-266">Recherchez votre cluster et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="d91d3-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="d91d3-267">Vous pouvez maintenant voir les détails de hello de votre cluster dans le tableau de bord hello, y compris le point de terminaison public du cluster hello et un lien de tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d91d3-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="d91d3-268">Hello **nœud Moniteur** section sur le panneau de tableau de bord du cluster hello indique le nombre hello d’ordinateurs virtuels qui sont sains et non intègre.</span><span class="sxs-lookup"><span data-stu-id="d91d3-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="d91d3-269">Vous trouverez plus de détails sur le contrôle d’intégrité du cluster hello à [introduction de modèle de contrôle d’intégrité de Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="d91d3-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="d91d3-270">Clusters service Fabric nécessitent un certain nombre de toobe nœuds toujours toomaintain disponibilité et conservent l’état - tooas référencé « en conservant le quorum ».</span><span class="sxs-lookup"><span data-stu-id="d91d3-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="d91d3-271">Clous, il n’est généralement pas tooshut sécurisé vers le bas de tous les ordinateurs dans un cluster de hello, sauf si vous avez tout d’abord exécuté un [une sauvegarde complète de votre état][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="d91d3-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="d91d3-272">Instance de tooa ensemble d’échelle de Machine virtuelle ou un nœud de cluster de connexion à distance</span><span class="sxs-lookup"><span data-stu-id="d91d3-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="d91d3-273">Chacun des hello NodeTypes vous spécifiez dans les résultats de cluster dans un ensemble de l’échelle de machines virtuelles mise en route de la configuration.</span><span class="sxs-lookup"><span data-stu-id="d91d3-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="d91d3-274">Consultez [de connexion à distance instance d’ensemble d’échelle de Machine virtuelle tooa] [ remote-connect-to-a-vm-scale-set] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d91d3-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d91d3-275">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d91d3-275">Next steps</span></span>
<span data-ttu-id="d91d3-276">À ce stade, vous avez un cluster sécurisé à l’aide de certificats pour l’authentification de la gestion.</span><span class="sxs-lookup"><span data-stu-id="d91d3-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="d91d3-277">Ensuite, [connecter tooyour cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment trop[gérer les secrets de l’application](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="d91d3-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="d91d3-278">Découvrez également les [options de support de Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="d91d3-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
