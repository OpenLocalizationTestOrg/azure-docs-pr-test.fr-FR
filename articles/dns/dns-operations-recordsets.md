---
title: "Gérer les enregistrements DNS dans Azure DNS avec Azure PowerShell | Microsoft Docs"
description: "Gestion des jeux d'enregistrements DNS et des enregistrements dans Azure DNS lorsque votre domaine est hébergé dans Azure DNS. Toutes les commandes PowerShell pour les opérations sur les jeux d'enregistrements et les enregistrements."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="0b293-104">Gérer les enregistrements et jeux d’enregistrements DNS dans Azure DNS à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b293-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b293-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0b293-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="0b293-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="0b293-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="0b293-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0b293-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="0b293-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b293-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="0b293-109">Cet article explique comment gérer les enregistrements DNS pour votre zone DNS avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b293-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="0b293-110">Vous pouvez également gérer les enregistrements DNS à l’aide de l’[interface de ligne de commande Azure (Azure CLI)](dns-operations-recordsets-cli.md) multiplateforme ou via le [portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0b293-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="0b293-111">Les exemples de cet article supposent que vous avez déjà [installé Azure PowerShell, ouvert une session et créé une zone DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="0b293-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="0b293-112">Introduction</span><span class="sxs-lookup"><span data-stu-id="0b293-112">Introduction</span></span>

<span data-ttu-id="0b293-113">Avant de créer des enregistrements DNS dans Azure DNS, vous devez comprendre comment Azure DNS organise les enregistrements DNS en jeux d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="0b293-114">Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0b293-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="0b293-115">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="0b293-115">Create a new DNS record</span></span>

<span data-ttu-id="0b293-116">Si votre nouvel enregistrement porte le même nom et est du même type qu’un enregistrement existant, vous devez l’[ajouter au jeu d’enregistrements existant](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="0b293-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="0b293-117">En revanche, si le nom et le type de votre nouvel enregistrement diffèrent de ceux de tous les enregistrements existants, vous devez créer un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="0b293-118">Créer des enregistrements « A » dans un nouveau jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="0b293-119">Vous pouvez utiliser l’applet de commande `New-AzureRmDnsRecordSet` pour créer des jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="0b293-120">Lors de la création d’un jeu d’enregistrements, vous devez en spécifier le nom, la zone et la durée de vie (TTL), ainsi que les enregistrements à créer et leur type.</span><span class="sxs-lookup"><span data-stu-id="0b293-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="0b293-121">Les paramètres pour ajouter des enregistrements à un jeu d'enregistrements varient selon le type de jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="0b293-122">Par exemple, si vous utilisez un jeu d’enregistrements de type « A », vous devez spécifier l’adresse IP à l’aide du paramètre `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="0b293-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="0b293-123">D’autres paramètres sont utilisés pour d’autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="0b293-124">Pour plus d’informations, voir les [autres exemples de types d’enregistrements](#additional-record-type-examples).</span><span class="sxs-lookup"><span data-stu-id="0b293-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="0b293-125">L’exemple suivant crée un jeu d’enregistrements avec le nom relatif « www » dans la zone DNS « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="0b293-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="0b293-126">Le nom complet du jeu d’enregistrements est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="0b293-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="0b293-127">Le type d’enregistrement est « A » et la durée de vie est de 3 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="0b293-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="0b293-128">Le jeu d’enregistrements ne contient qu’un seul enregistrement, dont l’adresse IP est « 1.2.3.4 ».</span><span class="sxs-lookup"><span data-stu-id="0b293-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="0b293-129">Pour créer un jeu d’enregistrements à l’apex (au sommet) d’une zone (en l’occurrence, « contoso.com »), utilisez le nom de jeu d’enregistrements « @ » (guillemets non compris) :</span><span class="sxs-lookup"><span data-stu-id="0b293-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="0b293-130">Si vous devez créer un jeu d’enregistrements contenant plusieurs enregistrements, commencez par créer un groupe local, ajoutez les enregistrements, puis transmettez le groupe à `New-AzureRmDnsRecordSet` comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b293-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="0b293-131">Vous pouvez utiliser des [métadonnées de jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) pour associer les données spécifiques de l’application à chaque jeu d’enregistrements, comme paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="0b293-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="0b293-132">L’exemple suivant montre comment créer un jeu d’enregistrements avec deux entrées de métadonnées, « dept=finance » et « environment=production ».</span><span class="sxs-lookup"><span data-stu-id="0b293-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="0b293-133">Azure DNS prend également en charge les jeux d’enregistrements « vides », qui peuvent servir d’espaces réservés pour réserver un nom DNS avant de créer des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="0b293-134">Les jeux d’enregistrements vides sont visibles dans le volet de contrôle d’Azure DNS, mais n’apparaissent pas sur les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="0b293-135">L’exemple suivant crée un jeu d’enregistrements vide :</span><span class="sxs-lookup"><span data-stu-id="0b293-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="0b293-136">Créer des enregistrements d’autres types</span><span class="sxs-lookup"><span data-stu-id="0b293-136">Create records of other types</span></span>

<span data-ttu-id="0b293-137">À présent que nous avons vu en détail comment créer des enregistrements de type « A », les exemples suivants montrent comment créer des enregistrements d’autres types pris en charge par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="0b293-138">Dans chaque cas, nous montrons comment créer un jeu d’enregistrements contenant un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="0b293-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="0b293-139">Vous pouvez adapter les exemples précédents pour les enregistrements de type « A » afin de créer des jeux d’enregistrements d’autres types contenant plusieurs enregistrements avec des métadonnées, ou des jeux d’enregistrements vides.</span><span class="sxs-lookup"><span data-stu-id="0b293-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="0b293-140">Nous ne donnons pas d’exemple de création de jeu d’enregistrements SOA (Architecture orientée services), car les enregistrements de ce type sont créés et supprimés avec chaque zone DNS, et ne peuvent pas l’être séparément.</span><span class="sxs-lookup"><span data-stu-id="0b293-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="0b293-141">En revanche, vous pouvez [modifier les enregistrements SOA en procédant de la manière décrite dans un exemple plus loin](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="0b293-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="0b293-142">Créer un jeu d’enregistrements AAAA avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="0b293-143">Créer un jeu d’enregistrements CNAME avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="0b293-144">Les normes DNS n’autorisent pas la présence d’enregistrements CNAME ou de jeux d’enregistrements contenant plusieurs enregistrements à l’apex (sommet) d’une zone (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="0b293-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="0b293-145">Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="0b293-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="0b293-146">Créer un jeu d’enregistrements MX avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="0b293-147">Dans cet exemple, nous utilisons le nom de jeu d’enregistrements « @ » pour créer un enregistrement MX à l’apex de la zone (dans ce cas, « contoso.com »).</span><span class="sxs-lookup"><span data-stu-id="0b293-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="0b293-148">Créer un jeu d’enregistrements NS avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="0b293-149">Créer un jeu d’enregistrements PTR avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="0b293-150">Dans ce cas, « my-arpa-zone.com » indique la zone ARPA de recherche inversée représentant votre plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="0b293-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="0b293-151">Chaque enregistrement PTR défini dans cette zone correspond à une adresse IP figurant dans cette plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="0b293-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="0b293-152">Le nom d’enregistrement « 10 » est le dernier octet de l’adresse IP dans cette plage d’IP représentée par cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="0b293-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="0b293-153">Créer un jeu d’enregistrements SRV avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="0b293-154">Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez le  *\_service* et le  *\_protocole* dans le nom du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="0b293-155">Il est inutile d’inclure « @ » dans le nom du jeu d’enregistrements lors de la création d’un jeu d’enregistrements SRV à l’apex de la zone.</span><span class="sxs-lookup"><span data-stu-id="0b293-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="0b293-156">Créer un jeu d’enregistrements TXT avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="0b293-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="0b293-157">L’exemple suivant montre comment créer un enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="0b293-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="0b293-158">Pour plus d’informations sur la longueur maximale de chaîne prise en charge dans les enregistrements TXT, voir [Enregistrements TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="0b293-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="0b293-159">Obtention d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-159">Get a record set</span></span>

<span data-ttu-id="0b293-160">Pour récupérer un jeu d’enregistrements existant, utilisez `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="0b293-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="0b293-161">Cette applet de commande renvoie un objet local représentant le jeu d’enregistrements dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="0b293-162">Comme avec l’applet de commande `New-AzureRmDnsRecordSet`, le nom du jeu d’enregistrements doit être un nom *relatif*, c’est-à-dire qu’il ne doit pas contenir le nom de la zone.</span><span class="sxs-lookup"><span data-stu-id="0b293-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="0b293-163">Vous devez également spécifier le type d’enregistrement et la zone contenant le jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="0b293-164">L’exemple suivant montre comment récupérer un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="0b293-165">Dans cet exemple, la zone est spécifiée à l’aide des paramètres `-ZoneName` et `-ResourceGroupName`.</span><span class="sxs-lookup"><span data-stu-id="0b293-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="0b293-166">Vous pouvez également spécifier la zone à l’aide d’un objet zone, transmis en utilisant le `-Zone` paramètre.</span><span class="sxs-lookup"><span data-stu-id="0b293-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="0b293-167">Liste des jeux d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-167">List record sets</span></span>

<span data-ttu-id="0b293-168">Vous pouvez également utiliser l’applet de commande `Get-AzureRmDnsZone` pour répertorier les jeux d’enregistrements présents dans une zone, en omettant les paramètres `-Name` et/ou `-RecordType`.</span><span class="sxs-lookup"><span data-stu-id="0b293-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="0b293-169">L’exemple suivant retourne tous les jeux d’enregistrements présents dans la zone :</span><span class="sxs-lookup"><span data-stu-id="0b293-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="0b293-170">L’exemple suivant montre comment récupérer tous les jeux d’enregistrements d’un type donné en spécifiant le type d’enregistrement, mais en omettant le nom du jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0b293-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="0b293-171">Pour récupérer parmi les types d’enregistrements tous les jeux d’enregistrements portant un nom spécifique, vous devez récupérer tous les jeux d’enregistrements, puis filtrer les résultats :</span><span class="sxs-lookup"><span data-stu-id="0b293-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="0b293-172">Dans tous les exemples ci-dessus, vous pouvez spécifier la zone à l’aide des paramètres `-ZoneName` et `-ResourceGroupName` (comme indiqué), ou en spécifiant un objet zone :</span><span class="sxs-lookup"><span data-stu-id="0b293-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="0b293-173">Ajouter un enregistrement à un jeu d’enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="0b293-173">Add a record to an existing record set</span></span>

<span data-ttu-id="0b293-174">Pour ajouter un enregistrement à un jeu d’enregistrements existant, suivez les trois étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b293-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="0b293-175">Obtenez le jeu d’enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="0b293-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="0b293-176">Ajoutez le nouvel enregistrement au jeu d’enregistrements local.</span><span class="sxs-lookup"><span data-stu-id="0b293-176">Add the new record to the local record set.</span></span> <span data-ttu-id="0b293-177">Cette opération se fait hors connexion.</span><span class="sxs-lookup"><span data-stu-id="0b293-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="0b293-178">Validez la modification sur le service Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="0b293-179">L’applet de commande `Set-AzureRmDnsRecordSet` *remplace* le jeu d’enregistrements existant dans Azure DNS (et tous les enregistrements qu’il contient) par le jeu d’enregistrements spécifié.</span><span class="sxs-lookup"><span data-stu-id="0b293-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="0b293-180">Des [vérifications ETag](dns-zones-records.md#etags) permettent d’éviter les conflits de modifications simultanées.</span><span class="sxs-lookup"><span data-stu-id="0b293-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="0b293-181">Le commutateur facultatif `-Overwrite` permet de supprimer ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="0b293-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="0b293-182">Vous pouvez également *canaliser* cette séquence d’opérations, c’est-à-dire transmettre l’objet jeu d’enregistrements en utilisant le canal plutôt qu’en le transmettant en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="0b293-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="0b293-183">Les exemples ci-dessus montrent comment ajouter un enregistrement « A » à un jeu existant d’enregistrements de type « A ».</span><span class="sxs-lookup"><span data-stu-id="0b293-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="0b293-184">Une séquence similaire d’opérations est utilisée pour ajouter des enregistrements à des jeux d’enregistrements d’autres types, en remplaçant le paramètre `-Ipv4Address` de l’applet de commande `Add-AzureRmDnsRecordConfig` par d’autres paramètres spécifiques de chaque type d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="0b293-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="0b293-185">Les paramètres pour chaque type d’enregistrement sont identiques à ceux de l’applet de commande `New-AzureRmDnsRecordConfig`, comme indiqué dans les [autres exemples de types d’enregistrements](#additional-record-type-examples) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0b293-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="0b293-186">Les jeux d’enregistrements de type « CNAME » ou « SOA » ne peuvent pas contenir plusieurs enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="0b293-187">Cette contrainte résulte des normes DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="0b293-188">Il ne s’agit pas d’une limitation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="0b293-189">Suppression d’un enregistrement d’un jeu d'enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="0b293-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="0b293-190">Le processus de suppression d’un enregistrement d’un jeu d’enregistrements est similaire au processus d’ajout d’un enregistrement à un jeu d’enregistrements existant :</span><span class="sxs-lookup"><span data-stu-id="0b293-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="0b293-191">Obtenez le jeu d’enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="0b293-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="0b293-192">Supprimez l’enregistrement de l’objet jeu d’enregistrements local.</span><span class="sxs-lookup"><span data-stu-id="0b293-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="0b293-193">Cette opération se fait hors connexion.</span><span class="sxs-lookup"><span data-stu-id="0b293-193">This is an off-line operation.</span></span> <span data-ttu-id="0b293-194">L’enregistrement à supprimer doit correspondre exactement à un enregistrement existant relativement à tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="0b293-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="0b293-195">Validez la modification sur le service Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="0b293-196">Utilisez le commutateur facultatif `-Overwrite` pour désactiver les [vérifications ETag](dns-zones-records.md#etags) des modifications simultanées.</span><span class="sxs-lookup"><span data-stu-id="0b293-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="0b293-197">La séquence utilisée ci-dessus pour supprimer le dernier enregistrement d’un jeu d’enregistrements n’a pas pour effet de supprimer celui-ci, mais de le laisser vide.</span><span class="sxs-lookup"><span data-stu-id="0b293-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="0b293-198">Pour supprimer entièrement un jeu d’enregistrements, voir [Supprimer un jeu d’enregistrements](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="0b293-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="0b293-199">Comme pour l’ajout d’enregistrements à un jeu d’enregistrements, vous pouvez canaliser la séquence des opérations de suppression d’un jeu d’enregistrements comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b293-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="0b293-200">Différents types d’enregistrements sont pris en charge en transmettant les paramètres spécifiques du type approprié à `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="0b293-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="0b293-201">Les paramètres pour chaque type d’enregistrement sont identiques à ceux de l’applet de commande `New-AzureRmDnsRecordConfig`, comme indiqué dans les [autres exemples de types d’enregistrements](#additional-record-type-examples) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0b293-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="0b293-202">Modifier un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-202">Modify an existing record set</span></span>

<span data-ttu-id="0b293-203">Pour modifier un jeu d’enregistrements, procédez de la même manière que pour y ajouter ou en supprimer des enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0b293-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="0b293-204">Récupérez le jeu d’enregistrements existant en utilisant `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="0b293-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="0b293-205">Modifiez l’objet jeu d’enregistrements local à l’aide des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b293-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="0b293-206">ajout ou suppression d’enregistrements ;</span><span class="sxs-lookup"><span data-stu-id="0b293-206">Adding or removing records</span></span>
    * <span data-ttu-id="0b293-207">modification des paramètres d’enregistrements existants ;</span><span class="sxs-lookup"><span data-stu-id="0b293-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="0b293-208">modification des métadonnées et de la durée de vie (TTL) du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="0b293-209">Validez vos modifications en utilisant l’applet de commande `Set-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="0b293-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="0b293-210">Celle-ci *remplace* le jeu d’enregistrement existant dans Azure DNS par le jeu d’enregistrements spécifié.</span><span class="sxs-lookup"><span data-stu-id="0b293-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="0b293-211">Lorsque vous utilisez l’applet de commande `Set-AzureRmDnsRecordSet`, des [vérifications ETag](dns-zones-records.md#etags) permettent d’éviter les conflits de modifications simultanées.</span><span class="sxs-lookup"><span data-stu-id="0b293-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="0b293-212">Le commutateur facultatif `-Overwrite` permet de supprimer ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="0b293-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="0b293-213">Pour mettre à jour un enregistrement dans un jeu d’enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="0b293-213">To update a record in an existing record set</span></span>

<span data-ttu-id="0b293-214">Dans cet exemple, nous modifions l’adresse IP d’un enregistrement « A » existant :</span><span class="sxs-lookup"><span data-stu-id="0b293-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="0b293-215">Pour modifier un enregistrement SOA</span><span class="sxs-lookup"><span data-stu-id="0b293-215">To modify an SOA record</span></span>

<span data-ttu-id="0b293-216">Vous ne pouvez pas ajouter ou supprimer d’enregistrements dans le jeu d’enregistrements SOA créé automatiquement à l’apex de la zone (`-Name "@"`, guillemets compris).</span><span class="sxs-lookup"><span data-stu-id="0b293-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="0b293-217">Vous pouvez cependant modifier les paramètres dans l’enregistrement SOA (à l’exception de « l’hôte ») et pendant la durée de vie du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="0b293-218">L’exemple suivant montre comment modifier la propriété *Email* de l’enregistrement SOA :</span><span class="sxs-lookup"><span data-stu-id="0b293-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="0b293-219">Pour modifier des enregistrements NS à l’apex de la zone</span><span class="sxs-lookup"><span data-stu-id="0b293-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="0b293-220">Le jeu d’enregistrements NS à l’apex de la zone est créé automatiquement avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="0b293-221">Il contient les noms des serveurs de noms Azure DNS attribués à la zone.</span><span class="sxs-lookup"><span data-stu-id="0b293-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="0b293-222">Vous pouvez ajouter des serveurs de noms supplémentaires à ce jeu d’enregistrements NS, pour prendre en charge le co-hébergement de domaines avec plusieurs fournisseurs DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="0b293-223">Vous pouvez également modifier la durée de vie et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="0b293-224">Toutefois, vous ne pouvez pas supprimer ni modifier les serveurs de noms Azure DNS préremplis.</span><span class="sxs-lookup"><span data-stu-id="0b293-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="0b293-225">Notez que cela s’applique uniquement au jeu d’enregistrements NS défini à l’apex de la zone.</span><span class="sxs-lookup"><span data-stu-id="0b293-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="0b293-226">Les autres jeux d’enregistrements NS dans votre zone (tels que ceux utilisés pour déléguer des zones enfants) peuvent être modifiés sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="0b293-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="0b293-227">L’exemple suivant montre comment ajouter un serveur de noms supplémentaire au jeu d’enregistrements NS défini à l’apex de la zone :</span><span class="sxs-lookup"><span data-stu-id="0b293-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="0b293-228">Pour modifier les métadonnées du jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-228">To modify record set metadata</span></span>

<span data-ttu-id="0b293-229">Vous pouvez utiliser des [métadonnées de jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) pour associer les données spécifiques de l’application à chaque jeu d’enregistrements, comme paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="0b293-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="0b293-230">L’exemple suivant montre comment modifier les métadonnées d’un jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0b293-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="0b293-231">Supprimer un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="0b293-231">Delete a record set</span></span>

<span data-ttu-id="0b293-232">Les jeux d’enregistrements peuvent être supprimés à l’aide de l’applet de commande `Remove-AzureRmDnsRecordSet` .</span><span class="sxs-lookup"><span data-stu-id="0b293-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="0b293-233">La suppression d’un jeu d’enregistrements a pour effet de supprimer également tous les enregistrements qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="0b293-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="0b293-234">Vous ne pouvez pas supprimer de jeux d’enregistrements SOA et NS au niveau de l’apex de la zone (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="0b293-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="0b293-235">Azure DNS les crée automatiquement lors de la création de la zone, et les supprime automatiquement lors de la suppression de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="0b293-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="0b293-236">L’exemple suivant montre comment supprimer un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="0b293-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="0b293-237">Dans cet exemple, le nom, le type, la zone et le groupe de ressources du jeu d’enregistrements sont spécifiés explicitement.</span><span class="sxs-lookup"><span data-stu-id="0b293-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="0b293-238">Vous pouvez également spécifier le jeu d’enregistrements par un nom et un type, et la zone à l’aide d’un objet :</span><span class="sxs-lookup"><span data-stu-id="0b293-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="0b293-239">Une troisième option consiste à spécifier le jeu d’enregistrements en utilisant un objet jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="0b293-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="0b293-240">Lorsque vous spécifiez le jeu d’enregistrements à supprimer à l’aide d’un objet jeu d’enregistrements, des [vérifications ETag](dns-zones-records.md#etags) veillent à ce que des modifications simultanées ne soient pas supprimées.</span><span class="sxs-lookup"><span data-stu-id="0b293-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="0b293-241">Le commutateur facultatif `-Overwrite` permet de supprimer ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="0b293-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="0b293-242">L'objet du jeu d'enregistrements peut également être envoyé au lieu d’être transmis en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="0b293-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="0b293-243">Invites de confirmation</span><span class="sxs-lookup"><span data-stu-id="0b293-243">Confirmation prompts</span></span>

<span data-ttu-id="0b293-244">Les applets de commande `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet` et `Remove-AzureRmDnsRecordSet` prennent en charge les invites de confirmation.</span><span class="sxs-lookup"><span data-stu-id="0b293-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="0b293-245">Chaque applet de commande demande une confirmation si la variable de préférence PowerShell `$ConfirmPreference` a la valeur `Medium` ou une valeur inférieure.</span><span class="sxs-lookup"><span data-stu-id="0b293-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="0b293-246">La valeur par défaut de la variable `$ConfirmPreference` étant `High`, ces invites ne s’affichent pas en cas d’utilisation des paramètres PowerShell par défaut.</span><span class="sxs-lookup"><span data-stu-id="0b293-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="0b293-247">Vous pouvez remplacer le paramétrage actuel de `$ConfirmPreference` par le paramètre `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="0b293-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="0b293-248">Si vous spécifiez les paramètres `-Confirm` ou `-Confirm:$True`, les applets de commande vous invitent à confirmer l’exécution.</span><span class="sxs-lookup"><span data-stu-id="0b293-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="0b293-249">Si vous spécifiez le paramètre `-Confirm:$False`, l’applet de commande ne demande pas de confirmation.</span><span class="sxs-lookup"><span data-stu-id="0b293-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="0b293-250">Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="0b293-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b293-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0b293-251">Next steps</span></span>

<span data-ttu-id="0b293-252">Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="0b293-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="0b293-253">Découvrez comment [protéger vos zones et enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="0b293-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="0b293-254">Examinez la [documentation de référence d’Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="0b293-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
