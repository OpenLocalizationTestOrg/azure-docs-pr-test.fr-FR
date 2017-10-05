---
title: "Personnaliser les règles de pare-feu d’applications web dans Azure Application Gateway - Portail Azure | Microsoft Docs"
description: "Cet article fournit des informations sur la personnalisation des règles de pare-feu d’applications web dans Application Gateway avec le portail Azure."
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
ms.openlocfilehash: cdcbadbc3765dfc583c26e1b1453863d421c9a72
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-web-application-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="e627f-103">Personnaliser les règles de pare-feu d’applications web via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="e627f-103">Customize web application firewall rules through the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e627f-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e627f-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="e627f-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e627f-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="e627f-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e627f-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="e627f-107">Le pare-feu d’applications web (WAF) Azure Application Gateway fournit une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="e627f-107">The Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="e627f-108">Ces protections sont fournies par le jeu de règles (Core Rule Set, CRS) de l’Open Web Application Security Project (OWASP).</span><span class="sxs-lookup"><span data-stu-id="e627f-108">These protections are provided by the Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="e627f-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="e627f-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="e627f-110">Par conséquent, Application Gateway permet de personnaliser des règles et des groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="e627f-110">For this reason, Application Gateway provides the capability to customize rule groups and rules.</span></span> <span data-ttu-id="e627f-111">Pour plus d’informations sur les règles et groupes de règles spécifiques, consultez la [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md) (Liste de règles et groupes de règles CRS de pare-feu d’applications web).</span><span class="sxs-lookup"><span data-stu-id="e627f-111">For more information on the specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="e627f-112">Si votre passerelle Application Gateway n’utilise pas la couche WAF, l’option de mise à niveau de la passerelle Application Gateway vers la couche WAF s’affiche dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="e627f-112">If your application gateway is not using the WAF tier, the option to upgrade the application gateway to the WAF tier appears in the right pane.</span></span> 

![Activer WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="e627f-114">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="e627f-114">View rule groups and rules</span></span>

<span data-ttu-id="e627f-115">**Pour afficher les règles et groupes de règles**</span><span class="sxs-lookup"><span data-stu-id="e627f-115">**To view rule groups and rules**</span></span>
   1. <span data-ttu-id="e627f-116">Accédez à la passerelle Application Gateway, puis sélectionnez **Pare-feu d’applications web**.</span><span class="sxs-lookup"><span data-stu-id="e627f-116">Browse to the application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="e627f-117">Sélectionnez **Configuration de règle avancée**.</span><span class="sxs-lookup"><span data-stu-id="e627f-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="e627f-118">Un tableau s’affiche sur la page de tous les groupes de règles fournis avec l’ensemble de règles choisi.</span><span class="sxs-lookup"><span data-stu-id="e627f-118">This view shows a table on the page of all the rule groups provided with the chosen rule set.</span></span> <span data-ttu-id="e627f-119">Toutes les cases à cocher de la règle sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="e627f-119">All of the rule's check boxes are selected.</span></span>

![Configurer des règles désactivées][1]

## <a name="search-for-rules-to-disable"></a><span data-ttu-id="e627f-121">Rechercher des règles à désactiver</span><span class="sxs-lookup"><span data-stu-id="e627f-121">Search for rules to disable</span></span>

<span data-ttu-id="e627f-122">Le panneau des **paramètres de pare-feu d’applications web** permet de filtrer les règles à l’aide d’une recherche de texte.</span><span class="sxs-lookup"><span data-stu-id="e627f-122">The **Web application firewall settings** blade provides the capability to filter the rules through a text search.</span></span> <span data-ttu-id="e627f-123">Le résultat affiche uniquement les groupes de règles et les règles contenant le texte que vous avez recherché.</span><span class="sxs-lookup"><span data-stu-id="e627f-123">The result displays only the rule groups and rules that contain the text you searched for.</span></span>

![Rechercher des règles][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="e627f-125">Désactiver les règles et les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="e627f-125">Disable rule groups and rules</span></span>

<span data-ttu-id="e627f-126">Lorsque vous désactivez des règles, vous pouvez désactiver un groupe de règles entier, ou des règles spécifiques sous un ou plusieurs groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="e627f-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="e627f-127">**Pour désactiver des groupes de règles ou des règles spécifiques**</span><span class="sxs-lookup"><span data-stu-id="e627f-127">**To disable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="e627f-128">Recherchez les règles ou les groupes de règles que vous voulez désactiver.</span><span class="sxs-lookup"><span data-stu-id="e627f-128">Search for the rules or rule groups that you want to disable.</span></span>
   2. <span data-ttu-id="e627f-129">Désactivez les cases à cocher correspondant aux règles que vous voulez désactiver.</span><span class="sxs-lookup"><span data-stu-id="e627f-129">Clear the check boxes for the rules that you want to disable.</span></span> 
   2. <span data-ttu-id="e627f-130">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e627f-130">Select **Save**.</span></span> 

![Enregistrer les modifications][3]

## <a name="next-steps"></a><span data-ttu-id="e627f-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e627f-132">Next steps</span></span>

<span data-ttu-id="e627f-133">Après avoir configuré vos règles désactivées, vous pouvez apprendre à afficher vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="e627f-133">After you configure your disabled rules, you can learn how to view your WAF logs.</span></span> <span data-ttu-id="e627f-134">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="e627f-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
