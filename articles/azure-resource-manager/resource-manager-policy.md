---
title: "stratégies de ressources aaaAzure | Documents Microsoft"
description: "Décrit comment les propriétés de ressource cohérent tooensure toouse Azure Resource Manager stratégies sont définies au cours du déploiement. Les stratégies peuvent être appliquées à des groupes d’abonnement ou une ressource hello."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Vue d’ensemble des stratégies de ressources
Stratégies de ressources permettent de conventions tooestablish pour les ressources de votre organisation. En définissant des conventions, vous pouvez contrôler les coûts et gérer plus facilement vos ressources. Par exemple, vous pouvez spécifier que seuls certains types de machines virtuelles sont autorisés. Vous pouvez aussi exiger que toutes les ressources soient marquées. Toutes les ressources enfants héritent des stratégies. Donc, si une stratégie est un groupe de ressources appliquée tooa, ressources de hello tooall applicable dans ce groupe de ressources.

Il existe deux concepts toounderstand, sur les stratégies :

* définition de stratégie - décrivent lorsque hello appliquée et le tootake d’action
* attribution de stratégie - que vous appliquez étendue tooa définition hello de stratégie (abonnement ou groupe de ressources)

Cette rubrique porte sur la définition de stratégie. Pour plus d’informations sur l’attribution de stratégie, consultez [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md) ou [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).

Les stratégies sont évaluées lors de la création et de la mise à jour des ressources (opérations PUT et PATCH).

> [!NOTE]
> Actuellement, la stratégie n’évalue pas les types de ressources qui ne prennent pas en charge les balises, type et emplacement, par exemple, type de ressource Microsoft.Resources/deployments hello. Cette prise en charge sera ajoutée prochainement. tooavoid des problèmes de compatibilité descendante, vous devez spécifier explicitement le type lors de la création de stratégies. Par exemple, une stratégie de balises sans spécification des types est appliquée à tous les types. Dans ce cas, un déploiement de modèle peut échouer s’il existe une ressource imbriquée qui ne prennent pas en charge les balises, et type de ressource de déploiement hello a été ajouté à l’évaluation toopolicy. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>Quelle est la différence avec RBAC ?
Il existe quelques différences importantes entre la stratégie et le contrôle d’accès en fonction du rôle (RBAC). RBAC porte sur les actions des **utilisateurs** dans différentes étendues. Par exemple, vous sont ajoutés toohello rôle de collaborateur pour un groupe de ressources de la portée de hello souhaité pour vous permettre de groupe de ressources toothat de modifications. La stratégie se focalise sur les propriétés des **ressources** pendant le déploiement. Par exemple, via des stratégies, vous pouvez contrôler les types de hello des ressources qui peuvent être configurées. Ou bien, vous pouvez restreindre les emplacements de hello dans lequel les ressources hello peuvent être configurés. Contrairement à RBAC, la stratégie est, par défaut, un système explicite d'autorisation et de refus. 

stratégies de toouse, vous devez être authentifié au moyen de RBAC. Plus précisément, votre compte a besoin de :

* `Microsoft.Authorization/policydefinitions/write`autorisation toodefine une stratégie
* `Microsoft.Authorization/policyassignments/write`autorisation tooassign une stratégie 

Ces autorisations ne sont pas incluses dans hello **collaborateur** rôle.

## <a name="built-in-policies"></a>Stratégies prédéfinies

Azure fournit des définitions de stratégie intégrée qui peuvent réduire hello nombre de stratégies, vous avez toodefine. Avant de procéder à des définitions de stratégie, vous devez envisager si une stratégie intégrée fournit déjà définition hello que nécessaire. les définitions de stratégie intégrée Hello sont :

* Emplacements autorisés
* Types de ressources autorisés
* Références SKU de compte de stockage autorisées
* Références SKU de machine virtuelle autorisées
* Appliquer la valeur par défaut et la balise
* Appliquer une balise et une valeur
* Types de ressources non autorisés
* Nécessitent SQL Server version 12.0
* Nécessitent le chiffrement du compte de stockage

Vous pouvez affecter une de ces stratégies via hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), ou [CLI d’Azure](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Structure de la définition de stratégie
Vous utilisez JSON toocreate une définition de stratégie. définition de stratégie Hello contient les éléments de :

* parameters
* le nom d’affichage
* description
* la règle de stratégie
  * évaluation logique
  * effet

Hello, l’exemple suivant illustre une stratégie qui limite où vous déployez des ressources :

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>Paramètres
À l’aide des paramètres permet de simplifier la gestion de stratégie en réduisant le nombre de hello de définitions de stratégie. Vous définissez une stratégie pour une propriété de ressource (par exemple, la limitation des emplacements de hello où les ressources peuvent être déployés) et incluez des paramètres dans la définition de hello. Ensuite, vous réutilisez cette définition de stratégie pour différents scénarios en passant des valeurs différentes (par exemple, la spécification d’un ensemble d’emplacements pour un abonnement) lorsque attribution de stratégie de hello.

Vous déclarez des paramètres lorsque vous créez des définitions de stratégies.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

type Hello d’un paramètre peut être une chaîne ou le tableau. propriété de métadonnées Hello est utilisée pour les outils, tels que les informations conviviales toodisplay portail Azure. 

Dans la règle de stratégie hello, vous faites référence aux paramètres hello selon la syntaxe : 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nom d’affichage et description

Vous utilisez hello **displayName** et **description** tooidentify hello de définition de la stratégie et fournissent un contexte pour lorsqu’il est utilisé.

## <a name="policy-rule"></a>Règle de stratégie

règle de stratégie Hello se compose de **si** et **puis** blocs. Bonjour **si** bloc, vous définissez une ou plusieurs conditions qui spécifient quand la stratégie de hello est appliquée. Vous pouvez appliquer des conditions de toothese d’opérateurs logiques tooprecisely définir scénario hello pour une stratégie. Bonjour **puis** bloc, vous définissez effet hello lorsque hello **si** conditions sont remplies.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Opérateurs logiques
les opérateurs logiques Hello pris en charge sont :

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Hello **pas** syntaxe inverse le résultat de hello de condition de hello. Hello **tous** syntaxe (toohello similaire logique **et** opération) nécessite le vrai de toobe toutes les conditions. Hello **anyOf** syntaxe (toohello similaire logique **ou** opération) nécessite un ou plusieurs conditions toobe la valeur true.

Vous pouvez imbriquer des opérateurs logiques. Hello suivant montre l’exemple un **pas** opération qui est imbriquée dans une **tous** opération. 

```json
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
```

### <a name="conditions"></a>Conditions
condition de Hello évalue si un **champ** répond à certains critères. conditions de Hello pris en charge sont :

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Lorsque vous utilisez hello **comme** condition, vous pouvez fournir un caractère générique (*) dans la valeur de hello.

Lorsque vous utilisez hello **correspond à** de condition, fournir `#` toorepresent un chiffre, `?` pour une lettre, ainsi que tout autre caractère toorepresent ce caractère réel. Pour obtenir des exemples, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Champs
Les conditions sont formées à partir de champs. Un champ représente des propriétés dans la charge utile de demande hello ressource qui est utilisé toodescribe hello état de ressource de hello.  

Hello champs qui suivent est pris en charge :

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* alias de propriété : pour en obtenir la liste, consultez [Alias](#aliases).

### <a name="effect"></a>Résultat
La stratégie prend en charge trois types d’effet : `deny`, `audit` et `append`. 

* **Refuser** génère un événement dans le journal d’audit de hello et faire échouer hello demande
* **Audit** génère un événement d’avertissement dans le journal d’audit, mais n’échoue pas de demande de hello
* **Ajouter** ajoute ensemble hello défini de champs toohello demande 

Pour **ajouter**, vous devez fournir hello les détails suivants :

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

valeur de Hello peut être une chaîne ou un objet du format JSON. 

## <a name="aliases"></a>Alias

Vous utilisez des alias tooaccess spécifique de propriétés pour un type de ressource. Les alias autorisent toorestrict les conditions ou les valeurs autorisées pour une propriété sur une ressource. Chaque alias mappe toopaths dans les différentes versions d’API pour un type de ressource donné. Lors de l’évaluation de stratégie, moteur de stratégie hello Obtient le chemin d’accès de propriété hello pour cette version de l’API.

**Microsoft.Cache/Redis**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | La valeur indique si de port du serveur de Redis de non-ssl hello (6379) est activée. |
| Microsoft.Cache/Redis/shardCount | Définir nombre hello de toobe de partitions créée sur un Cache de Cluster Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Définir la taille hello de hello Redis cache toodeploy.  |
| Microsoft.Cache/Redis/sku.family | Valeur toouse de famille hello référence (SKU). |
| Microsoft.Cache/Redis/sku.name | Définir le type hello du Cache Redis toodeploy. |

**Microsoft.Cdn/profiles**

| Alias | Description |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Hello le nom du niveau tarifaire de hello. |

**Microsoft.Compute/disks**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine. |


**Microsoft.Compute/virtualMachines**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Compute/imageId | Définir l’identificateur hello de machine virtuelle de hello image utilisée toocreate hello. |
| Microsoft.Compute/imageOffer | Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine. |
| Microsoft.Compute/licenseType | Définir cette image hello ou disque local sous licence. Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation de serveur Windows hello.  |
| Microsoft.Compute/virtualMachines/imageOffer | Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imagePublisher | Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imageSku | Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/imageVersion | Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Définir le disque dur virtuel hello URI. |
| Microsoft.Compute/virtualMachines/sku.name | Définir la taille hello de machine virtuelle de hello. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Hello le nom du serveur de publication de l’extension hello. |
| Microsoft.Compute/virtualMachines/extensions/type | Définir le type hello d’extension. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Définissez la version hello d’extension de hello. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Compute/imageId | Définir l’identificateur hello de machine virtuelle de hello image utilisée toocreate hello. |
| Microsoft.Compute/imageOffer | Offre de hello d’ensemble de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imagePublisher | Serveur de publication ensemble hello d’image de plateforme hello ou d’une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageSku | Ensemble hello référence (SKU) de l’image de plateforme hello ou une image marketplace utilisé toocreate hello virtual machine. |
| Microsoft.Compute/imageVersion | Définir la version de l’image de plateforme hello ou une image marketplace hello utilisé toocreate hello virtual machine. |
| Microsoft.Compute/licenseType | Définir cette image hello ou disque local sous licence. Cette valeur est utilisée uniquement pour les images qui contiennent le système d’exploitation de serveur Windows hello. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Définir le préfixe du nom d’ordinateur hello pour tous les ordinateurs virtuels hello dans un ensemble d’échelle hello. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Ensemble hello URI d’objet blob d’image de l’utilisateur. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Définir les URL du conteneur hello qui sont des disques de système d’exploitation toostore utilisé pour l’ensemble d’échelle hello. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Définir la taille hello des machines virtuelles dans un ensemble d’échelle. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Définir le niveau hello des ordinateurs virtuels dans un ensemble d’échelle. |
  
**Microsoft.Network/applicationGateways**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Définir la taille hello de passerelle de hello. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Valeur de type hello de cette passerelle de réseau virtuel. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Définir le nom de référence (SKU) de passerelle hello. |

**Microsoft.Sql/servers**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Définissez la version hello du serveur de hello. |

**Microsoft.Sql/databases**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Définir edition hello de base de données hello. |
| Microsoft.Sql/servers/databases/elasticPoolName | Nom de base de données hello pool élastique hello hello est dans. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Ensemble hello configuré ID objectif de niveau de service de base de données hello. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Nom du jeu hello Hello configuré objectif de niveau de service de base de données hello.  |

**Microsoft.Sql/elasticpools**

| Alias | Description |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Nombre total de SET hello partagé DTU pour le pool élastique de base de données hello. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Définir edition hello du pool élastique de hello. |

**Microsoft.Storage/storageAccounts**

| Alias | Description |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Niveau d’accès hello jeu utilisé pour la facturation. |
| Microsoft.Storage/storageAccounts/accountType | Définir le nom de référence (SKU) hello. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Définir si le service de hello chiffre les données de hello tel qu’il est stocké dans le service de stockage d’objets blob hello. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Définir si le service de hello chiffre les données de hello tel qu’il est stocké dans le service de stockage hello. |
| Microsoft.Storage/storageAccounts/sku.name | Définir le nom de référence (SKU) hello. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Définir les https uniquement tooallow service toostorage du trafic. |


## <a name="policy-examples"></a>Exemples de stratégies

Hello rubriques suivantes contiennent des exemples de stratégie :

* Pour obtenir des exemples de stratégies de balises, consultez [Apply resource policies for tags](resource-manager-policy-tags.md) (Appliquer des stratégies de ressources pour les balises).
* Pour obtenir des exemples de modèles d’affectation de noms et de texte, consultez [Appliquer des stratégies de ressources pour les noms et le texte](resource-manager-policy-naming-convention.md).
* Pour obtenir des exemples de stratégies de stockage, consultez [appliquer les comptes de ressources stratégies toostorage](resource-manager-policy-storage.md).
* Pour obtenir des exemples de stratégies de l’ordinateur virtuel, consultez [appliquer des stratégies de ressources tooLinux machines virtuelles](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) et [appliquer des stratégies de ressources tooWindows machines virtuelles](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Étapes suivantes
* Après avoir défini une règle de stratégie, attribuez-lui tooa étendue. stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md). stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md).
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).
* schéma de stratégie Hello est publiée à [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

