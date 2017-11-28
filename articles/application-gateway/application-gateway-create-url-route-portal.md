---
title: "Créer une règle basée sur un chemin - Passerelle Application Gateway Azure - Portail Azure | Microsoft Docs"
description: "Découvrir comment créer une règle basée sur le chemin pour une passerelle Application Gateway à l’aide du portail"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 87bd93bc-e1a6-45db-a226-555948f1feb7
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: c184e94a04cfbdedcae70ed154aeb7dd134d1baf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-the-portal"></a><span data-ttu-id="69a91-103">Créer une règle basée sur le chemin pour une passerelle Application Gateway à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="69a91-103">Create a Path-based rule for an application gateway by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69a91-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="69a91-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="69a91-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="69a91-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="69a91-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69a91-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="69a91-107">Le routage basé sur le chemin d’URL vous permet d’associer des itinéraires basés sur le chemin d’URL de la requête Http.</span><span class="sxs-lookup"><span data-stu-id="69a91-107">URL Path-based routing enables you to associate routes based on the URL path of Http request.</span></span> <span data-ttu-id="69a91-108">Il vérifie s’il existe une route vers un pool principal configuré pour les listes d’URL dans la passerelle Application Gateway et envoie le trafic réseau vers le pool principal défini.</span><span class="sxs-lookup"><span data-stu-id="69a91-108">It checks if there is a route to a back-end pool configured for the URL listed in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="69a91-109">Une utilisation courante du routage basé sur l’URL consiste à équilibrer la charge des demandes pour différents types de contenu entre différents pools de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="69a91-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="69a91-110">Le routage basé sur l’URL introduit un nouveau type de règle pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="69a91-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="69a91-111">La passerelle d’application a deux types de règles : des règles de base et des règles basées sur un chemin.</span><span class="sxs-lookup"><span data-stu-id="69a91-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="69a91-112">Le type de règle de base fournit le service de tourniquet (round robin) pour les pools principaux, tandis que les règles basées sur un chemin, en plus de la distribution en tourniquet, prennent également en compte le modèle de chemin de l’URL de demande lors du choix du pool back-end approprié.</span><span class="sxs-lookup"><span data-stu-id="69a91-112">The basic rule type, provides round-robin service for the back-end pools while path-based rules in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="69a91-113">Scénario</span><span class="sxs-lookup"><span data-stu-id="69a91-113">Scenario</span></span>

<span data-ttu-id="69a91-114">Le scénario suivant passe par la création d’une règle basée sur le chemin sur une passerelle Application Gateway existante.</span><span class="sxs-lookup"><span data-stu-id="69a91-114">The following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="69a91-115">Le scénario suppose que vous avez déjà suivi la procédure de [Création d’une passerelle Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69a91-115">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![itinéraire d’URL][scenario]

## <span data-ttu-id="69a91-117"><a name="createrule"></a>Créer la règle basée sur le chemin</span><span class="sxs-lookup"><span data-stu-id="69a91-117"><a name="createrule"></a>Create the Path-based rule</span></span>

<span data-ttu-id="69a91-118">Une règle basée sur le chemin requiert son propre écouteur. Avant de créer la règle, vérifiez que vous disposez d’un écouteur.</span><span class="sxs-lookup"><span data-stu-id="69a91-118">A Path-based rule requires its own listener, before creating the rule be sure to verify you have an available listener to use.</span></span>

### <a name="step-1"></a><span data-ttu-id="69a91-119">Étape 1</span><span class="sxs-lookup"><span data-stu-id="69a91-119">Step 1</span></span>

<span data-ttu-id="69a91-120">Accédez au [portail Azure](http://portal.azure.com) et sélectionnez une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="69a91-120">Navigate to the [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="69a91-121">Cliquer sur **Règles**</span><span class="sxs-lookup"><span data-stu-id="69a91-121">Click **Rules**</span></span>

![Vue d’ensemble d’Application Gateway][1]

### <a name="step-2"></a><span data-ttu-id="69a91-123">Étape 2</span><span class="sxs-lookup"><span data-stu-id="69a91-123">Step 2</span></span>

<span data-ttu-id="69a91-124">Cliquez sur le bouton **Basé sur le chemin** pour ajouter une nouvelle règle basée sur le chemin.</span><span class="sxs-lookup"><span data-stu-id="69a91-124">Click **Path-based** button to add a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="69a91-125">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="69a91-125">Step 3</span></span>

<span data-ttu-id="69a91-126">Le panneau **Add path-based rule (Ajouter une règle basée sur le chemin)** comporte deux sections.</span><span class="sxs-lookup"><span data-stu-id="69a91-126">The **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="69a91-127">La première section est celle où vous avez défini l’écouteur, le nom de la règle et les paramètres de chemin par défaut.</span><span class="sxs-lookup"><span data-stu-id="69a91-127">The first section is where you defined the listener, the name of the rule and the default path settings.</span></span> <span data-ttu-id="69a91-128">Les paramètres de chemin par défaut sont des itinéraires qui ne relèvent pas de l’itinéraire personnalisé basé sur le chemin.</span><span class="sxs-lookup"><span data-stu-id="69a91-128">The default path settings are for routes that do not fall under the custom path-based route.</span></span> <span data-ttu-id="69a91-129">La deuxième section du panneau **Add path-based rule (Ajouter une règle basée sur le chemin)** est celle où vous définissez les règles basées sur le chemin elles-mêmes.</span><span class="sxs-lookup"><span data-stu-id="69a91-129">The second section of the **Add path-based rule** blade is where you define the path-based rules themselves.</span></span>

<span data-ttu-id="69a91-130">**Paramètres de base**</span><span class="sxs-lookup"><span data-stu-id="69a91-130">**Basic Settings**</span></span>

* <span data-ttu-id="69a91-131">**Nom** - nom convivial de la règle accessible par le biais du portail.</span><span class="sxs-lookup"><span data-stu-id="69a91-131">**Name** - This value is a friendly name to the rule that is accessible in the portal.</span></span>
* <span data-ttu-id="69a91-132">**Écouteur** - écouteur utilisé pour la règle.</span><span class="sxs-lookup"><span data-stu-id="69a91-132">**Listener** - This value is the listener that is used for the rule.</span></span>
* <span data-ttu-id="69a91-133">**Default backend pool (Pool principal par défaut)** - pool principal à utiliser pour la règle par défaut.</span><span class="sxs-lookup"><span data-stu-id="69a91-133">**Default backend pool** - This setting is the setting that defines the back-end to be used for the default rule</span></span>
* <span data-ttu-id="69a91-134">**Default HTTP settings (Paramètres HTTP par défaut)** - paramètres HTTP à utiliser pour la règle par défaut.</span><span class="sxs-lookup"><span data-stu-id="69a91-134">**Default HTTP settings** - This setting is the setting that defines the HTTP settings to be used for the default rule.</span></span>

<span data-ttu-id="69a91-135">**Path-based rules (Règles basées sur le chemin)**</span><span class="sxs-lookup"><span data-stu-id="69a91-135">**Path-based rules**</span></span>

* <span data-ttu-id="69a91-136">**Nom** - nom convivial de la règle basée sur le chemin.</span><span class="sxs-lookup"><span data-stu-id="69a91-136">**Name** - This value is a friendly name to path-based rule.</span></span>
* <span data-ttu-id="69a91-137">**Chemins d’accès** - chemin d’accès que la règle recherche pour transférer le trafic.</span><span class="sxs-lookup"><span data-stu-id="69a91-137">**Paths** - This setting defines the path the rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="69a91-138">**Pool principal** - pool principal à utiliser pour la règle.</span><span class="sxs-lookup"><span data-stu-id="69a91-138">**Backend Pool** - This setting is the setting that defines the back-end to be used for the rule</span></span>
* <span data-ttu-id="69a91-139">**Paramètre HTTP** - paramètres HTTP à utiliser pour la règle.</span><span class="sxs-lookup"><span data-stu-id="69a91-139">**HTTP setting** - This setting is the setting that defines the HTTP settings to be used for the rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69a91-140">Chemins d’accès : liste de modèles de chemin d’accès à utiliser pour la correspondance.</span><span class="sxs-lookup"><span data-stu-id="69a91-140">Paths: The list of path patterns to match.</span></span> <span data-ttu-id="69a91-141">Chaque modèle doit commencer par le signe / et le seul endroit où un astérisque (\*) est autorisé est à la fin.</span><span class="sxs-lookup"><span data-stu-id="69a91-141">Each must start with / and the only place a "\*" is allowed is at the end.</span></span> <span data-ttu-id="69a91-142">/xyz, /xyz* ou /xyz/* sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="69a91-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Ajouter un panneau Règle basée sur le chemin contenant toutes les informations][2]

<span data-ttu-id="69a91-144">L’ajout d’une règle basée sur le chemin à une passerelle Application Gateway existante est un processus simple via le portail.</span><span class="sxs-lookup"><span data-stu-id="69a91-144">Adding a path-based rule to an existing application gateway is an easy process through the portal.</span></span> <span data-ttu-id="69a91-145">Une fois qu’une règle basée sur le chemin a été créée, elle peut être modifiée pour permettre l’ajout de règles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="69a91-145">After a path-based rule has been created, it can be edited to add additional rules.</span></span> 

![ajouter des règles supplémentaires basés sur le chemin][3]

<span data-ttu-id="69a91-147">Cette étape configure une route basée sur un chemin.</span><span class="sxs-lookup"><span data-stu-id="69a91-147">This step configures a path-based route.</span></span> <span data-ttu-id="69a91-148">Il est important de comprendre que les requêtes ne sont pas réécrites : au fil de l’arrivée des requêtes, la passerelle d’application examine la requête et, en fonction du modèle d’URL, envoie la requête au serveur principal approprié.</span><span class="sxs-lookup"><span data-stu-id="69a91-148">It is important to understand that requests are not rewritten, as requests come in application gateway inspects the request and basic on the url pattern sends the request to the appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69a91-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69a91-149">Next steps</span></span>

<span data-ttu-id="69a91-150">Pour découvrir comment configurer le déchargement SSL avec la passerelle Azure Application Gateway, consultez la [configuration du déchargement SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="69a91-150">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
