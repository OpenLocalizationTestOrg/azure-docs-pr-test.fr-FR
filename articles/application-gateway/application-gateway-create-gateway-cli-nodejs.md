---
title: "aaaCreate une passerelle d’Application Azure - Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment toocreate une passerelle d’Application à l’aide de hello Azure CLI 1.0 dans le Gestionnaire de ressources"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="590ac-103">Créer une passerelle d’application à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="590ac-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="590ac-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="590ac-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="590ac-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="590ac-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="590ac-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="590ac-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="590ac-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="590ac-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="590ac-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="590ac-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="590ac-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="590ac-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="590ac-110">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="590ac-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="590ac-111">Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="590ac-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="590ac-112">Passerelle d’application a hello suivant les fonctionnalités de remise d’applications : charger des sondes de l’intégrité personnalisée équilibrage de charge, l’affinité de basé sur cookie de session et déchargement de Secure Sockets Layer (SSL), HTTP et prise en charge de plusieurs sites.</span><span class="sxs-lookup"><span data-stu-id="590ac-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="590ac-113">Condition préalable : Installez hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="590ac-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="590ac-114">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](../xplat-cli-install.md) et que vous devez trop[session tooAzure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="590ac-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="590ac-115">Si vous n’avez pas de compte Azure, vous devez vous en procurer un.</span><span class="sxs-lookup"><span data-stu-id="590ac-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="590ac-116">Inscrivez-vous à un [essai gratuit ici](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="590ac-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="590ac-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="590ac-117">Scenario</span></span>

<span data-ttu-id="590ac-118">Dans ce scénario, vous découvrez comment une passerelle d’application à l’aide de toocreate hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="590ac-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="590ac-119">Ce scénario va :</span><span class="sxs-lookup"><span data-stu-id="590ac-119">This scenario will:</span></span>

* <span data-ttu-id="590ac-120">Créer une passerelle Application Gateway moyenne avec deux instances.</span><span class="sxs-lookup"><span data-stu-id="590ac-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="590ac-121">Créer un réseau virtuel nommé ContosoVNET avec un bloc CIDR réservé de 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="590ac-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="590ac-122">Créer un sous-réseau appelé subnet01 qui utilise 10.0.0.0/28 comme bloc CIDR.</span><span class="sxs-lookup"><span data-stu-id="590ac-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="590ac-123">Les tests de configuration supplémentaires de la passerelle d’application hello, y compris l’intégrité personnalisée, les adresses du pool principal et des règles supplémentaires sont configurés après la configuration de la passerelle d’application hello et non pendant le déploiement initial.</span><span class="sxs-lookup"><span data-stu-id="590ac-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="590ac-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="590ac-124">Before you begin</span></span>

<span data-ttu-id="590ac-125">La passerelle Application Gateway Azure requiert son propre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="590ac-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="590ac-126">Lorsque vous créez un réseau virtuel, assurez-vous que vous laissez suffisamment toohave d’espace adresse plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="590ac-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="590ac-127">Une fois que vous déployez un tooa de sous-réseau de la passerelle d’application, passerelles d’application supplémentaires seulement sont en mesure de toobe ajouté toohello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="590ac-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="590ac-128">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="590ac-128">Log in tooAzure</span></span>

<span data-ttu-id="590ac-129">Ouvrez hello **invite de commandes Microsoft Azure**et les journaux.</span><span class="sxs-lookup"><span data-stu-id="590ac-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="590ac-130">Une fois que vous tapez hello précédent exemple, un code est fourni.</span><span class="sxs-lookup"><span data-stu-id="590ac-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="590ac-131">Accédez toohttps://aka.ms/devicelogin dans un processus de connexion de navigateur toocontinue hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![Invite de commande affichant le code de l’appareil][1]

<span data-ttu-id="590ac-133">Dans le navigateur de hello, entrez le code hello que vous avez reçu.</span><span class="sxs-lookup"><span data-stu-id="590ac-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="590ac-134">Vous êtes redirigé tooa-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="590ac-134">You are redirected tooa sign-in page.</span></span>

![code de tooenter du navigateur][2]

<span data-ttu-id="590ac-136">Une fois que le code de hello a été entré. vous êtes connecté, fermer hello navigateur toocontinue avec le scénario hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![Connexion réussie][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="590ac-138">Commutateur tooResource Manager Mode</span><span class="sxs-lookup"><span data-stu-id="590ac-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="590ac-139">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="590ac-139">Create hello resource group</span></span>

<span data-ttu-id="590ac-140">Avant de créer la passerelle d’application hello, un groupe de ressources est créé de passerelle d’application toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="590ac-141">Hello Voici commande hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="590ac-142">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="590ac-142">Create a virtual network</span></span>

<span data-ttu-id="590ac-143">Une fois le groupe de ressources hello est créé, un réseau virtuel est créé pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="590ac-144">Bonjour l’exemple suivant, l’espace d’adressage hello a été en tant que 10.0.0.0/16 tel que défini dans hello précédant les notes de scénario.</span><span class="sxs-lookup"><span data-stu-id="590ac-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="590ac-145">Créer un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="590ac-145">Create a subnet</span></span>

<span data-ttu-id="590ac-146">Après la création du réseau virtuel hello, un sous-réseau est ajouté pour la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="590ac-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="590ac-147">Si vous envisagez de passerelle d’application toouse avec une application web hébergée Bonjour même virtuel réseau en tant que passerelle d’application hello, tooleave que suffisamment de place pour un autre sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="590ac-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="590ac-148">Créer une passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="590ac-148">Create hello application gateway</span></span>

<span data-ttu-id="590ac-149">Une fois que le sous-réseau et le réseau virtuel de hello sont créés, les conditions préalables pour la passerelle d’application hello hello sont terminées.</span><span class="sxs-lookup"><span data-stu-id="590ac-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="590ac-150">En outre un fichier .pfx exporté précédemment hello et certificat de mot de passe hello certificat sont requis pour hello suivant l’étape : hello IP adresses utilisées pour hello principal sont hello pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="590ac-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="590ac-151">Ces valeurs peuvent être des deux adresses IP privées dans le réseau virtuel de hello, des adresses IP publiques ou des noms de domaine complet pour vos serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="590ac-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> <span data-ttu-id="590ac-152">Pour obtenir la liste de paramètres qui peuvent être fournies lors de la création de l’exécuter hello de commande suivante : **créer de la passerelle d’application réseau azure--aide**.</span><span class="sxs-lookup"><span data-stu-id="590ac-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="590ac-153">Cet exemple crée une passerelle d’application de base avec les paramètres par défaut pour l’écouteur de hello, pool principal, paramètres http du serveur principal et les règles.</span><span class="sxs-lookup"><span data-stu-id="590ac-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="590ac-154">Vous pouvez modifier ces paramètres toosuit votre déploiement une fois l’approvisionnement de hello réussie.</span><span class="sxs-lookup"><span data-stu-id="590ac-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="590ac-155">Si vous avez déjà votre application web définie avec le pool principal d’hello Bonjour précédentes étapes, une fois créés, l’équilibrage de charge démarre.</span><span class="sxs-lookup"><span data-stu-id="590ac-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="590ac-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="590ac-156">Next steps</span></span>

<span data-ttu-id="590ac-157">Découvrez comment des sondes toocreate d’état personnalisé en vous rendant sur [créer une sonde d’intégrité personnalisé](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="590ac-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="590ac-158">Découvrez comment tooconfigure déchargement SSL et le déchiffrement SSL coûteux take hello désactivé vos serveurs web en vous rendant sur [configurer le déchargement SSL](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="590ac-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
