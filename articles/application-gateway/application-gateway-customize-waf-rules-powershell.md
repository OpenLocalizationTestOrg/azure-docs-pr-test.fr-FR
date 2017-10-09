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
# <a name="customize-web-application-firewall-rules-through-powershell"></a>Personnaliser les règles de pare-feu d’applications web par le biais de PowerShell

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

pare-feu d’applications web Hello Azure Application Gateway (WAF) offre une protection pour les applications web. Ces protections sont fournies par hello ouvrir Web Application sécurité projet (OWASP avoir) Core règle définie (DM). Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel. Pour cette raison, la passerelle d’Application fournit et hello capacité toocustomize groupes de règles. Pour plus d’informations sur les règles et les groupes de règles spécifiques hello, consultez [liste de web application pare-feu CRS groupes de règles et](application-gateway-crs-rulegroups-rules.md).

## <a name="view-rule-groups-and-rules"></a>Afficher les règles et groupes de règles

Hello, exemple de code suivant affiche la tooview des règles et groupes qui peuvent être configurés sur une passerelle d’application prenant en charge les WAF de règles.

### <a name="view-rule-groups"></a>Afficher les groupes de règles

Hello suivant montre l’exemple de comment tooview les groupes de règles :

```powershell
Get-AzureRmApplicationGatewayAvailableWafRuleSets
```

Hello suivant la sortie est une réponse tronquée hello précédent exemple :

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

## <a name="disable-rules"></a>Désactiver les règles

exemple Hello désactive les règles `910018` et `910017` sur une passerelle d’application :

```azurecli
az network application-gateway waf-config set --resource-group AdatumAppGatewayRG --gateway-name AdatumAppGateway --enabled true --rule-set-version 3.0 --disabled-rules 910018 910017
```

## <a name="next-steps"></a>Étapes suivantes

Après avoir configuré vos règles désactivées, vous pouvez apprendre comment tooview vos journaux WAF. Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
