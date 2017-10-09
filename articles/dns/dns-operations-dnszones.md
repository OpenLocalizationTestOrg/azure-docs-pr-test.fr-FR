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
# <a name="how-toomanage-dns-zones-using-powershell"></a>Comment les Zones DNS toomanage à l’aide de PowerShell

> [!div class="op_single_selector"]
> * [Portail](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Cet article explique comment toomanage votre DNS zones à l’aide d’Azure PowerShell. Vous pouvez également gérer vos zones DNS à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-dnszones-cli.md) ou de bienvenue du portail Azure.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>Création d’une zone DNS

Une zone DNS est créée à l’aide de hello `New-AzureRmDnsZone` applet de commande.

Hello exemple suivant crée une zone DNS appelée *contoso.com* dans le groupe de ressources hello appelé *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello suivant montre comment la zone avec deux toocreate DNS [Azure Resource Manager balises](dns-zones-records.md#tags), *projet = demo* et *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Obtention d’une zone DNS

tooretrieve une zone DNS, utilisez hello `Get-AzureRmDnsZone` applet de commande. Cette opération retourne l’objet correspondant tooan zone existante dans le système DNS Azure de zone DNS. Hello objet contient des données sur fuseau hello (par exemple, le nombre de hello de jeux d’enregistrements), mais ne contient pas de jeux d’enregistrements hello eux-mêmes (voir `Get-AzureRmDnsRecordSet`).

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

## <a name="list-dns-zones"></a>Création de la liste des zones DNS

En omettant le nom à partir de la zone hello `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones d’un groupe de ressources. Cette opération renvoie un tableau d’objets de la zone.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

En omettant le nom de la zone hello et nom du groupe de ressources à partir de hello `Get-AzureRmDnsZone`, vous pouvez énumérer toutes les zones de hello abonnement Azure.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Mise à jour d’une zone DNS

Modifie la ressource de zone DNS peut être effectuée à l’aide de tooa `Set-AzureRmDnsZone`. Cette applet de commande ne met pas à jour des jeux d’enregistrements DNS hello dans la zone de hello (consultez [comment les enregistrements DNS tooManage](dns-operations-recordsets.md)). Elle est utilisée uniquement tooupdate des propriétés de ressource de zone hello lui-même. propriétés de la zone accessible en écriture Hello sont actuellement limitée toohello [Azure Resource Manager « balises » pour les ressources de la zone hello](dns-zones-records.md#tags).

Utilisez une des hello suivant de deux façons tooupdate d’une zone DNS :

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Spécifiez la zone hello à l’aide du groupe de nom et les ressources de la zone hello

Cette approche remplace les balises de zone hello existantes avec les valeurs hello spécifiées.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Spécifiez la zone hello à l’aide d’un objet $zone

Cette approche récupère l’objet de zone hello existant, modifie les balises hello, puis valide les modifications hello. De cette façon, les balises existantes peuvent être conservées.

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

Lorsque vous utilisez `Set-AzureRmDnsZone` avec un objet $zone, [Etag vérifie](dns-zones-records.md#etags) servent tooensure des modifications simultanées ne sont pas remplacées. Vous pouvez utiliser hello facultatif `-Overwrite` commutateur toosuppress ces vérifications.

## <a name="delete-a-dns-zone"></a>Suppression d’une zone DNS

Zones DNS peuvent être supprimés à l’aide de hello `Remove-AzureRmDnsZone` applet de commande.

> [!NOTE]
> Suppression d’une zone DNS supprime également tous les enregistrements DNS dans la zone de hello. Il est impossible d’annuler cette opération. Si la zone DNS de hello est en cours d’utilisation, les services à l’aide de la zone de hello échoue lors de la zone de hello est supprimée.
>
>tooprotect contre la suppression accidentelle de zone, consultez [comment tooprotect DNS zones et enregistrements](dns-protect-zones-recordsets.md).


Utilisez une des hello suivant de deux façons toodelete d’une zone DNS :

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Spécifiez la zone hello à l’aide du nom de la zone hello et nom de groupe de ressources

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Spécifiez la zone hello à l’aide d’un objet $zone

Vous pouvez spécifier hello zone toobe est supprimé à l’aide un `$zone` objet retourné par `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

objet de fuseau Hello peut également être transmis au lieu de passé en tant que paramètre :

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

Comme avec `Set-AzureRmDnsZone`, en spécifiant hello à l’aide de la zone un `$zone` Active Etag vérifie les modifications simultanées tooensure ne sont pas supprimées de l’objet. Hello d’utilisation `-Overwrite` commutateur toosuppress ces vérifications.

## <a name="confirmation-prompts"></a>Invites de confirmation

Hello `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, et `Remove-AzureRmDnsZone` prend en charge les applets de commande toutes les invites de confirmation.

Les deux `New-AzureRmDnsZone` et `Set-AzureRmDnsZone` demander confirmation si hello `$ConfirmPreference` a la valeur de variable de préférence PowerShell `Medium` ou inférieure. En raison de toohello potentiellement fort impact de la suppression d’une zone DNS, hello `Remove-AzureRmDnsZone` applet de commande vous demande de confirmer si hello `$ConfirmPreference` PowerShell variable a une valeur autre que `None`.

Depuis la valeur par défaut de hello `$ConfirmPreference` est `High`, seule `Remove-AzureRmDnsZone` demande confirmation par défaut.

Vous pouvez remplacer hello actuel `$ConfirmPreference` paramètre à l’aide de hello `-Confirm` paramètre. Si vous spécifiez `-Confirm` ou `-Confirm:$True` , hello applet de commande vous demande confirmation avant qu’il s’exécute. Si vous spécifiez `-Confirm:$False` , applet de commande hello ne vous demande pas de confirmation.

Pour plus d’informations sur les paramètres `-Confirm` et `$ConfirmPreference`, voir [À propos des variables de préférence](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[gérer les jeux d’enregistrements et les enregistrements](dns-operations-recordsets.md) dans votre zone DNS.
<br>
Découvrez comment trop[déléguer votre tooAzure de domaine DNS](dns-domain-delegation.md).
<br>
Hello de révision [documentation de référence PowerShell pour Azure DNS](/powershell/module/azurerm.dns).

