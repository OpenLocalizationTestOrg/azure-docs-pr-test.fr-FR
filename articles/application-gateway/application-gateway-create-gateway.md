---
title: "aaaCreate, de démarrer ou de supprimer une passerelle d’application | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="643c9-103">Création, démarrage ou suppression d’une passerelle Application Gateway avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="643c9-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [<span data-ttu-id="643c9-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="643c9-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="643c9-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="643c9-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="643c9-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="643c9-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="643c9-107">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="643c9-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="643c9-108">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="643c9-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="643c9-109">La passerelle Azure Application Gateway est un équilibreur de charge de couche 7.</span><span class="sxs-lookup"><span data-stu-id="643c9-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="643c9-110">Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement.</span><span class="sxs-lookup"><span data-stu-id="643c9-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="643c9-111">Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc.</span><span class="sxs-lookup"><span data-stu-id="643c9-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="643c9-112">toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle Application](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="643c9-112">toofind a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="643c9-113">Cet article vous guide tout au long des hello étapes toocreate, configurer, démarrer et supprimer une passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="643c9-113">This article walks you through hello steps toocreate, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="643c9-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="643c9-114">Before you begin</span></span>

1. <span data-ttu-id="643c9-115">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="643c9-115">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="643c9-116">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="643c9-116">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="643c9-117">Si vous avez un réseau virtuel existant, sélectionnez un sous-réseau vide existant ou créer un sous-réseau dans votre réseau virtuel existant uniquement pour une utilisation par la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by hello application gateway.</span></span> <span data-ttu-id="643c9-118">Vous ne pouvez pas déployer hello application passerelle tooa autre réseau virtuel que les ressources hello vous avez l’intention toodeploy derrière la passerelle d’application hello, sauf si le réseau virtuel d’homologation est utilisé.</span><span class="sxs-lookup"><span data-stu-id="643c9-118">You cannot deploy hello application gateway tooa different virtual network than hello resources you intend toodeploy behind hello application gateway unless vnet peering is used.</span></span> <span data-ttu-id="643c9-119">toolearn visitez plus [d’homologation de réseau virtuel](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="643c9-119">toolearn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="643c9-120">Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.</span><span class="sxs-lookup"><span data-stu-id="643c9-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="643c9-121">Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-121">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="643c9-122">passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="643c9-122">hello application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="643c9-123">serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.</span><span class="sxs-lookup"><span data-stu-id="643c9-123">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-toocreate-an-application-gateway"></a><span data-ttu-id="643c9-124">Qu’est requis toocreate une passerelle d’application ?</span><span class="sxs-lookup"><span data-stu-id="643c9-124">What is required toocreate an application gateway?</span></span>

<span data-ttu-id="643c9-125">Lorsque vous utilisez hello `New-AzureApplicationGateway` passerelle d’application hello commande toocreate, aucune configuration n’est définie à ce stade et ressources de hello nouvellement créé sont configurés à l’aide de XML ou un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-125">When you use hello `New-AzureApplicationGateway` command toocreate hello application gateway, no configuration is set at this point and hello newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="643c9-126">les valeurs Hello sont :</span><span class="sxs-lookup"><span data-stu-id="643c9-126">hello values are:</span></span>

* <span data-ttu-id="643c9-127">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-127">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="643c9-128">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="643c9-128">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="643c9-129">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="643c9-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="643c9-130">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-130">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="643c9-131">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-131">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="643c9-132">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="643c9-132">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="643c9-133">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="643c9-133">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="643c9-134">**La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="643c9-134">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="643c9-135">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="643c9-135">Create an application gateway</span></span>

<span data-ttu-id="643c9-136">toocreate une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="643c9-136">toocreate an application gateway:</span></span>

1. <span data-ttu-id="643c9-137">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="643c9-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="643c9-138">Créez un fichier XML de configuration ou un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="643c9-139">Valider hello toohello de configuration qui vient d’être créé ressource passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="643c9-139">Commit hello configuration toohello newly created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="643c9-140">Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="643c9-140">If you need tooconfigure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md).</span></span> <span data-ttu-id="643c9-141">Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="643c9-141">Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.</span></span>

![Exemple de scénario][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="643c9-143">Créer une ressource de passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="643c9-143">Create an application gateway resource</span></span>

<span data-ttu-id="643c9-144">passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="643c9-144">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="643c9-145">La facturation pour la passerelle de hello ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="643c9-145">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="643c9-146">La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="643c9-146">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="643c9-147">Hello exemple suivant crée une passerelle d’application à l’aide d’un réseau virtuel appelé « testvnet1 » et un sous-réseau nommé « sous-réseau-1 » :</span><span class="sxs-lookup"><span data-stu-id="643c9-147">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="643c9-148">*Description*, *InstanceCount* et *GatewaySize* sont des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="643c9-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="643c9-149">toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-149">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> <span data-ttu-id="643c9-150">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="643c9-150">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="643c9-151">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="643c9-151">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="643c9-152">Vous pouvez choisir Small, Medium ou Large.</span><span class="sxs-lookup"><span data-stu-id="643c9-152">You can choose between Small, Medium and Large.</span></span>

<span data-ttu-id="643c9-153">*Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="643c9-153">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="643c9-154">Ceux-ci sont créés une fois la passerelle de hello en hello état en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="643c9-154">These are created once hello gateway is in hello running state.</span></span>

## <a name="configure-hello-application-gateway"></a><span data-ttu-id="643c9-155">Configurer la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="643c9-155">Configure hello application gateway</span></span>

<span data-ttu-id="643c9-156">Vous pouvez configurer la passerelle d’application hello à l’aide de XML ou un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-156">You can configure hello application gateway by using XML or a configuration object.</span></span>

### <a name="configure-hello-application-gateway-by-using-xml"></a><span data-ttu-id="643c9-157">Configurer la passerelle d’application hello à l’aide de XML</span><span class="sxs-lookup"><span data-stu-id="643c9-157">Configure hello application gateway by using XML</span></span>

<span data-ttu-id="643c9-158">Bonjour l’exemple suivant, un tooconfigure de fichier XML tous les paramètres de passerelle d’application et de les valider toohello ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="643c9-158">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="643c9-159">Étape 1</span><span class="sxs-lookup"><span data-stu-id="643c9-159">Step 1</span></span>

<span data-ttu-id="643c9-160">Copiez hello suivant tooNotepad de texte.</span><span class="sxs-lookup"><span data-stu-id="643c9-160">Copy hello following text tooNotepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="643c9-161">Modifier les valeurs hello entre parenthèses hello pour les éléments de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-161">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="643c9-162">Hello enregistrez-le avec l’extension .xml.</span><span class="sxs-lookup"><span data-stu-id="643c9-162">Save hello file with extension .xml.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="643c9-163">l’élément Hello protocole Http ou Https est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="643c9-163">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="643c9-164">Bonjour à l’exemple suivant montre comment toouse une configuration de fichier tooset de passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-164">hello following example shows how toouse a configuration file tooset up hello application gateway.</span></span> <span data-ttu-id="643c9-165">charge d’exemple Hello équilibre le trafic HTTP sur le port public 80 et envoie le trafic réseau tooback-end port80 entre deux adresses IP.</span><span class="sxs-lookup"><span data-stu-id="643c9-165">hello example load balances HTTP traffic on public port 80 and sends network traffic tooback-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

#### <a name="step-2"></a><span data-ttu-id="643c9-166">Étape 2</span><span class="sxs-lookup"><span data-stu-id="643c9-166">Step 2</span></span>

<span data-ttu-id="643c9-167">Définissez ensuite la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-167">Next, set hello application gateway.</span></span> <span data-ttu-id="643c9-168">Hello d’utilisation `Set-AzureApplicationGatewayConfig` applet de commande avec un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-168">Use hello `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="643c9-169">Configurer la passerelle d’application hello à l’aide d’un objet de configuration</span><span class="sxs-lookup"><span data-stu-id="643c9-169">Configure hello application gateway by using a configuration object</span></span>

<span data-ttu-id="643c9-170">Bonjour à l’exemple suivant montre comment tooconfigure hello passerelle d’application à l’aide d’objets de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-170">hello following example shows how tooconfigure hello application gateway by using configuration objects.</span></span> <span data-ttu-id="643c9-171">Tous les éléments de configuration doivent être configurées individuellement et ensuite ajoutés objet de configuration de passerelle tooan application.</span><span class="sxs-lookup"><span data-stu-id="643c9-171">All configuration items must be configured individually and then added tooan application gateway configuration object.</span></span> <span data-ttu-id="643c9-172">Après avoir créé un objet de configuration hello, vous utilisez hello `Set-AzureApplicationGateway` commande toocommit hello configuration toohello créé précédemment des ressources de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="643c9-172">After creating hello configuration object, you use hello `Set-AzureApplicationGateway` command toocommit hello configuration toohello previously created application gateway resource.</span></span>

> [!NOTE]
> <span data-ttu-id="643c9-173">Avant d’attribuer un objet de configuration de tooeach de valeur, vous devez toodeclare le type d’objet PowerShell utilise pour le stockage.</span><span class="sxs-lookup"><span data-stu-id="643c9-173">Before assigning a value tooeach configuration object, you need toodeclare what kind of object PowerShell uses for storage.</span></span> <span data-ttu-id="643c9-174">éléments individuels de Hello première ligne toocreate hello définit ce que `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` sont utilisés.</span><span class="sxs-lookup"><span data-stu-id="643c9-174">hello first line toocreate hello individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.</span></span>

#### <a name="step-1"></a><span data-ttu-id="643c9-175">Étape 1</span><span class="sxs-lookup"><span data-stu-id="643c9-175">Step 1</span></span>

<span data-ttu-id="643c9-176">Créez tous les éléments de configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-176">Create all individual configuration items.</span></span>

<span data-ttu-id="643c9-177">Créer un IP frontale de hello comme Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="643c9-177">Create hello front-end IP as shown in hello following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="643c9-178">Créer un port frontal de hello comme Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="643c9-178">Create hello front-end port as shown in hello following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="643c9-179">Créer un pool de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-179">Create hello back-end server pool.</span></span>

<span data-ttu-id="643c9-180">Définir les adresses IP hello ajoutés toohello pool de serveur principal comme indiqué dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-180">Define hello IP addresses that are added toohello back-end server pool as shown in hello next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="643c9-181">Utilisez hello $server tooadd hello valeurs toohello principal pool d’objet ($pool).</span><span class="sxs-lookup"><span data-stu-id="643c9-181">Use hello $server object tooadd hello values toohello back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="643c9-182">Créer un paramètre de pool hello serveur principal.</span><span class="sxs-lookup"><span data-stu-id="643c9-182">Create hello back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="643c9-183">Créer un écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-183">Create hello listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="643c9-184">Créer la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-184">Create hello rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="643c9-185">Étape 2</span><span class="sxs-lookup"><span data-stu-id="643c9-185">Step 2</span></span>

<span data-ttu-id="643c9-186">Attribuez toutes les configuration individuelle des éléments tooan application passerelle configuration objet ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="643c9-186">Assign all individual configuration items tooan application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="643c9-187">Ajouter hello frontal IP toohello configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-187">Add hello front-end IP toohello configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="643c9-188">Ajouter hello port frontal toohello configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-188">Add hello front-end port toohello configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="643c9-189">Ajouter hello serveur principal pool toohello configuration.</span><span class="sxs-lookup"><span data-stu-id="643c9-189">Add hello back-end server pool toohello configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="643c9-190">Ajoutez toohello configuration de pool de back-end hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-190">Add hello back-end pool setting toohello configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="643c9-191">Ajoutez toohello configuration de l’écouteur hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-191">Add hello listener toohello configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="643c9-192">Ajouter la configuration des règles de toohello hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-192">Add hello rule toohello configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="643c9-193">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="643c9-193">Step 3</span></span>
<span data-ttu-id="643c9-194">Valider les ressources de passerelle d’application toohello hello configuration objets à l’aide de `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="643c9-194">Commit hello configuration object toohello application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a><span data-ttu-id="643c9-195">Démarrer hello passerelle</span><span class="sxs-lookup"><span data-stu-id="643c9-195">Start hello gateway</span></span>

<span data-ttu-id="643c9-196">Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-196">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="643c9-197">Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="643c9-197">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="643c9-198">Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toofinish too15 à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="643c9-198">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="643c9-199">Vérifiez l’état de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="643c9-199">Verify hello gateway status</span></span>

<span data-ttu-id="643c9-200">Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-200">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="643c9-201">Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, *état* doit être en cours d’exécution, et *Vip* et *DnsName* doit avoir des entrées valides.</span><span class="sxs-lookup"><span data-stu-id="643c9-201">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="643c9-202">Hello suivant montre une passerelle d’application qui est en cours d’exécution, vers le haut et le trafic de prêt tootake destinés `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="643c9-202">hello following example shows an application gateway that is up, running, and ready tootake traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a><span data-ttu-id="643c9-203">Suppression de la passerelle d’application hello</span><span class="sxs-lookup"><span data-stu-id="643c9-203">Delete hello application gateway</span></span>

<span data-ttu-id="643c9-204">passerelle d’application toodelete hello :</span><span class="sxs-lookup"><span data-stu-id="643c9-204">toodelete hello application gateway:</span></span>

1. <span data-ttu-id="643c9-205">Hello d’utilisation `Stop-AzureApplicationGateway` passerelle de hello toostop applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-205">Use hello `Stop-AzureApplicationGateway` cmdlet toostop hello gateway.</span></span>
2. <span data-ttu-id="643c9-206">Hello d’utilisation `Remove-AzureApplicationGateway` passerelle de hello tooremove applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-206">Use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello gateway.</span></span>
3. <span data-ttu-id="643c9-207">Vérifiez cette passerelle hello a été supprimée à l’aide de hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-207">Verify that hello gateway has been removed by using hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="643c9-208">exemple Hello présente hello `Stop-AzureApplicationGateway` applet de commande sur la première ligne de hello, suivie des hello.</span><span class="sxs-lookup"><span data-stu-id="643c9-208">hello following example shows hello `Stop-AzureApplicationGateway` cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="643c9-209">Une fois que la passerelle d’application hello est dans un état arrêté, utilisez hello `Remove-AzureApplicationGateway` service de hello tooremove applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-209">Once hello application gateway is in a stopped state, use hello `Remove-AzureApplicationGateway` cmdlet tooremove hello service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="643c9-210">tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="643c9-210">tooverify that hello service has been removed, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="643c9-211">Cette étape n'est pas requise.</span><span class="sxs-lookup"><span data-stu-id="643c9-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="643c9-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="643c9-212">Next steps</span></span>

<span data-ttu-id="643c9-213">Si vous souhaitez tooconfigure le déchargement SSL, consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="643c9-213">If you want tooconfigure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="643c9-214">Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="643c9-214">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="643c9-215">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="643c9-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="643c9-216">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="643c9-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="643c9-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="643c9-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
