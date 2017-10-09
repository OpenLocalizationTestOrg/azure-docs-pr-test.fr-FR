---
title: "stratégies de ressources aaaAzure pour les comptes de stockage | Documents Microsoft"
description: "Décrit les stratégies Azure Resource Manager pour gérer le déploiement hello de comptes de stockage."
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
ms.date: 07/05/2017
ms.author: tomfitz
ms.openlocfilehash: d37fc4bcf7cdec71b0e14f6231fc138bfb6a7893
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-toostorage-accounts"></a>Appliquer des comptes de toostorage de stratégies de ressources
Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) vous pouvez appliquer des comptes de stockage tooAzure. Ces stratégies garantissent la cohérence pour les comptes de stockage hello déployé dans votre organisation. 

## <a name="define-permitted-storage-account-types"></a>Définir les types de compte de stockage autorisés

Hello stratégie suivante restreint qui [les types de compte de stockage](../storage/common/storage-redundancy.md) peut être déployé :

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/sku.name",
          "in": [
            "Standard_LRS",
            "Standard_GRS"
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Une règle de stratégie similaire avec un paramètre pour l’acceptation de hello autorisé des références (SKU) est disponible en tant qu’une définition de stratégie intégré. stratégie intégrée de Hello a hello les ID de ressource de `/providers/Microsoft.Authorization/policyDefinitions/7433c107-6db4-4ad1-b57a-a76dce0154a1`. 

## <a name="define-permitted-access-tier"></a>Définir le niveau d’accès autorisé

Hello stratégie suivante spécifie type hello de [couche d’accès aux](../storage/blobs/storage-blob-storage-tiers.md) qui peut être spécifiée pour les comptes de stockage :

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "field": "kind",
        "equals": "BlobStorage"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/accessTier",
          "equals": "cool"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="ensure-encryption-is-enabled"></a>Vérifier que le chiffrement est activé

Hello suivant stratégie nécessite que tous les tooenable de comptes de stockage [chiffrement de service de stockage](../storage/common/storage-service-encryption.md):

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "equals": "Microsoft.Storage/storageAccounts"
      },
      {
        "not": {
          "field": "Microsoft.Storage/storageAccounts/enableBlobEncryption",
          "equals": "true"
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

Cette règle de stratégie est également disponible sous une définition de stratégie intégrée avec l’ID de ressource hello de `/providers/Microsoft.Authorization/policyDefinitions/7c5a74bf-ae94-4a74-8fcf-644d1e0e6e6f`.

## <a name="next-steps"></a>Étapes suivantes
* Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue. étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource. stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md). stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md). 
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

