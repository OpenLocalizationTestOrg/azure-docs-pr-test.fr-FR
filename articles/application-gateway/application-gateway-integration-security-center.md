---
title: "intégration de la passerelle avec Azure Security Center d’aaaApplication | Documents Microsoft"
description: "Cette page fournit des informations sur l’intégration d’Application Gateway à Azure Security Center."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: e5ea5cf9-3b41-4b85-a12c-e758bff7f3ec
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: 
ms.workload: infrastructure-services
ms.date: 06/07/2017
ms.author: gwallace
ms.openlocfilehash: 6f6ace105e84c01f525ab02938e81ce040c5c9d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="3a683-103">Vue d’ensemble de l’intégration entre Application Gateway et Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3a683-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="3a683-104">Découvrez comment Application Gateway et Azure Security Center protègent vos ressources d’application web.</span><span class="sxs-lookup"><span data-stu-id="3a683-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="3a683-105">Pare-feu d’applications web application gateway (WAF) s’intègre à [centre de sécurité](../security-center/security-center-intro.md) tooprovide tooprevent une vue claire, détecter et traiter des toothreats toounprotected les applications web dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="3a683-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) tooprovide a seamless view tooprevent, detect and respond toothreats toounprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="3a683-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3a683-106">Overview</span></span>

<span data-ttu-id="3a683-107">Le WAF d’Application Gateway est une recommandation du Security Center visant à protéger les applications web des failles de sécurité et des vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="3a683-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="3a683-108">Les ressources Web activée qui ne sont pas protégés par WAF affichent dans le centre de sécurité hello sous forme de recommandations de gravité élevée.</span><span class="sxs-lookup"><span data-stu-id="3a683-108">Web enabled resources that are not protected by WAF show in hello security center as high severity recommendations.</span></span> <span data-ttu-id="3a683-109">Recommandations pour les pare-feu d’applications web sont affichées sur hello **vue d’ensemble** sous **Applications**.</span><span class="sxs-lookup"><span data-stu-id="3a683-109">Recommendations for web application firewalls are shown on hello **Overview** page, under **Applications**.</span></span>

![Intégration au centre de sécurité][1]

<span data-ttu-id="3a683-111">Cliquez sur les recommandations concernant les pare-feu d’applications web pour ouvrir un nouveau panneau présentant les détails de hello de recommandation de hello.</span><span class="sxs-lookup"><span data-stu-id="3a683-111">Clicking any recommendations regarding web application firewall opens a new blade showing hello details of hello recommendation.</span></span>

## <a name="add-a-web-application-firewall-tooan-existing-resource"></a><span data-ttu-id="3a683-112">Ajouter une ressource web application pare-feu tooan existant</span><span class="sxs-lookup"><span data-stu-id="3a683-112">Add a web application firewall tooan existing resource</span></span>

<span data-ttu-id="3a683-113">Accédez trop**plus Services** > **sécurité + identité** > **centre de sécurité** et hello **centre de sécurité - vue d’ensemble**  panneau, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="3a683-113">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="3a683-114">Sur hello **centre de sécurité - Applications** panneau, table de hello contient une liste d’applications centre de sécurité a détecté dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3a683-114">On hello **Security Center - Applications** blade, hello table contains a list of applications that Security Center detected in your subscription.</span></span>

![applications web][3]

<span data-ttu-id="3a683-116">En cliquant sur une application web avec un problème critique, vous obtenez hello **intégrité de la sécurité Application** panneau.</span><span class="sxs-lookup"><span data-stu-id="3a683-116">By clicking on a web application with a critical issue, you get hello **Application security health** blade.</span></span> <span data-ttu-id="3a683-117">Dans l’image hello ci-dessous, hello application web qui n’est pas protégée par un pare-feu d’applications web.</span><span class="sxs-lookup"><span data-stu-id="3a683-117">In hello image below, hello web application that is not protected by a web application firewall.</span></span> 

![ressources web non protégées][2]

<span data-ttu-id="3a683-119">Cliquez sur **ajouter un pare-feu d’applications web** sous **recommandations** tooopen hello **ajouter un pare-feu d’applications Web** panneau.</span><span class="sxs-lookup"><span data-stu-id="3a683-119">Click **Add a web application firewall** under **Recommendations** tooopen hello **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="3a683-120">Si vous n’ont pas une passerelle d’Application existant, ou souhaitez toocreate un nouveau, cliquez sur **créer un nouveau** et hello **créer un nouveau pare-feu d’applications Web** panneau, puis cliquez sur **Microsoft - Passerelle d’application**.</span><span class="sxs-lookup"><span data-stu-id="3a683-120">If you do not have an existing Application Gateway, or want toocreate a new one, click **Create New** and on hello **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="3a683-121">Vous accédez via hello étapes toocreate une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="3a683-121">This takes you through hello steps toocreate an application gateway.</span></span> <span data-ttu-id="3a683-122">À ce stade, votre application web est ajoutée sous forme de ressource protégée. Security Center effectue désormais le suivi de protection par un pare-feu d’applications web de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="3a683-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="3a683-123">Cela n’a pas pour effet de l’ajouter comme membre du pool principal.</span><span class="sxs-lookup"><span data-stu-id="3a683-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="3a683-124">S’il existe une passerelle d’application, vous pouvez la choisir sous **Utiliser la solution existante**</span><span class="sxs-lookup"><span data-stu-id="3a683-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![panneau d’ajout de pare-feu d’applications web][4]

<span data-ttu-id="3a683-126">Ajout de qu'une passerelle d’application web application tooan via le centre de sécurité n’ajoute pas de ressource de hello en tant qu’un membre du pool principal, il est indispensable sur les ressources de passerelle d’application hello directement.</span><span class="sxs-lookup"><span data-stu-id="3a683-126">Adding a web application tooan application gateway through Security Center does not add hello resource as a backend pool member, this must be done on hello application gateway resource directly.</span></span>

## <a name="add-a-resource-tooan-existing-web-application-firewall"></a><span data-ttu-id="3a683-127">Ajouter un pare-feu d’applications web existantes ressource tooan</span><span class="sxs-lookup"><span data-stu-id="3a683-127">Add a resource tooan existing web application firewall</span></span>

<span data-ttu-id="3a683-128">Accédez trop**plus Services** > **sécurité + identité** > **centre de sécurité** et hello **centre de sécurité - vue d’ensemble**  panneau, cliquez sur **solutions de partenaire**.</span><span class="sxs-lookup"><span data-stu-id="3a683-128">Navigate too**More Services** > **Security + Identity** > **Security Center** and on hello **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="3a683-129">Affichent les passerelles d’application prenant en charge le centre de sécurité existants dans hello **Solutions de partenaire** panneau.</span><span class="sxs-lookup"><span data-stu-id="3a683-129">Existing Security Center aware application gateways show in hello **Partner Solutions** blade.</span></span>

![Solutions de partenaires][7]

<span data-ttu-id="3a683-131">Cliquez sur **lien application** tooopen hello **lien Applications** panneau, vous pouvez soit les applications existantes hello options tooselect ici.</span><span class="sxs-lookup"><span data-stu-id="3a683-131">Click **Link app** tooopen hello **Link Applications** blade, here you are given hello options tooselect existing applications.</span></span> <span data-ttu-id="3a683-132">Choisissez hello applications tooprotect et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a683-132">Choose hello applications tooprotect and click **OK**.</span></span> <span data-ttu-id="3a683-133">Cette méthode n’ajoute pas pool hello web application toohello principal de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="3a683-133">This does not add hello web application toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="3a683-134">Définit les ressources hello comme une ressource protégée afin de centre de sécurité peut le suivre.</span><span class="sxs-lookup"><span data-stu-id="3a683-134">This sets hello resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="3a683-135">ressource de hello tooadd comme un membre du pool principal, ceci doit être fait sur la passerelle d’application hello, panneau actuel de hello vous pouvez cliquer sur **console de la Solution** toobe prise toohello ressource de passerelle d’application où vous pouvez ajouter le serveur web hello pool principal d’application toohello.</span><span class="sxs-lookup"><span data-stu-id="3a683-135">tooadd hello resource as a backend pool member, this must be done on hello application gateway, from hello current blade you can click **Solution console** toobe taken toohello application gateway resource where you can add hello web application toohello backend pool.</span></span>

![applications de solutions de partenaires][6]

## <a name="finalize-configuration"></a><span data-ttu-id="3a683-137">Finaliser la configuration</span><span class="sxs-lookup"><span data-stu-id="3a683-137">Finalize configuration</span></span>

<span data-ttu-id="3a683-138">Les applications assure le suivi du centre de sécurité ajouté tooan passerelle d’application comme une ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="3a683-138">Security Center tracks applications added tooan application gateway as a protected resource.</span></span>  <span data-ttu-id="3a683-139">Il surveille l’intégrité de hello de cette ressource et que vous permet de s’assurer qu’elle est protégée par une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="3a683-139">It monitors hello health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="3a683-140">étape suivante de Hello est tooadd hello privé IP, adresse IP publique ou carte réseau de votre pool de back-end toohello machine virtuelle de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="3a683-140">hello next step is tooadd hello private IP, public IP, or NIC of your virtual machine toohello backend pool of hello application gateway.</span></span> <span data-ttu-id="3a683-141">Jusqu'à ce que cette opération est effectuée une recommandation supplémentaire de **finaliser la protection de l’application** est indiqué en tant que ressource de hello est ajoutée.</span><span class="sxs-lookup"><span data-stu-id="3a683-141">Until this is done an additional recommendation of **Finalize application protection** is shown until hello resource is added.</span></span>

![panneau d’ajout de pare-feu d’applications web][5]

## <a name="security-alerts"></a><span data-ttu-id="3a683-143">Alertes de sécurité</span><span class="sxs-lookup"><span data-stu-id="3a683-143">Security Alerts</span></span>

<span data-ttu-id="3a683-144">Dans le centre de sécurité accédez trop**détection** > **alertes de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="3a683-144">Within Security Center navigate too**DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="3a683-145">Vous y trouverez des alertes WAF relatives aux passerelles de votre application.</span><span class="sxs-lookup"><span data-stu-id="3a683-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="3a683-146">Les alertes sont réparties selon la règle WAF.</span><span class="sxs-lookup"><span data-stu-id="3a683-146">Alerts are broken down by WAF rule.</span></span>

![alertes de sécurité][8]

<span data-ttu-id="3a683-148">Cliquez sur une règle pour fournir une liste des alertes relatives à cette règle WAF spécifique.</span><span class="sxs-lookup"><span data-stu-id="3a683-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="3a683-149">Chaque alerte affiche des détails supplémentaires sur la recherche de hello.</span><span class="sxs-lookup"><span data-stu-id="3a683-149">Each alert shows additional details on hello finding.</span></span> <span data-ttu-id="3a683-150">Détails de Hello fournissent une passerelle d’application toohello lien.</span><span class="sxs-lookup"><span data-stu-id="3a683-150">hello details provide a link toohello application gateway.</span></span>
 
![détails de l’alerte][9]

## <a name="next-steps"></a><span data-ttu-id="3a683-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3a683-152">Next steps</span></span>

<span data-ttu-id="3a683-153">toolearn comment tooenable pare-feu d’applications web sur une passerelle d’application existant, visitez [créer ou mettre à jour une passerelle d’Application Azure avec pare-feu d’applications web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span><span class="sxs-lookup"><span data-stu-id="3a683-153">toolearn how tooenable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png