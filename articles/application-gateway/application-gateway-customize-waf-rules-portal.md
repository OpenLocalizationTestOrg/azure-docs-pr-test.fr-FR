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
# <a name="customize-web-application-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="de352-103">Personnaliser les règles de pare-feu d’applications web via hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="de352-103">Customize web application firewall rules through hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="de352-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="de352-104">Azure portal</span></span>](application-gateway-customize-waf-rules-portal.md)
> * [<span data-ttu-id="de352-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de352-105">PowerShell</span></span>](application-gateway-customize-waf-rules-powershell.md)
> * [<span data-ttu-id="de352-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de352-106">Azure CLI 2.0</span></span>](application-gateway-customize-waf-rules-cli.md)

<span data-ttu-id="de352-107">pare-feu d’applications web Hello Azure Application Gateway (WAF) offre une protection pour les applications web.</span><span class="sxs-lookup"><span data-stu-id="de352-107">hello Azure Application Gateway web application firewall (WAF) provides protection for web applications.</span></span> <span data-ttu-id="de352-108">Ces protections sont fournies par hello ouvrir Web Application sécurité projet (OWASP avoir) Core règle définie (DM).</span><span class="sxs-lookup"><span data-stu-id="de352-108">These protections are provided by hello Open Web Application Security Project (OWASP) Core Rule Set (CRS).</span></span> <span data-ttu-id="de352-109">Certaines règles peuvent entraîner des faux positifs et bloquer le trafic réel.</span><span class="sxs-lookup"><span data-stu-id="de352-109">Some rules can cause false positives and block real traffic.</span></span> <span data-ttu-id="de352-110">Pour cette raison, la passerelle d’Application fournit et hello capacité toocustomize groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="de352-110">For this reason, Application Gateway provides hello capability toocustomize rule groups and rules.</span></span> <span data-ttu-id="de352-111">Pour plus d’informations sur les règles et les groupes de règles spécifiques hello, consultez [la liste des règles et des groupes de règles web application pare-feu CRS](application-gateway-crs-rulegroups-rules.md).</span><span class="sxs-lookup"><span data-stu-id="de352-111">For more information on hello specific rule groups and rules, see [List of web application firewall CRS rule groups and rules](application-gateway-crs-rulegroups-rules.md).</span></span>

>[!NOTE]
> <span data-ttu-id="de352-112">Si votre passerelle d’application n’utilise pas le niveau de WAF hello, hello option tooupgrade hello passerelle toohello WAF applicative s’affiche dans le volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="de352-112">If your application gateway is not using hello WAF tier, hello option tooupgrade hello application gateway toohello WAF tier appears in hello right pane.</span></span> 

![Activer WAF][fig1]

## <a name="view-rule-groups-and-rules"></a><span data-ttu-id="de352-114">Afficher les règles et groupes de règles</span><span class="sxs-lookup"><span data-stu-id="de352-114">View rule groups and rules</span></span>

<span data-ttu-id="de352-115">**règles et groupes de règles tooview**</span><span class="sxs-lookup"><span data-stu-id="de352-115">**tooview rule groups and rules**</span></span>
   1. <span data-ttu-id="de352-116">Parcourir la passerelle d’application toohello, puis sélectionnez **pare-feu d’applications Web**.</span><span class="sxs-lookup"><span data-stu-id="de352-116">Browse toohello application gateway, and then select **Web application firewall**.</span></span>  
   2. <span data-ttu-id="de352-117">Sélectionnez **Configuration de règle avancée**.</span><span class="sxs-lookup"><span data-stu-id="de352-117">Select **Advanced rule configuration**.</span></span>  
   <span data-ttu-id="de352-118">Cette vue affiche une table sur la page hello de tous les groupes de règles hello fourni avec hello choisi l’ensemble de règles.</span><span class="sxs-lookup"><span data-stu-id="de352-118">This view shows a table on hello page of all hello rule groups provided with hello chosen rule set.</span></span> <span data-ttu-id="de352-119">Toutes les cases à cocher de la règle hello sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="de352-119">All of hello rule's check boxes are selected.</span></span>

![Configurer des règles désactivées][1]

## <a name="search-for-rules-toodisable"></a><span data-ttu-id="de352-121">Recherche de règles toodisable</span><span class="sxs-lookup"><span data-stu-id="de352-121">Search for rules toodisable</span></span>

<span data-ttu-id="de352-122">Hello **paramètres de pare-feu d’applications Web** panneau permet hello toofilter les règles de hello via une recherche de texte.</span><span class="sxs-lookup"><span data-stu-id="de352-122">hello **Web application firewall settings** blade provides hello capability toofilter hello rules through a text search.</span></span> <span data-ttu-id="de352-123">résultat de Hello affiche uniquement les groupes de règles de hello et les règles qui contiennent du texte hello recherché.</span><span class="sxs-lookup"><span data-stu-id="de352-123">hello result displays only hello rule groups and rules that contain hello text you searched for.</span></span>

![Rechercher des règles][2]

## <a name="disable-rule-groups-and-rules"></a><span data-ttu-id="de352-125">Désactiver les règles et les groupes de règles</span><span class="sxs-lookup"><span data-stu-id="de352-125">Disable rule groups and rules</span></span>

<span data-ttu-id="de352-126">Lorsque vous désactivez des règles, vous pouvez désactiver un groupe de règles entier, ou des règles spécifiques sous un ou plusieurs groupes de règles.</span><span class="sxs-lookup"><span data-stu-id="de352-126">When your're disabling rules, you can disable an entire rule group or specific rules under one or more rule groups.</span></span> 

<span data-ttu-id="de352-127">**groupes de règles toodisable ou des règles spécifiques**</span><span class="sxs-lookup"><span data-stu-id="de352-127">**toodisable rule groups or specific rules**</span></span>

   1. <span data-ttu-id="de352-128">Rechercher des règles de hello ou des groupes de règles que vous souhaitez toodisable.</span><span class="sxs-lookup"><span data-stu-id="de352-128">Search for hello rules or rule groups that you want toodisable.</span></span>
   2. <span data-ttu-id="de352-129">Désactivez les cases à cocher hello hello des règles que vous souhaitez toodisable.</span><span class="sxs-lookup"><span data-stu-id="de352-129">Clear hello check boxes for hello rules that you want toodisable.</span></span> 
   2. <span data-ttu-id="de352-130">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="de352-130">Select **Save**.</span></span> 

![Enregistrer les modifications][3]

## <a name="next-steps"></a><span data-ttu-id="de352-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="de352-132">Next steps</span></span>

<span data-ttu-id="de352-133">Après avoir configuré vos règles désactivées, vous pouvez apprendre comment tooview vos journaux WAF.</span><span class="sxs-lookup"><span data-stu-id="de352-133">After you configure your disabled rules, you can learn how tooview your WAF logs.</span></span> <span data-ttu-id="de352-134">Pour plus d’informations, consultez [Diagnostics Application Gateway](application-gateway-diagnostics.md#diagnostic-logging).</span><span class="sxs-lookup"><span data-stu-id="de352-134">For more information, see [Application Gateway diagnostics](application-gateway-diagnostics.md#diagnostic-logging).</span></span>

[fig1]: ./media/application-gateway-customize-waf-rules-portal/1.png
[1]: ./media/application-gateway-customize-waf-rules-portal/figure1.png
[2]: ./media/application-gateway-customize-waf-rules-portal/figure2.png
[3]: ./media/application-gateway-customize-waf-rules-portal/figure3.png
