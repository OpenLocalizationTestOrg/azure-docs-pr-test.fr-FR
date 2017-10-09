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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="fb6ea-103">Erreur RequestDisallowedByPolicy avec une stratégie de ressource Azure</span><span class="sxs-lookup"><span data-stu-id="fb6ea-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="fb6ea-104">Cet article décrit la cause de hello d’erreur de RequestDisallowedByPolicy hello, il fournit également des solutions pour cette erreur.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="fb6ea-105">Symptôme</span><span class="sxs-lookup"><span data-stu-id="fb6ea-105">Symptom</span></span>

<span data-ttu-id="fb6ea-106">Lorsque vous essayez de toodo une action au cours du déploiement, vous pouvez recevoir un **RequestDisallowedByPolicy** erreur qui empêche l’action de hello être effectuée.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="fb6ea-107">Hello Voici un exemple d’erreur de hello :</span><span class="sxs-lookup"><span data-stu-id="fb6ea-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="fb6ea-108">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="fb6ea-108">Troubleshooting</span></span>

<span data-ttu-id="fb6ea-109">tooretrieve plus d’informations sur la stratégie hello qui a bloqué votre déploiement, utilisez hello suivant une des méthodes de hello :</span><span class="sxs-lookup"><span data-stu-id="fb6ea-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="fb6ea-110">Méthode 1</span><span class="sxs-lookup"><span data-stu-id="fb6ea-110">Method 1</span></span>

<span data-ttu-id="fb6ea-111">Dans PowerShell, fournissent à cet identificateur de stratégie en tant que hello **Id** détails du paramètre tooretrieve sur la stratégie hello qui a bloqué votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="fb6ea-112">Méthode 2</span><span class="sxs-lookup"><span data-stu-id="fb6ea-112">Method 2</span></span> 

<span data-ttu-id="fb6ea-113">Dans Azure CLI 2.0, fournissez le nom de hello de définition de stratégie hello :</span><span class="sxs-lookup"><span data-stu-id="fb6ea-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="fb6ea-114">Solution</span><span class="sxs-lookup"><span data-stu-id="fb6ea-114">Solution</span></span>

<span data-ttu-id="fb6ea-115">À des fins de sécurité ou de conformité, votre service informatique peut appliquer une stratégie de ressources qui interdit la création d’adresses IP publiques, de groupes de sécurité réseau, d’itinéraires définis par l’utilisateur ou de tables de routage.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="fb6ea-116">Dans l’exemple hello hello du message d’erreur est décrite dans la section « Symptômes » de hello, stratégie de hello est nommé **regionPolicyDefinition**, mais il peut être différent.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="fb6ea-117">tooresolve ce problème, travailler avec vos stratégies de ressources informatiques service tooreview hello et déterminer comment tooperform hello demandée action conformément à ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="fb6ea-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="fb6ea-118">Pour plus d’informations, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="fb6ea-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="fb6ea-119">Vue d’ensemble des stratégies de ressources</span><span class="sxs-lookup"><span data-stu-id="fb6ea-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="fb6ea-120">Erreurs de déploiement courantes-RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="fb6ea-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


