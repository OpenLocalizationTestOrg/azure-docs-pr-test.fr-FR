---
title: "à partir d’un modèle de cluster aaaCreate un Azure Service Fabric | Documents Microsoft"
description: "Cet article décrit comment tooset d’une infrastructure sécurisée de Service de cluster dans Azure à l’aide du Gestionnaire de ressources Azure, Azure Key Vault et Azure Active Directory (Azure AD) pour l’authentification du client."
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
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="b81b3-103">Créer un cluster Service Fabric à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b81b3-104">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="b81b3-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="b81b3-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="b81b3-106">Ce guide vous montre pas à pas comment configurer un cluster Azure Service Fabric sécurisé dans Azure à l’aide d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b81b3-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="b81b3-107">Nous accuser réception de que cet article hello est long.</span><span class="sxs-lookup"><span data-stu-id="b81b3-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="b81b3-108">Néanmoins, sauf si vous connaissez déjà soigneusement le contenu hello, être toofollow que chaque étape avec soin.</span><span class="sxs-lookup"><span data-stu-id="b81b3-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="b81b3-109">guide de Hello couvre hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="b81b3-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="b81b3-110">Configuration des certificats de tooupload coffre de clés Azure pour la sécurité de cluster et l’application</span><span class="sxs-lookup"><span data-stu-id="b81b3-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="b81b3-111">Création d’un cluster sécurisé dans Azure à l’aide d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="b81b3-112">Authentification des utilisateurs à l’aide d’Azure Active Directory (Azure AD) pour la gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="b81b3-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="b81b3-113">Un cluster sécurisé est un cluster qui empêche les opérations de toomanagement tout accès non autorisé.</span><span class="sxs-lookup"><span data-stu-id="b81b3-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="b81b3-114">Cela inclut le déploiement, la mise à niveau et suppression d’applications, services et données hello qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="b81b3-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="b81b3-115">Un cluster non sécurisé est un cluster que toute personne peut se connecter tooat à tout moment et effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="b81b3-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="b81b3-116">Bien qu’il soit possible de toocreate un cluster non sécurisé, nous vous recommandons vivement de créer un cluster sécurisé à partir du début de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="b81b3-117">En effet, un cluster non sécurisé ne peut pas être sécurisé ultérieurement, ce qui implique la création d’un nouveau cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="b81b3-118">concept de Hello de création de clusters sécurisés est hello identiques, qu’ils soient des clusters Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="b81b3-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="b81b3-119">Pour en savoir plus et accéder à des scripts d’assistance dédiés à la création de clusters Linux sécurisés, voir [Créer des clusters sécurisés sur Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="b81b3-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="b81b3-120">Se connecter tooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="b81b3-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="b81b3-121">Ce guide utilise [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="b81b3-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="b81b3-122">Lorsque vous démarrez une nouvelle session PowerShell, connectez-vous à tooyour compte Azure, puis sélectionnez votre abonnement avant d’exécuter des commandes Azure.</span><span class="sxs-lookup"><span data-stu-id="b81b3-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="b81b3-123">La connexion tooyour compte Azure :</span><span class="sxs-lookup"><span data-stu-id="b81b3-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b81b3-124">Sélectionnez votre abonnement :</span><span class="sxs-lookup"><span data-stu-id="b81b3-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="b81b3-125">Configurer un Key Vault</span><span class="sxs-lookup"><span data-stu-id="b81b3-125">Set up a key vault</span></span>
<span data-ttu-id="b81b3-126">Cette section explique comment créer un Key Vault pour un cluster Service Fabric dans Azure et pour des applications Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b81b3-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="b81b3-127">Pour un guide complet tooAzure le coffre de clés, consultez toohello [le coffre de clés mise en route][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="b81b3-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="b81b3-128">Service Fabric utilise toosecure de certificats X.509 un cluster et fournir des fonctionnalités de sécurité d’application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="b81b3-129">Vous utilisez des certificats de toomanage de coffre de clés pour les clusters Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b81b3-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="b81b3-130">Lorsqu’un cluster est déployé dans Azure, fournisseur de ressources Azure hello qui est chargé de créer des clusters Service Fabric extrait les certificats de coffre de clés et les installe sur les machines virtuelles du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="b81b3-131">Hello diagramme suivant illustre les relations hello entre Azure Key Vault, un cluster Service Fabric et le fournisseur de ressources Azure hello qui utilise les certificats stockés dans un coffre de clés lorsqu’il crée un cluster :</span><span class="sxs-lookup"><span data-stu-id="b81b3-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Diagramme de l’installation de certificats][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="b81b3-133">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b81b3-133">Create a resource group</span></span>
<span data-ttu-id="b81b3-134">première étape de Hello est toocreate un groupe de ressources spécifiquement pour votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="b81b3-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="b81b3-135">Nous vous recommandons de placer le coffre de clés hello dans son propre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b81b3-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="b81b3-136">Cette action permet de supprimer des groupes ressources de calcul et de stockage hello, y compris le groupe de ressources hello qui contient votre cluster Service Fabric, sans perdre vos clés et les clés secrètes.</span><span class="sxs-lookup"><span data-stu-id="b81b3-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="b81b3-137">groupe de ressources Hello qui contient votre coffre de clés _doit être Bonjour même région_ en tant que cluster hello qui l’utilise.</span><span class="sxs-lookup"><span data-stu-id="b81b3-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="b81b3-138">Si vous envisagez de clusters toodeploy dans plusieurs régions, nous vous suggérons de nom de groupe de ressources hello et coffre de clés hello d’une manière qui indique quelle région auquel il appartient.</span><span class="sxs-lookup"><span data-stu-id="b81b3-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="b81b3-139">sortie de Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b81b3-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="b81b3-140">Créer un coffre de clés dans le nouveau groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="b81b3-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="b81b3-141">coffre de clés Hello _doit être activée pour le déploiement_ tooallow hello certificats de tooget de fournisseur de ressources de calcul à partir de celui-ci et l’installer sur les instances de machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="b81b3-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="b81b3-142">sortie de Hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b81b3-142">hello output should look like this:</span></span>

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
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="b81b3-143">Utiliser un Key Vault existant</span><span class="sxs-lookup"><span data-stu-id="b81b3-143">Use an existing key vault</span></span>

<span data-ttu-id="b81b3-144">toouse un coffre de clés existant, vous _devez l’activer pour le déploiement_ tooallow hello certificats de tooget de fournisseur de ressources de calcul à partir de celui-ci et l’installer sur les nœuds de cluster :</span><span class="sxs-lookup"><span data-stu-id="b81b3-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="b81b3-145">Ajouter le coffre de clés de certificats tooyour</span><span class="sxs-lookup"><span data-stu-id="b81b3-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="b81b3-146">Certificats sont utilisés dans les toosecure Service Fabric tooprovide l’authentification et chiffrement divers aspects d’un cluster et ses applications.</span><span class="sxs-lookup"><span data-stu-id="b81b3-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="b81b3-147">Pour plus d’informations sur l’utilisation de certificats dans Service Fabric, consultez la page [Scénarios de sécurité d’un cluster Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="b81b3-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="b81b3-148">Certificat de cluster et de serveur (obligatoire)</span><span class="sxs-lookup"><span data-stu-id="b81b3-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="b81b3-149">Ce certificat est requis toosecure un cluster et empêcher tout accès non autorisé tooit.</span><span class="sxs-lookup"><span data-stu-id="b81b3-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="b81b3-150">Il assure la sécurité du cluster de deux manières :</span><span class="sxs-lookup"><span data-stu-id="b81b3-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="b81b3-151">Authentification du cluster : authentifie la communication nœud à nœud pour la fédération du cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="b81b3-152">Seuls les nœuds qui peuvent prouver leur identité avec ce certificat peuvent être ajouté hello cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="b81b3-153">L’authentification du serveur : authentifie hello gestion des points de terminaison tooa gestion client de cluster, afin que hello gestion client sait qu’il communique avec le véritable toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="b81b3-154">Ce certificat fournit également une connexion SSL pour hello API de gestion HTTPS et pour le Service Fabric Explorer via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b81b3-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="b81b3-155">tooserve ces fins, les certificats de hello doit respecter hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="b81b3-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="b81b3-156">certificat de Hello doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="b81b3-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="b81b3-157">certificat de Hello doit être créé pour l’échange de clés, qui est exportable tooa fichier d’échange d’informations personnelles (.pfx).</span><span class="sxs-lookup"><span data-stu-id="b81b3-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="b81b3-158">nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b81b3-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="b81b3-159">Cette mise en correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b81b3-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b81b3-160">Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification (CA) pour hello. cloudapp.azure.com domaine.</span><span class="sxs-lookup"><span data-stu-id="b81b3-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="b81b3-161">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b81b3-162">Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="b81b3-163">Certificats d’application (facultatif)</span><span class="sxs-lookup"><span data-stu-id="b81b3-163">Application certificates (optional)</span></span>
<span data-ttu-id="b81b3-164">Un nombre quelconque de certificats supplémentaires peut être installé sur un cluster pour sécuriser une application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="b81b3-165">Avant de créer votre cluster, tenez compte des scénarios de sécurité hello qui nécessitent un toobe certificat installé sur les nœuds de hello, tel que :</span><span class="sxs-lookup"><span data-stu-id="b81b3-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="b81b3-166">Le chiffrement et déchiffrement de valeurs de configuration d’application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="b81b3-167">Le chiffrement des données sur les nœuds lors de la réplication.</span><span class="sxs-lookup"><span data-stu-id="b81b3-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="b81b3-168">Mise en forme de certificats pour une utilisation par un fournisseur de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="b81b3-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="b81b3-169">Vous pouvez ajouter et utiliser les fichiers de clé privée (.pfx) directement via votre Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b81b3-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="b81b3-170">Toutefois, le fournisseur de ressources de calcul Azure hello nécessite toobe clés stockée dans un format spécial de JavaScript Objet Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="b81b3-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="b81b3-171">format de Hello inclut le fichier .pfx de hello comme un base 64-chaîne encodée au format et le mot de passe clé privée hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="b81b3-172">tooaccommodate ces exigences, hello clés doivent être placés dans une chaîne JSON et ensuite stockées en tant que « clés secrètes » dans la clé de hello coffre.</span><span class="sxs-lookup"><span data-stu-id="b81b3-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="b81b3-173">toomake ce processus, un [module PowerShell est disponible sur GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="b81b3-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="b81b3-174">module de hello toouse, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b81b3-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="b81b3-175">Téléchargez hello intégralité du contenu du référentiel de hello dans un répertoire local.</span><span class="sxs-lookup"><span data-stu-id="b81b3-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="b81b3-176">Accédez toohello répertoire local.</span><span class="sxs-lookup"><span data-stu-id="b81b3-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="b81b3-177">Importez le module de ServiceFabricRPHelpers hello dans la fenêtre PowerShell :</span><span class="sxs-lookup"><span data-stu-id="b81b3-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="b81b3-178">Hello `Invoke-AddCertToKeyVault` commande dans ce module PowerShell met en forme une clé privée du certificat en une chaîne JSON et télécharge le coffre de clés toohello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b81b3-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="b81b3-179">Utiliser le certificat de cluster hello commande tooadd hello et un coffre de clés toohello de certificats supplémentaires de l’application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="b81b3-180">Répétez cette étape pour tous les certificats supplémentaires que vous souhaitez tooinstall dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="b81b3-181">Chargement d’un certificat existant</span><span class="sxs-lookup"><span data-stu-id="b81b3-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="b81b3-182">Si vous obtenez une erreur, par exemple hello celui présenté ici, cela signifie que vous disposez d’un conflit d’URL de ressource.</span><span class="sxs-lookup"><span data-stu-id="b81b3-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="b81b3-183">conflit de hello tooresolve, modifier le nom de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="b81b3-184">Une fois que la résolution du conflit de hello, sortie de hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b81b3-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="b81b3-185">Vous devez hello trois précédent chaînes CertificateThumbprint, SourceVault et CertificateURL, tooset un tooobtain et un cluster Service Fabric sécurisée tous les certificats de l’application que vous pouvez utiliser pour la sécurité de l’application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="b81b3-186">Si vous n’enregistrez pas les chaînes de hello, il peut être difficile tooretrieve en interrogeant hello clé de coffre ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b81b3-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="b81b3-187">Création d’un certificat auto-signé et de les télécharger toohello coffre de clés</span><span class="sxs-lookup"><span data-stu-id="b81b3-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="b81b3-188">Si vous avez déjà téléchargé votre coffre de clés de certificats toohello, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="b81b3-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="b81b3-189">Cette étape est de générer un nouveau certificat auto-signé et de les télécharger tooyour coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="b81b3-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="b81b3-190">Une fois que vous modifiez les paramètres de hello Bonjour script suivant et exécutez, vous devez fournir un mot de passe du certificat.</span><span class="sxs-lookup"><span data-stu-id="b81b3-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="b81b3-191">Si vous obtenez une erreur, par exemple hello celui présenté ici, cela signifie que vous disposez d’un conflit d’URL de ressource.</span><span class="sxs-lookup"><span data-stu-id="b81b3-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="b81b3-192">conflit de hello tooresolve, modifier le nom de coffre de clés hello, nom de groupe de routage et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="b81b3-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="b81b3-193">Une fois que la résolution du conflit de hello, sortie de hello doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b81b3-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="b81b3-194">Vous devez hello trois précédent chaînes CertificateThumbprint, SourceVault et CertificateURL, tooset un tooobtain et un cluster Service Fabric sécurisée tous les certificats de l’application que vous pouvez utiliser pour la sécurité de l’application.</span><span class="sxs-lookup"><span data-stu-id="b81b3-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="b81b3-195">Si vous n’enregistrez pas les chaînes de hello, il peut être difficile tooretrieve en interrogeant hello clé de coffre ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b81b3-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="b81b3-196">À ce stade, vous devez avoir hello suit les éléments en place :</span><span class="sxs-lookup"><span data-stu-id="b81b3-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="b81b3-197">groupe de ressources du coffre de clés Hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-197">hello key vault resource group.</span></span>
* <span data-ttu-id="b81b3-198">Bonjour coffre de clés et de son URL (appelé SourceVault Bonjour précédant la sortie PowerShell).</span><span class="sxs-lookup"><span data-stu-id="b81b3-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="b81b3-199">certificat d’authentification serveur Hello cluster et son URL dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="b81b3-200">certificats d’application Hello et leurs URL dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="b81b3-201">Configuration d’Azure Active Directory pour l’authentification des clients</span><span class="sxs-lookup"><span data-stu-id="b81b3-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="b81b3-202">Azure AD permet aux organisations (appelés clients) toomanage utilisateur accès tooapplications.</span><span class="sxs-lookup"><span data-stu-id="b81b3-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="b81b3-203">Ces dernières se composent d’applications avec une interface utilisateur de connexion web et d’applications avec une expérience client natif.</span><span class="sxs-lookup"><span data-stu-id="b81b3-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="b81b3-204">Dans cet article, nous partons du principe que vous avez déjà créé un locataire.</span><span class="sxs-lookup"><span data-stu-id="b81b3-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="b81b3-205">Si vous n’avez pas le cas, commencez par lire [comment tooget Azure Active Directory locataire][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="b81b3-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="b81b3-206">Un cluster Service Fabric offre plusieurs tooits de points d’entrée des fonctionnalités de gestion, y compris hello basée sur le web [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] et [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="b81b3-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="b81b3-207">Par conséquent, vous créez le cluster de deux accès Azure AD applications toocontrol toohello, une application web et une application native.</span><span class="sxs-lookup"><span data-stu-id="b81b3-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="b81b3-208">toosimplify certaines des étapes de hello concernés par la configuration d’Azure AD avec un cluster Service Fabric, nous avons créé un ensemble de scripts Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b81b3-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="b81b3-209">Vous devez effectuer hello comme suit avant de créer le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="b81b3-210">Étant donné que les scripts hello attendent des points de terminaison et les noms de cluster, les valeurs hello doivent être planifiées et pas les valeurs que vous avez déjà créé.</span><span class="sxs-lookup"><span data-stu-id="b81b3-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="b81b3-211">[Télécharger les scripts hello] [ sf-aad-ps-script-download] tooyour ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b81b3-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="b81b3-212">Avec le bouton hello fichier zip, sélectionnez **propriétés**, sélectionnez hello **Unblock** case à cocher, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="b81b3-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="b81b3-213">Extrayez le fichier zip de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="b81b3-214">Exécutez `SetupApplications.ps1`et fournir hello TenantId, ClusterName et WebApplicationReplyUrl en tant que paramètres.</span><span class="sxs-lookup"><span data-stu-id="b81b3-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="b81b3-215">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b81b3-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="b81b3-216">Vous pouvez trouver votre TenantId en exécutant la commande PowerShell de hello `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="b81b3-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="b81b3-217">L’exécution de cette commande affiche hello TenantId pour chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="b81b3-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="b81b3-218">ClusterName est applications hello Azure AD tooprefix utilisés qui sont créées par le script de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="b81b3-219">Il n’a pas besoin nom du cluster actuel toomatch hello exactement.</span><span class="sxs-lookup"><span data-stu-id="b81b3-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="b81b3-220">Il est prévu toomake uniquement il plus facile toomap Azure AD artefacts toohello Service Fabric cluster qu’ils sont utilisés avec.</span><span class="sxs-lookup"><span data-stu-id="b81b3-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="b81b3-221">WebApplicationReplyUrl est hello par défaut point de terminaison Azure AD renvoie tooyour utilisateurs une fois qu’elles sont terminées la signature.</span><span class="sxs-lookup"><span data-stu-id="b81b3-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="b81b3-222">Définissez ce point de terminaison en tant que point de terminaison de Service Fabric Explorer hello pour votre cluster, qui est par défaut :</span><span class="sxs-lookup"><span data-stu-id="b81b3-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="b81b3-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="b81b3-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="b81b3-224">Vous êtes invité à toosign tooan compte disposant des privilèges d’administrateur pour le client de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b81b3-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="b81b3-225">Après que vous être connecté, hello script crée les web hello et applications natives toorepresent votre cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b81b3-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="b81b3-226">Si vous examinez les applications du locataire hello Bonjour [portail Azure classic][azure-classic-portal], vous devez voir deux entrées :</span><span class="sxs-lookup"><span data-stu-id="b81b3-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="b81b3-227">*ClusterName*\_Cluster</span><span class="sxs-lookup"><span data-stu-id="b81b3-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="b81b3-228">*ClusterName*\_Client</span><span class="sxs-lookup"><span data-stu-id="b81b3-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="b81b3-229">script de Hello imprime hello JSON requis par le modèle de gestionnaire de ressources Azure hello lorsque vous créez le cluster de hello dans la section suivante de hello, par conséquent, il est une fenêtre PowerShell de bonne idée tookeep hello ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b81b3-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="b81b3-230">Création d’un modèle Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="b81b3-231">Dans cette section, hello génère de hello précédent des commandes PowerShell sont utilisés dans un modèle de gestionnaire de ressources du cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b81b3-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="b81b3-232">Modèles de l’exemple de gestionnaire de ressources sont disponibles dans hello [la galerie de modèle de démarrage rapide Azure sur GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="b81b3-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="b81b3-233">Ces modèles peuvent être utilisés comme point de départ pour votre modèle de cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="b81b3-234">Créer le modèle de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="b81b3-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="b81b3-235">Ce guide utilise hello [cluster sécurisée à 5 nœuds] [ service-fabric-secure-cluster-5-node-1-nodetype] exemple de modèle et les paramètres de modèle.</span><span class="sxs-lookup"><span data-stu-id="b81b3-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="b81b3-236">Télécharger `azuredeploy.json` et `azuredeploy.parameters.json` tooyour ordinateur et ouvrez les deux fichiers dans votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="b81b3-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="b81b3-237">Ajout de certificats</span><span class="sxs-lookup"><span data-stu-id="b81b3-237">Add certificates</span></span>
<span data-ttu-id="b81b3-238">Vous ajouter le modèle de gestionnaire de ressources du cluster certificats tooa en référençant le coffre de clés hello qui contient les clés de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="b81b3-239">Nous vous recommandons de placer les valeurs hello coffre de clés dans un fichier de paramètres de modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="b81b3-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="b81b3-240">Cela conserve hello Gestionnaire de ressources du fichier de modèle réutilisables et de déploiement tooa spécifique de valeurs.</span><span class="sxs-lookup"><span data-stu-id="b81b3-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="b81b3-241">Ajouter des qu'ensembles de l’échelle de machines virtuelles de tous les certificats toohello osProfile</span><span class="sxs-lookup"><span data-stu-id="b81b3-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="b81b3-242">Chaque certificat est installé dans un cluster de hello doit être configuré dans la section d’osProfile hello de ressource de jeu de mise à l’échelle hello (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="b81b3-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="b81b3-243">Cette action indique à hello fournisseur tooinstall hello du certificat de ressources sur les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="b81b3-244">Cette installation inclut le certificat de cluster hello et tous les certificats de sécurité d’application que vous envisagez de toouse pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="b81b3-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

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

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="b81b3-245">Configurer le certificat de cluster Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="b81b3-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="b81b3-246">certificat d’authentification Hello cluster doit être configuré dans les deux ressources de cluster Service Fabric hello (Microsoft.ServiceFabric/clusters) et hello extension Service Fabric pour l’échelle de machines virtuelles définit dans la ressource de jeu de mise à l’échelle hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b81b3-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="b81b3-247">Ce procédé permet tooconfigure de fournisseur de ressources de Service Fabric hello pour les utiliser pour l’authentification du cluster et serveur pour les points de terminaison de gestion.</span><span class="sxs-lookup"><span data-stu-id="b81b3-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="b81b3-248">Ressource des groupes de machines virtuelles identiques :</span><span class="sxs-lookup"><span data-stu-id="b81b3-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="b81b3-249">Ressource Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="b81b3-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="b81b3-250">Insérer la configuration Azure AD</span><span class="sxs-lookup"><span data-stu-id="b81b3-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="b81b3-251">configuration de Hello Azure AD que vous avez créé précédemment peut être insérée directement dans votre modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="b81b3-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="b81b3-252">Toutefois, il est recommandé d’abord extraire les valeurs de hello dans un réutilisable de modèle de gestionnaire de ressources paramètres fichier tookeep hello et libres de déploiement tooa spécifique de valeurs.</span><span class="sxs-lookup"><span data-stu-id="b81b3-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

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

### <span data-ttu-id="b81b3-253"><a "configure-arm" ></a>Configuration des paramètres de modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="b81b3-254">Enfin, utilisez les valeurs de sortie de hello du coffre de clés hello et le fichier de paramètres de Azure AD PowerShell commandes toopopulate hello :</span><span class="sxs-lookup"><span data-stu-id="b81b3-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

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
<span data-ttu-id="b81b3-255">À ce stade, vous devez avoir hello suit les éléments en place :</span><span class="sxs-lookup"><span data-stu-id="b81b3-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="b81b3-256">Groupe de ressources du Key Vault</span><span class="sxs-lookup"><span data-stu-id="b81b3-256">Key vault resource group</span></span>
  * <span data-ttu-id="b81b3-257">Coffre de clés</span><span class="sxs-lookup"><span data-stu-id="b81b3-257">Key vault</span></span>
  * <span data-ttu-id="b81b3-258">Certificat d’authentification de serveur de clusters</span><span class="sxs-lookup"><span data-stu-id="b81b3-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="b81b3-259">Certificat de chiffrement de données</span><span class="sxs-lookup"><span data-stu-id="b81b3-259">Data encipherment certificate</span></span>
* <span data-ttu-id="b81b3-260">Locataire Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b81b3-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="b81b3-261">Application Azure AD pour la gestion basée sur le web et Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="b81b3-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="b81b3-262">Application Azure AD pour la gestion du client natif</span><span class="sxs-lookup"><span data-stu-id="b81b3-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="b81b3-263">Utilisateurs et rôles qui leur sont affectés</span><span class="sxs-lookup"><span data-stu-id="b81b3-263">Users and their assigned roles</span></span>
* <span data-ttu-id="b81b3-264">Modèle Service Fabric Cluster Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b81b3-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="b81b3-265">Certificats configurés par le biais du Key Vault</span><span class="sxs-lookup"><span data-stu-id="b81b3-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="b81b3-266">Configuration d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b81b3-266">Azure Active Directory configured</span></span>

<span data-ttu-id="b81b3-267">Hello suivant schéma montre où interviennent les votre coffre de clés et de la configuration d’Azure AD dans votre modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="b81b3-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Mappage de dépendances de Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="b81b3-269">Créer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="b81b3-269">Create hello cluster</span></span>
<span data-ttu-id="b81b3-270">Vous êtes maintenant cluster de hello toocreate prêt à l’aide de [déploiement de modèle de ressource Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="b81b3-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="b81b3-271">Testez-le</span><span class="sxs-lookup"><span data-stu-id="b81b3-271">Test it</span></span>
<span data-ttu-id="b81b3-272">Utilisez hello suivant tootest de commande PowerShell de votre modèle de gestionnaire de ressources avec un fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="b81b3-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="b81b3-273">Déployez-le</span><span class="sxs-lookup"><span data-stu-id="b81b3-273">Deploy it</span></span>
<span data-ttu-id="b81b3-274">Si le test de modèle de gestionnaire de ressources hello réussit, utilisez hello suivant toodeploy de commande PowerShell votre modèle de gestionnaire de ressources avec un fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="b81b3-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="b81b3-275">Affecter des utilisateurs tooroles</span><span class="sxs-lookup"><span data-stu-id="b81b3-275">Assign users tooroles</span></span>
<span data-ttu-id="b81b3-276">Après avoir créé hello applications toorepresent votre cluster, affecter vos utilisateurs des rôles toohello pris en charge par le Service Fabric : en lecture seule et administrateur. Vous pouvez attribuer des rôles de hello à l’aide de hello [portail Azure classic][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="b81b3-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="b81b3-277">Bonjour portail Azure, accédez à tooyour client, puis sélectionnez **Applications**.</span><span class="sxs-lookup"><span data-stu-id="b81b3-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="b81b3-278">Sélectionnez l’application web hello, qui porte un nom comme `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="b81b3-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="b81b3-279">Cliquez sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="b81b3-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="b81b3-280">Sélectionnez un tooassign d’utilisateur, puis cliquez sur hello **affecter** bouton bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Les utilisateurs tooroles bouton affecter][assign-users-to-roles-button]
5. <span data-ttu-id="b81b3-282">Sélectionnez hello rôle tooassign toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b81b3-282">Select hello role tooassign toohello user.</span></span>

    ![Boîte de dialogue Affecter des utilisateurs][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="b81b3-284">Pour plus d’informations sur les rôles dans Service Fabric, consultez [Contrôle d’accès en fonction du rôle pour les clients de Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="b81b3-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="b81b3-285">Créer des clusters sécurisés sur Linux</span><span class="sxs-lookup"><span data-stu-id="b81b3-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="b81b3-286">processus de hello toomake plus facile, nous avons fourni un [script du programme d’assistance](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="b81b3-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="b81b3-287">Avant d’utiliser ce script d’assistance, assurez-vous que l’interface de ligne de commande Azure (CLI) est déjà installée, et qu’il se trouve dans votre chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="b81b3-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="b81b3-288">Assurez-vous que le script de hello a tooexecute d’autorisations en exécutant `chmod +x cert_helper.py` après l’avoir téléchargé.</span><span class="sxs-lookup"><span data-stu-id="b81b3-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="b81b3-289">première étape de Hello est toosign dans tooyour compte Azure à l’aide de CLI avec hello `azure login` commande.</span><span class="sxs-lookup"><span data-stu-id="b81b3-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="b81b3-290">Une fois connectés tooyour compte Azure, utiliser un script d’assistance hello avec votre autorité de certification signé le certificat, en tant que hello ci-dessous illustre de commande :</span><span class="sxs-lookup"><span data-stu-id="b81b3-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="b81b3-291">paramètre d’IFichier - Hello peut prendre un fichier .pfx ou un fichier .pem comme entrée, avec le type de certificat hello (pfx ou pem ou ss s’il s’agit d’un certificat auto-signé).</span><span class="sxs-lookup"><span data-stu-id="b81b3-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="b81b3-292">paramètre -h Hello imprime texte d’aide hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="b81b3-293">Cette commande renvoie hello suivant trois chaînes en tant que sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="b81b3-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="b81b3-294">SourceVaultID, qui est l’ID de hello pour hello nouvelle KeyVault ResourceGroup il créé pour vous</span><span class="sxs-lookup"><span data-stu-id="b81b3-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="b81b3-295">CertificateUrl pour accéder au certificat de hello</span><span class="sxs-lookup"><span data-stu-id="b81b3-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="b81b3-296">CertificateThumbprint, qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="b81b3-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="b81b3-297">Bonjour à l’exemple suivant montre comment toouse hello commande :</span><span class="sxs-lookup"><span data-stu-id="b81b3-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="b81b3-298">L’exécution de hello précédant donne de commande vous hello trois chaînes comme suit :</span><span class="sxs-lookup"><span data-stu-id="b81b3-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="b81b3-299">nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b81b3-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="b81b3-300">Cette correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b81b3-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b81b3-301">Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification pour hello `.cloudapp.azure.com` domaine.</span><span class="sxs-lookup"><span data-stu-id="b81b3-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="b81b3-302">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b81b3-303">Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="b81b3-304">Ces noms de sujet sont entrées hello toocreate un cluster Service Fabric sécurisé (sans Azure AD), comme décrit dans [les paramètres de modèle de configurer le Gestionnaire de ressources](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="b81b3-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="b81b3-305">Vous pouvez vous connecter à cluster sécurisée de toohello en suivant les instructions de hello pour [l’authentification client le cluster tooa accès](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b81b3-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="b81b3-306">Les clusters Linux en version préliminaire ne prennent pas en charge l’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b81b3-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="b81b3-307">Vous pouvez attribuer des rôles d’administrateur et le client comme décrit dans hello [affecter des rôles toousers](#assign-roles) section.</span><span class="sxs-lookup"><span data-stu-id="b81b3-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="b81b3-308">Lorsque vous spécifiez les rôles administrateur et le client pour un cluster de version d’évaluation de Linux, vous avez tooprovide empreintes numériques de certificat pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="b81b3-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="b81b3-309">(Vous ne spécifiez aucun nom de sujet hello, car aucune validation de la chaîne ou de la révocation n’est effectuée dans cette version préliminaire.)</span><span class="sxs-lookup"><span data-stu-id="b81b3-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="b81b3-310">Si vous voulez toouse un certificat auto-signé pour le test, vous pouvez utiliser hello même toogenerate script un.</span><span class="sxs-lookup"><span data-stu-id="b81b3-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="b81b3-311">Vous pouvez ensuite télécharger le coffre de clés tooyour certificat hello en fournissant l’indicateur de hello `ss` au lieu de fournir le nom de chemin d’accès et le certificat du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="b81b3-312">Par exemple, consultez hello commande pour la création et téléchargement d’un certificat auto-signé suivante :</span><span class="sxs-lookup"><span data-stu-id="b81b3-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="b81b3-313">Cette commande retourne hello mêmes trois chaînes : SourceVault, CertificateUrl et CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="b81b3-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="b81b3-314">Vous pouvez ensuite utiliser hello chaînes toocreate un cluster Linux sécurisé et un emplacement où le certificat auto-signé de hello est placé.</span><span class="sxs-lookup"><span data-stu-id="b81b3-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="b81b3-315">Vous avez besoin de cluster de toohello tooconnect hello certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="b81b3-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="b81b3-316">Vous pouvez vous connecter à cluster sécurisée de toohello en suivant les instructions de hello pour [l’authentification client le cluster tooa accès](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="b81b3-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="b81b3-317">nom du sujet du certificat Hello doit correspondre au domaine hello que vous utilisez cluster Service Fabric de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b81b3-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="b81b3-318">Cette correspondance est requise tooprovide une connexion SSL pour les points de terminaison de gestion du cluster hello HTTPS et le Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b81b3-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="b81b3-319">Vous ne pouvez pas obtenir un certificat SSL à partir d’une autorité de certification pour hello `.cloudapp.azure.com` domaine.</span><span class="sxs-lookup"><span data-stu-id="b81b3-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="b81b3-320">Vous devez obtenir un nom de domaine personnalisé pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="b81b3-321">Lorsque vous demandez un certificat à partir d’une autorité de certification, hello nom du sujet du certificat doit correspondre au nom de domaine personnalisé hello que vous utilisez pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="b81b3-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="b81b3-322">Vous pouvez remplir les paramètres de hello à partir de script d’assistance hello hello portail Azure, comme décrit dans hello [créer un cluster Bonjour Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span><span class="sxs-lookup"><span data-stu-id="b81b3-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b81b3-323">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b81b3-323">Next steps</span></span>
<span data-ttu-id="b81b3-324">À ce stade, vous avez un cluster sécurisé avec l’authentification de gestion fournie par Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b81b3-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="b81b3-325">Ensuite, [connecter tooyour cluster](service-fabric-connect-to-secure-cluster.md) et découvrez comment trop[gérer les secrets de l’application](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="b81b3-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="b81b3-326">Résoudre les problèmes de configuration d’Azure Active Directory pour l’authentification des clients</span><span class="sxs-lookup"><span data-stu-id="b81b3-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="b81b3-327">Si vous rencontrez un problème pendant que vous configurez Azure AD pour l’authentification du client, passez en revue les solutions possibles hello dans cette section.</span><span class="sxs-lookup"><span data-stu-id="b81b3-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="b81b3-328">Service Fabric Explorer invite tooselect un certificat</span><span class="sxs-lookup"><span data-stu-id="b81b3-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="b81b3-329">Problème</span><span class="sxs-lookup"><span data-stu-id="b81b3-329">Problem</span></span>
<span data-ttu-id="b81b3-330">Après que vous être connecté avec succès tooAzure dans l’Explorateur de l’infrastructure de Service Active Directory, navigateur de hello retourne la page d’accueil toohello mais un message vous invite à entrer tooselect un certificat.</span><span class="sxs-lookup"><span data-stu-id="b81b3-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Boîte de dialogue SFX de sélection d’un certificat][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="b81b3-332">Motif</span><span class="sxs-lookup"><span data-stu-id="b81b3-332">Reason</span></span>
<span data-ttu-id="b81b3-333">utilisateur de Hello n’est pas affecté un rôle dans hello application de cluster Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b81b3-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="b81b3-334">Par conséquent, l’authentification Azure AD échoue sur le cluster Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b81b3-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="b81b3-335">Service Fabric Explorer revient toocertificate authentification.</span><span class="sxs-lookup"><span data-stu-id="b81b3-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="b81b3-336">Solution</span><span class="sxs-lookup"><span data-stu-id="b81b3-336">Solution</span></span>
<span data-ttu-id="b81b3-337">Suivez les instructions de hello pour la configuration d’Azure AD, puis attribuer des rôles d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b81b3-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="b81b3-338">En outre, nous vous recommandons de tension « Utilisateur d’application affectation tooaccess requis », en tant que `SetupApplications.ps1` est.</span><span class="sxs-lookup"><span data-stu-id="b81b3-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="b81b3-339">Connexion avec PowerShell échoue avec une erreur : « hello spécifié des informations d’identification ne sont pas valides »</span><span class="sxs-lookup"><span data-stu-id="b81b3-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="b81b3-340">Problème</span><span class="sxs-lookup"><span data-stu-id="b81b3-340">Problem</span></span>
<span data-ttu-id="b81b3-341">Lorsque vous utilisez PowerShell tooconnect toohello cluster en utilisant le mode de sécurité « AzureActiveDirectory », après vous être connecté avec succès tooAzure AD, la connexion de hello échoue avec une erreur : « hello spécifié informations d’identification ne sont pas valides. »</span><span class="sxs-lookup"><span data-stu-id="b81b3-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="b81b3-342">Solution</span><span class="sxs-lookup"><span data-stu-id="b81b3-342">Solution</span></span>
<span data-ttu-id="b81b3-343">Cette solution est hello qu'identique hello précédant une.</span><span class="sxs-lookup"><span data-stu-id="b81b3-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="b81b3-344">Lorsque vous vous connectez, Service Fabric Explorer renvoie un message d’échec : « AADSTS50011 »</span><span class="sxs-lookup"><span data-stu-id="b81b3-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="b81b3-345">Problème</span><span class="sxs-lookup"><span data-stu-id="b81b3-345">Problem</span></span>
<span data-ttu-id="b81b3-346">Lorsque vous essayez de toosign dans tooAzure AD dans l’Explorateur de l’infrastructure de Service, page de hello retourne une erreur : « AADSTS50011 : hello adresse de réponse &lt;url&gt; ne correspondent pas aux adresses de réponse de hello configurés pour l’application hello : &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="b81b3-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![L’adresse de réponse SFX ne correspond pas][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="b81b3-348">Motif</span><span class="sxs-lookup"><span data-stu-id="b81b3-348">Reason</span></span>
<span data-ttu-id="b81b3-349">application Hello cluster (web) qui représente le Service Fabric Explorer tente tooauthenticate auprès d’Azure AD, et dans le cadre de la demande de hello fournit des URL de retour de redirection hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="b81b3-350">Mais hello URL n’est pas répertorié dans l’application hello Azure AD **URL de réponse** liste.</span><span class="sxs-lookup"><span data-stu-id="b81b3-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="b81b3-351">Solution</span><span class="sxs-lookup"><span data-stu-id="b81b3-351">Solution</span></span>
<span data-ttu-id="b81b3-352">Sur hello **configurer** onglet Hello application (web) de cluster, ajoutez hello URL de Service Fabric Explorer toohello **URL de réponse** répertorier ou remplacez un des éléments hello dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b81b3-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="b81b3-353">Lorsque vous avez terminé, enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="b81b3-353">When you have finished, save your change.</span></span>

![URL de réponse d’application web][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="b81b3-355">Connecter le cluster de hello en utilisant l’authentification Azure AD via PowerShell</span><span class="sxs-lookup"><span data-stu-id="b81b3-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="b81b3-356">tooconnect hello cluster Service Fabric, utilisez hello exemple de commande PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="b81b3-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="b81b3-357">toolearn sur l’applet de commande Connect-ServiceFabricCluster de hello, consultez [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="b81b3-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="b81b3-358">Puis-je réutiliser locataire hello même instance Azure AD dans plusieurs clusters ?</span><span class="sxs-lookup"><span data-stu-id="b81b3-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="b81b3-359">Oui.</span><span class="sxs-lookup"><span data-stu-id="b81b3-359">Yes.</span></span> <span data-ttu-id="b81b3-360">Mais n’oubliez pas d’application de cluster (web) tooyour tooadd hello URL de Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b81b3-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="b81b3-361">Si vous ne le faites pas, Service Fabric Explorer ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="b81b3-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="b81b3-362">Pourquoi dois-je disposer d’un certificat de serveur lorsqu’Azure AD est activé ?</span><span class="sxs-lookup"><span data-stu-id="b81b3-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="b81b3-363">FabricClient et FabricGateway effectuent une authentification mutuelle.</span><span class="sxs-lookup"><span data-stu-id="b81b3-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="b81b3-364">Lors de l’authentification Azure AD, intégration d’Azure AD fournit un client serveur toohello d’identité et certificat de serveur hello est utilisé tooverify hello identité du serveur.</span><span class="sxs-lookup"><span data-stu-id="b81b3-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="b81b3-365">Pour plus d’informations sur les certificats Service Fabric, consultez [Certificats X.509 et Service Fabric][x509-certificates-and-service-fabric]</span><span class="sxs-lookup"><span data-stu-id="b81b3-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

