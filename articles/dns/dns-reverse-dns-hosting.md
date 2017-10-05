---
title: "Hébergement de zones de recherche inversées DNS dans Azure DNS | Microsoft Docs"
description: "Découvrez comment utiliser Azure DNS pour héberger les zones de recherche inversées DNS pour vos plages d’adresses IP"
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="1d1ab-103">Hébergement de zones de recherche inversées DNS dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="1d1ab-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="1d1ab-104">Cet article explique comment héberger les zones de recherche inversées DNS pour vos plages d’adresses IP attribuées dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="1d1ab-105">En règle générale, votre fournisseur de services Internet attribue à votre organisation les plages d’adresses IP représentées par la zone de recherche inversée.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="1d1ab-106">Pour configurer un DNS inversé pour une adresse IP gérée par Azure ayant été attribuée à votre service Azure, consultez [configurer la recherche inversée pour les adresses IP allouées à votre service Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="1d1ab-107">Avant de lire cet article, prenez connaissance de cette [Vue d’ensemble des DNS inversés et de la prise en charge dans Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="1d1ab-108">Cet article vous indique la procédure à suivre pour créer votre première zone de recherche inversée DNS et votre premier enregistrement à l’aide du portail Azure, d’Azure PowerShell, d’Azure CLI 1.0 ou d’Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="1d1ab-109">Créer une zone de recherche inversée DNS</span><span class="sxs-lookup"><span data-stu-id="1d1ab-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="1d1ab-110">Connectez-vous au [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1d1ab-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="1d1ab-111">Dans le menu Hub, cliquez sur **Nouveau** > **Mise en réseau** >, puis cliquez sur **Zone DNS** pour ouvrir le panneau **Créer une zone DNS** .</span><span class="sxs-lookup"><span data-stu-id="1d1ab-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![Zone DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="1d1ab-113">Dans le panneau **Créer une zone DNS** , nommez votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="1d1ab-114">Le nom de la zone a été conçu différemment pour les préfixes IPv4 et IPv6.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="1d1ab-115">Utilisez les instructions relatives à [IPV4](#ipv4) ou à [IPv6](#ipv6) pour nommer votre zone.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="1d1ab-116">Lorsque vous avez terminé cliquez sur **Créer** pour créer la zone.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1d1ab-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="1d1ab-117">IPv4</span></span>

<span data-ttu-id="1d1ab-118">Le nom d’une zone de recherche inversée IPv4 est basé sur la plage d’adresses IP qu’il représente.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="1d1ab-119">Il doit se présenter sous la forme suivante : `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="1d1ab-120">Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="1d1ab-121">Lorsque vous créez des zones de recherche inversées DNS sans classe dans Azure DNS, vous devez utiliser un trait d’union (`-`) à la place d’une barre oblique (« / ») dans le nom de zone.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="1d1ab-122">Par exemple, pour la plage d’adresses IP 192.0.2.1.128/26, vous devez utiliser `128-26.2.0.192.in-addr.arpa` comme nom de zone à la place de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="1d1ab-123">En effet, bien qu’ils soient tous deux pris en charge par les normes DNS, les noms de zones DNS contenant une barre oblique (`/`) ne sont pas pris en charge dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="1d1ab-124">L’exemple suivant montre comment créer une zone DNS inversée de « Classe C » nommée `2.0.192.in-addr.arpa` dans Azure DNS via le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![Créer une zone DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="1d1ab-126">L’ « emplacement du Groupe de ressources » définit l’emplacement du groupe de ressources et n’a aucun impact sur la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="1d1ab-127">L’emplacement de la zone DNS est toujours « global » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1d1ab-128">Les exemples suivants montrent comment effectuer cette tâche à l’aide d’Azure PowerShell et Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1d1ab-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1d1ab-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1d1ab-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="1d1ab-132">IPv6</span></span>

<span data-ttu-id="1d1ab-133">Le nom d’une zone de recherche inversée IPv6 doit se présenter sous la forme suivante : `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="1d1ab-134">Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="1d1ab-135">L’exemple suivant montre comment créer une zone de recherche inversée DNS IPv6 nommée `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` dans Azure DNS via le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![créer une zone DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="1d1ab-137">L’ « emplacement du Groupe de ressources » définit l’emplacement du groupe de ressources et n’a aucun impact sur la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="1d1ab-138">L’emplacement de la zone DNS est toujours « global » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1d1ab-139">Les exemples suivants montrent comment effectuer cette tâche à l’aide d’Azure PowerShell et Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="1d1ab-141">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="1d1ab-142">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="1d1ab-143">Déléguer une zone de recherche inversée DNS</span><span class="sxs-lookup"><span data-stu-id="1d1ab-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="1d1ab-144">Après la création de votre zone de recherche inversée DNS, vous devez vous assurer que la zone est déléguée depuis la zone parente.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="1d1ab-145">La délégation DNS permet au processus de résolution de nom DNS de trouver les serveurs de noms hébergeant votre zone de recherche inversée DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="1d1ab-146">Ainsi les serveurs de noms peuvent répondre aux requêtes DNS inverses pour les adresses IP de votre plage d’adresses.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="1d1ab-147">Pour les zones de recherche directe, le processus de délégation de zone DNS est décrit dans [Déléguer votre domaine à Azure DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="1d1ab-148">La délégation pour les zones de recherche inversée fonctionne de façon similaire.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="1d1ab-149">La seule différence est que vous devez configurer les serveurs de noms avec le fournisseur de services Internet qui a fourni votre plage d’adresses IP, plutôt qu’avec votre bureau d'enregistrement de noms de domaine.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="1d1ab-150">Créer un enregistrement PTR DNS</span><span class="sxs-lookup"><span data-stu-id="1d1ab-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="1d1ab-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="1d1ab-151">IPv4</span></span>

<span data-ttu-id="1d1ab-152">L’exemple suivant vous guide tout au long du processus de création d’un enregistrement PTR dans une zone DNS inversée dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="1d1ab-153">Pour découvrir d’autres types d’enregistrements et pour modifier les enregistrements existants, consultez [Gestion d’enregistrements et de jeux d’enregistrements DNS à l’aide du portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="1d1ab-154">En haut du panneau **Zone DNS**, sélectionnez **+ Jeu d’enregistrements** pour ouvrir le panneau **Ajouter un jeu d’enregistrements**.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![Zone DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="1d1ab-156">Sur le panneau **Ajouter un jeu d’enregistrements** .</span><span class="sxs-lookup"><span data-stu-id="1d1ab-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="1d1ab-157">Sélectionnez **PTR** depuis le menu «**Type**» d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="1d1ab-158">Le nom du jeu d’enregistrements d’un enregistrement PTR doit correspondre à la fin de l’adresse IPv4 dans l’ordre inverse.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="1d1ab-159">Dans cet exemple, les trois premiers octets figurent déjà dans le nom de la zone (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="1d1ab-160">Par conséquent, seul le dernier octet figure dans le champ nom.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="1d1ab-161">Vous pouvez par exemple nommer votre jeu d’enregistrements «**15**» pour une ressource dont l’adresse IP est 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="1d1ab-162">Dans le champ «**Nom de domaine**», entrez le nom de domaine complet (FQDN) de la ressource à l’aide de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="1d1ab-163">Sélectionnez **OK** en bas du panneau pour créer l’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![ajouter un jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="1d1ab-165">Les exemples suivants montrent comment effectuer cette tâche à l’aide d’Azure PowerShell et d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="1d1ab-167">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="1d1ab-168">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="1d1ab-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="1d1ab-169">IPv6</span></span>

<span data-ttu-id="1d1ab-170">L’exemple suivant vous guide tout au long du processus de création d’un nouvel enregistrement « PTR ».</span><span class="sxs-lookup"><span data-stu-id="1d1ab-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="1d1ab-171">Pour découvrir d’autres types d’enregistrements et pour modifier les enregistrements existants, consultez [Gestion d’enregistrements et de jeux d’enregistrements DNS à l’aide du portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="1d1ab-172">En haut du **panneau zone DNS**, sélectionnez **+ Jeu d’enregistrements** pour ouvrir le panneau **Ajouter un jeu d’enregistrements**.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![panneau zone DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="1d1ab-174">Sur le panneau **Ajouter un jeu d’enregistrements** .</span><span class="sxs-lookup"><span data-stu-id="1d1ab-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="1d1ab-175">Sélectionnez **PTR** depuis le menu «**Type**» d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="1d1ab-176">Le nom du jeu d’enregistrements d’un enregistrement PTR doit correspondre à la fin de l’adresse IPv6 dans l’ordre inverse.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="1d1ab-177">Il ne doit inclure aucune compression des zéros.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-177">It must not include any zero compression.</span></span> <span data-ttu-id="1d1ab-178">Dans cet exemple, les 64 premiers bits de l’IPv6 figurent déjà dans le cadre du nom de zone (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="1d1ab-179">Par conséquent, seuls les 64 derniers bits figurent dans le champ nom.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="1d1ab-180">Les 64 derniers bits de l’adresse IP sont entrés dans l’ordre inverse, à l’aide d’un point comme séparateur entre chaque nombre hexadécimal.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="1d1ab-181">Par exemple, vous pouvez nommer votre jeu d’enregistrements «**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**» pour une ressource dont l’adresse IP est 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="1d1ab-182">Dans le champ «**Nom de domaine**», entrez le nom de domaine complet (FQDN) de la ressource à l’aide de l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="1d1ab-183">Sélectionnez **OK** en bas du panneau pour créer l’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![ajouter un panneau du jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="1d1ab-185">Les exemples suivants montrent comment effectuer cette tâche à l’aide d’Azure PowerShell et d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="1d1ab-187">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="1d1ab-188">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="1d1ab-189">Afficher des Enregistrements</span><span class="sxs-lookup"><span data-stu-id="1d1ab-189">View Records</span></span>

<span data-ttu-id="1d1ab-190">Pour afficher les enregistrements que vous avez créés, accédez à votre zone DNS dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="1d1ab-191">Vous pouvez afficher les enregistrements de la zone DNS dans la partie inférieure du panneau **zone DNS** .</span><span class="sxs-lookup"><span data-stu-id="1d1ab-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="1d1ab-192">Vous devez voir les enregistrements NS et SOA par défaut, qui sont créés dans chaque zone, ainsi que les nouveaux enregistrements que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1d1ab-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="1d1ab-193">IPv4</span></span>

<span data-ttu-id="1d1ab-194">Panneau zone DNS, affichant les enregistrements PTR de IPv4 :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="1d1ab-196">Les exemples suivants montrent comment afficher les enregistrements PTR à l’aide de PowerShell ou d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1d1ab-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1d1ab-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1d1ab-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="1d1ab-200">IPv6</span></span>

<span data-ttu-id="1d1ab-201">Panneau zone DNS, affichant les enregistrements PTR de IPv6 :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="1d1ab-203">Les exemples suivants montrent comment afficher les enregistrements à l’aide de PowerShell et d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="1d1ab-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1d1ab-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d1ab-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1d1ab-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1d1ab-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1d1ab-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="1d1ab-207">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1d1ab-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="1d1ab-208">Puis-je héberger des zones de recherche inversée DNS pour les blocs IP attribués par mon fournisseur de services Internet sur Azure DNS ?</span><span class="sxs-lookup"><span data-stu-id="1d1ab-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="1d1ab-209">Oui.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-209">Yes.</span></span> <span data-ttu-id="1d1ab-210">L’hébergement des zones de recherche inversée pour vos propres plages d’adresses IP dans Azure DNS est entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="1d1ab-211">Créez la zone de recherche inversée dans Azure DNS comme expliqué dans cet article, puis travailler avec votre fournisseur de services Internet pour [déléguer la zone](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="1d1ab-212">Vous pouvez ensuite gérer les enregistrements PTR pour chaque recherche inversée de la même façon que d’autres types d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="1d1ab-213">Combien coûte l’hébergement de ma zone de recherche DNS inversée ?</span><span class="sxs-lookup"><span data-stu-id="1d1ab-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="1d1ab-214">L’hébergement de la zone de recherche inversée DNS pour le bloc IP attribué par votre fournisseur de services Internet dans Azure DNS est facturé selon les [tarifs Azure DNS standard](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="1d1ab-215">Puis-je héberger des zones de recherche inversée DNS pour les adresses IPv4 et IPv6 dans Azure DNS ?</span><span class="sxs-lookup"><span data-stu-id="1d1ab-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="1d1ab-216">Oui.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-216">Yes.</span></span> <span data-ttu-id="1d1ab-217">Cet article explique comment créer des zones de recherche DNS IPv4 et IPv6 dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="1d1ab-218">Puis-je importer une zone de recherche DNS inversée existante ?</span><span class="sxs-lookup"><span data-stu-id="1d1ab-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="1d1ab-219">Oui.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-219">Yes.</span></span> <span data-ttu-id="1d1ab-220">Vous pouvez utiliser Azure CLI pour importer des zones DNS existantes dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="1d1ab-221">Cela fonctionne pour les zones de recherche directe et des zones de recherche inversée.</span><span class="sxs-lookup"><span data-stu-id="1d1ab-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="1d1ab-222">Pour plus d’informations, consultez [Importer et exporter un fichier de zone DNS à l’aide d’Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d1ab-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d1ab-223">Next steps</span></span>

<span data-ttu-id="1d1ab-224">Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="1d1ab-225">Découvrez comment [gérer des enregistrements DNS inversés pour vos services Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1d1ab-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
