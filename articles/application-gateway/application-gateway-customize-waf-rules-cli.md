---
title: "Personnaliser les règles de pare-feu d’applications web dans Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs"
description: "Cet article fournit des informations sur la personnalisation des règles de pare-feu d’applications web dans Application Gateway avec Azure CLI 2.0."
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
ms.openlocfilehash: 456be048dc2d82cd50d145b71f17a84a7189ea96
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-cli-20"></a><span data-ttu-id="15c55-103">Personnaliser les règles de pare-feu d’applications web par le biais d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="15c55-103">Customize web application firewall rules through the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="15c55-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="15c55-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="15c55-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15c55-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="15c55-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="15c55-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="15c55-107">Le pare-feu d’applications web (WAF) Azure Application Gateway fournit une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="15c55-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="15c55-108">Ces protections sont fournies par le jeu de règles (Core Rule Set, CRS) de l’Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="15c55-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="15c55-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="15c55-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="15c55-110">Par conséquent, Application Gateway permet de personnaliser des règles et des groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="15c55-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="15c55-111">Pour plus d’informations sur les règles et groupes de règles spécifiques, consultez la [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md) (Liste de règles et groupes de règles CRS de pare-feu d’applications web).</span><span class="sxs-lookup"><span data-stu-id="15c55-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="15c55-112">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="15c55-112">View rule groups and rules</span></span>

<span data-ttu-id="15c55-113">Voici des exemples de code montrant comment afficher les règles et les groupes de règles qui peuvent être configurés.</span><span class="sxs-lookup"><span data-stu-id="15c55-113">The following code examples show how to view rules and rule groups that are configurable.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="15c55-114">Afficher les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="15c55-114">View rule groups</span></span>

<span data-ttu-id="15c55-115">L’exemple suivant montre comment afficher les groupes de règles :</span><span class="sxs-lookup"><span data-stu-id="15c55-115">The following example shows how to view the rule groups:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --type OWASP
```

<span data-ttu-id="15c55-116">Voici un extrait de réponse issu de l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="15c55-116">The following output is a truncated response from the preceding example:</span></span>

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

### <a name="view-rules-in-a-rule-group"></a><span data-ttu-id="15c55-117">Afficher les règles dans un groupe de règles</span><span class="sxs-lookup"><span data-stu-id="15c55-117">View rules in a rule group</span></span>

<span data-ttu-id="15c55-118">L’exemple suivant montre comment afficher les règles dans un groupe de règles spécifique :</span><span class="sxs-lookup"><span data-stu-id="15c55-118">The following example shows how to view rules in a specified rule group:</span></span>

```azurecli-interactive
az network application-gateway waf-config list-rule-sets --group "REQUEST-910-IP-REPUTATION"
```

<span data-ttu-id="15c55-119">Voici un extrait de réponse issu de l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="15c55-119">The following output is a truncated response from the preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="15c55-120">Désactiver les règles</span><span class="sxs-lookup"><span data-stu-id="15c55-120">Disable rules</span></span>

<span data-ttu-id="15c55-121">L’exemple suivant montre comment désactiver les règles `910018` et `910017` sur une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="15c55-121">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli-interactive
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="15c55-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="15c55-122">Next steps</span></span>

<span data-ttu-id="15c55-123">Après avoir configuré vos règles désactivées, vous pouvez apprendre à afficher vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="15c55-123">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="15c55-124">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="15c55-124">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
