---
title: "stratégies de ressources aaaAzure pour les balises | Documents Microsoft"
description: "Fournit des exemples de stratégies de ressources pour gérer les balises sur les ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: tomfitz
ms.openlocfilehash: 5a5b3d5ed52b47544b397694b9da0070f61b1faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-tags"></a>Appliquer des stratégies de ressources pour les balises

Cette rubrique fournit une stratégie commune de règles que vous pouvez appliquer tooensure une utilisation cohérente de balises de ressources.

Application d’un abonnement à des ressources existantes ou groupe de ressources de balise stratégie tooa ne s’appliquent pas rétroactivement toothose ressources de la stratégie hello. stratégies de hello tooenforce sur ces ressources, déclencher un toohello de mise à jour de ressources existantes. Cet article comprend un exemple PowerShell de déclenchement d’une mise à jour.

## <a name="ensure-all-resources-in-a-resource-group-have-a-tagvalue"></a>Vérifier que toutes les ressources d’un groupe de ressources ont une balise / valeur

Il est souvent exigé que toutes les ressources d’un groupe de ressources aient une valeur et une balise particulières. Cette exigence est souvent nécessaire tootrack les coûts par département. Hello conditions suivantes doit être remplie :

* Hello requis balise valeur toonew ajouté et sont mis à jour des ressources qui n’ont pas de balise de hello.
* balise obligatoire de Hello et valeur ne peut pas être supprimée à partir de toutes les ressources existantes.

Vous satisfaire cette exigence en appliquant le groupe de ressources de deux stratégies intégrées tooa.

| ID | Description |
| ---- | ---- |
| 2a0e14a6-b0a6-4fab-991a-187a4f81c498 | Applique une balise requise et sa valeur par défaut lorsqu’il n’est pas spécifié par l’utilisateur de hello. |
| 1e30110a-5ceb-460c-a204-c1c3969c6d62 | Applique une balise requise et sa valeur. |

### <a name="powershell"></a>PowerShell

Hello PowerShell script suivant affecte le groupe de ressources tooa hello stratégie intégrée deux définitions. Avant d’exécuter le script de hello, affecter le groupe de ressources de toutes les balises nécessaires toohello. Chaque balise de groupe de ressources hello est requis pour les ressources hello dans le groupe de hello. groupes de ressources tooassign tooall dans votre abonnement, ne fournissent pas hello `-Name` paramètre lors de l’obtention des groupes de ressources hello.

```powershell
$appendpolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '2a0e14a6-b0a6-4fab-991a-187a4f81c498'}
$denypolicy = Get-AzureRmPolicyDefinition | Where-Object {$_.Name -eq '1e30110a-5ceb-460c-a204-c1c3969c6d62'}

$rgs = Get-AzureRMResourceGroup -Name ExampleGroup

foreach($rg in $rgs)
{
    $tags = $rg.Tags
    foreach($key in $tags.Keys){
        $key 
        $tags[$key]
        New-AzureRmPolicyAssignment -Name ("append"+$key+"tag") -PolicyDefinition $appendpolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
        New-AzureRmPolicyAssignment -Name ("denywithout"+$key+"tag") -PolicyDefinition $denypolicy -Scope $rg.ResourceId -tagName $key -tagValue  $tags[$key]
    }
}
```

Après avoir affecté les stratégies hello, vous pouvez déclencher un tooall de mise à jour existant ressources tooenforce hello balise des stratégies que vous avez ajouté. Hello script suivant conserve toutes les autres balises qui existaient sur les ressources hello :

```powershell
$group = Get-AzureRmResourceGroup -Name "ExampleGroup" 

$resources = Find-AzureRmResource -ResourceGroupName $group.ResourceGroupName 

foreach($r in $resources)
{
    try{
        $r | Set-AzureRmResource -Tags ($a=if($r.Tags -eq $NULL) { @{}} else {$r.Tags}) -Force -UsePatchSemantics
    }
    catch{
        Write-Host  $r.ResourceId + "can't be updated"
    }
}
```

## <a name="require-tags-for-a-resource-type"></a>Exiger des balises pour un type de ressource
Hello, l’exemple suivant montre comment la balise toonest opérateurs logiques toorequire une application pour un type de ressource spécifié (dans ce cas, comptes de stockage).

```json
{
    "if": {
        "allOf": [
          {
            "not": {
              "field": "tags",
              "containsKey": "application"
            }
          },
          {
            "field": "type",
            "equals": "Microsoft.Storage/storageAccounts"
          }
        ]
    },
    "then": {
        "effect": "audit"
    }
}
```

## <a name="require-tag"></a>Exiger une balise
Hello stratégie suivant refuse les demandes qui n’ont pas une balise qui contient la clé « Centre de coût » (n’importe quelle valeur peut être appliquée) :

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

## <a name="next-steps"></a>Étapes suivantes
* Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue. étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource. stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md). stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).
* Pour un tooresource des stratégies de présentation, consultez [vue d’ensemble des stratégies de ressources](resource-manager-policy.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

