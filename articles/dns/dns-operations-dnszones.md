---
title: aaaManage DNS zones DNS de Azure - PowerShell | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure Powershell. Cet article décrit comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a><span data-ttu-id="a65cf-104">Comment les Zones DNS toomanage à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a65cf-104">How toomanage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a65cf-105">Portail</span><span class="sxs-lookup"><span data-stu-id="a65cf-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="a65cf-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a65cf-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="a65cf-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a65cf-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="a65cf-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a65cf-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="a65cf-109">Cet article explique comment toomanage votre DNS zones à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a65cf-109">This article shows you how toomanage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="a65cf-110">Vous pouvez également gérer vos zones DNS à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-dnszones-cli.md) ou de bienvenue du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a65cf-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="a65cf-111">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a65cf-111">Create a DNS zone</span></span>

<span data-ttu-id="a65cf-112">Une zone DNS est créée à l’aide de hello `New-AzureRmDnsZone` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a65cf-112">A DNS zone is created by using hello `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="a65cf-113">Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="a65cf-113">hello following example creates a DNS zone called *contoso.com* in hello resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a65cf-114">Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*:</span><span class="sxs-lookup"><span data-stu-id="a65cf-114">hello following example shows how toocreate a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="a65cf-115">Obtention d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a65cf-115">Get a DNS zone</span></span>

<span data-ttu-id="a65cf-116">tooretrieve une zone DNS, utilisez hello `Get-AzureRmDnsZone` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a65cf-116">tooretrieve a DNS zone, use hello `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="a65cf-117">Cette opération retourne l’objet correspondant tooan zone existante dans le système DNS Azure de zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a65cf-117">This operation returns a DNS zone object corresponding tooan existing zone in Azure DNS.</span></span> <span data-ttu-id="a65cf-118">Hello objet contient des données sur fuseau hello (par exemple, le nombre de hello de jeux d’enregistrements), mais ne contient pas de jeux d’enregistrements hello eux-mêmes (voir `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="a65cf-118">hello object contains data about hello zone (such as hello number of record sets), but does not contain hello record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a><span data-ttu-id="a65cf-119">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="a65cf-119">List DNS zones</span></span>

<span data-ttu-id="a65cf-120">En omettant le nom à partir de la zone hello `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a65cf-120">By omitting hello zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="a65cf-121">Cette opération renvoie un tableau d’objets de la zone.</span><span class="sxs-lookup"><span data-stu-id="a65cf-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="a65cf-122">En omettant le nom de la zone hello et nom du groupe de ressources à partir de hello `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones de hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a65cf-122">By omitting both hello zone name and hello resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in hello Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="a65cf-123">Mise à jour d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a65cf-123">Update a DNS zone</span></span>

<span data-ttu-id="a65cf-124">Modifie la ressource de zone DNS peut être effectuée à l’aide de tooa `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a65cf-124">Changes tooa DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="a65cf-125">Cette applet de commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="a65cf-125">This cmdlet does not update any of hello DNS record sets within hello zone (see [How tooManage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="a65cf-126">Elle est utilisée uniquement tooupdate des propriétés de ressource de zone hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="a65cf-126">It's only used tooupdate properties of hello zone resource itself.</span></span> <span data-ttu-id="a65cf-127">propriétés de la zone accessible en écriture Hello sont actuellement limitée toohello [Azure Resource Manager « balises » pour les ressources de la zone hello](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="a65cf-127">hello writable zone properties are currently limited toohello [Azure Resource Manager ‘tags’ for hello zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="a65cf-128">Utilisez une des hello suivant de deux façons tooupdate d’une zone DNS :</span><span class="sxs-lookup"><span data-stu-id="a65cf-128">Use one of hello following two ways tooupdate a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a><span data-ttu-id="a65cf-129">Spécifiez la zone hello à l’aide du groupe de nom et les ressources de la zone hello</span><span class="sxs-lookup"><span data-stu-id="a65cf-129">Specify hello zone using hello zone name and resource group</span></span>

<span data-ttu-id="a65cf-130">Cette approche remplace les balises de zone hello existantes avec les valeurs hello spécifiées.</span><span class="sxs-lookup"><span data-stu-id="a65cf-130">This approach replaces hello existing zone tags with hello values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="a65cf-131">Spécifiez la zone hello à l’aide d’un objet $zone</span><span class="sxs-lookup"><span data-stu-id="a65cf-131">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="a65cf-132">Cette approche récupère l’objet de zone hello existant, modifie les balises hello, puis valide les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="a65cf-132">This approach retrieves hello existing zone object, modifies hello tags, and then commits hello changes.</span></span> <span data-ttu-id="a65cf-133">De cette façon, les balises existantes peuvent être conservées.</span><span class="sxs-lookup"><span data-stu-id="a65cf-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a65cf-134">Lorsque vous utilisez `Set-AzureRmDnsZone` avec un objet $zone, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées.</span><span class="sxs-lookup"><span data-stu-id="a65cf-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="a65cf-135">Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="a65cf-135">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="a65cf-136">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a65cf-136">Delete a DNS Zone</span></span>

<span data-ttu-id="a65cf-137">Zones DNS peuvent être supprimés à l’aide de hello `Remove-AzureRmDnsZone` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a65cf-137">DNS zones can be deleted using hello `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="a65cf-138">Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="a65cf-138">Deleting a DNS zone also deletes all DNS records within hello zone.</span></span> <span data-ttu-id="a65cf-139">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="a65cf-139">This operation cannot be undone.</span></span> <span data-ttu-id="a65cf-140">Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.</span><span class="sxs-lookup"><span data-stu-id="a65cf-140">If hello DNS zone is in use, services using hello zone will fail when hello zone is deleted.</span></span>
>
><span data-ttu-id="a65cf-141">tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="a65cf-141">tooprotect against accidental zone deletion, see [How tooprotect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="a65cf-142">Utilisez une des hello suivant de deux façons toodelete d’une zone DNS :</span><span class="sxs-lookup"><span data-stu-id="a65cf-142">Use one of hello following two ways toodelete a DNS zone:</span></span>

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a><span data-ttu-id="a65cf-143">Spécifiez la zone hello à l’aide du nom de la zone hello et nom de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a65cf-143">Specify hello zone using hello zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a><span data-ttu-id="a65cf-144">Spécifiez la zone hello à l’aide d’un objet $zone</span><span class="sxs-lookup"><span data-stu-id="a65cf-144">Specify hello zone using a $zone object</span></span>

<span data-ttu-id="a65cf-145">Vous pouvez spécifier hello zone toobe est supprimé à l’aide un `$zone` objet retourné par `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="a65cf-145">You can specify hello zone toobe deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="a65cf-146">objet de fuseau Hello peut également être transmis au lieu de passé en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="a65cf-146">hello zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="a65cf-147">Comme avec `Set-AzureRmDnsZone`, en spécifiant hello à l’aide de la zone un `$zone` Active Etag vérifie les modifications simultanées tooensure ne sont pas supprimées de l’objet.</span><span class="sxs-lookup"><span data-stu-id="a65cf-147">As with `Set-AzureRmDnsZone`, specifying hello zone using a `$zone` object enables Etag checks tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="a65cf-148">Hello d’utilisation `-Overwrite` commutateur toosuppress ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="a65cf-148">Use hello `-Overwrite` switch toosuppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="a65cf-149">Invites de confirmation</span><span class="sxs-lookup"><span data-stu-id="a65cf-149">Confirmation prompts</span></span>

<span data-ttu-id="a65cf-150">Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, et `Remove-AzureRmDnsZone` prend en charge les applets de commande toutes les invites de confirmation.</span><span class="sxs-lookup"><span data-stu-id="a65cf-150">hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="a65cf-151">Les deux `New-AzureRmDnsZone` et `Set-AzureRmDnsZone` demander confirmation si hello `$ConfirmPreference` a la valeur de variable de préférence PowerShell `Medium` ou inférieure.</span><span class="sxs-lookup"><span data-stu-id="a65cf-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="a65cf-152">En raison de toohello potentiellement fort impact de la suppression d’une zone DNS, hello `Remove-AzureRmDnsZone` applet de commande vous demande de confirmer si hello `$ConfirmPreference` PowerShell variable a une valeur autre que `None`.</span><span class="sxs-lookup"><span data-stu-id="a65cf-152">Due toohello potentially high impact of deleting a DNS zone, hello `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="a65cf-153">Depuis la valeur par défaut de hello `$ConfirmPreference` est `High`, seule `Remove-AzureRmDnsZone` demande confirmation par défaut.</span><span class="sxs-lookup"><span data-stu-id="a65cf-153">Since hello default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="a65cf-154">Vous pouvez remplacer hello actuel `$ConfirmPreference` paramètre à l’aide de hello `-Confirm` paramètre.</span><span class="sxs-lookup"><span data-stu-id="a65cf-154">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="a65cf-155">Si vous spécifiez `-Confirm` ou `-Confirm:$True` , hello applet de commande vous demande confirmation avant qu’il s’exécute.</span><span class="sxs-lookup"><span data-stu-id="a65cf-155">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="a65cf-156">Si vous spécifiez `-Confirm:$False` , applet de commande hello ne vous demande pas de confirmation.</span><span class="sxs-lookup"><span data-stu-id="a65cf-156">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="a65cf-157">Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="a65cf-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a65cf-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a65cf-158">Next steps</span></span>

<span data-ttu-id="a65cf-159">Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-operations-recordsets.md) dans votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a65cf-159">Learn how too[manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="a65cf-160">Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a65cf-160">Learn how too[delegate your domain tooAzure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="a65cf-161">Hello de révision [documentation de référence PowerShell pour Azure DNS](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="a65cf-161">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

