---
title: "règles de pare-feu aaaCustomize web application dans la passerelle d’Application Azure - portail Azure | Documents Microsoft"
description: "Cet article fournit des informations sur le fonctionnement des règles de pare-feu d’applications web toocustomize dans la passerelle d’Application avec hello portail Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 1159500b-17ba-41e7-88d6-b96986795084
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: gwallace
ms.openlocfilehash: 36a999279e0370b9f803e12257856a56753b23a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a>Personnaliser les règles de pare-feu d’applications web via hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-customize-waf-rules-portal.md)
> * [PowerShell](application-gateway-customize-waf-rules-powershell.md)
> * [Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md)

pare-feu d’applications web Hello Azure Application Gateway (WAF) offre une protection pour les applications web. Ces protections sont fournies par hello ouvrir Web Application sécurité projet (OWASP avoir) Core règle définie (DM). Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel. Pour cette raison, la passerelle d’Application fournit et hello capacité toocustomize groupes de règles. Pour plus d’informations sur les règles et les groupes de règles spécifiques hello, consultez [la liste des règles et des groupes de règles web application pare-feu CRS](application-gateway-crs-rulegroups-rules.md).

>[!NOTE]
> Si votre passerelle d’application n’utilise pas le niveau de WAF hello, hello option tooupgrade hello passerelle toohello WAF applicative s’affiche dans le volet de droite hello. 

![Activer WAF][fig1]

## <a name="view-rule-groups-and-rules"></a>Afficher les règles et groupes de règles

**règles et groupes de règles tooview**
   1. Parcourir la passerelle d’application toohello, puis sélectionnez **pare-feu d’applications Web**.  
   2. Sélectionnez **Configuration de règle avancée**.  
   Cette vue affiche une table sur la page hello de tous les groupes de règles hello fourni avec hello choisi l’ensemble de règles. Toutes les cases à cocher de la règle hello sont sélectionnées.

![Configurer des règles désactivées][1]

## <a name="search-for-rules-toodisable"></a>Recherche de règles toodisable

Hello **paramètres de pare-feu d’applications Web** panneau permet hello toofilter les règles de hello via une recherche de texte. résultat de Hello affiche uniquement les groupes de règles de hello et les règles qui contiennent du texte hello recherché.

![Rechercher des règles][2]

## <a name="disable-rule-groups-and-rules"></a>Désactiver les règles et les groupes de règles

Lorsque vous désactivez des règles, vous pouvez désactiver un groupe de règles entier, ou des règles spécifiques sous un ou plusieurs groupes de règles. 

**groupes de règles toodisable ou des règles spécifiques**

   1. Rechercher des règles de hello ou des groupes de règles que vous souhaitez toodisable.
   2. Désactivez les cases à cocher hello hello des règles que vous souhaitez toodisable. 
   2. Sélectionnez **Enregistrer**. 

![Enregistrer les modifications][3]

## <a name="next-steps"></a>Étapes suivantes

Après avoir configuré vos règles désactivées, vous pouvez apprendre comment tooview vos journaux WAF. Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
