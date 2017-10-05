---
title: "Créer une passerelle d’application avec des règles de routage d’URL -Azure CLI 2.0 | Microsoft Docs"
description: "Cette page fournit des instructions pour créer et configurer une passerelle Application Gateway Azure avec les règles de routage d’URL"
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
ms.openlocfilehash: 958049830d6753ec26635f18f8f8b2fabdec0733
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="24bed-103">Créer une passerelle d’application à l’aide du routage basé sur le chemin avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="24bed-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="24bed-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="24bed-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="24bed-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="24bed-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="24bed-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="24bed-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="24bed-107">Le routage basé sur le chemin d’URL vous permet d’associer des routes basées sur le chemin d’URL de la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="24bed-107">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="24bed-108">Il vérifie s’il existe une route vers un pool principal configuré pour les listes d’URL dans la passerelle Application Gateway et envoie le trafic réseau vers le pool principal défini.</span><span class="sxs-lookup"><span data-stu-id="24bed-108">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="24bed-109">Une utilisation courante du routage basé sur l’URL consiste à équilibrer la charge des demandes pour différents types de contenu entre différents pools de serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="24bed-109">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="24bed-110">Le routage basé sur l’URL introduit un nouveau type de règle pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="24bed-110">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="24bed-111">La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="24bed-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="24bed-112">Le type de règle niveau De base de sites Web fournit le service de tourniquet (round robin) pour les pools principaux alors que PathBasedRouting, en plus de la distribution de tourniquet, prend également en compte le modèle de chemin de l’URL de requête lors du choix du pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-112">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="24bed-113">Scénario</span><span class="sxs-lookup"><span data-stu-id="24bed-113">Scenario</span></span>

<span data-ttu-id="24bed-114">Dans l’exemple suivant, la passerelle Application Gateway gère le trafic pour contoso.com avec deux pools de serveurs principaux : un pool de serveurs par défaut et un pool de serveurs d’images.</span><span class="sxs-lookup"><span data-stu-id="24bed-114">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="24bed-115">Les requêtes concernant http://contoso.com/image* sont acheminées vers le pool de serveurs d’images (imagesBackendPool). Si le modèle de chemin d’accès ne correspond pas, un pool de serveurs par défaut (appGatewayBackendPool) est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="24bed-115">Requests for http://contoso.com/image* are routed to image server pool (imagesBackendPool), if the path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![itinéraire d’URL](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="24bed-117">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="24bed-117">Log in to Azure</span></span>

<span data-ttu-id="24bed-118">Ouvrez **l’invite de commandes Microsoft Azure**et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="24bed-118">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="24bed-119">Vous pouvez également utiliser `az login` sans le commutateur destiné à la connexion de l’appareil et qui nécessite la saisie d’un code sur aka.ms/devicelogin.</span><span class="sxs-lookup"><span data-stu-id="24bed-119">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="24bed-120">Une fois que vous avez tapé l’exemple précédent, un code est fourni.</span><span class="sxs-lookup"><span data-stu-id="24bed-120">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="24bed-121">Accédez à https://aka.ms/devicelogin dans un navigateur pour continuer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="24bed-121">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![Invite de commande affichant le code de l’appareil][1]

<span data-ttu-id="24bed-123">Dans le navigateur, entrez le code que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="24bed-123">In the browser, enter the code you received.</span></span> <span data-ttu-id="24bed-124">Vous êtes redirigé vers une page de connexion.</span><span class="sxs-lookup"><span data-stu-id="24bed-124">You are redirected to a sign-in page.</span></span>

![Page de navigateur pour la saisie du code][2]

<span data-ttu-id="24bed-126">Une fois que vous êtes connecté, fermez le navigateur pour poursuivre le scénario.</span><span class="sxs-lookup"><span data-stu-id="24bed-126">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![Connexion réussie][3]

## <a name="add-a-path-based-rule-to-an-existing-application-gateway"></a><span data-ttu-id="24bed-128">Ajouter une règle basée sur le chemin à une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="24bed-128">Add a path-based rule to an existing application gateway</span></span>

<span data-ttu-id="24bed-129">Créer une passerelle d’application avec une règle de chemin personnalisée</span><span class="sxs-lookup"><span data-stu-id="24bed-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="24bed-130">Créer un pool principal</span><span class="sxs-lookup"><span data-stu-id="24bed-130">Create a new back-end pool</span></span>

<span data-ttu-id="24bed-131">Configurez le paramètre de passerelle d’application **imagesBackendPool** pour le trafic à charge équilibrée dans le pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-131">Configure application gateway setting **imagesBackendPool** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="24bed-132">Dans cet exemple, vous configurez différents paramètres pour le nouveau pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-132">In this example, you configure different back-end pool settings for the new back-end pool.</span></span> <span data-ttu-id="24bed-133">Chaque pool principal peut avoir son propre paramètre de pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="24bed-134">Les paramètres HTTP du serveur principal sont utilisés par des règles pour router le trafic vers les membres appropriés du pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-134">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="24bed-135">Ils déterminent le protocole et le port utilisés lors de l’envoi du trafic vers les membres du pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-135">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="24bed-136">Les sessions basées sur les cookies sont également déterminées par les paramètres HTTP du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-136">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="24bed-137">Si elle est activée, l’affinité de session basée sur les cookies envoie le trafic vers le même serveur principal que les requêtes précédentes pour chaque paquet.</span><span class="sxs-lookup"><span data-stu-id="24bed-137">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="24bed-138">Créer un port frontal</span><span class="sxs-lookup"><span data-stu-id="24bed-138">Create a new front-end port</span></span>

<span data-ttu-id="24bed-139">Configurez le port frontal pour une passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="24bed-139">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="24bed-140">L’objet de configuration du port frontal est utilisé par un écouteur pour définir le port écouté par Application Gateway pour connaître le trafic sur l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="24bed-140">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="24bed-141">Créer un écouteur</span><span class="sxs-lookup"><span data-stu-id="24bed-141">Create a new listener</span></span>

<span data-ttu-id="24bed-142">Configurez l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="24bed-142">Configure the listener.</span></span> <span data-ttu-id="24bed-143">Cette étape configure l’écouteur pour l’adresse IP publique et le port utilisé pour recevoir le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="24bed-143">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="24bed-144">L’exemple suivant utilise la configuration de l’adresse IP frontale configurée précédemment, la configuration de port frontal et un protocole (http ou https), et configure l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="24bed-144">The following example takes the previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="24bed-145">Dans cet exemple, l’écouteur écoute le trafic HTTP sur le port 82 sur l’adresse IP publique créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="24bed-145">In this example, the listener listens to HTTP traffic on port 82 on the public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-the-url-path-map"></a><span data-ttu-id="24bed-146">Créer le mappage de chemin d’accès d’URL</span><span class="sxs-lookup"><span data-stu-id="24bed-146">Create the Url path map</span></span>

<span data-ttu-id="24bed-147">Configurez les chemins de règles d’URL pour les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="24bed-147">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="24bed-148">Cette étape configure le chemin relatif utilisé par la passerelle Application Gateway pour définir le mappage entre le chemin d’URL et le pool principal qui est affecté pour gérer le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="24bed-148">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24bed-149">Chaque chemin d’accès doit commencer par le signe / et le seul endroit où un astérisque (\*) est autorisé est à la fin.</span><span class="sxs-lookup"><span data-stu-id="24bed-149">Each path must start with / and the only place a "\*" is allowed, is at the end.</span></span> <span data-ttu-id="24bed-150">/xyz, /xyz ou /xyz/ sont des exemples valides.</span><span class="sxs-lookup"><span data-stu-id="24bed-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="24bed-151">La chaîne transmise à l’outil de correspondance de chemin n’inclut pas de texte après le premier signe ? ou #. De plus, ces caractères ne sont pas autorisés.</span><span class="sxs-lookup"><span data-stu-id="24bed-151">The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="24bed-152">L’exemple suivant crée une règle pour le chemin d’accès « /images/* » acheminant le trafic vers le pool principal « imagesBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="24bed-152">The following example creates one rule for "/images/*" path routing traffic to back-end "imagesBackendPool."</span></span> <span data-ttu-id="24bed-153">Cette règle garantit que le trafic de chaque ensemble d’URL est acheminé vers le pool principal.</span><span class="sxs-lookup"><span data-stu-id="24bed-153">This rule ensures that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="24bed-154">Par exemple, http://adatum.com/images/figure1.jpg accède à « imagesBackendPool ».</span><span class="sxs-lookup"><span data-stu-id="24bed-154">For example, http://adatum.com/images/figure1.jpg goes to "imagesBackendPool."</span></span> <span data-ttu-id="24bed-155">Si le chemin ne correspond à aucune des règles de chemins prédéfinies, la configuration de mappage des chemins de règles configure également un pool d’adresses principal par défaut.</span><span class="sxs-lookup"><span data-stu-id="24bed-155">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="24bed-156">Par exemple, http://adatum.com/shoppingcart/test.html accède à pool1, car il est défini en tant que pool par défaut pour le trafic sans correspondance.</span><span class="sxs-lookup"><span data-stu-id="24bed-156">For example, http://adatum.com/shoppingcart/test.html goes to pool1 as it is defined as the default pool for unmatched traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="24bed-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="24bed-157">Next steps</span></span>

<span data-ttu-id="24bed-158">Pour en savoir plus sur le déchargement SSL (Secure Sockets Layer), consultez [Configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="24bed-158">If you want to learn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
