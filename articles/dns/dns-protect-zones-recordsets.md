---
title: aaaProtecting Zones et enregistrements DNS | Documents Microsoft
description: "Comment les zones DNS tooprotect et enregistrement définit dans le système DNS de Microsoft Azure."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a>Comment tooprotect DNS zones et enregistrements

Les enregistrements et zones DNS sont des ressources critiques. La suppression d’une zone DNS, voire d’un seul enregistrement DNS, peut entraîner une interruption de service totale.  Il est donc important que les zones et enregistrements DNS critiques soient protégés contre toute modification non autorisée ou accidentelle.

Cet article explique comment Azure DNS permet de vous tooprotect vos zones et enregistrements DNS contre de telles modifications.  Nous appliquons deux puissantes fonctionnalités de sécurité d’Azure Resource Manager : le [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md) et les [verrous de ressources](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Contrôle d’accès en fonction du rôle

Le contrôle d’accès en fonction du rôle (RBAC) Azure permet une gestion précise de l’accès pour les clients, groupes et ressources Azure. À l’aide de RBAC, vous pouvez accorder précisément hello quantité accès que les utilisateurs doivent tooperform leur travail. Pour plus d’informations sur la gestion des droits d’accès avec RBAC, voir [Qu’est-ce que le contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>rôle de « Collaborateur de Zone DNS » Hello

rôle de « Collaborateur de Zone DNS » Hello est un rôle intégré fourni par Azure pour la gestion des ressources DNS.  Affectation de collaborateur de Zone DNS autorisations tooa utilisateur ou un groupe permet de ce regroupement des ressources DNS toomanage, mais pas les ressources d’un autre type.

Par exemple, groupe de ressources hello 'myzones' contient les cinq zones de Contoso Corporation. Accorder hello DNS administrateur « Collaborateur de Zone DNS » autorisations toothat groupe de ressources, permet un contrôle total sur les zones DNS. Il permet également d’éviter l’octroi d’autorisations inutiles, par exemple l’administrateur DNS hello ne peut pas créer ou arrêter les Machines virtuelles.

autorisations de RBAC Hello la plus simple façon tooassign est [via le portail Azure de hello](../active-directory/role-based-access-control-configure.md).  Ouvrez le panneau hello « contrôle d’accès (IAM) » pour le groupe de ressources hello, puis 'Add', puis sur rôle de « Collaborateur de Zone DNS » hello et les utilisateurs de sélectionner hello requis ou groupes des autorisations toogrant.

![Niveau de groupe de ressources RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac1.png)

Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>RBAC au niveau zone 

Les règles RBAC Azure peuvent être appliqués tooa abonnement, un groupe ou tooan individuelle ressource. Dans les cas de hello de Azure DNS, cette ressource peut être une zone DNS individuelle, ou même un jeu d’enregistrements individuel.

Par exemple, groupe de ressources hello 'myzones' contient hello zone « contoso.com » et sous-zone 'customers.contoso.com' dans lequel les enregistrements CNAME sont créés pour chaque compte client.  Hello compte utilisé toomanage ces enregistrements CNAME doivent être attribués autorisations toocreate enregistrements dans la zone « customers.contoso.com » hello, il ne doit comporter accès toohello autres zones.

Les autorisations de niveau zone RBAC peuvent être accordées via hello portail Azure.  Pour ouvrir Panneau de 'Contrôle d’accès (IAM)' hello pour la zone de hello, puis 'Add', puis sur rôle de « Collaborateur de Zone DNS » hello et les utilisateurs de sélectionner hello requis ou groupes des autorisations toogrant.

![Zone DNS de niveau RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac2.png)

Vous pouvez également [accorder des autorisations à l’aide d’Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>RBAC au niveau jeu d’enregistrements

Nous pouvons aller plus loin. Envisagez d’administrateur de messagerie hello pour Contoso Corporation, qui a besoin d’accès toohello MX et les enregistrements TXT au sommet de hello de zone de « contoso.com » hello.  Elle ne doivent accéder à tooany autres enregistrements MX ou TXT ou tooany les enregistrements d’un autre type.  DNS Azure permet de vous tooassign des autorisations à hello jeu d’enregistrements niveau tooprecisely hello enregistrements hello administrateur de messagerie a besoin d’accéder à.  Hello administrateur de messagerie est accordé avec précision les contrôle hello elle a besoin et est toomake Impossible de toutes les autres modifications.

Autorisations de RBAC de niveau de jeu d’enregistrements peuvent être configurées via hello portail Azure, à l’aide du bouton de hello « utilisateurs » dans le panneau de jeu d’enregistrements hello :

![Jeu d’enregistrements au niveau RBAC via hello portail Azure](./media/dns-protect-zones-recordsets/rbac3.png)

Vous pouvez également accorder les autorisations RBAC au niveau jeu d’enregistrements en utilisant [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) :

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

commande équivalent Hello est également [disponible via hello CLI d’Azure](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Rôles personnalisés

Hello intégré « Collaborateur de Zone DNS » rôle permet d’un contrôle total sur une ressource DNS. Il est également possible de toobuild votre propre client Azure rôles, contrôle de tooprovide même plus précise.

Prenez de nouveau exemple hello dans laquelle un enregistrement CNAME dans la zone hello 'customers.contoso.com' est créé pour chaque compte client de Contoso Corporation.  Hello compte utilisé toomanage ces enregistrements CNAME doit être accordées autorisation toomanage enregistrements CNAME du uniquement.  Il est impossible toomodify des enregistrements d’autres types (telles que la modification des enregistrements MX) ou effectuer des opérations de niveau zone telles que supprimer de la zone.

Bonjour à l’exemple suivant montre une définition de rôle personnalisé pour la gestion des enregistrements CNAME uniquement :

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

Hello propriété Actions définit hello les autorisations spécifiques à DNS suivantes :

* `Microsoft.Network/dnsZones/CNAME/*` accorde un contrôle total sur les enregistrements CNAME.
* `Microsoft.Network/dnsZones/read`accorde les zones DNS tooread autorisation, mais pas les toomodify les, l’activation de toosee vous hello zone dans quel hello CNAME est créée.

Hello Actions restantes sont copiées à partir de hello [rôle intégré du collaborateur de Zone DNS](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> À l’aide d’un tooprevent de rôle RBAC personnalisé, suppression de l’enregistrement définit alors qu’en autorisant toobe mis à jour n’est pas un contrôle efficace. Cela empêche la suppression de jeux d’enregistrements, mais pas leur modification.  Modifications autorisées incluent l’ajout et suppression d’enregistrements de jeu d’enregistrements hello, notamment la suppression de tous les enregistrements tooleave un jeu d’enregistrements 'empty'. Cela a hello même effet que la suppression de l’enregistrement hello définie à partir d’un point de vue de la résolution DNS.

Les définitions de rôle personnalisé ne peut actuellement être définies via hello portail Azure. Vous pouvez créer un rôle personnalisé basé sur cette définition de rôle en utilisant Azure PowerShell :

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Il peut également être créé via hello CLI d’Azure :

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Hello rôle peut ensuite être attribué Bonjour même façon que les rôles intégrés, comme décrit précédemment dans cet article.

Pour plus d’informations sur la façon dont toocreate, gérer et attribuer des rôles personnalisés, consultez [des rôles personnalisés dans Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Verrous de ressources

Ajout tooRBAC, Azure Resource Manager prend en charge un autre type de contrôle de sécurité, à savoir les too'lock possibilité hello' ressources. Lorsque les règles RBAC vous toocontrol hello les actions d’autorisation des utilisateurs et groupes spécifiques, verrous des ressources toohello appliqué des ressources et sont en vigueur dans tous les utilisateurs et les rôles. Pour plus d’informations, consultez [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

Il existe deux types de verrous de ressources : **DoNotDelete** (Ne pas supprimer) et **ReadOnly** (Lecture seule). Ils peuvent être appliqués zone DNS de tooa ou de jeu d’enregistrements individuels tooan.  Hello sections suivantes décrivent plusieurs scénarios courants et comment toosupport les à l’aide de verrous de ressources.

### <a name="protecting-against-all-changes"></a>Protection contre toute modification

tooprevent toutes les modifications apportées, appliquez une zone toohello de verrou en lecture seule.  Cela empêche toute création, modification ou suppression de jeux d’enregistrements.

Verrous de ressources de niveau zone peuvent être créés via hello portail Azure.  À partir du Panneau de zone DNS hello, cliquez sur « Verrous », puis 'Add' :

![Verrous de ressources de niveau zone via hello portail Azure](./media/dns-protect-zones-recordsets/locks1.png)

Vous pouvez également créer des verrous de ressources au niveau zone via Azure PowerShell :

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Configuration des verrous de ressources Azure n’est actuellement pas pris en charge via hello CLI d’Azure.

### <a name="protecting-individual-records"></a>Protection d’enregistrements spécifiques

tooprevent un enregistrement DNS existant défini contre la modification, appliquer un jeu d’enregistrements toohello verrou en lecture seule.

> [!NOTE]
> Application d’un tooa de verrou DoNotDelete jeu d’enregistrements n’est pas un contrôle efficace. Il empêche hello jeu d’enregistrements d’être supprimé, mais il ne l’empêche pas d’être modifiées.  Modifications autorisées incluent l’ajout et suppression d’enregistrements de jeu d’enregistrements hello, notamment la suppression de tous les enregistrements tooleave un jeu d’enregistrements 'empty'. Cela a hello même effet que la suppression de l’enregistrement hello définie à partir d’un point de vue de la résolution DNS.

Vous pouvez actuellement configurer des verrous de ressources au niveau jeu d’enregistrements uniquement à l’aide d’Azure PowerShell.  Elles ne sont pas prises en charge dans hello portail Azure ou CLI d’Azure.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Protection contre la suppression de zone

Lorsqu’une zone est supprimée dans le système DNS Azure, tous les jeux d’enregistrements dans la zone de hello sont également supprimés.  Il est impossible d’annuler cette opération.  Suppression accidentelle d’une zone critique a toohave potentielle de hello un impact significatif pour l’entreprise.  Il est donc très important tooprotect contre la suppression accidentelle de zone.

Une zone de tooa DoNotDelete verrou empêche les zone hello d’être supprimé.  Toutefois, étant donné que les verrous sont héritées par les ressources enfants, elle évite également les jeux d’enregistrements dans la zone hello d’être supprimé, ce qui peut être indésirable.  En outre, comme décrit dans la Remarque hello ci-dessus, il est également inefficace, car les enregistrements peuvent toujours être supprimés à partir de jeux d’enregistrements existants hello.

En guise d’alternative, envisagez d’appliquer un enregistrement tooa de verrou DoNotDelete définie dans la zone hello, par exemple de jeu d’enregistrements hello SOA.  Étant donné que la zone de hello ne peut pas être supprimée sans supprimer également les jeux d’enregistrements hello, cela protège contre la suppression de zone, tout en permettant aux jeux d’enregistrements dans toobe de zone hello modifiées librement. Si une tentative est faite de zone de hello toodelete, Azure Resource Manager détecte cela serait également supprimer le jeu d’enregistrements hello SOA et blocs hello appel car hello SOA est verrouillé.  Aucun jeu d’enregistrements n’est supprimé.

Hello suivant de commande PowerShell crée un verrou DoNotDelete par rapport à l’enregistrement SOA de hello Hello donné zone :

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Une autre façon tooprevent la suppression accidentelle de zone est en utilisant un opérateur de rôle personnalisé tooensure hello et toomanage des comptes de service que vos zones ne pas avoir de zone supprimer des autorisations. Lorsque vous avez besoin d’une zone de toodelete, vous pouvez appliquer une suppression en deux étapes, autorisations de suppression de zone accorder premier (à l’étendue de la zone hello, tooprevent suppression d’une zone de hello) et la deuxième zone de hello toodelete.

Cette seconde approche a l’avantage hello qu’il fonctionne pour toutes les zones accessibles par ces comptes, sans avoir à tooremember toocreate tous les verrous. Il a inconvénient hello que tous les comptes avec des autorisations de suppression de zone, telles que le propriétaire d’abonnement hello, toujours accidentellement à supprimer une zone critique.

Il est possible de toouse les deux approches, verrous des ressources et des rôles personnalisés, à hello même moment, la protection de zone tooDNS une approche de défense en profondeur.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’utilisation de RBAC, consultez [commencer avec la gestion des accès Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).
* Pour plus d’informations sur l’utilisation des verrous de ressources, voir [Verrouiller des ressources avec Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).

