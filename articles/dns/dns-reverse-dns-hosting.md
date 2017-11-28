---
title: "aaaHosting inverser les zones de recherche DNS dans le système DNS Azure | Documents Microsoft"
description: "Découvrez comment hello de toohost toouse Azure DNS inverse des zones de recherche DNS pour vos plages IP"
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
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="1bc5b-103">Hébergement de zones de recherche inversées DNS dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="1bc5b-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="1bc5b-104">Cet article explique comment toohost hello inverser les zones de recherche DNS pour vos plages IP affectées dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="1bc5b-105">plages d’adresses IP Hello représentés par la zone de recherche inversée hello doivent être assignés tooyour organisation, généralement par votre fournisseur de services Internet.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="1bc5b-106">tooconfigure la recherche DNS inversée pour Azure appartenant à l’IP adresse affectée tooyour service Azure, consultez [configurer inversée hello pour les adresses IP hello allouée tooyour service Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="1bc5b-107">Avant de lire cet article, prenez connaissance de cette [Vue d’ensemble des DNS inversés et de la prise en charge dans Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="1bc5b-108">Cet article vous assiste hello étapes toocreate votre première zone de recherche inversée DNS et un enregistrement à l’aide de hello portail Azure, Azure PowerShell, Azure CLI 1.0 ou 2.0 de CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="1bc5b-109">Créer une zone de recherche inversée DNS</span><span class="sxs-lookup"><span data-stu-id="1bc5b-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="1bc5b-110">Connectez-vous à toohello [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="1bc5b-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="1bc5b-111">Dans le menu du Hub hello, cliquez sur, puis cliquez sur **nouveau** > **mise en réseau** > puis cliquez sur **zone DNS** tooopen hello **créer Directory**panneau.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![Zone DNS](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="1bc5b-113">Sur hello **zone DNS de créer** panneau, nommez votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="1bc5b-114">nom Hello de zone de hello est spécialement conçu différemment pour les préfixes IPv4 et IPv6.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="1bc5b-115">Utilisez deux instructions hello pour [IPV4](#ipv4) ou [IPv6](#ipv6) tooname votre zone.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="1bc5b-116">Lorsque vous avez terminé cliquez **créer** zone de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1bc5b-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="1bc5b-117">IPv4</span></span>

<span data-ttu-id="1bc5b-118">nom de Hello d’une zone de recherche inversée IPv4 est basé sur une plage d’adresses IP hello qu’il représente.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="1bc5b-119">Devrait être hello suivant le format : `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="1bc5b-120">Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="1bc5b-121">Lors de la création de routage interdomaine sans classe zones de recherche DNS inversées dans DNS de Azure, vous devez utiliser un trait d’union (`-`) au lieu d’une barre oblique (« / ») dans le nom de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="1bc5b-122">Par exemple, pour hello IP plage 192.0.2.128/26, vous devez utiliser `128-26.2.0.192.in-addr.arpa` en tant que nom de la zone hello au lieu de `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="1bc5b-123">C’est pourquoi, tandis que les deux sont pris en charge par les normes DNS hello, de noms contenant la barre oblique hello zone DNS (`/`) caractères ne sont pas pris en charge dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="1bc5b-124">Hello suivant montre comment toocreate une classe C inverser la zone DNS nommé `2.0.192.in-addr.arpa` dans le système DNS Azure via hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![créer une zone DNS](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="1bc5b-126">Bonjour 'Emplacement de groupe de ressources' définit l’emplacement de hello pour le groupe de ressources hello et n’a aucun impact sur la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="1bc5b-127">emplacement des zones DNS Hello est toujours 'global' et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1bc5b-128">Hello exemples suivants montrent comment toocomplete cette tâche, avec Azure PowerShell et hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1bc5b-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1bc5b-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1bc5b-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="1bc5b-132">IPv6</span></span>

<span data-ttu-id="1bc5b-133">nom Hello d’une zone de recherche inversée IPv6 doit être Bonjour suivant du formulaire : `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="1bc5b-134">Pour obtenir des exemples, consultez [vue d’ensemble des DNS inversés et prise en charge dans Azure](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="1bc5b-135">Hello suivant montre comment toocreate une zone de recherche DNS inversée IPv6 nommé `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` dans le système DNS Azure via hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![créer une zone DNS](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="1bc5b-137">Bonjour 'Emplacement de groupe de ressources' définit l’emplacement de hello pour le groupe de ressources hello et n’a aucun impact sur la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="1bc5b-138">emplacement des zones DNS Hello est toujours 'global' et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="1bc5b-139">Hello exemples suivants montrent comment toocomplete cette tâche, avec Azure PowerShell et hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="1bc5b-141">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="1bc5b-142">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="1bc5b-143">Déléguer une zone de recherche inversée DNS</span><span class="sxs-lookup"><span data-stu-id="1bc5b-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="1bc5b-144">Après avoir créé votre zone de recherche DNS inversée, vous devez vous assurer que zone hello est déléguée à partir de la zone parente de hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="1bc5b-145">La délégation DNS Active hello résolution processus toofind hello nom serveurs DNS qui héberge la zone de recherche DNS inversée.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="1bc5b-146">Ainsi, ces serveurs tooanswer DNS inverses requêtes de noms pour les adresses IP de hello dans votre plage d’adresses.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="1bc5b-147">Pour les zones de recherche directe, processus hello de délégation de zone DNS est décrite dans [déléguer votre tooAzure de domaine DNS](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="1bc5b-148">Fonctionnement de la délégation pour les zones de recherche inversée hello identique.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="1bc5b-149">Hello seule différence est que vous avez besoin de serveurs de noms hello tooconfigure avec hello fournisseur de services Internet qui vous a fourni votre plage IP, plutôt que sur votre bureau d’enregistrement du nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="1bc5b-150">Créer un enregistrement PTR DNS</span><span class="sxs-lookup"><span data-stu-id="1bc5b-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="1bc5b-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="1bc5b-151">IPv4</span></span>

<span data-ttu-id="1bc5b-152">Hello exemple suivant vous guide hello processus de création d’un enregistrement PTR dans une zone de recherche inversée DNS dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="1bc5b-153">Pour d’autres types d’enregistrements et les enregistrements existants de toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="1bc5b-154">En haut de hello Hello **zone DNS** panneau, sélectionnez **+ enregistrer ensemble** tooopen hello **ajouter le jeu d’enregistrements** panneau.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![Zone DNS](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="1bc5b-156">Sur hello **ajouter le jeu d’enregistrements** panneau.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="1bc5b-157">Sélectionnez **PTR** à partir de l’enregistrement de hello »**Type**« menu.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="1bc5b-158">Hello nom du jeu d’enregistrements hello pour un enregistrement PTR doit reste hello toobe hello adresse IPv4 dans l’ordre inverse.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="1bc5b-159">Dans cet exemple, hello trois premiers octets sont déjà remplies en tant que partie du nom de la zone hello (.2.0.192).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="1bc5b-160">Par conséquent, seuls hello dernier octet est fournie dans le champ de nom hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="1bc5b-161">Vous pouvez par exemple nommer votre jeu d’enregistrements «**15**» pour une ressource dont l’adresse IP est 192.0.2.15.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="1bc5b-162">Bonjour »**nom de domaine**», entrez le nom de domaine complet (FQDN) hello de ressource hello à l’aide de hello IP.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="1bc5b-163">Sélectionnez **OK** bas l’enregistrement DNS de hello panneau toocreate hello hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![ajouter un jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="1bc5b-165">Hello Voici des exemples sur la façon de toocomplete cette tâche avec PowerShell et hello AzureCLI :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="1bc5b-167">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="1bc5b-168">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="1bc5b-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="1bc5b-169">IPv6</span></span>

<span data-ttu-id="1bc5b-170">Bonjour à l’exemple suivant vous guide tout au long des processus de hello de création d’enregistrement « PTR ».</span><span class="sxs-lookup"><span data-stu-id="1bc5b-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="1bc5b-171">Pour d’autres types d’enregistrements et les enregistrements existants de toomodify, consultez [enregistrements DNS de gérer et jeux d’enregistrements à l’aide de portail Azure hello](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="1bc5b-172">En haut de hello Hello **Panneau de zone DNS**, sélectionnez **+ enregistrer ensemble** tooopen hello **ajouter le jeu d’enregistrements** panneau.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![panneau zone DNS](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="1bc5b-174">Sur hello **ajouter le jeu d’enregistrements** panneau.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="1bc5b-175">Sélectionnez **PTR** à partir de l’enregistrement de hello »**Type**« menu.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="1bc5b-176">Hello nom du jeu d’enregistrements hello pour un enregistrement PTR doit reste hello toobe hello adresse IPv6 dans l’ordre inverse.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="1bc5b-177">Il ne doit inclure aucune compression des zéros.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-177">It must not include any zero compression.</span></span> <span data-ttu-id="1bc5b-178">Dans cet exemple, hello 64 premiers bits de hello IPv6 figurent déjà dans le cadre du nom de la zone hello (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="1bc5b-179">Par conséquent, seuls hello 64 derniers bits sont fournis dans le champ de nom hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="1bc5b-180">Hello dernière 64 bits de l’adresse IP de hello sont entrés dans l’ordre inverse, en utilisant un point comme séparateur hello entre chaque nombre hexadécimal.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="1bc5b-181">Par exemple, vous pouvez nommer votre jeu d’enregistrements «**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**» pour une ressource dont l’adresse IP est 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="1bc5b-182">Bonjour »**nom de domaine**», entrez le nom de domaine complet (FQDN) hello de ressource hello à l’aide de hello IP.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="1bc5b-183">Sélectionnez **OK** bas l’enregistrement DNS de hello panneau toocreate hello hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![ajouter un panneau du jeu d’enregistrements](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="1bc5b-185">Hello Voici des exemples sur la façon de toocomplete cette tâche avec PowerShell et hello AzureCLI :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="1bc5b-187">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="1bc5b-188">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="1bc5b-189">Afficher des Enregistrements</span><span class="sxs-lookup"><span data-stu-id="1bc5b-189">View Records</span></span>

<span data-ttu-id="1bc5b-190">les enregistrements de hello tooview vous avez créé, accédez à zone DNS de tooyour Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="1bc5b-191">Bonjour partie basse de hello **zone DNS** panneau, vous pouvez voir des enregistrements hello pour la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="1bc5b-192">Vous devez voir hello par défaut enregistrements NS et SOA, qui sont créées dans chaque zone, ainsi que les nouveaux enregistrements que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="1bc5b-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="1bc5b-193">IPv4</span></span>

<span data-ttu-id="1bc5b-194">Panneau zone DNS, affichant les enregistrements PTR de IPv4 :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="1bc5b-196">Hello exemples suivants montrent comment tooview hello PTR enregistre à l’aide de PowerShell ou hello CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1bc5b-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1bc5b-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="1bc5b-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="1bc5b-200">IPv6</span></span>

<span data-ttu-id="1bc5b-201">Panneau zone DNS, affichant les enregistrements PTR de IPv6 :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![panneau zone DNS](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="1bc5b-203">Hello Voici des exemples sur la modification des enregistrements tooview hello avec PowerShell et hello AzureCLI :</span><span class="sxs-lookup"><span data-stu-id="1bc5b-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="1bc5b-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bc5b-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="1bc5b-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="1bc5b-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1bc5b-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="1bc5b-207">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="1bc5b-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="1bc5b-208">Puis-je héberger des zones de recherche inversée DNS pour les blocs IP attribués par mon fournisseur de services Internet sur Azure DNS ?</span><span class="sxs-lookup"><span data-stu-id="1bc5b-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="1bc5b-209">Oui.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-209">Yes.</span></span> <span data-ttu-id="1bc5b-210">Hébergeant des zones de recherche inversée (ARPA) hello pour vos propres plages IP dans le système DNS Azure est entièrement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="1bc5b-211">Créer une zone de recherche inversée hello dans le système DNS Azure comme expliqué dans cet article, puis de travailler avec votre fournisseur de services Internet trop[délégué hello zone](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="1bc5b-212">Vous pouvez ensuite gérer les enregistrements PTR hello pour chaque recherche inversée Bonjour même façon que d’autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="1bc5b-213">Combien coûte l’hébergement de ma zone de recherche DNS inversée ?</span><span class="sxs-lookup"><span data-stu-id="1bc5b-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="1bc5b-214">Zone de recherche DNS inversée hello d’hébergement pour votre bloc IP affectée par le fournisseur de services Internet dans DNS Azure est facturée au [taux Azure DNS standard](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="1bc5b-215">Puis-je héberger des zones de recherche inversée DNS pour les adresses IPv4 et IPv6 dans Azure DNS ?</span><span class="sxs-lookup"><span data-stu-id="1bc5b-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="1bc5b-216">Oui.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-216">Yes.</span></span> <span data-ttu-id="1bc5b-217">Cet article explique comment toocreate à la fois IPv4 et IPv6 de zones de recherche DNS dans Azure DNS inversée.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="1bc5b-218">Puis-je importer une zone de recherche DNS inversée existante ?</span><span class="sxs-lookup"><span data-stu-id="1bc5b-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="1bc5b-219">Oui.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-219">Yes.</span></span> <span data-ttu-id="1bc5b-220">Vous pouvez utiliser des zones DNS existantes de hello CLI d’Azure tooimport dans le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="1bc5b-221">Cela fonctionne pour les zones de recherche directe et des zones de recherche inversée.</span><span class="sxs-lookup"><span data-stu-id="1bc5b-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="1bc5b-222">Pour plus d’informations, consultez [importer et exporter un fichier de zone DNS à l’aide de CLI d’Azure hello](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bc5b-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bc5b-223">Next steps</span></span>

<span data-ttu-id="1bc5b-224">Pour plus d’informations sur le DNS inversé, consultez [Recherche DNS inversée sur Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="1bc5b-225">Découvrez comment trop[gère les enregistrements DNS inverses pour vos services Azure](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="1bc5b-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
