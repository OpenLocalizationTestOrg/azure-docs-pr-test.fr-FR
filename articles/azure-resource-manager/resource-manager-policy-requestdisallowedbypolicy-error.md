---
title: "Erreur RequestDisallowedByPolicy avec une stratégie de ressource Azure | Microsoft Docs"
description: "Décrit la cause de l’erreur RequestDisallowedByPolicy."
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
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="0ff3c-103">Erreur RequestDisallowedByPolicy avec une stratégie de ressource Azure</span><span class="sxs-lookup"><span data-stu-id="0ff3c-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="0ff3c-104">Cet article décrit la cause de l’erreur RequestDisallowedByPolicy. Il fournit également des solutions pour la résoudre.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="0ff3c-105">Symptôme</span><span class="sxs-lookup"><span data-stu-id="0ff3c-105">Symptom</span></span>

<span data-ttu-id="0ff3c-106">Lorsque vous essayez d’effectuer une action lors du déploiement, vous pouvez recevoir une erreur **RequestDisallowedByPolicy** empêchant l’action de s’effectuer.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-106">When you try to do an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents the action be performed.</span></span> <span data-ttu-id="0ff3c-107">Voici un exemple de cette erreur :</span><span class="sxs-lookup"><span data-stu-id="0ff3c-107">The following is a sample of the error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="0ff3c-108">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="0ff3c-108">Troubleshooting</span></span>

<span data-ttu-id="0ff3c-109">Pour extraire des informations sur la stratégie qui a bloqué votre déploiement, utilisez l’une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0ff3c-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="0ff3c-110">Méthode 1</span><span class="sxs-lookup"><span data-stu-id="0ff3c-110">Method 1</span></span>

<span data-ttu-id="0ff3c-111">Dans PowerShell, fournissez cet identificateur de stratégie en tant que paramètre **Id** pour extraire des informations sur la stratégie qui a bloqué votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-111">In PowerShell, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="0ff3c-112">Méthode 2</span><span class="sxs-lookup"><span data-stu-id="0ff3c-112">Method 2</span></span> 

<span data-ttu-id="0ff3c-113">Dans Azure CLI 2.0, indiquez le nom de la définition de stratégie :</span><span class="sxs-lookup"><span data-stu-id="0ff3c-113">In Azure CLI 2.0, provide the name of the policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="0ff3c-114">Solution</span><span class="sxs-lookup"><span data-stu-id="0ff3c-114">Solution</span></span>

<span data-ttu-id="0ff3c-115">À des fins de sécurité ou de conformité, votre service informatique peut appliquer une stratégie de ressources qui interdit la création d’adresses IP publiques, de groupes de sécurité réseau, d’itinéraires définis par l’utilisateur ou de tables de routage.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="0ff3c-116">Dans l’exemple de message d’erreur décrit dans la section « Symptômes », la stratégie est nommée **regionPolicyDefinition**, mais il pourrait s’agir d’une autre stratégie.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-116">In the sample of the error message that is described in the "Symptoms" section, the policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="0ff3c-117">Pour résoudre ce problème, contactez votre service informatique pour passer en revue les stratégies de ressources et déterminer comment effectuer l’action demandée conformément à ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="0ff3c-117">To resolve this problem, work with your IT department to review the resource policies, and determine how to perform the requested action in compliance with those policies.</span></span>


<span data-ttu-id="0ff3c-118">Pour plus d’informations, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="0ff3c-118">For more information, see the following articles:</span></span>

- [<span data-ttu-id="0ff3c-119">Vue d’ensemble des stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="0ff3c-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="0ff3c-120">Erreurs de déploiement courantes-RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="0ff3c-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


