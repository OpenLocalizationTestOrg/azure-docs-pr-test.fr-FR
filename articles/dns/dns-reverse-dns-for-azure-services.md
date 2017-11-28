---
title: aaaReverse DNS pour les services Azure | Documents Microsoft
description: "Découvrez comment tooconfigure DNS inversées pour les services hébergés dans Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="367c6-103">Configurer des DNS inversés dans les services hébergés par Azure</span><span class="sxs-lookup"><span data-stu-id="367c6-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="367c6-104">Cet article explique comment tooconfigure DNS inversées pour les services hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="367c6-105">Les services Azure utilisent des adresses IP assignées par Azure et détenues par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="367c6-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="367c6-106">Ces enregistrements DNS inverses (enregistrements PTR) doivent être créés dans hello correspondant appartenant à Microsoft recherche les zones DNS inverses.</span><span class="sxs-lookup"><span data-stu-id="367c6-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="367c6-107">Cet article explique comment toodo cela.</span><span class="sxs-lookup"><span data-stu-id="367c6-107">This article explains how toodo this.</span></span>

<span data-ttu-id="367c6-108">Ce scénario ne doit pas être confondu avec possibilité de hello trop[héberger des zones de recherche DNS inverses hello pour vos plages IP affectées dans Azure DNS](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="367c6-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="367c6-109">Dans ce cas, les plages d’adresses IP hello représentés par la zone de recherche inversée hello doivent être assignés tooyour organisation, généralement par votre fournisseur de services Internet.</span><span class="sxs-lookup"><span data-stu-id="367c6-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="367c6-110">Avant de lire cet article, prenez connaissance de cette [Vue d’ensemble des DNS inversés et de la prise en charge dans Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="367c6-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="367c6-111">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="367c6-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="367c6-112">Dans le modèle de déploiement du Gestionnaire de ressources hello, les ressources de calcul (par exemple, les ordinateurs virtuels, machines virtuelles identiques ou clusters Service Fabric) sont exposées via une ressource d’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="367c6-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="367c6-113">Recherche DNS inversée est configurée à l’aide de la propriété « Valeur de ReverseFqdn » hello hello adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="367c6-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="367c6-114">Dans le modèle de déploiement classique hello, les ressources de calcul sont exposées à l’aide des Services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="367c6-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="367c6-115">Recherche DNS inversée est configurée à l’aide de la propriété de 'ReverseDnsFqdn' hello Hello Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="367c6-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="367c6-116">DNS inverse n’est pas prise en charge pour hello du Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="367c6-117">Validation des enregistrements DNS inversés</span><span class="sxs-lookup"><span data-stu-id="367c6-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="367c6-118">Un tiers ne doit pas être en mesure de toocreate des enregistrements DNS inverses pour leurs service Azure mappage tooyour DNS des domaines.</span><span class="sxs-lookup"><span data-stu-id="367c6-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="367c6-119">tooprevent, Azure n’autorise la création d’un enregistrement DNS inverse, où le nom de domaine spécifié dans l’enregistrement DNS inverse de hello est hello identique ou soit résolu en hello nom DNS ou l’adresse IP d’une adresse IP publique ou un Cloud Service Bonjour même hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="367c6-120">Cette validation est effectuée uniquement lors de l’enregistrement DNS inversé de hello est défini ou modifié.</span><span class="sxs-lookup"><span data-stu-id="367c6-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="367c6-121">Aucune nouvelle validation périodique n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="367c6-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="367c6-122">Par exemple : supposons que hello ressource d’adresse IP publique a contosoapp1.northus.cloudapp.azure.com de nom DNS hello et l’adresse IP 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="367c6-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="367c6-123">Hello valeur de ReverseFqdn pour hello qu'adresse IP publique peut être spécifié en tant que :</span><span class="sxs-lookup"><span data-stu-id="367c6-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="367c6-124">nom DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="367c6-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="367c6-125">Hello de noms DNS pour une autre adresse IP publique Bonjour même abonnement, par exemple contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="367c6-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="367c6-126">Un personnel de nom DNS, tel que app1.contoso.com, tant que ce nom est *premier* configuré comme un CNAME toocontosoapp1.northus.cloudapp.azure.com ou tooa PublicIpAddress différents Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="367c6-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="367c6-127">Un personnel de nom DNS, tel que app1.contoso.com, tant que ce nom est *premier* configuré en tant qu’un enregistrement toohello IP adresse 23.96.52.53 ou adresse IP de toohello d’une adresse IP publique différents Bonjour même abonnement.</span><span class="sxs-lookup"><span data-stu-id="367c6-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="367c6-128">Hello mêmes contraintes s’appliquent tooreverse DNS pour les Services Cloud.</span><span class="sxs-lookup"><span data-stu-id="367c6-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="367c6-129">Les DNS inversés pour les ressources PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="367c6-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="367c6-130">Cette section fournit des instructions détaillées pour la tooconfigure DNS inverse pour les ressources d’adresse IP publique dans hello Gestionnaire de ressources du modèle de déploiement utilisant Azure PowerShell, Azure CLI 1.0 ou 2.0 de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="367c6-131">Configuration de DNS inverse pour les ressources d’adresse IP publique n’est pas actuellement pris en charge via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="367c6-132">Actuellement, Azure ne prend en charge les DNS inversés que pour les ressources PublicIpAddress IPv4.</span><span class="sxs-lookup"><span data-stu-id="367c6-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="367c6-133">Non pris en charge pour IPv6.</span><span class="sxs-lookup"><span data-stu-id="367c6-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="367c6-134">Ajouter inverse tooan DNS existant PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="367c6-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="367c6-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="367c6-135">PowerShell</span></span>

<span data-ttu-id="367c6-136">tooadd inversée DNS tooan existant d’adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="367c6-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="367c6-137">tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :</span><span class="sxs-lookup"><span data-stu-id="367c6-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="367c6-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="367c6-138">Azure CLI 1.0</span></span>

<span data-ttu-id="367c6-139">tooadd inversée DNS tooan existant d’adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="367c6-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="367c6-140">tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :</span><span class="sxs-lookup"><span data-stu-id="367c6-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="367c6-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="367c6-141">Azure CLI 2.0</span></span>

<span data-ttu-id="367c6-142">tooadd inversée DNS tooan existant d’adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="367c6-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="367c6-143">tooadd inverser tooan DNS existant d’adresse IP publique qui n’a pas encore un nom DNS, vous devez également spécifier un nom DNS :</span><span class="sxs-lookup"><span data-stu-id="367c6-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="367c6-144">Création d’une adresse IP publique avec un DNS inversé</span><span class="sxs-lookup"><span data-stu-id="367c6-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="367c6-145">toocreate une nouvelle adresse IP publique avec la propriété DNS inverse hello déjà spécifiée :</span><span class="sxs-lookup"><span data-stu-id="367c6-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="367c6-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="367c6-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="367c6-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="367c6-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="367c6-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="367c6-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="367c6-149">Afficher DNS inversé pour des adresses IP publiques existantes</span><span class="sxs-lookup"><span data-stu-id="367c6-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="367c6-150">tooview hello la valeur configurée pour une adresse IP publique existante :</span><span class="sxs-lookup"><span data-stu-id="367c6-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="367c6-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="367c6-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="367c6-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="367c6-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="367c6-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="367c6-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="367c6-154">Suppression d’un enregistrement DNS inversé d’une adresse IP publique existante</span><span class="sxs-lookup"><span data-stu-id="367c6-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="367c6-155">tooremove une propriété DNS inversée à partir d’une adresse IP publique existante :</span><span class="sxs-lookup"><span data-stu-id="367c6-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="367c6-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="367c6-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="367c6-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="367c6-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="367c6-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="367c6-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="367c6-159">Configurer un DNS inversé pour les services Cloud</span><span class="sxs-lookup"><span data-stu-id="367c6-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="367c6-160">Cette section fournit des instructions détaillées pour la tooconfigure DNS inverse pour les Services de cloud computing dans le modèle de déploiement classique de hello, à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="367c6-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="367c6-161">Configuration du service DNS inverse pour les Services Cloud n’est pas pris en charge via hello portail Azure, Azure CLI 1.0 ou 2.0 de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="367c6-162">Ajouter des Services de cloud computing tooexisting DNS inverse</span><span class="sxs-lookup"><span data-stu-id="367c6-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="367c6-163">tooadd un tooan d’enregistrement DNS inverse existant du Service Cloud :</span><span class="sxs-lookup"><span data-stu-id="367c6-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="367c6-164">Création d’un service cloud avec un DNS inversé</span><span class="sxs-lookup"><span data-stu-id="367c6-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="367c6-165">toocreate un nouveau Service Cloud avec la propriété DNS inverse hello déjà spécifiée :</span><span class="sxs-lookup"><span data-stu-id="367c6-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="367c6-166">Affichage d’un DNS inversé pour les services cloud existants</span><span class="sxs-lookup"><span data-stu-id="367c6-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="367c6-167">tooview hello inverse la propriété DNS pour un Service Cloud existant :</span><span class="sxs-lookup"><span data-stu-id="367c6-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="367c6-168">Suppression d’un DNS inversé des services cloud existants</span><span class="sxs-lookup"><span data-stu-id="367c6-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="367c6-169">tooremove une propriété DNS inverse d’un Service Cloud existant :</span><span class="sxs-lookup"><span data-stu-id="367c6-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="367c6-170">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="367c6-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="367c6-171">Combien coûtent les enregistrements DNS inversés ?</span><span class="sxs-lookup"><span data-stu-id="367c6-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="367c6-172">Ils sont gratuits.</span><span class="sxs-lookup"><span data-stu-id="367c6-172">They're free!</span></span>  <span data-ttu-id="367c6-173">Les enregistrements DNS inversés ou les requêtes n’entraînent aucun frais supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="367c6-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="367c6-174">Sera mon résoudre les enregistrements DNS inverse de hello internet ?</span><span class="sxs-lookup"><span data-stu-id="367c6-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="367c6-175">Oui.</span><span class="sxs-lookup"><span data-stu-id="367c6-175">Yes.</span></span> <span data-ttu-id="367c6-176">Une fois que vous définissez la propriété DNS inverse hello pour votre service Azure, Azure gère toutes les délégations DNS de hello et zones DNS requis tooensure qui inverse l’enregistrement DNS est résolu pour tous les utilisateurs d’Internet.</span><span class="sxs-lookup"><span data-stu-id="367c6-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="367c6-177">Des enregistrements DNS inversés par défaut sont-ils créés pour mes services Azure ?</span><span class="sxs-lookup"><span data-stu-id="367c6-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="367c6-178">Non.</span><span class="sxs-lookup"><span data-stu-id="367c6-178">No.</span></span> <span data-ttu-id="367c6-179">Le DNS inversé est une fonctionnalité optionnelle.</span><span class="sxs-lookup"><span data-stu-id="367c6-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="367c6-180">Sans valeur par défaut des enregistrements DNS inverses sont créés, si vous ne choisissez pas tooconfigure les.</span><span class="sxs-lookup"><span data-stu-id="367c6-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="367c6-181">Quel est le format hello pour le nom de domaine complet de hello (FQDN) ?</span><span class="sxs-lookup"><span data-stu-id="367c6-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="367c6-182">Les noms de domaine complets sont spécifiés dans l’ordre chronologique et doivent se terminer par un point (par exemple, « app1.contoso.com. »).</span><span class="sxs-lookup"><span data-stu-id="367c6-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="367c6-183">Que se passe-t-il si le contrôle de validation hello pour hello inverse DNS j’ai spécifié échoue ?</span><span class="sxs-lookup"><span data-stu-id="367c6-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="367c6-184">Où hello inversée DNS validation échoue, hello tooconfigure hello inversée DNS enregistrement de l’opération échoue.</span><span class="sxs-lookup"><span data-stu-id="367c6-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="367c6-185">Corrigez la valeur DNS inverse hello en fonction des besoins et réessayez.</span><span class="sxs-lookup"><span data-stu-id="367c6-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="367c6-186">Puis-je configurer un DNS inversé pour Azure App Service ?</span><span class="sxs-lookup"><span data-stu-id="367c6-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="367c6-187">Non.</span><span class="sxs-lookup"><span data-stu-id="367c6-187">No.</span></span> <span data-ttu-id="367c6-188">DNS inverse n’est pas pris en charge pour hello du Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="367c6-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="367c6-189">Puis-je configurer plusieurs enregistrements DNS inversés pour mon service Azure ?</span><span class="sxs-lookup"><span data-stu-id="367c6-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="367c6-190">Non.</span><span class="sxs-lookup"><span data-stu-id="367c6-190">No.</span></span> <span data-ttu-id="367c6-191">Azure ne prend en charge qu’un seul enregistrement DNS inversé pour chaque service cloud Azure ou adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="367c6-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="367c6-192">Puis-je configurer un DNS inversé pour des ressources PublicIpAddress IPv6 ?</span><span class="sxs-lookup"><span data-stu-id="367c6-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="367c6-193">Non.</span><span class="sxs-lookup"><span data-stu-id="367c6-193">No.</span></span> <span data-ttu-id="367c6-194">Actuellement, Azure ne prend en charge le DNS inversé que pour les ressources PublicIpAddress IPv4.</span><span class="sxs-lookup"><span data-stu-id="367c6-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="367c6-195">Puis-je envoyer des messages électroniques tooexternal domaines à partir de mes services de calcul Azure ?</span><span class="sxs-lookup"><span data-stu-id="367c6-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="367c6-196">Non.</span><span class="sxs-lookup"><span data-stu-id="367c6-196">No.</span></span> [<span data-ttu-id="367c6-197">Les services de calcul Azure ne prennent pas en charge les domaines de tooexternal envoi des messages électroniques</span><span class="sxs-lookup"><span data-stu-id="367c6-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="367c6-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="367c6-198">Next steps</span></span>

<span data-ttu-id="367c6-199">Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="367c6-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="367c6-200">Découvrez comment trop[zone de recherche inversée hello hôte pour votre plage IP affectée par le fournisseur de services Internet dans Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="367c6-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

