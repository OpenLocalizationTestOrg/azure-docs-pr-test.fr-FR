---
title: "aaaCreate basée sur un chemin d’accès de règle - passerelle d’Application Azure - Azure Portal | Documents Microsoft"
description: "Découvrez comment toocreate une règle basée sur le chemin d’accès pour une passerelle d’application à l’aide de hello portail"
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
ms.openlocfilehash: 21cb52c426ca5f7dfedf07a96e87fbc85d243647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-path-based-rule-for-an-application-gateway-by-using-hello-portal"></a><span data-ttu-id="116ed-103">Créer une règle basée sur le chemin d’accès pour une passerelle d’application à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="116ed-103">Create a Path-based rule for an application gateway by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="116ed-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="116ed-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="116ed-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="116ed-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="116ed-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="116ed-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="116ed-107">Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous basés sur le chemin de l’URL de demande Http hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-107">URL Path-based routing enables you tooassociate routes based on hello URL path of Http request.</span></span> <span data-ttu-id="116ed-108">Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour les URL hello répertorié dans hello passerelle d’Application et envoie toohello de trafic réseau hello défini par pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="116ed-108">It checks if there is a route tooa back-end pool configured for hello URL listed in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="116ed-109">Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.</span><span class="sxs-lookup"><span data-stu-id="116ed-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="116ed-110">Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle.</span><span class="sxs-lookup"><span data-stu-id="116ed-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="116ed-111">La passerelle d’application a deux types de règles : des règles de base et des règles basées sur un chemin.</span><span class="sxs-lookup"><span data-stu-id="116ed-111">Application gateway has two rule types: basic and path-based rules.</span></span> <span data-ttu-id="116ed-112">Hello du type de règle de base, fournit service tourniquet pour les principaux hello pools lors de règles basées sur le chemin d’accès en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte tout en appuyant sur le pool principal approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-112">hello basic rule type, provides round-robin service for hello back-end pools while path-based rules in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello appropriate backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="116ed-113">Scénario</span><span class="sxs-lookup"><span data-stu-id="116ed-113">Scenario</span></span>

<span data-ttu-id="116ed-114">Hello scénario suivant passe par la création d’une règle basée sur le chemin d’accès dans une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="116ed-114">hello following scenario goes through creating a Path-based rule in an existing application gateway.</span></span>
<span data-ttu-id="116ed-115">Hello scénario part du principe que vous avez déjà suivi les étapes de hello trop[créer une passerelle d’Application](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="116ed-115">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

![itinéraire d’URL][scenario]

## <span data-ttu-id="116ed-117"><a name="createrule"></a>Créer une règle basée sur le chemin d’accès hello</span><span class="sxs-lookup"><span data-stu-id="116ed-117"><a name="createrule"></a>Create hello Path-based rule</span></span>

<span data-ttu-id="116ed-118">Une règle basée sur le chemin d’accès requiert son propre port d’écoute, avant de créer la règle de hello être tooverify que vous avez un toouse écouteur disponible.</span><span class="sxs-lookup"><span data-stu-id="116ed-118">A Path-based rule requires its own listener, before creating hello rule be sure tooverify you have an available listener toouse.</span></span>

### <a name="step-1"></a><span data-ttu-id="116ed-119">Étape 1</span><span class="sxs-lookup"><span data-stu-id="116ed-119">Step 1</span></span>

<span data-ttu-id="116ed-120">Accédez toohello [portail Azure](http://portal.azure.com) et sélectionnez une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="116ed-120">Navigate toohello [Azure portal](http://portal.azure.com) and select an existing application gateway.</span></span> <span data-ttu-id="116ed-121">Cliquer sur **Règles**</span><span class="sxs-lookup"><span data-stu-id="116ed-121">Click **Rules**</span></span>

![Vue d’ensemble d’Application Gateway][1]

### <a name="step-2"></a><span data-ttu-id="116ed-123">Étape 2</span><span class="sxs-lookup"><span data-stu-id="116ed-123">Step 2</span></span>

<span data-ttu-id="116ed-124">Cliquez sur **basée sur le chemin d’accès** bouton tooadd une règle basée sur le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="116ed-124">Click **Path-based** button tooadd a new Path-based rule.</span></span>

### <a name="step-3"></a><span data-ttu-id="116ed-125">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="116ed-125">Step 3</span></span>

<span data-ttu-id="116ed-126">Hello **ajouter une règle basée sur le chemin d’accès** panneau a deux sections.</span><span class="sxs-lookup"><span data-stu-id="116ed-126">hello **Add path-based rule** blade has two sections.</span></span> <span data-ttu-id="116ed-127">première section de Hello est où vous avez défini l’écouteur de hello, nom hello de règle de hello et les paramètres de chemin d’accès par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-127">hello first section is where you defined hello listener, hello name of hello rule and hello default path settings.</span></span> <span data-ttu-id="116ed-128">paramètres de chemin d’accès par défaut Hello sont pour les itinéraires qui ne relèvent pas de l’itinéraire de basée sur le chemin d’accès personnalisées hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-128">hello default path settings are for routes that do not fall under hello custom path-based route.</span></span> <span data-ttu-id="116ed-129">Hello deuxième section Hello **ajouter une règle basée sur le chemin d’accès** lame est où vous définissez les règles de chemin d’accès hello eux-mêmes.</span><span class="sxs-lookup"><span data-stu-id="116ed-129">hello second section of hello **Add path-based rule** blade is where you define hello path-based rules themselves.</span></span>

<span data-ttu-id="116ed-130">**Paramètres de base**</span><span class="sxs-lookup"><span data-stu-id="116ed-130">**Basic Settings**</span></span>

* <span data-ttu-id="116ed-131">**Nom** -cette valeur est une règle de toohello nom convivial qui est accessible dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-131">**Name** - This value is a friendly name toohello rule that is accessible in hello portal.</span></span>
* <span data-ttu-id="116ed-132">**Écouteur** -cette valeur est le port d’écoute hello est utilisé pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-132">**Listener** - This value is hello listener that is used for hello rule.</span></span>
* <span data-ttu-id="116ed-133">**Par défaut du pool principal** -ce paramètre est le paramètre hello qui définit hello principal toobe est utilisé pour la règle par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="116ed-133">**Default backend pool** - This setting is hello setting that defines hello back-end toobe used for hello default rule</span></span>
* <span data-ttu-id="116ed-134">**Paramètres HTTP par défaut** -ce paramètre est le paramètre hello qui définit toobe de paramètres hello HTTP utilisé pour la règle par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-134">**Default HTTP settings** - This setting is hello setting that defines hello HTTP settings toobe used for hello default rule.</span></span>

<span data-ttu-id="116ed-135">**Path-based rules (Règles basées sur le chemin)**</span><span class="sxs-lookup"><span data-stu-id="116ed-135">**Path-based rules**</span></span>

* <span data-ttu-id="116ed-136">**Nom** -cette valeur est une règle nom toopath convivial.</span><span class="sxs-lookup"><span data-stu-id="116ed-136">**Name** - This value is a friendly name toopath-based rule.</span></span>
* <span data-ttu-id="116ed-137">**Chemins d’accès** -ce paramètre définit hello chemin hello règle recherche lors de la transmission du trafic</span><span class="sxs-lookup"><span data-stu-id="116ed-137">**Paths** - This setting defines hello path hello rule looks for when forwarding traffic</span></span>
* <span data-ttu-id="116ed-138">**Pool principal** -ce paramètre est le paramètre hello qui définit hello principal toobe est utilisé pour la règle de hello</span><span class="sxs-lookup"><span data-stu-id="116ed-138">**Backend Pool** - This setting is hello setting that defines hello back-end toobe used for hello rule</span></span>
* <span data-ttu-id="116ed-139">**Paramètre HTTP** -ce paramètre est le paramètre hello qui définit toobe de paramètres hello HTTP utilisé pour la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-139">**HTTP setting** - This setting is hello setting that defines hello HTTP settings toobe used for hello rule.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="116ed-140">Chemins d’accès : liste hello de toomatch de modèles de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="116ed-140">Paths: hello list of path patterns toomatch.</span></span> <span data-ttu-id="116ed-141">Chacun doit commencer par / et hello uniquement une «\*» est autorisé à hello fin.</span><span class="sxs-lookup"><span data-stu-id="116ed-141">Each must start with / and hello only place a "\*" is allowed is at hello end.</span></span> <span data-ttu-id="116ed-142">/xyz, /xyz* ou /xyz/* sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="116ed-142">Valid examples are /xyz, /xyz* or /xyz/*.</span></span>  

![Ajouter un panneau Règle basée sur le chemin contenant toutes les informations][2]

<span data-ttu-id="116ed-144">Ajout d’une règle basée sur le chemin d’accès de tooan passerelle d’application existant est un processus simple via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="116ed-144">Adding a path-based rule tooan existing application gateway is an easy process through hello portal.</span></span> <span data-ttu-id="116ed-145">Après avoir créé une règle basée sur le chemin d’accès, il peut être modifié tooadd des règles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="116ed-145">After a path-based rule has been created, it can be edited tooadd additional rules.</span></span> 

![ajouter des règles supplémentaires basés sur le chemin][3]

<span data-ttu-id="116ed-147">Cette étape configure une route basée sur un chemin.</span><span class="sxs-lookup"><span data-stu-id="116ed-147">This step configures a path-based route.</span></span> <span data-ttu-id="116ed-148">Il toounderstand important que les demandes ne sont pas réécrit, comme les demandes proviennent de la passerelle d’application inspecte la demande de hello et basic en hello url modèle envoie hello demande toohello approprié back-end.</span><span class="sxs-lookup"><span data-stu-id="116ed-148">It is important toounderstand that requests are not rewritten, as requests come in application gateway inspects hello request and basic on hello url pattern sends hello request toohello appropriate back-end.</span></span>

## <a name="next-steps"></a><span data-ttu-id="116ed-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="116ed-149">Next steps</span></span>

<span data-ttu-id="116ed-150">toolearn tooconfigure le déchargement SSL avec la passerelle d’Application Azure, voir [configurer le déchargement SSL](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="116ed-150">toolearn how tooconfigure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>

[1]: ./media/application-gateway-create-url-route-portal/figure1.png
[2]: ./media/application-gateway-create-url-route-portal/figure2.png
[3]: ./media/application-gateway-create-url-route-portal/figure3.png
[scenario]: ./media/application-gateway-create-url-route-portal/scenario.png
