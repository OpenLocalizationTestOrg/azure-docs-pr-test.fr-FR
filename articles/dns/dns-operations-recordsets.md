---
title: "aaaManage DNS des enregistrements dans DNS Azure à l’aide d’Azure PowerShell | Documents Microsoft"
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
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="4e1ac-104">Gérer les enregistrements et jeux d’enregistrements DNS dans Azure DNS à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e1ac-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e1ac-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4e1ac-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="4e1ac-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4e1ac-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="4e1ac-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e1ac-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="4e1ac-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e1ac-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="4e1ac-109">Cet article explique la modification des enregistrements par toomanage DNS pour votre zone DNS à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="4e1ac-110">Enregistrements DNS peuvent également être gérés à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-recordsets-cli.md) ou hello [portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="4e1ac-111">exemples Hello dans cet article supposent que vous avez déjà [installé Azure PowerShell, signé et la création d’une zone DNS](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="4e1ac-112">Introduction</span><span class="sxs-lookup"><span data-stu-id="4e1ac-112">Introduction</span></span>

<span data-ttu-id="4e1ac-113">Avant de créer des enregistrements DNS dans le système DNS d’Azure, vous devez d’abord toounderstand comment Azure DNS organise les enregistrements DNS dans les jeux d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="4e1ac-114">Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="4e1ac-115">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="4e1ac-115">Create a new DNS record</span></span>

<span data-ttu-id="4e1ac-116">Si votre nouvel enregistrement hello même nom et le type en tant qu’un enregistrement existant, vous devez trop[ajouter le jeu d’enregistrements existant toohello](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="4e1ac-117">Si votre nouvel enregistrement a un tooall de nom et type de différents enregistrements existants, vous devez toocreate un nouveau jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="4e1ac-118">Créer des enregistrements « A » dans un nouveau jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="4e1ac-119">Vous créez des jeux d’enregistrements à l’aide de hello `New-AzureRmDnsRecordSet` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="4e1ac-120">Lorsque vous créez un jeu d’enregistrements, vous avez besoin de nom de jeu d’enregistrements toospecify hello, zone de hello, hello création toolive (TTL), type d’enregistrement hello et hello enregistrements toobe.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="4e1ac-121">paramètres de Hello pour ajouter le jeu d’enregistrements enregistrements tooa varient en fonction de type hello du jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="4e1ac-122">Par exemple, lorsque vous utilisez un jeu d’enregistrements de type « A », vous avez besoin d’adresse IP de toospecify hello à l’aide du paramètre hello `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="4e1ac-123">D’autres paramètres sont utilisés pour d’autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="4e1ac-124">Pour plus d’informations, voir les [autres exemples de types d’enregistrements](#additional-record-type-examples).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="4e1ac-125">Hello exemple suivant crée un enregistrement avec le nom relatif de hello « www » Bonjour Zone du DNS « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="4e1ac-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="4e1ac-126">nom qualifié complet de Hello du jeu d’enregistrements hello est « www.contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="4e1ac-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="4e1ac-127">type d’enregistrement Hello est « A » et hello durée de vie est 3 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="4e1ac-128">jeu d’enregistrements Hello contient un enregistrement unique, avec l’adresse IP « 1.2.3.4 ».</span><span class="sxs-lookup"><span data-stu-id="4e1ac-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="4e1ac-129">toocreate un jeu d’enregistrements à hello 'apex » d’une zone (dans ce cas, « contoso.com »), utilisez le nom de jeu d’enregistrements hello ' @' (sans guillemets) :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="4e1ac-130">Si vous avez besoin d’un jeu d’enregistrements contenant plusieurs enregistrements de toocreate, tout d’abord créer un tableau local et ajouter des enregistrements de hello, puis passer le tableau de hello trop`New-AzureRmDnsRecordSet` comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="4e1ac-131">[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="4e1ac-132">Hello suivant montre comment toocreate un jeu d’enregistrements avec deux entrées de métadonnées, « dept = finance' et ' environnement = production ».</span><span class="sxs-lookup"><span data-stu-id="4e1ac-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="4e1ac-133">DNS Azure prend également en charge les jeux d’enregistrements 'empty', qui peut agir comme un espace réservé tooreserve un nom DNS avant de créer des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="4e1ac-134">Jeux d’enregistrements vides est visibles dans le plan de contrôle hello Azure DNS, mais s’affichent sur les serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="4e1ac-135">Bonjour à l’exemple suivant crée un jeu d’enregistrements vide :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="4e1ac-136">Créer des enregistrements d’autres types</span><span class="sxs-lookup"><span data-stu-id="4e1ac-136">Create records of other types</span></span>

<span data-ttu-id="4e1ac-137">Après avoir vu en détail comment toocreate 'A' enregistre, hello suivant exemples montrent comment toocreate les enregistrements d’autres types pris en charge par le système DNS Azure d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="4e1ac-138">Dans chaque cas, nous montrons comment toocreate un enregistrement défini contenant un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="4e1ac-139">Hello les exemples précédents pour les enregistrements 'A' peuvent être adapté toocreate jeux d’enregistrements d’autres types contenant plusieurs enregistrements avec des métadonnées, ou des jeux d’enregistrements de vide toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="4e1ac-140">Nous ne donnent pas une toocreate exemple un jeu d’enregistrements SOA, étant donné que SOA est créées et supprimées avec chaque zone DNS et ne peut pas être créée ou supprimée séparément.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="4e1ac-141">Toutefois, [hello SOA peut être modifiée, comme indiqué dans un exemple plus loin](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-142">Créer un jeu d’enregistrements AAAA avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-143">Créer un jeu d’enregistrements CNAME avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="4e1ac-144">les normes DNS Hello n’autorisent pas les enregistrements CNAME au sommet de hello d’une zone (`-Name '@'`), ni font qu’ils autorisent les jeux d’enregistrements contenant plusieurs enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="4e1ac-145">Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-146">Créer un jeu d’enregistrements MX avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="4e1ac-147">Dans cet exemple, nous utilisons le nom du jeu d’enregistrements hello ' @' enregistrement toocreate un MX au sommet de zone hello (dans ce cas, « contoso.com »).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-148">Créer un jeu d’enregistrements NS avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-149">Créer un jeu d’enregistrements PTR avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="4e1ac-150">Dans ce cas, « my-arpa-zone.com' représente hello zone de recherche inversée ARPA représentant votre plage IP.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="4e1ac-151">Chaque enregistrement PTR dans cette zone correspond à adresse IP de tooan au sein de cette plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="4e1ac-152">nom de l’enregistrement Hello « 10 » est le dernier octet de hello d’adresse IP de hello dans cette plage IP représentée par cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-153">Créer un jeu d’enregistrements SRV avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="4e1ac-154">Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez hello  *\_service* et  *\_protocole* Bonjour nom du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="4e1ac-155">Il n’existe aucun besoin tooinclude ' @' Bonjour jeu d’enregistrements nom lors de la création d’un enregistrement SRV définie au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="4e1ac-156">Créer un jeu d’enregistrements TXT avec un seul enregistrement</span><span class="sxs-lookup"><span data-stu-id="4e1ac-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="4e1ac-157">Hello suivant montre comment enregistrer des toocreate un TXT.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="4e1ac-158">Pour plus d’informations sur la longueur maximale de la chaîne hello pris en charge dans les enregistrements TXT, consultez [enregistrements TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="4e1ac-159">Obtention d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-159">Get a record set</span></span>

<span data-ttu-id="4e1ac-160">tooretrieve un jeu d’enregistrements existant, utilisez `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="4e1ac-161">Cette applet de commande retourne un objet local représentant hello jeu d’enregistrements dans DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="4e1ac-162">Comme avec `New-AzureRmDnsRecordSet`, nom du jeu d’enregistrements hello donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="4e1ac-163">Vous devez également le type d’enregistrement toospecify hello et zone hello contenant le jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="4e1ac-164">Hello suivant montre comment tooretrieve un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="4e1ac-165">Dans cet exemple, les zones de hello est spécifié à l’aide de hello `-ZoneName` et `-ResourceGroupName` paramètres.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="4e1ac-166">Vous pouvez également spécifier également zone hello à l’aide d’un objet de fuseau, passé à l’aide de hello `-Zone` paramètre.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="4e1ac-167">Liste des jeux d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-167">List record sets</span></span>

<span data-ttu-id="4e1ac-168">Vous pouvez également utiliser `Get-AzureRmDnsZone` des jeux d’enregistrements de toolist dans une zone, en omettant hello `-Name` et/ou `-RecordType` paramètres.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="4e1ac-169">Hello exemple suivant retourne tous les enregistrements définit dans la zone de hello :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="4e1ac-170">Hello suivant montre comment tous les jeux d’un type donné d’enregistrements peuvent être récupérées en spécifiant le type d’enregistrement hello pendant enregistrement de hello l'omission de définie le nom :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="4e1ac-171">tooretrieve définit de tous les enregistrements avec un nom donné, entre les types d’enregistrement, vous devez tooretrieve tous les jeux d’enregistrements, puis filtre hello résultats :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="4e1ac-172">Bonjour tous les exemples ci-dessus, zone de hello peut être spécifié à l’aide de hello `-ZoneName` et `-ResourceGroupName`paramètres (comme indiqué), ou en spécifiant un objet de la zone :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="4e1ac-173">Ajouter un enregistrement tooan existante du jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="4e1ac-174">tooadd un enregistrement existant tooan enregistrement défini, procédez comme hello trois comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="4e1ac-175">Obtenir le jeu d’enregistrements existant hello</span><span class="sxs-lookup"><span data-stu-id="4e1ac-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="4e1ac-176">Ajoutez hello nouvel enregistrement toohello local ensemble d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="4e1ac-177">Cette opération se fait hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="4e1ac-178">Valider hello modification toohello arrière service DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="4e1ac-179">À l’aide de `Set-AzureRmDnsRecordSet` *remplace* hello enregistrement existant, défini dans le système DNS Azure (et tous les enregistrements qu’il contient) avec le jeu d’enregistrements hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="4e1ac-180">[Vérification ETag](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4e1ac-181">Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="4e1ac-182">Séquence d’opérations peut également être *dirigés*, ce qui signifie que vous passez un objet de jeu d’enregistrements hello par une barre verticale hello plutôt que d’en lui passant comme paramètre :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="4e1ac-183">exemples de Hello ci-dessus montrent comment définie des tooadd un 'A' enregistrement existant tooan enregistrements de type « A ».</span><span class="sxs-lookup"><span data-stu-id="4e1ac-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="4e1ac-184">Une séquence d’opérations similaire est utilisé tooadd enregistrements toorecord définit d’autres types, en remplaçant hello `-Ipv4Address` paramètre de `Add-AzureRmDnsRecordConfig` avec un autre type d’enregistrement Paramètres tooeach spécifique.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="4e1ac-185">Hello paramètres pour chaque type d’enregistrement sont hello même que pour hello `New-AzureRmDnsRecordConfig` applet de commande, comme indiqué dans [exemples du type d’enregistrement supplémentaires](#additional-record-type-examples) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="4e1ac-186">Les jeux d’enregistrements de type « CNAME » ou « SOA » ne peuvent pas contenir plusieurs enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="4e1ac-187">Cette contrainte se produit à partir des normes DNS hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="4e1ac-188">Il ne s’agit pas d’une limitation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="4e1ac-189">Suppression d’un enregistrement d’un jeu d'enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="4e1ac-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="4e1ac-190">Bonjour processus tooremove un enregistrement à partir d’un jeu d’enregistrements est similaire tooadd de processus toohello un enregistrement tooan existant enregistrer ensemble :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="4e1ac-191">Obtenir le jeu d’enregistrements existant hello</span><span class="sxs-lookup"><span data-stu-id="4e1ac-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="4e1ac-192">Supprimer l’enregistrement de hello à partir de l’objet de jeu d’enregistrements local hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="4e1ac-193">Cette opération se fait hors connexion.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-193">This is an off-line operation.</span></span> <span data-ttu-id="4e1ac-194">enregistrement Hello est en cours de suppression doit être une correspondance exacte avec un enregistrement existant entre tous les paramètres.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="4e1ac-195">Valider hello modification toohello arrière service DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="4e1ac-196">Hello utilisation facultative `-Overwrite` commutateur toosuppress [Etag vérifie](dns-zones-records.md#etags) de modifications simultanées.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="4e1ac-197">À l’aide de hello ci-dessus séquence tooremove hello dernier à partir d’un jeu d’enregistrements ne supprime pas le jeu d’enregistrements hello, au lieu de cela, elle laisse un jeu d’enregistrements vide.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="4e1ac-198">tooremove un jeu d’enregistrements, consultez [supprimer un jeu d’enregistrements](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="4e1ac-199">De même tooadding enregistrements tooa jeu d’enregistrements, séquence hello de tooremove opérations un jeu d’enregistrements peut également être transmis :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="4e1ac-200">Différents types d’enregistrements sont pris en charge en passant les paramètres spécifiques au type approprié hello trop`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="4e1ac-201">Hello paramètres pour chaque type d’enregistrement sont hello même que pour hello `New-AzureRmDnsRecordConfig` applet de commande, comme indiqué dans [exemples du type d’enregistrement supplémentaires](#additional-record-type-examples) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="4e1ac-202">Modifier un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-202">Modify an existing record set</span></span>

<span data-ttu-id="4e1ac-203">Hello étapes permettant de modifier un jeu d’enregistrements existant sont similaires toohello que vous prenez lors de l’ajout ou la suppression des enregistrements à partir d’un jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="4e1ac-204">Récupérer hello existant jeu d’enregistrements à l’aide de `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="4e1ac-205">Modifier un objet de jeu d’enregistrements local hello par :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="4e1ac-206">ajout ou suppression d’enregistrements ;</span><span class="sxs-lookup"><span data-stu-id="4e1ac-206">Adding or removing records</span></span>
    * <span data-ttu-id="4e1ac-207">Modification des paramètres de hello des enregistrements existants</span><span class="sxs-lookup"><span data-stu-id="4e1ac-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="4e1ac-208">La modification d’enregistrement de hello définie toolive TTL (time) et les métadonnées</span><span class="sxs-lookup"><span data-stu-id="4e1ac-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="4e1ac-209">Valider les modifications apportées à l’aide de hello `Set-AzureRmDnsRecordSet` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="4e1ac-210">Cela *remplace* hello enregistrement existant défini dans Azure DNS avec le jeu d’enregistrements hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="4e1ac-211">Lorsque vous utilisez `Set-AzureRmDnsRecordSet`, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="4e1ac-212">Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="4e1ac-213">définie des tooupdate un enregistrement d’un enregistrement existant</span><span class="sxs-lookup"><span data-stu-id="4e1ac-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="4e1ac-214">Dans cet exemple, nous changeons hello adresseIP de 'A' enregistrement existant :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="4e1ac-215">toomodify un enregistrement SOA</span><span class="sxs-lookup"><span data-stu-id="4e1ac-215">toomodify an SOA record</span></span>

<span data-ttu-id="4e1ac-216">Impossible d’ajouter ou supprimer des enregistrements de hello créé automatiquement SOA jeu d’enregistrements au sommet de zone hello (`-Name "@"`, y compris les guillemets).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="4e1ac-217">Toutefois, vous pouvez modifier les paramètres de hello dans hello enregistrement SOA (à l’exception de « hôte ») et enregistrement de hello définie la durée de vie.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="4e1ac-218">Hello suivant montre l’exemple de comment toochange hello *messagerie* propriété Hello enregistrement SOA :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="4e1ac-219">enregistrements toomodify NS au sommet de zone hello</span><span class="sxs-lookup"><span data-stu-id="4e1ac-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="4e1ac-220">jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="4e1ac-221">Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="4e1ac-222">Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="4e1ac-223">Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="4e1ac-224">Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="4e1ac-225">Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="4e1ac-226">Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="4e1ac-227">Bonjour à l’exemple suivant montre comment tooadd un enregistrement de noms supplémentaires server toohello NS définie les au sommet de zone hello :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="4e1ac-228">métadonnées du jeu d’enregistrement de toomodify</span><span class="sxs-lookup"><span data-stu-id="4e1ac-228">toomodify record set metadata</span></span>

<span data-ttu-id="4e1ac-229">[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="4e1ac-230">Hello suivant montre comment définir les métadonnées de hello toomodify d’un enregistrement existant :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="4e1ac-231">Supprimer un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="4e1ac-231">Delete a record set</span></span>

<span data-ttu-id="4e1ac-232">Jeux d’enregistrements peut être supprimés à l’aide de hello `Remove-AzureRmDnsRecordSet` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="4e1ac-233">Suppression d’un jeu d’enregistrements supprime également tous les enregistrements dans le jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="4e1ac-234">Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="4e1ac-235">DNS Azure ces créés automatiquement lors de la zone de hello a été créé et supprime automatiquement lors de la zone de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="4e1ac-236">Hello suivant montre comment toodelete un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="4e1ac-237">Dans cet exemple, nom du jeu d’enregistrements hello, type de jeu d’enregistrements, nom de la zone et groupe de ressources sont chacun spécifiés explicitement.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="4e1ac-238">Sinon, jeu d’enregistrements hello peut être spécifié par le nom et le type et hello spécifié à l’aide d’un objet de la zone :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="4e1ac-239">Comme une troisième option, hello jeu d’enregistrements lui-même peuvent être spécifié à l’aide d’un objet de jeu d’enregistrements :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="4e1ac-240">Lorsque vous spécifiez l’enregistrement de hello défini toobe supprimée à l’aide d’un objet de jeu d’enregistrements, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas supprimées.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="4e1ac-241">Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="4e1ac-242">objet de jeu d’enregistrements Hello peut également être transmis au lieu de passé en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="4e1ac-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="4e1ac-243">Invites de confirmation</span><span class="sxs-lookup"><span data-stu-id="4e1ac-243">Confirmation prompts</span></span>

<span data-ttu-id="4e1ac-244">Hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, et `Remove-AzureRmDnsRecordSet` prend en charge les applets de commande toutes les invites de confirmation.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="4e1ac-245">Chaque applet de commande vous demande de confirmer si hello `$ConfirmPreference` a la valeur de variable de préférence PowerShell `Medium` ou inférieure.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="4e1ac-246">Depuis la valeur par défaut de hello `$ConfirmPreference` est `High`, ces messages ne sont pas affectés lors de l’utilisation de paramètres de PowerShell hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="4e1ac-247">Vous pouvez remplacer hello actuel `$ConfirmPreference` paramètre à l’aide de hello `-Confirm` paramètre.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="4e1ac-248">Si vous spécifiez `-Confirm` ou `-Confirm:$True` , hello applet de commande vous demande confirmation avant qu’il s’exécute.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="4e1ac-249">Si vous spécifiez `-Confirm:$False` , applet de commande hello ne vous demande pas de confirmation.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="4e1ac-250">Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e1ac-251">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e1ac-251">Next steps</span></span>

<span data-ttu-id="4e1ac-252">Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="4e1ac-253">Découvrez comment trop[protéger les zones et les enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="4e1ac-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="4e1ac-254">Hello de révision [documentation de référence PowerShell pour Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="4e1ac-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
