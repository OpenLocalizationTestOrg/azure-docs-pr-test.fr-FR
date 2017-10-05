---
title: "Intégration d’Application Gateway à Azure Security Center | Microsoft Docs"
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
ms.openlocfilehash: 737cdff3140be68cf9d6d396b470dd09c65c52f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-integration-between-application-gateway-and-azure-security-center"></a><span data-ttu-id="f69f8-103">Vue d’ensemble de l’intégration entre Application Gateway et Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f69f8-103">Overview of integration between Application Gateway and Azure Security Center</span></span>

<span data-ttu-id="f69f8-104">Découvrez comment Application Gateway et Azure Security Center protègent vos ressources d’application web.</span><span class="sxs-lookup"><span data-stu-id="f69f8-104">Learn how Application Gateway and Security Center help protect your web application resources.</span></span> <span data-ttu-id="f69f8-105">Le pare-feu d’applications web de la passerelle Application Gateway (WAF) s’intègre à [Security Center](../security-center/security-center-intro.md) afin de fournir une vue claire pour empêcher, détecter et répondre aux menaces auxquelles les applications web non protégées de votre environnement sont confrontées.</span><span class="sxs-lookup"><span data-stu-id="f69f8-105">Application gateway web application firewall (WAF) integrates with [Security Center](../security-center/security-center-intro.md) to provide a seamless view to prevent, detect and respond to threats to unprotected web applications in your environment.</span></span>

## <a name="overview"></a><span data-ttu-id="f69f8-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f69f8-106">Overview</span></span>

<span data-ttu-id="f69f8-107">Le WAF d’Application Gateway est une recommandation du Security Center visant à protéger les applications web des failles de sécurité et des vulnérabilités.</span><span class="sxs-lookup"><span data-stu-id="f69f8-107">Application Gateway WAF is a recommendation in Security Center for protecting web applications from exploits and vulnerabilities.</span></span> <span data-ttu-id="f69f8-108">Les ressources web qui ne sont pas protégées par le WAF apparaissent dans le centre de sécurité sous la forme de recommandations à gravité élevée.</span><span class="sxs-lookup"><span data-stu-id="f69f8-108">Web enabled resources that are not protected by WAF show in the security center as high severity recommendations.</span></span> <span data-ttu-id="f69f8-109">Les recommandations relatives aux pare-feux d’applications web s’affichent sur la page **Vue d’ensemble** sous **Applications**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-109">Recommendations for web application firewalls are shown on the **Overview** page, under **Applications**.</span></span>

![Intégration au centre de sécurité][1]

<span data-ttu-id="f69f8-111">Cliquez sur n’importe quelle recommandation relative au pare-feu d’applications web pour ouvrir un nouveau panneau présentant les détails de la recommandation.</span><span class="sxs-lookup"><span data-stu-id="f69f8-111">Clicking any recommendations regarding web application firewall opens a new blade showing the details of the recommendation.</span></span>

## <a name="add-a-web-application-firewall-to-an-existing-resource"></a><span data-ttu-id="f69f8-112">Ajouter un pare-feu d’applications web à une ressource existante</span><span class="sxs-lookup"><span data-stu-id="f69f8-112">Add a web application firewall to an existing resource</span></span>

<span data-ttu-id="f69f8-113">Accédez à **Plus de services** > **Sécurité + Identité** > **Security Center** et sur le panneau **Security Center - Vue d’ensemble**, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-113">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Applications**.</span></span> <span data-ttu-id="f69f8-114">Sur le panneau **Security Center - Applications**, la table contient une liste d’applications détectées par Security Center dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f69f8-114">On the **Security Center - Applications** blade, the table contains a list of applications that Security Center detected in your subscription.</span></span>

![applications web][3]

<span data-ttu-id="f69f8-116">Cliquez sur une application web confrontée à un problème critique pour afficher le panneau **État de la sécurité de l’application**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-116">By clicking on a web application with a critical issue, you get the **Application security health** blade.</span></span> <span data-ttu-id="f69f8-117">Dans l’image ci-dessous, l’application web qui n’est pas protégée par un pare-feu d’applications web s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f69f8-117">In the image below, the web application that is not protected by a web application firewall.</span></span> 

![ressources web non protégées][2]

<span data-ttu-id="f69f8-119">Cliquez sur **Ajouter un pare-feu d’applications web** sous **Recommandations** pour ouvrir le panneau **Ajouter un pare-feu d’applications web**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-119">Click **Add a web application firewall** under **Recommendations** to open the **Add a Web Application Firewall** blade.</span></span>

<span data-ttu-id="f69f8-120">S’il n’existe aucune passerelle Application Gateway existante, ou si vous voulez en créer une, cliquez sur **Créer nouveau** et sur le panneau **Créer un nouveau pare-feu d’applications web**, puis sur **Microsoft - Application Gateway**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-120">If you do not have an existing Application Gateway, or want to create a new one, click **Create New** and on the **Create a new Web Application Firewall** blade, and click **Microsoft - Application Gateway**.</span></span> <span data-ttu-id="f69f8-121">Vous serez dirigé vers les étapes de création d’une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="f69f8-121">This takes you through the steps to create an application gateway.</span></span> <span data-ttu-id="f69f8-122">À ce stade, votre application web est ajoutée sous forme de ressource protégée. Security Center effectue désormais le suivi de protection par un pare-feu d’applications web de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="f69f8-122">At this point, your web application is added as a protected resource, Security Center now tracks that this resource is protected by a web application firewall.</span></span> <span data-ttu-id="f69f8-123">Cela n’a pas pour effet de l’ajouter comme membre du pool principal.</span><span class="sxs-lookup"><span data-stu-id="f69f8-123">This does not add it as a backend pool member.</span></span>

<span data-ttu-id="f69f8-124">S’il existe une passerelle d’application, vous pouvez la choisir sous **Utiliser la solution existante**</span><span class="sxs-lookup"><span data-stu-id="f69f8-124">If you have an existing application gateway, you can choose it under **Use existing solution**</span></span>

![panneau d’ajout de pare-feu d’applications web][4]

<span data-ttu-id="f69f8-126">L’ajout d’une application web à une passerelle d’application via Security Center n’ajoute pas la ressource en tant que membre du pool principal. Cette opération doit être effectuée directement sur la ressource de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-126">Adding a web application to an application gateway through Security Center does not add the resource as a backend pool member, this must be done on the application gateway resource directly.</span></span>

## <a name="add-a-resource-to-an-existing-web-application-firewall"></a><span data-ttu-id="f69f8-127">Ajouter une ressource à un pare-feu d’applications web existant</span><span class="sxs-lookup"><span data-stu-id="f69f8-127">Add a resource to an existing web application firewall</span></span>

<span data-ttu-id="f69f8-128">Accédez à **Plus de services** > **Sécurité + Identité** > **Security Center** et sur le panneau **Security Center - Vue d’ensemble**, cliquez sur **Solutions de partenaires**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-128">Navigate to **More Services** > **Security + Identity** > **Security Center** and on the **Security Center - Overview** blade, click **Partner solutions**.</span></span> <span data-ttu-id="f69f8-129">Les passerelles d’application prises en charge par les passerelles d’application s’affichent dans le panneau **Solutions de partenaires**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-129">Existing Security Center aware application gateways show in the **Partner Solutions** blade.</span></span>

![Solutions de partenaires][7]

<span data-ttu-id="f69f8-131">Cliquez sur **Lier l’application** pour ouvrir le panneau **Lier les applications**. Vous avez ici la possibilité de sélectionner les applications existantes.</span><span class="sxs-lookup"><span data-stu-id="f69f8-131">Click **Link app** to open the **Link Applications** blade, here you are given the options to select existing applications.</span></span> <span data-ttu-id="f69f8-132">Choisissez les applications à protéger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-132">Choose the applications to protect and click **OK**.</span></span> <span data-ttu-id="f69f8-133">Cette méthode n’ajoute pas l’application web au pool principal de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-133">This does not add the web application to the backend pool of the application gateway.</span></span> <span data-ttu-id="f69f8-134">Cette opération définit les ressources sous forme de ressource protégée de sorte que Security Center puisse en assurer le suivi.</span><span class="sxs-lookup"><span data-stu-id="f69f8-134">This sets the resources as a protected resource so Security Center can track it.</span></span> <span data-ttu-id="f69f8-135">Pour ajouter la ressource en tant que membre du pool principal, cette opération doit être effectuée sur la passerelle d’application. Depuis le panneau actif, vous pouvez cliquer sur **Console de solution** pour accéder à la ressource de passerelle d’application d’où vous pouvez ajouter l’application web au pool principal.</span><span class="sxs-lookup"><span data-stu-id="f69f8-135">To add the resource as a backend pool member, this must be done on the application gateway, from the current blade you can click **Solution console** to be taken to the application gateway resource where you can add the web application to the backend pool.</span></span>

![applications de solutions de partenaires][6]

## <a name="finalize-configuration"></a><span data-ttu-id="f69f8-137">Finaliser la configuration</span><span class="sxs-lookup"><span data-stu-id="f69f8-137">Finalize configuration</span></span>

<span data-ttu-id="f69f8-138">Security Center effectue le suivi des applications ajoutées à une passerelle d’application sous forme de ressource protégée.</span><span class="sxs-lookup"><span data-stu-id="f69f8-138">Security Center tracks applications added to an application gateway as a protected resource.</span></span>  <span data-ttu-id="f69f8-139">Il analyse l’état de cette ressource et permet de s’assurer qu’elle est protégée par une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-139">It monitors the health of this resource and ensures that it is protected by an application gateway.</span></span> <span data-ttu-id="f69f8-140">L’étape suivante consiste à ajouter l’adresse IP privée, l’adresse IP publique ou la carte réseau de votre machine virtuelle au pool principal de la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-140">The next step is to add the private IP, public IP, or NIC of your virtual machine to the backend pool of the application gateway.</span></span> <span data-ttu-id="f69f8-141">Tant que cette opération n’est pas effectuée, une recommandation supplémentaire de **finalisation de la protection de l’application** s’affiche jusqu’à ce que la ressource soit ajoutée.</span><span class="sxs-lookup"><span data-stu-id="f69f8-141">Until this is done an additional recommendation of **Finalize application protection** is shown until the resource is added.</span></span>

![panneau d’ajout de pare-feu d’applications web][5]

## <a name="security-alerts"></a><span data-ttu-id="f69f8-143">Alertes de sécurité</span><span class="sxs-lookup"><span data-stu-id="f69f8-143">Security Alerts</span></span>

<span data-ttu-id="f69f8-144">Dans Security Center, accédez à **DÉTECTION** > **Alertes de sécurité**.</span><span class="sxs-lookup"><span data-stu-id="f69f8-144">Within Security Center navigate to **DETECTION** > **Security Alerts**.</span></span>  <span data-ttu-id="f69f8-145">Vous y trouverez des alertes WAF relatives aux passerelles de votre application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-145">Here you find WAF alerts for your application gateways.</span></span> <span data-ttu-id="f69f8-146">Les alertes sont réparties selon la règle WAF.</span><span class="sxs-lookup"><span data-stu-id="f69f8-146">Alerts are broken down by WAF rule.</span></span>

![alertes de sécurité][8]

<span data-ttu-id="f69f8-148">Cliquez sur une règle pour fournir une liste des alertes relatives à cette règle WAF spécifique.</span><span class="sxs-lookup"><span data-stu-id="f69f8-148">Clicking an rule will provide a list of alerts for that specific WAF rule.</span></span> <span data-ttu-id="f69f8-149">Chaque alerte affiche des informations supplémentaires sur la recherche.</span><span class="sxs-lookup"><span data-stu-id="f69f8-149">Each alert shows additional details on the finding.</span></span> <span data-ttu-id="f69f8-150">Les informations comportent un lien vers la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="f69f8-150">The details provide a link to the application gateway.</span></span>
 
![détails de l’alerte][9]

## <a name="next-steps"></a><span data-ttu-id="f69f8-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f69f8-152">Next steps</span></span>

<span data-ttu-id="f69f8-153">Pour savoir comment activer un pare-feu d’applications web sur une passerelle d’application existante, consultez [Créer ou mettre à jour une passerelle d’application Azure avec un pare-feu d’applications web](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway).</span><span class="sxs-lookup"><span data-stu-id="f69f8-153">To learn how to enable web application firewall on an existing application gateway, visit [Create or update an Azure Application Gateway with web application firewall](application-gateway-web-application-firewall-portal.md#add-web-application-firewall-to-an-existing-application-gateway)</span></span>

[1]: ./media/application-gateway-integration-security-center/figure1.png
[2]: ./media/application-gateway-integration-security-center/figure2.png
[3]: ./media/application-gateway-integration-security-center/figure3.png
[4]: ./media/application-gateway-integration-security-center/figure4.png
[5]: ./media/application-gateway-integration-security-center/figure5.png
[6]: ./media/application-gateway-integration-security-center/figure6.png
[7]: ./media/application-gateway-integration-security-center/figure7.png
[8]: ./media/application-gateway-integration-security-center/securitycenter.png
[9]: ./media/application-gateway-integration-security-center/figure9.png