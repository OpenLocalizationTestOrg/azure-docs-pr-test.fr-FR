---
title: "aaaManage les enregistrements DNS à l’aide d’Azure DNS hello Azure CLI 2.0 | Documents Microsoft"
description: "Gestion des jeux d'enregistrements DNS et des enregistrements dans Azure DNS lorsque votre domaine est hébergé dans Azure DNS. Toutes les commandes CLI 2.0 destinées aux opérations sur les jeux d’enregistrements et les enregistrements."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="a955e-104">Gérer les enregistrements DNS et les jeux d’enregistrements dans DNS Azure à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a955e-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a955e-105">portail Azure</span><span class="sxs-lookup"><span data-stu-id="a955e-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="a955e-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a955e-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="a955e-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a955e-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="a955e-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a955e-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="a955e-109">Cet article vous explique comment toomanage les enregistrements DNS pour votre zone DNS à l’aide de hello multiplateforme Azure interface de ligne de commande (CLI) 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="a955e-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="a955e-110">Vous pouvez également gérer vos enregistrements DNS à l’aide de [Azure PowerShell](dns-operations-recordsets.md) ou hello [portail Azure](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a955e-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a955e-111">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="a955e-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="a955e-112">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a955e-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="a955e-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -notre CLI pour les modèles de déploiement gestion classique et les ressources des hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="a955e-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="a955e-115">exemples Hello dans cet article supposent que vous avez déjà [installé hello Azure CLI 2.0, signé et créé une zone DNS](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a955e-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="a955e-116">Introduction</span><span class="sxs-lookup"><span data-stu-id="a955e-116">Introduction</span></span>

<span data-ttu-id="a955e-117">Avant de créer des enregistrements DNS dans le système DNS d’Azure, vous devez d’abord toounderstand comment Azure DNS organise les enregistrements DNS dans les jeux d’enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="a955e-118">Pour plus d’informations sur les enregistrements DNS dans Azure DNS, voir [Enregistrements et zones DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="a955e-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="a955e-119">Créer un enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="a955e-119">Create a DNS record</span></span>

<span data-ttu-id="a955e-120">toocreate un enregistrement DNS, utilisez hello `az network dns record-set <record-type> set-record` commande (où `<record-type>` est de type hello d’enregistrement, c'est-à-dire</span><span class="sxs-lookup"><span data-stu-id="a955e-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="a955e-121">a, srv, txt, etc.) Pour obtenir de l’aide, consultez l’article `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="a955e-122">Lorsque vous créez un enregistrement, vous devez le nom du groupe ressource toospecify hello, nom de la zone, jeu d’enregistrements nom, type d’enregistrement hello et détails hello d’enregistrement hello en cours de création.</span><span class="sxs-lookup"><span data-stu-id="a955e-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="a955e-123">Hello nom de jeu d’enregistrements donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="a955e-124">Si le jeu d’enregistrements hello n’existe pas déjà, cette commande crée pour vous.</span><span class="sxs-lookup"><span data-stu-id="a955e-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="a955e-125">En cas d’enregistrement hello déjà définie, cette commande ajoute enregistrement hello vous spécifiez le jeu d’enregistrements existant toohello.</span><span class="sxs-lookup"><span data-stu-id="a955e-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="a955e-126">Si un jeu d’enregistrements est créé, une durée de vie (TTL) de 3600 est utilisée par défaut.</span><span class="sxs-lookup"><span data-stu-id="a955e-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="a955e-127">Pour obtenir des instructions sur toouse TTLs différents, voir [créer un jeu d’enregistrements DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="a955e-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="a955e-128">Hello exemple suivant crée un enregistrement A appelé *www* dans la zone de hello *contoso.com* dans le groupe de ressources hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a955e-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="a955e-129">Hello d’adresse IP de hello un enregistrement est *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="a955e-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="a955e-130">toocreate un enregistrement défini dans apex hello de zone de hello (dans ce cas, « contoso.com »), utilisez le nom de l’enregistrement hello « @ », y compris les guillemets hello :</span><span class="sxs-lookup"><span data-stu-id="a955e-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="a955e-131">Créer un jeu d’enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="a955e-131">Create a DNS record set</span></span>

<span data-ttu-id="a955e-132">Bonjour exemples ci-dessus, un enregistrement DNS hello a été soit ajouté tooan existante du jeu d’enregistrements ou de création de jeu d’enregistrements hello *implicitement*.</span><span class="sxs-lookup"><span data-stu-id="a955e-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="a955e-133">Vous pouvez également créer le jeu d’enregistrements hello *explicitement* avant l’ajout d’enregistrements tooit.</span><span class="sxs-lookup"><span data-stu-id="a955e-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="a955e-134">DNS Azure prend en charge les jeux d’enregistrements 'empty', qui peut agir comme un espace réservé tooreserve un nom DNS avant de créer des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="a955e-135">Jeux d’enregistrements vides est visibles dans hello Azure DNS plan de contrôle, mais n’apparaissent pas sur les serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="a955e-136">Jeux d’enregistrements est créés à l’aide de hello `az network dns record-set <record-type> create` commande.</span><span class="sxs-lookup"><span data-stu-id="a955e-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="a955e-137">Pour obtenir de l’aide, consultez l’article `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="a955e-138">Création d’enregistrement hello définie explicitement vous permet de propriétés du jeu d’enregistrements toospecify tels que hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) et les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a955e-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="a955e-139">[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="a955e-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="a955e-140">Hello exemple suivant crée un jeu d’enregistrements vide de type 'A' avec une durée de vie de 60 secondes, à l’aide de hello `--ttl` paramètre (forme abrégée : `-l`) :</span><span class="sxs-lookup"><span data-stu-id="a955e-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="a955e-141">Hello exemple suivant crée un jeu enregistrements avec deux entrées de métadonnées, « dept = finance » et « environnement = production », à l’aide de hello `--metadata` paramètre :</span><span class="sxs-lookup"><span data-stu-id="a955e-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="a955e-142">Après avoir créé un jeu d’enregistrements vide, les enregistrements peuvent être ajoutés à l’aide de `azure network dns record-set <record-type> set-record`, comme décrit dans [Création d’un enregistrement DNS](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="a955e-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="a955e-143">Créer des enregistrements d’autres types</span><span class="sxs-lookup"><span data-stu-id="a955e-143">Create records of other types</span></span>

<span data-ttu-id="a955e-144">Après avoir vu en détail comment toocreate 'A' enregistre, hello suivant exemples montrent comment enregistrement toocreate d’autres types d’enregistrements pris en charge par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="a955e-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="a955e-145">les paramètres de Hello utilisés enregistrement de hello toospecify données varient en fonction de type hello d’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="a955e-146">Par exemple, pour un enregistrement de type « A », vous spécifiez l’adresse de hello IPv4 avec le paramètre hello `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="a955e-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="a955e-147">Hello des paramètres pour chaque type d’enregistrement peut être à l’aide de `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="a955e-148">Dans chaque cas, nous montrons comment toocreate un enregistrement unique.</span><span class="sxs-lookup"><span data-stu-id="a955e-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="a955e-149">enregistrement de Hello est ajouté toohello existante du jeu d’enregistrements, ou un jeu d’enregistrements créé implicitement.</span><span class="sxs-lookup"><span data-stu-id="a955e-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="a955e-150">Pour plus d’informations sur la création de jeux d’enregistrements et la définition explicite des paramètres de jeu d’enregistrements, consultez [Création d’un jeu d’enregistrements DNS](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="a955e-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="a955e-151">Nous ne donnent pas une toocreate exemple un jeu d’enregistrements SOA, étant donné que SOA est créées et supprimées avec chaque zone DNS et ne peut pas être créée ou supprimée séparément.</span><span class="sxs-lookup"><span data-stu-id="a955e-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="a955e-152">Toutefois, [hello SOA peut être modifiée, comme indiqué dans un exemple plus loin](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="a955e-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="a955e-153">Créer un enregistrement AAAA</span><span class="sxs-lookup"><span data-stu-id="a955e-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="a955e-154">Créer un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="a955e-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="a955e-155">les normes DNS Hello n’autorisent pas les enregistrements CNAME au sommet de hello d’une zone (`--Name "@"`), ni font qu’ils autorisent les jeux d’enregistrements contenant plusieurs enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="a955e-156">Pour plus d’informations, voir [Enregistrements CNAME](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="a955e-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="a955e-157">Créer un enregistrement MX</span><span class="sxs-lookup"><span data-stu-id="a955e-157">Create an MX record</span></span>

<span data-ttu-id="a955e-158">Dans cet exemple, nous utilisons le nom du jeu d’enregistrements hello « @ » toocreate hello enregistrement MX au sommet de zone hello (dans ce cas, « contoso.com »).</span><span class="sxs-lookup"><span data-stu-id="a955e-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="a955e-159">Créer un enregistrement NS</span><span class="sxs-lookup"><span data-stu-id="a955e-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="a955e-160">Création d’un enregistrement PTR</span><span class="sxs-lookup"><span data-stu-id="a955e-160">Create a PTR record</span></span>

<span data-ttu-id="a955e-161">Dans ce cas, « my-arpa-zone.com' représente hello zone ARPA représentant votre plage IP.</span><span class="sxs-lookup"><span data-stu-id="a955e-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="a955e-162">Chaque enregistrement PTR dans cette zone correspond à adresse IP de tooan au sein de cette plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="a955e-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="a955e-163">nom de l’enregistrement Hello « 10 » est le dernier octet de hello d’adresse IP de hello dans cette plage IP représentée par cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a955e-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="a955e-164">Création d’un enregistrement SRV</span><span class="sxs-lookup"><span data-stu-id="a955e-164">Create an SRV record</span></span>

<span data-ttu-id="a955e-165">Lorsque vous créez un [jeu d’enregistrements SRV](dns-zones-records.md#srv-records), spécifiez hello  *\_service* et  *\_protocole* Bonjour nom du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="a955e-166">Il n’existe aucun besoin tooinclude « @ » Bonjour jeu d’enregistrements nom lors de la création d’un enregistrement SRV définie au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="a955e-167">Création d’un enregistrement TXT</span><span class="sxs-lookup"><span data-stu-id="a955e-167">Create a TXT record</span></span>

<span data-ttu-id="a955e-168">Hello suivant montre comment enregistrer des toocreate un TXT.</span><span class="sxs-lookup"><span data-stu-id="a955e-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="a955e-169">Pour plus d’informations sur la longueur maximale de la chaîne hello pris en charge dans les enregistrements TXT, consultez [enregistrements TXT](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="a955e-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="a955e-170">Obtention d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="a955e-170">Get a record set</span></span>

<span data-ttu-id="a955e-171">tooretrieve un jeu d’enregistrements existant, utilisez `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="a955e-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="a955e-172">Pour obtenir de l’aide, consultez l’article `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="a955e-173">Lorsque vous créez un enregistrement ou un jeu d’enregistrements, enregistrement de hello SET nom donné doit être un *relatif* nom, qui signifie qu’il doit exclure le nom de la zone hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="a955e-174">Vous devez également le type d’enregistrement toospecify hello, zone hello contenant hello enregistrement défini et hello contenant hello zone de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a955e-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="a955e-175">Hello exemple suivant récupère les enregistrement hello *www* d’un type de zone *contoso.com* dans le groupe de ressources *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a955e-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="a955e-176">Liste des jeux d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="a955e-176">List record sets</span></span>

<span data-ttu-id="a955e-177">Vous pouvez répertorier tous les enregistrements dans une zone DNS à l’aide de hello `az network dns record-set list` commande.</span><span class="sxs-lookup"><span data-stu-id="a955e-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="a955e-178">Pour obtenir de l’aide, consultez l’article `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="a955e-179">Cet exemple retourne tous les enregistrements définit dans la zone de hello *contoso.com*, dans le groupe de ressources *MyResourceGroup*, quel que soit le nom ou le type d’enregistrement :</span><span class="sxs-lookup"><span data-stu-id="a955e-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="a955e-180">Cet exemple retourne tous les jeux d’enregistrements qui correspondent aux hello donné du type d’enregistrement (dans ce cas, les enregistrements de 'A') :</span><span class="sxs-lookup"><span data-stu-id="a955e-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="a955e-181">Ajouter un enregistrement tooan existante du jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="a955e-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="a955e-182">Vous pouvez utiliser `az network dns record-set <record-type> set-record` les deux toocreate un enregistrement dans un nouvel enregistrement défini ou tooadd un enregistrement existant tooan enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a955e-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="a955e-183">Pour plus d’informations, consultez [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a955e-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="a955e-184">Suppression d’un enregistrement d’un jeu d'enregistrements existant.</span><span class="sxs-lookup"><span data-stu-id="a955e-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="a955e-185">tooremove DNS enregistrer à partir d’un jeu d’enregistrements existant, utilisez `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="a955e-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="a955e-186">Pour obtenir de l’aide, consultez l’article `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="a955e-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="a955e-187">Cette commande supprime un enregistrement DNS d’un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="a955e-188">Si le dernier enregistrement dans un jeu d’enregistrements de hello est supprimé, hello jeu d’enregistrements lui-même sont également supprimé.</span><span class="sxs-lookup"><span data-stu-id="a955e-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="a955e-189">jeu d’enregistrements vide tookeep hello utilisez hello `--keep-empty-record-set` option.</span><span class="sxs-lookup"><span data-stu-id="a955e-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="a955e-190">Vous devez toospecify hello enregistrement toobe est supprimé et zone hello qui doit être supprimée à partir, à l’aide de hello les mêmes paramètres que lors de la création d’un enregistrement à l’aide `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="a955e-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="a955e-191">Ces paramètres sont décrits dans [Création d’un enregistrement DNS](#create-a-dns-record) et [Création d’enregistrements d’autres types](#create-records-of-other-types) ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a955e-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="a955e-192">Hello suivant supprime de l’exemple hello un enregistrement avec la valeur « 1.2.3.4 » à partir de l’enregistrement de hello définir nommée *www* dans la zone de hello *contoso.com*, dans le groupe de ressources hello *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a955e-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="a955e-193">Modifier un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="a955e-193">Modify an existing record set</span></span>

<span data-ttu-id="a955e-194">Chaque jeu d’enregistrements contient une [durée de vie (TTL)](dns-zones-records.md#time-to-live), des [métadonnées](dns-zones-records.md#tags-and-metadata) et des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="a955e-195">Hello sections suivantes expliquent comment toomodify de ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="a955e-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="a955e-196">toomodify un enregistrement A, AAAA, MX, NS, PTR, SRV ou TXT</span><span class="sxs-lookup"><span data-stu-id="a955e-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="a955e-197">toomodify un enregistrement existant de type A, AAAA, MX, NS, PTR, SRV ou TXT, vous devez tout d’abord ajouter un nouvel enregistrement, puis hello un enregistrement existant.</span><span class="sxs-lookup"><span data-stu-id="a955e-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="a955e-198">Pour obtenir des instructions détaillées sur la façon de toodelete et ajouter des enregistrements, consultez hello les premières sections de cet article.</span><span class="sxs-lookup"><span data-stu-id="a955e-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="a955e-199">Hello, l’exemple suivant montre comment la corriger toomodify un enregistrement de « A », à partir de l’IP adresse 1.2.3.4 tooIP 5.6.7.8 :</span><span class="sxs-lookup"><span data-stu-id="a955e-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="a955e-200">Vous ne pouvez pas ajouter, supprimer ou modifier les enregistrements hello hello créé automatiquement NS jeu d’enregistrements au sommet de zone hello (`--Name "@"`, y compris les guillemets).</span><span class="sxs-lookup"><span data-stu-id="a955e-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="a955e-201">Pour ce jeu d’enregistrements, hello seules modifications autorisées sont jeu d’enregistrements de hello de toomodify durée de vie et les métadonnées.</span><span class="sxs-lookup"><span data-stu-id="a955e-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="a955e-202">toomodify un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="a955e-202">toomodify a CNAME record</span></span>

<span data-ttu-id="a955e-203">Contrairement à la plupart des autres types d’enregistrements, un jeu d’enregistrements CNAME ne peut contenir qu’un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a955e-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="a955e-204">Par conséquent, vous ne peut pas remplacer la valeur actuelle de hello en ajoutant un nouvel enregistrement et de suppression de l’enregistrement existant hello, que pour d’autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="a955e-205">Toomodify un enregistrement CNAME, utilisez `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="a955e-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="a955e-206">Pour obtenir de l’aide, consultez `az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="a955e-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="a955e-207">exemple Hello modifie jeu d’enregistrements CNAME hello *www* dans la zone de hello *contoso.com*, dans le groupe de ressources *MyResourceGroup*, toopoint trop 'www.fabrikam.net' à la place de son valeur existante :</span><span class="sxs-lookup"><span data-stu-id="a955e-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="a955e-208">toomodify un enregistrement SOA</span><span class="sxs-lookup"><span data-stu-id="a955e-208">toomodify an SOA record</span></span>

<span data-ttu-id="a955e-209">Contrairement à la plupart des autres types d’enregistrements, un jeu d’enregistrements CNAME ne peut contenir qu’un seul enregistrement.</span><span class="sxs-lookup"><span data-stu-id="a955e-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="a955e-210">Par conséquent, vous ne peut pas remplacer la valeur actuelle de hello en ajoutant un nouvel enregistrement et de suppression de l’enregistrement existant hello, que pour d’autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="a955e-211">Toomodify hello enregistrement SOA, utilisez `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="a955e-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="a955e-212">Pour obtenir de l’aide, consultez l’article `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="a955e-213">Hello suivant montre comment enregistrer des propriété tooset hello « email » de hello SOA de zone de hello *contoso.com* dans le groupe de ressources hello *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a955e-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="a955e-214">enregistrements toomodify NS au sommet de zone hello</span><span class="sxs-lookup"><span data-stu-id="a955e-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="a955e-215">jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="a955e-216">Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.</span><span class="sxs-lookup"><span data-stu-id="a955e-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="a955e-217">Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="a955e-218">Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="a955e-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="a955e-219">Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.</span><span class="sxs-lookup"><span data-stu-id="a955e-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="a955e-220">Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="a955e-221">Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="a955e-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="a955e-222">Bonjour à l’exemple suivant montre comment tooadd un enregistrement de noms supplémentaires server toohello NS définie les au sommet de zone hello :</span><span class="sxs-lookup"><span data-stu-id="a955e-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="a955e-223">définie des toomodify hello durée de vie d’un enregistrement existant</span><span class="sxs-lookup"><span data-stu-id="a955e-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="a955e-224">définie des toomodify hello durée de vie d’un enregistrement existant, utilisez `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="a955e-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="a955e-225">Pour obtenir de l’aide, consultez l’article `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="a955e-226">Bonjour à l’exemple suivant montre comment toomodify un jeu d’enregistrements durée de vie, dans ce cas too60 secondes :</span><span class="sxs-lookup"><span data-stu-id="a955e-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="a955e-227">définir des métadonnées de hello toomodify d’un enregistrement existant</span><span class="sxs-lookup"><span data-stu-id="a955e-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="a955e-228">[Métadonnées du jeu d’enregistrements](dns-zones-records.md#tags-and-metadata) peuvent être des données spécifiques à l’application tooassociate utilisées avec chaque jeu d’enregistrements, en tant que paires clé-valeur.</span><span class="sxs-lookup"><span data-stu-id="a955e-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="a955e-229">définir des métadonnées de hello toomodify d’un enregistrement existant, utilisez `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="a955e-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="a955e-230">Pour obtenir de l’aide, consultez l’article `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="a955e-231">Hello suivant montre comment toomodify un jeu d’enregistrements avec deux entrées de métadonnées, « dept = finance » et « environnement = production ».</span><span class="sxs-lookup"><span data-stu-id="a955e-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="a955e-232">Notez que toutes les métadonnées existantes sont *remplacé* par les valeurs hello donnés.</span><span class="sxs-lookup"><span data-stu-id="a955e-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="a955e-233">Supprimer un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="a955e-233">Delete a record set</span></span>

<span data-ttu-id="a955e-234">Jeux d’enregistrements peut être supprimés à l’aide de hello `az network dns record-set <record-type> delete` commande.</span><span class="sxs-lookup"><span data-stu-id="a955e-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="a955e-235">Pour obtenir de l’aide, consultez l’article `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="a955e-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="a955e-236">Suppression d’un jeu d’enregistrements supprime également tous les enregistrements dans le jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="a955e-237">Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="a955e-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="a955e-238">Ceux-ci sont créés automatiquement lorsque hello zone a été créé et sont automatiquement supprimés lorsque la zone de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="a955e-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="a955e-239">exemple Hello supprime hello jeu d’enregistrements nommé *www* d’un type de zone de hello *contoso.com* dans le groupe de ressources *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a955e-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="a955e-240">Vous êtes opération de suppression demandées tooconfirm hello.</span><span class="sxs-lookup"><span data-stu-id="a955e-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="a955e-241">toosuppress ce invite de commandes, utilisez hello `--yes` basculer.</span><span class="sxs-lookup"><span data-stu-id="a955e-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a955e-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a955e-242">Next steps</span></span>

<span data-ttu-id="a955e-243">Apprenez-en davantage sur les [zones et enregistrements dans Azure DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="a955e-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="a955e-244">Découvrez comment trop[protéger les zones et les enregistrements](dns-protect-zones-recordsets.md) lors de l’utilisation d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a955e-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
