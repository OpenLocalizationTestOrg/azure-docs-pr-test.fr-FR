---
title: "stratégies de ressources aaaAzure pour les conventions d’affectation de noms | Documents Microsoft"
description: "Décrit les stratégies Azure Resource Manager pour les conventions d’affectation de noms des ressources."
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
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: c8384b231263fb694aed8b936a953d5c0ca31e71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-resource-policies-for-names-and-text"></a>Appliquer des stratégies de ressources pour les noms et le texte
Cette rubrique montre plusieurs [stratégies de ressources](resource-manager-policy.md) vous pouvez appliquer des conventions d’affectation de noms et le texte de tooestablish. Ces stratégies garantissent la cohérence des noms de ressources et des valeurs de balise. 

## <a name="set-naming-convention-with-wildcard"></a>Définir une convention d’affectation de noms avec un caractère générique
exemple Hello présente utilisez hello de caractère générique, ce qui est pris en charge par hello **comme** condition. Hello condition stipule que si hello nom correspond au modèle mentionné de hello (namePrefix\*nameSuffix) puis refuser la demande de hello :

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-naming-convention-with-pattern"></a>Définir une convention d’affectation de noms avec un modèle

toospecify que les noms des ressources correspondent à un modèle, utilisez hello correspondent à la condition. exemple Hello nécessite toostart de noms avec `contoso` et contenir des six lettres supplémentaires :

```json
{
  "if": {
    "not": {
      "field": "name",
      "match": "contoso??????"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="set-date-pattern-for-tag-value"></a>Définir le modèle de date pour la valeur de balise

toorequire un modèle de date de deux chiffres, tiret, trois lettres, tiret et quatre chiffres, utilisez :

```json
{
  "if": {
    "field": "tags.date",
    "match": "##-???-####"
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a>Étapes suivantes
* Après avoir défini une règle de stratégie (comme indiqué dans hello précédents exemples), vous devez la définition de la stratégie toocreate hello et affectez tooa étendue. étendue de Hello peut être un abonnement, le groupe de ressources ou la ressource. stratégies tooassign via le portail de hello, voir [tooassign de portail utilisez Azure et de gérer les stratégies de ressources](resource-manager-policy-portal.md). stratégies tooassign via l’API REST, PowerShell ou CLI d’Azure, consultez [affecter et gérer des stratégies dans le script](resource-manager-policy-create-assign.md). 
* Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).

