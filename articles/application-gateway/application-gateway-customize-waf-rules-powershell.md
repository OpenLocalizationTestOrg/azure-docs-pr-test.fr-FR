---
title: "Personnaliser les règles de pare-feu d’applications web dans Azure Application Gateway -PowerShell | Microsoft Docs"
description: "Cet article fournit des informations sur la personnalisation des règles de pare-feu d’applications web dans Application Gateway avec PowerShell."
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
ms.openlocfilehash: 681625e40035b05c593c6161236cb80b7db576b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="a9c6a-103">Personnaliser les règles de pare-feu d’applications web par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c6a-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9c6a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="a9c6a-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="a9c6a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9c6a-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="a9c6a-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a9c6a-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="a9c6a-107">Le pare-feu d’applications web (WAF) Azure Application Gateway fournit une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="a9c6a-108">Ces protections sont fournies par le jeu de règles (Core Rule Set, CRS) de l’Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="a9c6a-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="a9c6a-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="a9c6a-110">Par conséquent, Application Gateway permet de personnaliser des règles et des groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="a9c6a-111">Pour plus d’informations sur les règles et groupes de règles spécifiques, consultez la [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md) (Liste de règles et groupes de règles CRS de pare-feu d’applications web).</span><span class="sxs-lookup"><span data-stu-id="a9c6a-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="a9c6a-112">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="a9c6a-112">View rule groups and rules</span></span>

<span data-ttu-id="a9c6a-113">Voici des exemples de code montrant comment afficher les règles et les groupes de règles qui peuvent être configurés sur une passerelle d’application avec WAF activé.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-113">The following code examples show how to view rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="a9c6a-114">Afficher les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="a9c6a-114">View rule groups</span></span>

<span data-ttu-id="a9c6a-115">L’exemple suivant montre comment afficher les groupes de règles :</span><span class="sxs-lookup"><span data-stu-id="a9c6a-115">The following example shows how to view rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="a9c6a-116">Voici un extrait de réponse issu de l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="a9c6a-116">The following output is a truncated response from the preceding example:</span></span>

```
OWASP (Ver. 3.0):

    REQUEST-910-IP-REPUTATION:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            910011     Rule 910011
            910012     Rule 910012
            ...        ...

    REQUEST-911-METHOD-ENFORCEMENT:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            911011     Rule 911011
            ...        ...

OWASP (Ver. 2.2.9):

    crs_20_protocol_violations:
        Description:
            
        Rules:
            RuleId     Description
            ------     -----------
            960911     Invalid HTTP Request Line
            981227     Apache Error: Invalid URI in Request.
            960000     Attempted multipart/form-data bypass
            ...        ...
```

## <a name="disable-rules"></a><span data-ttu-id="a9c6a-117">Désactiver les règles</span><span class="sxs-lookup"><span data-stu-id="a9c6a-117">Disable rules</span></span>

<span data-ttu-id="a9c6a-118">L’exemple suivant montre comment désactiver les règles `910018` et `910017` sur une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="a9c6a-118">The following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="a9c6a-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9c6a-119">Next steps</span></span>

<span data-ttu-id="a9c6a-120">Après avoir configuré vos règles désactivées, vous pouvez apprendre à afficher vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="a9c6a-120">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="a9c6a-121">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="a9c6a-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
