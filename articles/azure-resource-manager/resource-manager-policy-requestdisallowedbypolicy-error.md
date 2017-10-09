---
title: "erreur aaaRequestDisallowedByPolicy avec la stratégie de ressources Azure | Documents Microsoft"
description: "Décrit la cause hello Hello RequestDisallowedByPolicy erreur."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Erreur RequestDisallowedByPolicy avec une stratégie de ressource Azure

Cet article décrit la cause de hello d’erreur de RequestDisallowedByPolicy hello, il fournit également des solutions pour cette erreur.

## <a name="symptom"></a>Symptôme

Lorsque vous essayez de toodo une action au cours du déploiement, vous pouvez recevoir un **RequestDisallowedByPolicy** erreur qui empêche l’action de hello être effectuée. Hello Voici un exemple d’erreur de hello :

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Résolution des problèmes

tooretrieve plus d’informations sur la stratégie hello qui a bloqué votre déploiement, utilisez hello suivant une des méthodes de hello :

### <a name="method-1"></a>Méthode 1

Dans PowerShell, fournissent à cet identificateur de stratégie en tant que hello **Id** détails du paramètre tooretrieve sur la stratégie hello qui a bloqué votre déploiement.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Méthode 2 

Dans Azure CLI 2.0, fournissez le nom de hello de définition de stratégie hello : 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Solution

À des fins de sécurité ou de conformité, votre service informatique peut appliquer une stratégie de ressources qui interdit la création d’adresses IP publiques, de groupes de sécurité réseau, d’itinéraires définis par l’utilisateur ou de tables de routage. Dans l’exemple hello hello du message d’erreur est décrite dans la section « Symptômes » de hello, stratégie de hello est nommé **regionPolicyDefinition**, mais il peut être différent.
tooresolve ce problème, travailler avec vos stratégies de ressources informatiques service tooreview hello et déterminer comment tooperform hello demandée action conformément à ces stratégies.


Pour plus d’informations, consultez hello suivant des articles :

- [Vue d’ensemble des stratégies de ressources](resource-manager-policy.md)
- [Erreurs de déploiement courantes-RequestDisallowedByPolicy](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


