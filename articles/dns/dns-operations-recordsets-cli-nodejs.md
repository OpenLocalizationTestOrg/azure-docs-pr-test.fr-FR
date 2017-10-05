---
title: "Gérer les enregistrements DNS dans Azure DNS à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Gestion des jeux d'enregistrements DNS et des enregistrements dans Azure DNS lorsque votre domaine est hébergé dans Azure DNS. Toutes les commandes CLI 1.0 destinées aux opérations sur les jeux d’enregistrements et les enregistrements."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="87533-104">Gérer les enregistrements DNS dans Azure DNS à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87533-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="87533-105">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="87533-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="87533-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="87533-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="87533-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="87533-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="87533-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="87533-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="87533-109">Cet article explique comment gérer des enregistrements DNS pour votre zone DNS à l’aide de l’interface de ligne de commande (CLI) Azure multiplateforme, disponible sur Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="87533-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="87533-110">Vous pouvez également gérer vos enregistrements DNS à l’aide [d’Azure PowerShell](dns-operations-recordsets.md) ou du [portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="87533-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="87533-111">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="87533-111">CLI versions to complete the task</span></span>

<span data-ttu-id="87533-112">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="87533-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="87533-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="87533-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="87533-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="87533-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="87533-115">Les exemples de cet article supposent que vous ayez déjà [installé Azure CLI 1.0, ouvert une session et créé une zone DNS](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="87533-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="87533-116">Introduction</span><span class="sxs-lookup"><span data-stu-id="87533-116">Introduction</span></span>

<span data-ttu-id="87533-117">Avant de créer des enregistrements DNS dans Azure DNS, vous devez comprendre comment Azure DNS organise les enregistrements DNS en jeux d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="87533-118">Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="87533-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="87533-119">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="87533-119">Create a DNS record</span></span>

<span data-ttu-id="87533-120">Pour créer un enregistrement DNS, utilisez la commande `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="87533-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="87533-121">Pour obtenir de l’aide, consultez l’article `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="87533-122">Lors de la création d’un enregistrement, vous devez spécifier le nom du groupe de ressources, le nom de la zone, le type d’enregistrement et les détails de l’enregistrement créé.</span><span class="sxs-lookup"><span data-stu-id="87533-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="87533-123">Le nom du jeu d’enregistrements doit être un nom *relatif*, c’est-à-dire qu’il ne doit pas contenir le nom de la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="87533-124">Si le jeu d’enregistrements n’existe pas, cette commande le crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="87533-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="87533-125">Si le jeu d’enregistrements existe déjà, cette commande ajoute l’enregistrement spécifié au jeu d’enregistrements existant.</span><span class="sxs-lookup"><span data-stu-id="87533-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="87533-126">Si un jeu d’enregistrements est créé, une durée de vie (TTL) de 3600 est utilisée par défaut.</span><span class="sxs-lookup"><span data-stu-id="87533-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="87533-127">Pour plus d’instructions sur l’utilisation de différents TTL, consultez [Création d’un jeu d’enregistrements DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="87533-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="87533-128">L’exemple suivant crée un enregistrement A appelé *www* dans la zone *contoso.com* du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="87533-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="87533-129">L’adresse IP de l’enregistrement A est *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="87533-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="87533-130">Pour créer un enregistrement à l’extrémité de la zone (dans cet exemple, « contoso.com »), utilisez le nom d’enregistrement "@" (guillemets compris) :</span><span class="sxs-lookup"><span data-stu-id="87533-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="87533-131">Créer un jeu d’enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="87533-131">Create a DNS record set</span></span>

<span data-ttu-id="87533-132">Dans les exemples ci-dessus, l’enregistrement DNS a été ajouté à un jeu d’enregistrements existant, ou le jeu d’enregistrements a été créé *implicitement*.</span><span class="sxs-lookup"><span data-stu-id="87533-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="87533-133">Vous pouvez également créer le jeu d’enregistrements *explicitement* avant d’ajouter des enregistrements à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="87533-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="87533-134">Azure DNS prend en charge les jeux d’enregistrements « vides », qui peuvent servir d’espaces réservés pour réserver un nom DNS avant de créer des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="87533-135">Les jeux d’enregistrements vides sont visibles dans le volet de contrôle d’Azure DNS, mais n’apparaissent pas sur les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="87533-136">Des jeux d’enregistrements sont créés à l’aide de la commande `azure network dns record-set create`.</span><span class="sxs-lookup"><span data-stu-id="87533-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="87533-137">Pour obtenir de l’aide, consultez l’article `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="87533-138">La création explicite du jeu d’enregistrements permet de spécifier les propriétés de jeu d’enregistrements, comme la [Durée de vie (TTL)](dns-zones-records.md#time-to-live) et les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="87533-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="87533-139">Vous pouvez utiliser des [métadonnées de jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) pour associer les données spécifiques de l’application à chaque jeu d’enregistrements, comme paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="87533-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="87533-140">L’exemple suivant crée un jeu d’enregistrements vide avec une durée de vie de 60 secondes, à l’aide du paramètre `--ttl` (forme abrégée `-l`) :</span><span class="sxs-lookup"><span data-stu-id="87533-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="87533-141">L’exemple suivant crée un jeu d’enregistrements avec deux entrées de métadonnées, « dept=finance » et « environment=production », en utilisant le paramètre `--metadata` (forme abrégée `-m`) :</span><span class="sxs-lookup"><span data-stu-id="87533-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="87533-142">Après avoir créé un jeu d’enregistrements vide, les enregistrements peuvent être ajoutés à l’aide de `azure network dns record-set add-record`, comme décrit dans [Création d’un enregistrement DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="87533-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="87533-143">Créer des enregistrements d’autres types</span><span class="sxs-lookup"><span data-stu-id="87533-143">Create records of other types</span></span>

<span data-ttu-id="87533-144">À présent que nous avons vu en détail comment créer des enregistrements de type « A », les exemples suivants montrent comment créer des enregistrements d’autres types pris en charge par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="87533-145">Les paramètres utilisés pour spécifier les données de l’enregistrement varient selon le type de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="87533-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="87533-146">Par exemple, pour un enregistrement de type « A », vous spécifiez l’adresse IPv4 avec le paramètre `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="87533-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="87533-147">Les paramètres pour chaque type d’enregistrement peuvent être spécifiés à l’aide de `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="87533-148">Dans chaque cas, nous montrons comment créer un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="87533-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="87533-149">L’enregistrement est ajouté au jeu d’enregistrements existant, ou à un jeu d’enregistrements créé implicitement.</span><span class="sxs-lookup"><span data-stu-id="87533-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="87533-150">Pour plus d’informations sur la création de jeux d’enregistrements et la définition explicite des paramètres de jeu d’enregistrements, consultez [Création d’un jeu d’enregistrements DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="87533-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="87533-151">Nous ne donnons pas d’exemple de création de jeu d’enregistrements SOA (Architecture orientée services), car les enregistrements de ce type sont créés et supprimés avec chaque zone DNS, et ne peuvent pas l’être séparément.</span><span class="sxs-lookup"><span data-stu-id="87533-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="87533-152">En revanche, vous pouvez [modifier les enregistrements SOA en procédant de la manière décrite dans un exemple plus loin](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="87533-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="87533-153">Créer un enregistrement AAAA</span><span class="sxs-lookup"><span data-stu-id="87533-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="87533-154">Créer un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="87533-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="87533-155">Les normes DNS n’autorisent pas la présence d’enregistrements CNAME ou de jeux d’enregistrements contenant plusieurs enregistrements à l’apex (sommet) d’une zone (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="87533-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="87533-156">Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="87533-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="87533-157">Créer un enregistrement MX</span><span class="sxs-lookup"><span data-stu-id="87533-157">Create an MX record</span></span>

<span data-ttu-id="87533-158">Dans cet exemple, nous utilisons le nom de jeu d’enregistrements « @ » pour créer l’enregistrement MX à l’apex de la zone (dans ce cas, « contoso.com »).</span><span class="sxs-lookup"><span data-stu-id="87533-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="87533-159">Créer un enregistrement NS</span><span class="sxs-lookup"><span data-stu-id="87533-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="87533-160">Création d’un enregistrement PTR</span><span class="sxs-lookup"><span data-stu-id="87533-160">Create a PTR record</span></span>

<span data-ttu-id="87533-161">Dans ce cas, « my-arpa-zone.com » indique la zone ARPA représentant votre plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="87533-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="87533-162">Chaque enregistrement PTR défini dans cette zone correspond à une adresse IP figurant dans cette plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="87533-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="87533-163">Le nom d’enregistrement « 10 » est le dernier octet de l’adresse IP dans cette plage d’IP représentée par cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="87533-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="87533-164">Création d’un enregistrement SRV</span><span class="sxs-lookup"><span data-stu-id="87533-164">Create an SRV record</span></span>

<span data-ttu-id="87533-165">Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez le *\_service* et le *\_protocole* dans le nom du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="87533-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="87533-166">Il est inutile d’inclure "@" dans le nom du jeu d’enregistrements lors de la création d’un enregistrement SRV défini à l’extrémité de la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="87533-167">Création d’un enregistrement TXT</span><span class="sxs-lookup"><span data-stu-id="87533-167">Create a TXT record</span></span>

<span data-ttu-id="87533-168">L’exemple suivant montre comment créer un enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="87533-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="87533-169">Pour plus d’informations sur la longueur maximale de chaîne prise en charge dans les enregistrements TXT, voir [Enregistrements TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="87533-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="87533-170">Obtention d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-170">Get a record set</span></span>

<span data-ttu-id="87533-171">Pour récupérer un jeu d’enregistrements existant, utilisez `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="87533-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="87533-172">Pour obtenir de l’aide, consultez l’article `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="87533-173">Comme lors de la création d’un enregistrement ou jeu d’enregistrements, le nom du jeu d’enregistrements doit être un nom *relatif*, c’est-à-dire qu’il ne doit pas contenir le nom de la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="87533-174">Vous devez également spécifier le type d’enregistrement, la zone contenant le jeu d’enregistrements et le groupe de ressources contenant la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="87533-175">L’exemple suivant retrouve l’enregistrement *www* de type A dans la zone *contoso.com* du groupe de ressources *MyResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="87533-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="87533-176">Liste des jeux d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-176">List record sets</span></span>

<span data-ttu-id="87533-177">Vous pouvez répertorier tous les enregistrements d’une zone DNS à l’aide de la commande `azure network dns record-set list` .</span><span class="sxs-lookup"><span data-stu-id="87533-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="87533-178">Pour obtenir de l’aide, consultez l’article `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="87533-179">Cet exemple renvoie tous les jeux d’enregistrements dans la zone *contoso.com*, dans le groupe de ressources *MyResourceGroup*, quel que soit le nom ou le type d’enregistrement :</span><span class="sxs-lookup"><span data-stu-id="87533-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="87533-180">Cet exemple retourne tous les jeux d’enregistrements correspondant au type d’enregistrement donné (dans ce cas, les enregistrements « A ») :</span><span class="sxs-lookup"><span data-stu-id="87533-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="87533-181">Ajouter un enregistrement à un jeu d’enregistrements existant</span><span class="sxs-lookup"><span data-stu-id="87533-181">Add a record to an existing record set</span></span>

<span data-ttu-id="87533-182">Vous pouvez utiliser `azure network dns record-set add-record` à la fois pour créer un enregistrement dans un nouveau jeu d’enregistrements ou pour ajouter un enregistrement à un jeu d’enregistrements existant.</span><span class="sxs-lookup"><span data-stu-id="87533-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="87533-183">Pour plus d’informations, consultez [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="87533-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="87533-184">Suppression d’un enregistrement d’un jeu d'enregistrements existant.</span><span class="sxs-lookup"><span data-stu-id="87533-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="87533-185">Pour supprimer un enregistrement DNS d’un jeu d'enregistrements existant, utilisez `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="87533-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="87533-186">Pour obtenir de l’aide, consultez l’article `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="87533-187">Cette commande supprime un enregistrement DNS d’un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="87533-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="87533-188">Si le dernier enregistrement d’un jeu d’enregistrements est supprimé, le jeu d’enregistrements lui-même n’est **pas** supprimé.</span><span class="sxs-lookup"><span data-stu-id="87533-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="87533-189">Un jeu d’enregistrements vide est laissé à la place.</span><span class="sxs-lookup"><span data-stu-id="87533-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="87533-190">Pour supprimer le jeu d’enregistrements à la place, consultez [Suppression d’un jeu d’enregistrements](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="87533-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="87533-191">Vous devez spécifier l’enregistrement à supprimer et la zone de laquelle il doit être supprimé, en utilisant les mêmes paramètres que lors de la création d’un enregistrement avec `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="87533-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="87533-192">Ces paramètres sont décrits dans [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="87533-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="87533-193">Cette commande vous demande de confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="87533-193">This command prompts for confirmation.</span></span> <span data-ttu-id="87533-194">Ce message peut être supprimé en utilisant le switch `--quiet` (forme abrégée `-q`).</span><span class="sxs-lookup"><span data-stu-id="87533-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="87533-195">L’exemple suivant supprime l’enregistrement A avec la valeur « 1.2.3.4 » du jeu d’enregistrements *www* dans la zone *contoso.com* du groupe de ressources *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="87533-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="87533-196">L’invite de confirmation est supprimée.</span><span class="sxs-lookup"><span data-stu-id="87533-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="87533-197">Modifier un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-197">Modify an existing record set</span></span>

<span data-ttu-id="87533-198">Chaque jeu d’enregistrements contient une [durée de vie (TTL)](dns-zones-records.md#time-to-live), des [métadonnées](dns-zones-records.md#tags-and-metadata) et des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="87533-199">Les sections suivantes expliquent comment modifier chacune de ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="87533-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="87533-200">Pour modifier un enregistrement A, AAAA, MX, NS, PTR, SRV ou TXT</span><span class="sxs-lookup"><span data-stu-id="87533-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="87533-201">Pour modifier un enregistrement existant de type A, AAAA, MX, NS, PTR, SRV ou TXT, vous devez d’abord ajouter un nouvel enregistrement, puis supprimer l’enregistrement existant.</span><span class="sxs-lookup"><span data-stu-id="87533-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="87533-202">Pour obtenir des instructions détaillées sur la façon de supprimer et ajouter des enregistrements, consultez les sections précédentes de cet article.</span><span class="sxs-lookup"><span data-stu-id="87533-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="87533-203">L’exemple suivant montre comment modifier un enregistrement « A », de l’adresse IP 1.2.3.4 à l’adresse IP 5.6.7.8 :</span><span class="sxs-lookup"><span data-stu-id="87533-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="87533-204">Pour modifier un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="87533-204">To modify a CNAME record</span></span>

<span data-ttu-id="87533-205">Pour modifier un enregistrement CNAME, utilisez `azure network dns record-set add-record` pour ajouter la nouvelle valeur de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="87533-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="87533-206">Contrairement aux autres types d’enregistrements, un jeu d’enregistrements CNAME ne peut contenir qu’un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="87533-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="87533-207">Par conséquent, l’enregistrement existant est *remplacé* lorsque le nouvel enregistrement est ajouté et n’a pas besoin d’être supprimé séparément.</span><span class="sxs-lookup"><span data-stu-id="87533-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="87533-208">Une invite vous demande d’accepter ce remplacement.</span><span class="sxs-lookup"><span data-stu-id="87533-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="87533-209">Cet exemple modifie le jeu d’enregistrements CNAME *www* dans la zone *contoso.com*, dans le groupe de ressources *MyResourceGroup*, pour pointer vers « www.fabrikam.net » au lieu de sa valeur existante :</span><span class="sxs-lookup"><span data-stu-id="87533-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="87533-210">Pour modifier un enregistrement SOA</span><span class="sxs-lookup"><span data-stu-id="87533-210">To modify an SOA record</span></span>

<span data-ttu-id="87533-211">Utilisez `azure network dns record-set set-soa-record` pour modifier l’enregistrement SOA pour une zone DNS donnée.</span><span class="sxs-lookup"><span data-stu-id="87533-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="87533-212">Pour obtenir de l’aide, consultez l’article `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="87533-213">L’exemple suivant montre comment définir la propriété « email » de l’enregistrement SOA pour la zone *contoso.com* dans le groupe de ressources *MyResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="87533-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="87533-214">Pour modifier des enregistrements NS à l’apex de la zone</span><span class="sxs-lookup"><span data-stu-id="87533-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="87533-215">Le jeu d’enregistrements NS à l’apex de la zone est créé automatiquement avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="87533-216">Il contient les noms des serveurs de noms Azure DNS attribués à la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="87533-217">Vous pouvez ajouter des serveurs de noms supplémentaires à ce jeu d’enregistrements NS, pour prendre en charge le co-hébergement de domaines avec plusieurs fournisseurs DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="87533-218">Vous pouvez également modifier la durée de vie et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="87533-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="87533-219">Toutefois, vous ne pouvez pas supprimer ni modifier les serveurs de noms Azure DNS préremplis.</span><span class="sxs-lookup"><span data-stu-id="87533-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="87533-220">Notez que cela s’applique uniquement au jeu d’enregistrements NS défini à l’apex de la zone.</span><span class="sxs-lookup"><span data-stu-id="87533-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="87533-221">Les autres jeux d’enregistrements NS dans votre zone (tels que ceux utilisés pour déléguer des zones enfants) peuvent être modifiés sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="87533-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="87533-222">L’exemple suivant montre comment ajouter un serveur de noms supplémentaire au jeu d’enregistrements NS défini à l’apex de la zone :</span><span class="sxs-lookup"><span data-stu-id="87533-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="87533-223">Pour modifier la durée de vie (TTL) d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="87533-224">Pour modifier la durée de vie (TTL) d’un jeu d’enregistrements, utilisez `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="87533-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="87533-225">Pour obtenir de l’aide, consultez l’article `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="87533-226">L’exemple suivant montre comment modifier la durée de vie d’un jeu d’enregistrements, dans ce cas sur 60 secondes :</span><span class="sxs-lookup"><span data-stu-id="87533-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="87533-227">Pour modifier les métadonnées d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="87533-228">Vous pouvez utiliser des [métadonnées de jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) pour associer les données spécifiques de l’application à chaque jeu d’enregistrements, comme paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="87533-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="87533-229">Pour modifier les métadonnées d’un jeu d’enregistrements, utilisez `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="87533-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="87533-230">Pour obtenir de l’aide, consultez l’article `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="87533-231">L’exemple suivant montre comment modifier un jeu d’enregistrements avec deux entrées de métadonnées, « dept=finance » et « environment=production », en utilisant le paramètre `--metadata` (forme abrégée `-m`).</span><span class="sxs-lookup"><span data-stu-id="87533-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="87533-232">Notez que toutes les métadonnées existantes sont *remplacées* par les valeurs fournies.</span><span class="sxs-lookup"><span data-stu-id="87533-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="87533-233">Supprimer un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="87533-233">Delete a record set</span></span>

<span data-ttu-id="87533-234">Les jeux d’enregistrements peuvent être supprimés à l’aide de la commande `azure network dns record-set delete`.</span><span class="sxs-lookup"><span data-stu-id="87533-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="87533-235">Pour obtenir de l’aide, consultez l’article `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="87533-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="87533-236">La suppression d’un jeu d’enregistrements a pour effet de supprimer également tous les enregistrements qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="87533-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="87533-237">Vous ne pouvez pas supprimer de jeux d’enregistrements SOA et NS au niveau de l’apex de la zone (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="87533-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="87533-238">Ceux-ci sont créés automatiquement lors de la création de la zone, et automatiquement supprimés lors de la suppression de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="87533-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="87533-239">L’exemple suivant supprime le jeu d’enregistrements *www* de type A dans la zone *contoso.com* du groupe de ressources *MyResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="87533-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="87533-240">Vous êtes invité à confirmer l’opération de suppression.</span><span class="sxs-lookup"><span data-stu-id="87533-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="87533-241">Pour supprimer cette invite, utilisez le switch `--quiet` (forme abrégée `-q`).</span><span class="sxs-lookup"><span data-stu-id="87533-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87533-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87533-242">Next steps</span></span>

<span data-ttu-id="87533-243">Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="87533-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="87533-244">Découvrez comment [protéger vos zones et enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="87533-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
