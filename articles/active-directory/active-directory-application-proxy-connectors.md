---
title: "Connecteurs de proxy d’application Azure AD du portail Classic | Microsoft Docs"
description: "Explique comment créer et gérer des groupes de connecteurs dans le proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: fc65c4053c45d9c16c62ee0fe65924133a4bb94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a><span data-ttu-id="d1e4f-103">Publier des applications sur des réseaux et emplacements distincts à l’aide de groupes de connecteurs</span><span class="sxs-lookup"><span data-stu-id="d1e4f-103">Publish applications on separate networks and locations using connector groups</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1e4f-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d1e4f-104">Azure portal</span></span>](active-directory-application-proxy-connectors-azure-portal.md)
> * [<span data-ttu-id="d1e4f-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="d1e4f-105">Azure classic portal</span></span>](active-directory-application-proxy-connectors.md)
>
>

<span data-ttu-id="d1e4f-106">Les groupes de connecteurs sont utiles dans divers scénarios, notamment les suivants :</span><span class="sxs-lookup"><span data-stu-id="d1e4f-106">Connector groups are useful for various scenarios, including:</span></span>

* <span data-ttu-id="d1e4f-107">Sites contenant plusieurs centres de données interconnectés.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-107">Sites with multiple interconnected datacenters.</span></span> <span data-ttu-id="d1e4f-108">Dans ce cas, vous souhaitez conserver autant de trafic que possible au sein du centre de données, car les liaisons entre les centres de données sont coûteuses et lentes.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-108">In this case, you want to keep as much traffic within the datacenter as possible because cross-datacenter links are expensive and slow.</span></span> <span data-ttu-id="d1e4f-109">Vous pouvez déployer des connecteurs dans chaque centre de données pour traiter uniquement les applications contenues dans le centre de données.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-109">You can deploy connectors in each datacenter to serve only the applications that reside within the datacenter.</span></span> <span data-ttu-id="d1e4f-110">Cette approche réduit au minimum les liaisons entre centres de données et fournit à vos utilisateurs une expérience entièrement transparente.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-110">This approach minimizes cross-datacenter links and provides an entirely transparent experience to your users.</span></span>
* <span data-ttu-id="d1e4f-111">Gestion d’applications installées sur des réseaux isolés qui ne font pas partie du réseau d’entreprise principal.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-111">Managing applications installed on isolated networks that are not part of the main corporate network.</span></span> <span data-ttu-id="d1e4f-112">Vous pouvez utiliser des groupes de connecteurs pour installer des connecteurs dédiés sur des réseaux isolés afin d’isoler les applications sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-112">You can use connector groups to install dedicated connectors on isolated networks to also isolate applications to the network.</span></span>
* <span data-ttu-id="d1e4f-113">Pour les applications installées sur IaaS pour l’accès au cloud, les groupes de connecteurs fournissent un service commun pour sécuriser l’accès à toutes les applications.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-113">For applications installed on IaaS for cloud access, connector groups provide a common service to secure the access to all the apps.</span></span> <span data-ttu-id="d1e4f-114">Les groupes de connecteurs ne créent pas de dépendances supplémentaires sur votre réseau d’entreprise, et ne fragmentent pas l’expérience de l’application.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-114">Connector groups don't create additional dependency on your corporate network, or fragment the app experience.</span></span> <span data-ttu-id="d1e4f-115">Les connecteurs peuvent être installés sur chaque centre de données du cloud et servir uniquement les applications qui se trouvent sur ce réseau.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-115">Connectors can be installed on every cloud datacenter and serve only applications that reside in this network.</span></span> <span data-ttu-id="d1e4f-116">Vous pouvez installer plusieurs connecteurs pour atteindre une haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-116">You can install several connectors to achieve high availability.</span></span>
* <span data-ttu-id="d1e4f-117">Prise en charge des environnements à plusieurs forêts dans lesquels des connecteurs spécifiques peuvent être déployés par forêt et définis pour servir des applications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-117">Support for multi-forest environments in which specific connectors can be deployed per forest and set to serve specific applications.</span></span>
* <span data-ttu-id="d1e4f-118">Des groupes de connecteurs peuvent être utilisés dans les sites de récupération d’urgence pour détecter le basculement ou faire office de sauvegarde pour le site principal.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-118">Connector groups can be used in Disaster Recovery sites to either detect failover or as backup for the main site.</span></span>
* <span data-ttu-id="d1e4f-119">Des groupes de connecteurs peuvent également être utilisés pour servir plusieurs sociétés à partir d’un client unique.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-119">Connector groups can also be used to serve multiple companies from a single tenant.</span></span>

## <a name="prerequisite-create-your-connectors"></a><span data-ttu-id="d1e4f-120">Condition préalable : créez vos connecteurs</span><span class="sxs-lookup"><span data-stu-id="d1e4f-120">Prerequisite: Create your connectors</span></span>
<span data-ttu-id="d1e4f-121">Pour regrouper vos connecteurs, [installez plusieurs connecteurs](active-directory-application-proxy-enable.md), puis nommez-les et regroupez-les.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-121">To group your connectors, [install multiple connectors](active-directory-application-proxy-enable.md), then name and group them.</span></span> <span data-ttu-id="d1e4f-122">Enfin, vous devez les affecter à des applications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-122">Finally you have to assign them to specific apps.</span></span>

## <a name="step-1-create-connector-groups"></a><span data-ttu-id="d1e4f-123">Étape 1 : créer des groupes de connecteurs</span><span class="sxs-lookup"><span data-stu-id="d1e4f-123">Step 1: Create connector groups</span></span>
<span data-ttu-id="d1e4f-124">Vous pouvez créer autant de groupes de connecteurs que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-124">You can create as many connector groups as you want.</span></span> <span data-ttu-id="d1e4f-125">La création de groupes de connecteurs s’effectue dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-125">Connector group creation is accomplished in the Azure classic portal.</span></span>

1. <span data-ttu-id="d1e4f-126">Sélectionnez votre annuaire, puis cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-126">Select your directory and click **Configure**.</span></span>  
    <span data-ttu-id="d1e4f-127">![Capture d’écran de la configuration du proxy d’application - cliquez sur Gérer les groupes de connecteurs](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span><span class="sxs-lookup"><span data-stu-id="d1e4f-127">![Application proxy, configure screenshot - click manage connector groups](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)</span></span>
2. <span data-ttu-id="d1e4f-128">Sous Proxy d’application, cliquez sur **Gérer les groupes de connecteurs** et créez un groupe de connecteurs en attribuant un nom au groupe.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-128">Under Application Proxy, click **Manage Connector Groups** and create a connector group by giving the group a name.</span></span>  
    <span data-ttu-id="d1e4f-129">![Capture d’écran de groupes de connecteurs du proxy d’application - nommez le nouveau groupe](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span><span class="sxs-lookup"><span data-stu-id="d1e4f-129">![Application proxy connector groups screenshot - name new group](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)</span></span>

## <a name="step-2-assign-connectors-to-your-groups"></a><span data-ttu-id="d1e4f-130">Étape 2 : affecter des connecteurs à vos groupes</span><span class="sxs-lookup"><span data-stu-id="d1e4f-130">Step 2: Assign connectors to your groups</span></span>
<span data-ttu-id="d1e4f-131">Une fois les groupes de connecteurs créés, déplacez les connecteurs vers le groupe approprié.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-131">Once the connector groups are created, move the connectors to the appropriate group.</span></span>

1. <span data-ttu-id="d1e4f-132">Sous **Proxy d’application**, cliquez sur **Gérer les connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-132">Under **Application Proxy**, click **Manage Connectors**.</span></span>
2. <span data-ttu-id="d1e4f-133">Sous **Groupe**, sélectionnez le groupe souhaité pour chaque connecteur.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-133">Under **Group**, select the group you want for each connector.</span></span> <span data-ttu-id="d1e4f-134">L’activation des connecteurs dans le nouveau groupe peut prendre jusqu’à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-134">It might take the connectors up to 10 minutes to become active in the new group.</span></span>  
    <span data-ttu-id="d1e4f-135">![Capture d’écran de connecteurs du proxy d’application - sélectionnez un groupe dans le menu déroulant](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span><span class="sxs-lookup"><span data-stu-id="d1e4f-135">![Application proxy connectors screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)</span></span>

## <a name="step-3-assign-applications-to-your-connector-groups"></a><span data-ttu-id="d1e4f-136">Étape 3 : affecter des applications à vos groupes de connecteurs</span><span class="sxs-lookup"><span data-stu-id="d1e4f-136">Step 3: Assign applications to your connector groups</span></span>
<span data-ttu-id="d1e4f-137">La dernière étape consiste à définir chaque application sur le groupe de connecteurs qui le sert.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-137">The last step is to set each application to the connector group that serves it.</span></span>

1. <span data-ttu-id="d1e4f-138">Dans le portail Azure Classic, dans votre annuaire, sélectionnez l’application que vous voulez affecter au groupe, puis cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-138">In the Azure classic portal, in your directory, select the Application you want to assign to the group and click **Configure**.</span></span>
2. <span data-ttu-id="d1e4f-139">Sous **Groupe de connecteurs**, sélectionnez le groupe que l’application doit utiliser.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-139">Under **Connector group**, select the group you want the application to use.</span></span> <span data-ttu-id="d1e4f-140">Cette modification est appliquée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="d1e4f-140">This change is immediately applied.</span></span>  
    <span data-ttu-id="d1e4f-141">![Capture d’écran de groupe de connecteurs du proxy d’application - sélectionnez un groupe dans le menu déroulant](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span><span class="sxs-lookup"><span data-stu-id="d1e4f-141">![Application proxy connector group screenshot - select group from dropdown menu](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)</span></span>

## <a name="see-also"></a><span data-ttu-id="d1e4f-142">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d1e4f-142">See also</span></span>
* [<span data-ttu-id="d1e4f-143">Activer le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="d1e4f-143">Enable Application Proxy</span></span>](active-directory-application-proxy-enable.md)
* [<span data-ttu-id="d1e4f-144">Activer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d1e4f-144">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="d1e4f-145">Activer l’accès conditionnel</span><span class="sxs-lookup"><span data-stu-id="d1e4f-145">Enable conditional access</span></span>](active-directory-application-proxy-conditional-access.md)
* [<span data-ttu-id="d1e4f-146">Résoudre les problèmes rencontrés avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="d1e4f-146">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)

<span data-ttu-id="d1e4f-147">Pour les dernières nouvelles et mises à jour, visitez [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="d1e4f-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>