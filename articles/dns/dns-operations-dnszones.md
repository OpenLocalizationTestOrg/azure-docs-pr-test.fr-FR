---
title: "Gérer des zones DNS dans Azure DNS - PowerShell | Microsoft Docs"
description: "Vous pouvez gérer des zones DNS à l’aide d’Azure Powershell. Cet article décrit comment mettre à jour, supprimer et créer des zones DNS sur Azure DNS."
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
ms.openlocfilehash: 92f1da660d875c76d5d826669d6c1d12018c3d0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-using-powershell"></a><span data-ttu-id="3a37a-104">Gestion des zones DNS à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a37a-104">How to manage DNS Zones using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3a37a-105">Portail</span><span class="sxs-lookup"><span data-stu-id="3a37a-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="3a37a-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a37a-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="3a37a-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3a37a-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="3a37a-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3a37a-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="3a37a-109">Cet article vous montre comment gérer vos zones DNS avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a37a-109">This article shows you how to manage your DNS zones by using Azure PowerShell.</span></span> <span data-ttu-id="3a37a-110">Vous pouvez également gérer vos zones DNS à l’aide de [l’interface de ligne de commande Azure](dns-operations-dnszones-cli.md) multiplateforme ou du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3a37a-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure portal.</span></span>

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a><span data-ttu-id="3a37a-111">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="3a37a-111">Create a DNS zone</span></span>

<span data-ttu-id="3a37a-112">Une zone DNS est créée à l’aide de l’applet de commande `New-AzureRmDnsZone` .</span><span class="sxs-lookup"><span data-stu-id="3a37a-112">A DNS zone is created by using the `New-AzureRmDnsZone` cmdlet.</span></span>

<span data-ttu-id="3a37a-113">L’exemple ci-dessous crée une zone DNS appelée *contoso.com* dans le groupe de ressources *MyResourceGroup* :</span><span class="sxs-lookup"><span data-stu-id="3a37a-113">The following example creates a DNS zone called *contoso.com* in the resource group called *MyResourceGroup*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="3a37a-114">L’exemple suivant montre comment créer une zone DNS avec deux [balises Azure Resource Manager](dns-zones-records.md#tags), *projet = demo* et *env = test* :</span><span class="sxs-lookup"><span data-stu-id="3a37a-114">The following example shows how to create a DNS zone with two [Azure Resource Manager tags](dns-zones-records.md#tags), *project = demo* and *env = test*:</span></span>

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a><span data-ttu-id="3a37a-115">Obtention d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="3a37a-115">Get a DNS zone</span></span>

<span data-ttu-id="3a37a-116">Pour récupérer une zone DNS, utilisez l’applet de commande `Get-AzureRmDnsZone` :</span><span class="sxs-lookup"><span data-stu-id="3a37a-116">To retrieve a DNS zone, use the `Get-AzureRmDnsZone` cmdlet.</span></span> <span data-ttu-id="3a37a-117">Cette opération retourne un objet de zone DNS correspondant à une zone existante dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="3a37a-117">This operation returns a DNS zone object corresponding to an existing zone in Azure DNS.</span></span> <span data-ttu-id="3a37a-118">Cet objet contient des données sur la zone (par exemple le nombre de jeux d’enregistrements), mais ne contient pas les jeux d’enregistrement eux-mêmes (voir `Get-AzureRmDnsRecordSet`).</span><span class="sxs-lookup"><span data-stu-id="3a37a-118">The object contains data about the zone (such as the number of record sets), but does not contain the record sets themselves (see `Get-AzureRmDnsRecordSet`).</span></span>

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

## <a name="list-dns-zones"></a><span data-ttu-id="3a37a-119">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="3a37a-119">List DNS zones</span></span>

<span data-ttu-id="3a37a-120">En omettant le nom de la zone dans `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3a37a-120">By omitting the zone name from `Get-AzureRmDnsZone`, you can enumerate all zones in a resource group.</span></span> <span data-ttu-id="3a37a-121">Cette opération renvoie un tableau d’objets de la zone.</span><span class="sxs-lookup"><span data-stu-id="3a37a-121">This operation returns an array of zone objects.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

<span data-ttu-id="3a37a-122">En omettant le nom de zone et le nom du groupe de ressources de `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones dans l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3a37a-122">By omitting both the zone name and the resource group name from `Get-AzureRmDnsZone`, you can enumerate all zones in the Azure subscription.</span></span>

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a><span data-ttu-id="3a37a-123">Mise à jour d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="3a37a-123">Update a DNS zone</span></span>

<span data-ttu-id="3a37a-124">Vous pouvez apporter des modifications à une ressource de zone DNS à l’aide de `Set-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="3a37a-124">Changes to a DNS zone resource can be made by using `Set-AzureRmDnsZone`.</span></span> <span data-ttu-id="3a37a-125">Cette applet de commande ne met pas à jour les jeux d’enregistrements DNS dans la zone (voir [Gestion des enregistrements DNS](dns-operations-recordsets.md)).</span><span class="sxs-lookup"><span data-stu-id="3a37a-125">This cmdlet does not update any of the DNS record sets within the zone (see [How to Manage DNS records](dns-operations-recordsets.md)).</span></span> <span data-ttu-id="3a37a-126">Elle est utilisée seulement pour mettre à jour les propriétés de la ressource de zone elle-même.</span><span class="sxs-lookup"><span data-stu-id="3a37a-126">It's only used to update properties of the zone resource itself.</span></span> <span data-ttu-id="3a37a-127">Les propriétés de zone accessibles en écriture sont actuellement limitées aux [« balises » Azure Resource Manager de la ressource de zone](dns-zones-records.md#tags).</span><span class="sxs-lookup"><span data-stu-id="3a37a-127">The writable zone properties are currently limited to the [Azure Resource Manager ‘tags’ for the zone resource](dns-zones-records.md#tags).</span></span>

<span data-ttu-id="3a37a-128">Utilisez l’une des options suivantes pour mettre à jour la zone DNS :</span><span class="sxs-lookup"><span data-stu-id="3a37a-128">Use one of the following two ways to update a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group"></a><span data-ttu-id="3a37a-129">Spécifier la zone en utilisant le nom de zone et le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3a37a-129">Specify the zone using the zone name and resource group</span></span>

<span data-ttu-id="3a37a-130">Cette approche remplace les balises de zone existantes par les valeurs spécifiées.</span><span class="sxs-lookup"><span data-stu-id="3a37a-130">This approach replaces the existing zone tags with the values specified.</span></span>

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="3a37a-131">Spécifier la zone en utilisant un objet $zone</span><span class="sxs-lookup"><span data-stu-id="3a37a-131">Specify the zone using a $zone object</span></span>

<span data-ttu-id="3a37a-132">Cette approche récupère l’objet existant de la zone, modifie les balises, puis valide les modifications.</span><span class="sxs-lookup"><span data-stu-id="3a37a-132">This approach retrieves the existing zone object, modifies the tags, and then commits the changes.</span></span> <span data-ttu-id="3a37a-133">De cette façon, les balises existantes peuvent être conservées.</span><span class="sxs-lookup"><span data-stu-id="3a37a-133">In this way, existing tags can be preserved.</span></span>

```powershell
# Get the zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="3a37a-134">Lors de l’utilisation de `Set-AzureRmDnsZone` avec un objet $zone, les [vérifications d’ETag](dns-zones-records.md#etags) sont utilisées pour éviter que les modifications simultanées soient remplacées.</span><span class="sxs-lookup"><span data-stu-id="3a37a-134">When using `Set-AzureRmDnsZone` with a $zone object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="3a37a-135">Le commutateur facultatif `-Overwrite` permet de supprimer ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="3a37a-135">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

## <a name="delete-a-dns-zone"></a><span data-ttu-id="3a37a-136">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="3a37a-136">Delete a DNS Zone</span></span>

<span data-ttu-id="3a37a-137">Les zones DNS peuvent être supprimées à l’aide de l’applet de commande `Remove-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="3a37a-137">DNS zones can be deleted using the `Remove-AzureRmDnsZone` cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="3a37a-138">Supprimer une zone DNS supprime également tous les enregistrements DNS de la zone.</span><span class="sxs-lookup"><span data-stu-id="3a37a-138">Deleting a DNS zone also deletes all DNS records within the zone.</span></span> <span data-ttu-id="3a37a-139">Il est impossible d’annuler cette opération.</span><span class="sxs-lookup"><span data-stu-id="3a37a-139">This operation cannot be undone.</span></span> <span data-ttu-id="3a37a-140">Si la zone DNS est en cours d’utilisation, les services utilisant la zone échouent lors de la suppression de la zone.</span><span class="sxs-lookup"><span data-stu-id="3a37a-140">If the DNS zone is in use, services using the zone will fail when the zone is deleted.</span></span>
>
><span data-ttu-id="3a37a-141">Pour vous protéger contre la suppression accidentelle de zones, consultez la page [Comment protéger des zones et enregistrements DNS](dns-protect-zones-recordsets.md).</span><span class="sxs-lookup"><span data-stu-id="3a37a-141">To protect against accidental zone deletion, see [How to protect DNS zones and records](dns-protect-zones-recordsets.md).</span></span>


<span data-ttu-id="3a37a-142">Utilisez l’une des options suivantes pour supprimer une zone DNS :</span><span class="sxs-lookup"><span data-stu-id="3a37a-142">Use one of the following two ways to delete a DNS zone:</span></span>

### <a name="specify-the-zone-using-the-zone-name-and-resource-group-name"></a><span data-ttu-id="3a37a-143">Spécifier la zone en utilisant le nom de zone et le nom de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="3a37a-143">Specify the zone using the zone name and resource group name</span></span>

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-the-zone-using-a-zone-object"></a><span data-ttu-id="3a37a-144">Spécifier la zone en utilisant un objet $zone</span><span class="sxs-lookup"><span data-stu-id="3a37a-144">Specify the zone using a $zone object</span></span>

<span data-ttu-id="3a37a-145">Vous pouvez spécifier la zone à supprimer à l’aide d’un objet `$zone` retourné par `Get-AzureRmDnsZone`.</span><span class="sxs-lookup"><span data-stu-id="3a37a-145">You can specify the zone to be deleted using a `$zone` object returned by `Get-AzureRmDnsZone`.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

<span data-ttu-id="3a37a-146">L’objet de zone peut également être redirigé au lieu d’être transmis en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="3a37a-146">The zone object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

<span data-ttu-id="3a37a-147">Comme avec `Set-AzureRmDnsZone`, la spécification de la zone avec un objet `$zone` active les vérifications d’ETag et permet de s’assurer que les modifications simultanées ne sont pas supprimées.</span><span class="sxs-lookup"><span data-stu-id="3a37a-147">As with `Set-AzureRmDnsZone`, specifying the zone using a `$zone` object enables Etag checks to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="3a37a-148">Utilisez le commutateur `-Overwrite` pour supprimer ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="3a37a-148">Use the `-Overwrite` switch to suppress these checks.</span></span>

## <a name="confirmation-prompts"></a><span data-ttu-id="3a37a-149">Invites de confirmation</span><span class="sxs-lookup"><span data-stu-id="3a37a-149">Confirmation prompts</span></span>

<span data-ttu-id="3a37a-150">Les applets de commande `New-AzureRmDnsZone`, `Set-AzureRmDnsZone` et `Remove-AzureRmDnsZone` prennent en charge les invites de confirmation.</span><span class="sxs-lookup"><span data-stu-id="3a37a-150">The `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, and `Remove-AzureRmDnsZone` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="3a37a-151">Les invites `New-AzureRmDnsZone` et `Set-AzureRmDnsZone` demandent une confirmation si la variable de préférence PowerShell `$ConfirmPreference` a la valeur `Medium` ou une valeur inférieure.</span><span class="sxs-lookup"><span data-stu-id="3a37a-151">Both `New-AzureRmDnsZone` and `Set-AzureRmDnsZone` prompt for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="3a37a-152">En raison de l’impact potentiellement élevé de la suppression d’une zone DNS, l’applet de commande `Remove-AzureRmDnsZone` vous demande de confirmer si la variable PowerShell `$ConfirmPreference` a une valeur autre que `None`.</span><span class="sxs-lookup"><span data-stu-id="3a37a-152">Due to the potentially high impact of deleting a DNS zone, the `Remove-AzureRmDnsZone` cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell variable has any value other than `None`.</span></span>

<span data-ttu-id="3a37a-153">Étant donné que la valeur par défaut `$ConfirmPreference` est `High`, seule la commande `Remove-AzureRmDnsZone` demande une confirmation par défaut.</span><span class="sxs-lookup"><span data-stu-id="3a37a-153">Since the default value for `$ConfirmPreference` is `High`, only `Remove-AzureRmDnsZone` prompts for confirmation by default.</span></span>

<span data-ttu-id="3a37a-154">Vous pouvez remplacer le paramétrage actuel de `$ConfirmPreference` par le paramètre `-Confirm`.</span><span class="sxs-lookup"><span data-stu-id="3a37a-154">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="3a37a-155">Si vous spécifiez les paramètres `-Confirm` ou `-Confirm:$True`, les applets de commande vous invitent à confirmer l’exécution.</span><span class="sxs-lookup"><span data-stu-id="3a37a-155">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="3a37a-156">Si vous spécifiez le paramètre `-Confirm:$False`, l’applet de commande ne demande pas de confirmation.</span><span class="sxs-lookup"><span data-stu-id="3a37a-156">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span>

<span data-ttu-id="3a37a-157">Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="3a37a-157">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a37a-158">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a37a-158">Next steps</span></span>

<span data-ttu-id="3a37a-159">Découvrez comment [gérer des jeux d’enregistrements et des enregistrements](dns-operations-recordsets.md) dans votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="3a37a-159">Learn how to [manage record sets and records](dns-operations-recordsets.md) in your DNS zone.</span></span>
<br>
<span data-ttu-id="3a37a-160">Découvrez comment [déléguer votre domaine à Azure DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="3a37a-160">Learn how to [delegate your domain to Azure DNS](dns-domain-delegation.md).</span></span>
<br>
<span data-ttu-id="3a37a-161">Examinez la [documentation de référence d’Azure DNS PowerShell](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="3a37a-161">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>

