---
title: "aaaCreate des rôles personnalisés pour Azure RBAC. | Documents Microsoft"
description: "Découvrez comment toodefine des rôles personnalisés avec du contrôle d’accès pour la gestion d’identité plus précise dans votre abonnement Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Créer des rôles personnalisés pour le contrôle d’accès en fonction du rôle Azure
Créer un rôle personnalisé dans le contrôle d’accès du (RBAC) si aucun des rôles intégrés de hello répond à vos besoins spécifiques. Des rôles personnalisés peuvent être créés à l’aide de [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) et hello [API REST](role-based-access-control-manage-access-rest.md). Tout comme les rôles intégrés, vous pouvez affecter toousers de rôles personnalisés, des groupes et des applications au niveau d’abonnement, de groupe de ressources et de portées de ressource. Les rôles personnalisés sont stockés dans un client Azure AD et peuvent être partagés entre les abonnements.

Chaque client peut créer des rôles personnalisés de too2000. 

Hello suivant montre un rôle personnalisé pour la surveillance et le redémarrage des ordinateurs virtuels :

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Actions
Hello **Actions** propriété d’un rôle personnalisé spécifie hello opérations Azure toowhich hello rôle accorde un accès. Il s’agit d’un ensemble de chaînes d’opération qui identifient les opérations sécurisables des fournisseurs de ressources Azure. Chaînes d’opération suivent le format hello `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Chaînes d’opération qui contiennent des caractères génériques (\*) tooall les opérations qui correspondent à la chaîne d’opération hello accorder l’accès. Exemple :

* `*/read`octroie accéder à des opérations de tooread pour tous les types de ressources de tous les fournisseurs de ressources Azure.
* `Microsoft.Compute/*`octroie accéder à des opérations de tooall pour tous les types de ressource dans le fournisseur de ressources Microsoft.Compute hello.
* `Microsoft.Network/*/read`octroie accéder à des opérations de tooread pour tous les types de ressource dans le fournisseur de ressources Microsoft.Network hello de Azure.
* `Microsoft.Compute/virtualMachines/*`octroie accéder à des opérations de tooall des ordinateurs virtuels et de ses types de ressources enfants.
* `Microsoft.Web/sites/restart/Action`octroie accéder aux sites Web de toorestart.

Utilisez `Get-AzureRmProviderOperation` (dans PowerShell) ou `azure provider operations show` (dans Azure CLI) opérations toolist des fournisseurs de ressources Azure. Vous pouvez également utiliser ces tooverify commandes qu’une chaîne de l’opération est valide et les chaînes d’opération tooexpand génériques.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Capture d’écran PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Capture d’écran de l’interface de ligne de commande Azure ; les opérations du fournisseur azure affichent « Microsoft.Compute/virtualMachines/\*/action » ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Hello d’utilisation **NotActions** propriété si hello d’opérations que vous souhaitez tooallow plus facilement définie en excluant les opérations restreintes. accès accordé par un rôle personnalisé Hello est calculé en soustrayant hello **NotActions** opérations hello **Actions** operations.

> [!NOTE]
> Si un utilisateur est assigné à un rôle qui exclut une opération dans **NotActions**et est affectée à un second rôle qui accorde l’accès toohello même opération, utilisateur de hello est autorisée tooperform cette opération. **NotActions** n’est pas une instruction deny de règle : il est simplement un toocreate facilement un ensemble d’opérations autorisées lorsque des opérations spécifiques doivent toobe exclu.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Hello **AssignableScopes** la propriété du rôle personnalisé de hello spécifie étendues hello (des abonnements, des groupes de ressources ou des ressources) au sein de quel hello rôle personnalisé est disponible pour l’attribution. Vous pouvez faire de rôle personnalisé hello disponibles pour l’assignation dans uniquement les abonnements hello ou groupes de ressources qui nécessitent et pas l’utilisateur l’encombrement de l’expérience pour rest hello d’abonnements de hello ou des groupes de ressources.

Voici des exemples d’étendues assignables valides :

* « / subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e », « / subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624 » - permet de disponible pour l’attribution de rôle de hello dans deux abonnements.
* « / subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e » - permet de disponible pour l’attribution de rôle de hello dans un seul abonnement.
* « / abonnements/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/réseau » - rend hello rôle disponible pour l’assignation uniquement dans le groupe de ressources réseau hello.

> [!NOTE]
> Vous devez utiliser au moins un abonnement, groupe de ressources ou ID de ressource.
>
>

## <a name="custom-roles-access-control"></a>Contrôle d’accès des rôles personnalisés
Hello **AssignableScopes** la propriété du rôle personnalisé de hello contrôle également qui peut afficher, modifier et supprimer le rôle de hello.

* Qui peut créer un rôle personnalisé ?
    Les propriétaires (et les administrateurs de l’accès utilisateur) d’abonnements, de groupes de ressources et de ressources peuvent créer des rôles personnalisés utilisables au sein de ces étendues.
    utilisateur qui crée le rôle de hello Hello doit tooperform en mesure de toobe `Microsoft.Authorization/roleDefinition/write` opération sur tous les hello **AssignableScopes** du rôle de hello.
* Qui peut modifier un rôle personnalisé ?
    Les propriétaires (et les administrateurs de l’accès utilisateur) d’abonnements, de groupes de ressources et de ressources peuvent modifier des rôles personnalisés au sein de ces étendues. Les utilisateurs doivent toobe tooperform en mesure de hello `Microsoft.Authorization/roleDefinition/write` opération sur tous les hello **AssignableScopes** d’un rôle personnalisé.
* Qui peut afficher des rôles personnalisés ?
    Tous les rôles intégrés dans le contrôle d’accès en fonction du rôle Azure permettent d’afficher les rôles pouvant être affectés. Les utilisateurs qui peuvent effectuer hello `Microsoft.Authorization/roleDefinition/read` opération sur une étendue peut afficher rôles RBAC hello qui sont disponibles pour l’assignation dans cette portée.

## <a name="see-also"></a>Voir aussi
* [Contrôle d’accès basé sur rôle](role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.
* Découvrez comment accéder à toomanage avec :
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Interface de ligne de commande Azure](role-based-access-control-manage-access-azure-cli.md)
  * [API REST](role-based-access-control-manage-access-rest.md)
* [Rôles intégrés](role-based-access-built-in-roles.md): obtenir des informations sur les rôles hello livrés dans RBAC.
