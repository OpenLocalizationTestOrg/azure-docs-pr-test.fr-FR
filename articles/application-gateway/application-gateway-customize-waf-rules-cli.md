---
title: "règles de pare-feu aaaCustomize web application dans Azure Azure CLI 2.0 - passerelle d’Application | Documents Microsoft"
description: "Cet article fournit des informations sur le fonctionnement des règles de pare-feu d’applications web toocustomize dans la passerelle d’Application avec hello Azure CLI 2.0."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b83ffb9f6a7e0d0c8c970885d2bcb3b63d32581c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-cli-20"></a><span data-ttu-id="2e352-103">Personnaliser les règles de pare-feu d’applications web via hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2e352-103">Customize web application firewall rules through hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2e352-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2e352-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="2e352-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2e352-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="2e352-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2e352-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="2e352-107">pare-feu d’applications web Hello Azure Application Gateway (WAF) offre une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="2e352-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="2e352-108">Ces protections sont fournies par hello ouvrir Web Application sécurité projet (OWASP avoir) Core règle définie (DM).</span><span class="sxs-lookup"><span data-stu-id="2e352-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="2e352-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="2e352-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="2e352-110">Pour cette raison, la passerelle d’Application fournit et hello capacité toocustomize groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="2e352-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="2e352-111">Pour plus d’informations sur les règles et les groupes de règles spécifiques hello, consultez [la liste des règles et des groupes de règles web application pare-feu CRS](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2e352-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="2e352-112">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="2e352-112">View rule groups and rules</span></span>

<span data-ttu-id="2e352-113">Hello, exemple de code suivant affiche la tooview des règles et groupes qui sont configurables de règles.</span><span class="sxs-lookup"><span data-stu-id="2e352-113">hello following code examples show how tooview rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="2e352-114">Afficher les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="2e352-114">View rule groups</span></span>

<span data-ttu-id="2e352-115">Bonjour à l’exemple suivant montre comment tooview hello des groupes de règles :</span><span class="sxs-lookup"><span data-stu-id="2e352-115">hello following example shows how tooview hello rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="2e352-116">Hello suivant la sortie est une réponse tronquée hello précédent exemple :</span><span class="sxs-lookup"><span data-stu-id="2e352-116">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  },
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_2.2.9",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
   "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "crs_20_protocol_violations",
        "rules": null
      },
      ...
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "2.2.9",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="2e352-117">Afficher les règles dans un groupe de règles</span><span class="sxs-lookup"><span data-stu-id="2e352-117">View rules in a rule group</span></span>

<span data-ttu-id="2e352-118">Hello l’exemple suivant illustre le fonctionnement des règles de tooview dans un groupe de règles spécifié :</span><span class="sxs-lookup"><span data-stu-id="2e352-118">hello following example shows how tooview rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="2e352-119">Hello suivant la sortie est une réponse tronquée hello précédent exemple :</span><span class="sxs-lookup"><span data-stu-id="2e352-119">hello following output is a truncated response from hello preceding example:</span></span>

```
[
  {
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/applicationGatewayAvailableWafRuleSets/",
    "location": null,
    "name": "OWASP_3.0",
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "ruleGroups": [
      {
        "description": "",
        "ruleGroupName": "REQUEST-910-IP-REPUTATION",
        "rules": [
          {
            "description": "Rule 910011",
            "ruleId": 910011
          },
          ...
        ]
      }
    ],
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "tags": null,
    "type": "Microsoft.Network/applicationGatewayAvailableWafRuleSets"
  }
]
```

## <a name="disable-rules"></a><span data-ttu-id="2e352-120">Désactiver les règles</span><span class="sxs-lookup"><span data-stu-id="2e352-120">Disable rules</span></span>

<span data-ttu-id="2e352-121">exemple Hello désactive les règles `910018` et `910017` sur une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="2e352-121">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="2e352-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e352-122">Next steps</span></span>

<span data-ttu-id="2e352-123">Après avoir configuré vos règles désactivées, vous pouvez apprendre comment tooview vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="2e352-123">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="2e352-124">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="2e352-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
