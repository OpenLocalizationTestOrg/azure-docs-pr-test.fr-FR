---
title: "règles de pare-feu aaaCustomize web application dans Azure PowerShell - passerelle d’Application | Documents Microsoft"
description: "Cet article fournit des informations sur le fonctionnement des règles de pare-feu d’applications web toocustomize dans la passerelle d’Application avec PowerShell."
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
ms.openlocfilehash: f320e687b0f621515255469dac8e375cdd900dda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-powershell"></a><span data-ttu-id="24d42-103">Personnaliser les règles de pare-feu d’applications web par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="24d42-103">Customize web application firewall rules through PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24d42-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="24d42-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="24d42-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24d42-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="24d42-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="24d42-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="24d42-107">pare-feu d’applications web Hello Azure Application Gateway (WAF) offre une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="24d42-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="24d42-108">Ces protections sont fournies par hello ouvrir Web Application sécurité projet (OWASP avoir) Core règle définie (DM).</span><span class="sxs-lookup"><span data-stu-id="24d42-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="24d42-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="24d42-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="24d42-110">Pour cette raison, la passerelle d’Application fournit et hello capacité toocustomize groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="24d42-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="24d42-111">Pour plus d’informations sur les règles et les groupes de règles spécifiques hello, consultez [liste de web application pare-feu CRS groupes de règles et](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="24d42-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS Rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="24d42-112">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="24d42-112">View rule groups and rules</span></span>

<span data-ttu-id="24d42-113">Hello, exemple de code suivant affiche la tooview des règles et groupes qui peuvent être configurés sur une passerelle d’application prenant en charge les WAF de règles.</span><span class="sxs-lookup"><span data-stu-id="24d42-113">hello following code examples show how tooview rules and rule groups that are configurable on a WAF-enabled application gateway.</span></span>

### <a name="view-rule-groups"></a><span data-ttu-id="24d42-114">Afficher les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="24d42-114">View rule groups</span></span>

<span data-ttu-id="24d42-115">Hello suivant montre l’exemple de comment tooview les groupes de règles :</span><span class="sxs-lookup"><span data-stu-id="24d42-115">hello following example shows how tooview rule groups:</span></span>

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

<span data-ttu-id="24d42-116">Hello suivant la sortie est une réponse tronquée hello précédent exemple :</span><span class="sxs-lookup"><span data-stu-id="24d42-116">hello following output is a truncated response from hello preceding example:</span></span>

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

## <a name="disable-rules"></a><span data-ttu-id="24d42-117">Désactiver les règles</span><span class="sxs-lookup"><span data-stu-id="24d42-117">Disable rules</span></span>

<span data-ttu-id="24d42-118">exemple Hello désactive les règles `910018` et `910017` sur une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="24d42-118">hello following example disables rules `910018` and `910017` on an application gateway:</span></span>

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a><span data-ttu-id="24d42-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24d42-119">Next steps</span></span>

<span data-ttu-id="24d42-120">Après avoir configuré vos règles désactivées, vous pouvez apprendre comment tooview vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="24d42-120">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="24d42-121">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="24d42-121">For more information, see [Application Gateway Diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
