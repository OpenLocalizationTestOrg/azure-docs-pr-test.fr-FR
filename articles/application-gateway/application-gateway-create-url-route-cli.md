---
title: "aaaCreate une passerelle d’application à l’aide de routage d’URL règles - Azure CLI 2.0 | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure à l’aide des règles de routage d’URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="2a414-103">Créer une passerelle d’application à l’aide du routage basé sur le chemin avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2a414-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a414-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="2a414-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="2a414-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2a414-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="2a414-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2a414-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="2a414-107">Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous selon le chemin d’URL de hello d’une requête Http.</span><span class="sxs-lookup"><span data-stu-id="2a414-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="2a414-108">Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour hello les URL présentée dans hello passerelle d’Application et envoie toohello de trafic réseau hello défini par pool de back-end.</span><span class="sxs-lookup"><span data-stu-id="2a414-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="2a414-109">Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.</span><span class="sxs-lookup"><span data-stu-id="2a414-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="2a414-110">Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle.</span><span class="sxs-lookup"><span data-stu-id="2a414-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="2a414-111">La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="2a414-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="2a414-112">Type de règle de base fournit des service tourniquet pour les principaux hello pools lors PathBasedRouting en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte tout en appuyant sur le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="2a414-113">Scénario</span><span class="sxs-lookup"><span data-stu-id="2a414-113">Scenario</span></span>

<span data-ttu-id="2a414-114">Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com avec deux pools de serveur principal : un pool de serveurs par défaut et un pool de serveurs d’image.</span><span class="sxs-lookup"><span data-stu-id="2a414-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="2a414-115">Demandes de http://contoso.com/image * sont routés de pool de serveurs tooimage (imagesBackendPool), si hello modèle du chemin d’accès ne correspond pas, un pool de serveurs par défaut (appGatewayBackendPool) est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="2a414-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![itinéraire d’URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="2a414-117">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="2a414-117">Log in tooAzure</span></span>

<span data-ttu-id="2a414-118">Ouvrez hello **invite de commandes Microsoft Azure**et les journaux.</span><span class="sxs-lookup"><span data-stu-id="2a414-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="2a414-119">Vous pouvez également utiliser `az login` sans commutateur hello pour la connexion de périphérique qui requiert la saisie d’un code à aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="2a414-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="2a414-120">Une fois que vous tapez hello précédent exemple, un code est fourni.</span><span class="sxs-lookup"><span data-stu-id="2a414-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="2a414-121">Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Invite de commande affichant le code de l’appareil][1]

<span data-ttu-id="2a414-123">Dans le navigateur de hello, entrez le code hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="2a414-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="2a414-124">Vous êtes redirigé tooa-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="2a414-124">You are redirected tooa sign-in page.</span></span>

![code de tooenter du navigateur][2]

<span data-ttu-id="2a414-126">Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Connexion réussie][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="2a414-128">Ajouter une passerelle d’application existant du tooan une règle basée sur le chemin d’accès</span><span class="sxs-lookup"><span data-stu-id="2a414-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="2a414-129">Créer une passerelle d’application avec une règle de chemin personnalisée</span><span class="sxs-lookup"><span data-stu-id="2a414-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="2a414-130">Créer un pool principal</span><span class="sxs-lookup"><span data-stu-id="2a414-130">Create a new back-end pool</span></span>

<span data-ttu-id="2a414-131">Configurer le paramètre de passerelle d’application **imagesBackendPool** hello équilibrés en charge le trafic réseau dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="2a414-132">Dans cet exemple, vous configurez les paramètres de pool principal différent pour le nouveau pool de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="2a414-133">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="2a414-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="2a414-134">Paramètres HTTP du serveur principal sont utilisées par les règles tooroute trafic toohello les membres du pool principal approprié.</span><span class="sxs-lookup"><span data-stu-id="2a414-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="2a414-135">Ce paramètre détermine le protocole de hello et port qui est utilisé lors de l’envoi de trafic toohello les membres du pool principal.</span><span class="sxs-lookup"><span data-stu-id="2a414-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="2a414-136">Sessions basées sur un cookie sont également déterminées par les paramètres HTTP hello principal.</span><span class="sxs-lookup"><span data-stu-id="2a414-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="2a414-137">S’il est activé, l’affinité de basé sur cookie de session envoie le trafic toohello même principal en tant que requêtes précédentes pour chaque paquet.</span><span class="sxs-lookup"><span data-stu-id="2a414-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="2a414-138">Créer un port frontal</span><span class="sxs-lookup"><span data-stu-id="2a414-138">Create a new front-end port</span></span>

<span data-ttu-id="2a414-139">Configurer le port frontal de hello pour une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="2a414-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="2a414-140">objet de configuration du port frontal Hello est utilisé par un toodefine écoute le port d’écoute de passerelle d’Application hello pour le trafic sur le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="2a414-141">Créer un écouteur</span><span class="sxs-lookup"><span data-stu-id="2a414-141">Create a new listener</span></span>

<span data-ttu-id="2a414-142">Configurer un écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-142">Configure hello listener.</span></span> <span data-ttu-id="2a414-143">Cette étape configure l’écouteur hello pour l’adresse IP publique de hello et le port utilisé tooreceive du trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="2a414-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="2a414-144">Hello, l’exemple suivant prend une configuration IP frontale de hello précédemment configuré, la configuration de port frontal et un protocole (http ou https) et configure l’écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="2a414-145">Dans cet exemple, port d’écoute hello écoute tooHTTP du trafic sur le port 82 hello adresse IP publique qui a été créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="2a414-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="2a414-146">Créer le mappage de chemin d’accès d’Url hello</span><span class="sxs-lookup"><span data-stu-id="2a414-146">Create hello Url path map</span></span>

<span data-ttu-id="2a414-147">Configurer les chemins d’accès de la règle URL pour les pools principaux hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="2a414-148">Cette étape configure le chemin d’accès relatif hello utilisé par la passerelle toodefine hello mappage entre le chemin d’accès de l’URL et le pool principal reçoit le trafic entrant de toohandle hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2a414-149">Chaque chemin d’accès doit commencer par / et hello uniquement une «\*» est autorisé, à la fin de hello.</span><span class="sxs-lookup"><span data-stu-id="2a414-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="2a414-150">/xyz, /xyz* ou /xyz/* sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="2a414-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="2a414-151">Hello chaîne fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord « ? » ou « # » et ces caractères ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="2a414-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="2a414-152">Hello exemple suivant crée une règle pour « / images / * « chemin d’accès de routage du trafic tooback-end « imagesBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="2a414-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="2a414-153">Cette règle garantit que le trafic pour chaque jeu d’URL est routé toohello principal.</span><span class="sxs-lookup"><span data-stu-id="2a414-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="2a414-154">Par exemple, http://adatum.com/images/figure1.jpg devient trop « imagesBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="2a414-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="2a414-155">Si le chemin d’accès hello ne correspond pas à une des règles de chemin d’accès prédéterminé hello, configuration de mappage de chemin d’accès de règle hello configure également un pool d’adresses principal par défaut.</span><span class="sxs-lookup"><span data-stu-id="2a414-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="2a414-156">Par exemple, http://adatum.com/shoppingcart/test.html devient toopool1 telle qu’elle est définie en tant que pool par défaut de hello pour le trafic non apparié.</span><span class="sxs-lookup"><span data-stu-id="2a414-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="2a414-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2a414-157">Next steps</span></span>

<span data-ttu-id="2a414-158">Si vous souhaitez toolearn sur le déchargement de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2a414-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
