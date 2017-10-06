---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - PowerShell classique | Documents Microsoft"
description: "Cet article fournit des instructions toocreate déchargement d’une passerelle d’application avec SSL à l’aide de hello modèle de déploiement classique Azure."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 5cb128015747ed4b71802cf751c80b60634601a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-classic-deployment-model"></a><span data-ttu-id="c1943-103">Configurer une passerelle d’application pour le déchargement SSL à l’aide du modèle de déploiement classique de hello</span><span class="sxs-lookup"><span data-stu-id="c1943-103">Configure an application gateway for SSL offload by using hello classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1943-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c1943-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="c1943-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1943-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="c1943-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1943-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="c1943-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c1943-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="c1943-108">Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="c1943-109">Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1943-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c1943-110">Before you begin</span></span>

1. <span data-ttu-id="c1943-111">Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c1943-111">Install hello latest version of hello Azure PowerShell cmdlets by using hello Web Platform Installer.</span></span> <span data-ttu-id="c1943-112">Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c1943-112">You can download and install hello latest version from hello **Windows PowerShell** section of hello [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c1943-113">Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.</span><span class="sxs-lookup"><span data-stu-id="c1943-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="c1943-114">Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-114">Make sure that no virtual machines or cloud deployments are using hello subnet.</span></span> <span data-ttu-id="c1943-115">passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="c1943-115">hello application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="c1943-116">serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.</span><span class="sxs-lookup"><span data-stu-id="c1943-116">hello servers that you configure toouse hello application gateway must exist or have their endpoints created either in hello virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="c1943-117">tooconfigure SSL décharger sur une passerelle d’application, hello dans l’ordre de hello répertoriés comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1943-117">tooconfigure SSL offload on an application gateway, do hello following steps in hello order listed:</span></span>

1. [<span data-ttu-id="c1943-118">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1943-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="c1943-119">Télécharger des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="c1943-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="c1943-120">Configurer la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="c1943-120">Configure hello gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="c1943-121">Jeu de configuration de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="c1943-121">Set hello gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="c1943-122">Démarrer hello passerelle</span><span class="sxs-lookup"><span data-stu-id="c1943-122">Start hello gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="c1943-123">Vérifiez l’état de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="c1943-123">Verify hello gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="c1943-124">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c1943-124">Create an application gateway</span></span>

<span data-ttu-id="c1943-125">passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="c1943-125">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="c1943-126">La facturation pour la passerelle de hello ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="c1943-126">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="c1943-127">La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="c1943-127">Billing begins in a later step, when hello gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="c1943-128">toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c1943-128">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="c1943-129">Dans l’exemple hello, *Description*, *InstanceCount*, et *GatewaySize* sont des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="c1943-129">In hello sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="c1943-130">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="c1943-130">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c1943-131">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="c1943-131">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c1943-132">Les autres valeurs disponibles sont Small et Large.</span><span class="sxs-lookup"><span data-stu-id="c1943-132">Small and Large are other available values.</span></span> <span data-ttu-id="c1943-133">*Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="c1943-133">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="c1943-134">Ces valeurs sont créés une fois la passerelle de hello en hello état en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c1943-134">These values are created once hello gateway is in hello running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="c1943-135">Télécharger des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="c1943-135">Upload SSL certificates</span></span>

<span data-ttu-id="c1943-136">Utilisez `Add-AzureApplicationGatewaySslCertificate` certificat de serveur hello tooupload dans *pfx* passerelle d’application toohello format.</span><span class="sxs-lookup"><span data-stu-id="c1943-136">Use `Add-AzureApplicationGatewaySslCertificate` tooupload hello server certificate in *pfx* format toohello application gateway.</span></span> <span data-ttu-id="c1943-137">nom du certificat Hello est un nom d’utilisateur choisi et doit être unique au sein de la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-137">hello certificate name is a user-chosen name and must be unique within hello application gateway.</span></span> <span data-ttu-id="c1943-138">Ce certificat est tooby auxquels ce nom dans toutes les opérations de gestion de certificat sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-138">This certificate is referred tooby this name in all certificate management operations on hello application gateway.</span></span>

<span data-ttu-id="c1943-139">Cet exemple suivant montre l’applet de commande hello, remplacez les valeurs hello dans l’exemple hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="c1943-139">This following sample shows hello cmdlet, replace hello values in hello sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path toopfx file>
```

<span data-ttu-id="c1943-140">Ensuite, validez chargement du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-140">Next, validate hello certificate upload.</span></span> <span data-ttu-id="c1943-141">Hello d’utilisation `Get-AzureApplicationGatewayCertificate` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c1943-141">Use hello `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="c1943-142">Cet exemple montre l’applet de commande hello sur la première ligne de hello, suivi par la sortie hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-142">This sample shows hello cmdlet on hello first line, followed by hello output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> <span data-ttu-id="c1943-143">mot de passe du certificat Hello a toobe entre 4 too12 caractères, des lettres ou chiffres.</span><span class="sxs-lookup"><span data-stu-id="c1943-143">hello certificate password has toobe between 4 too12 characters, letters, or numbers.</span></span> <span data-ttu-id="c1943-144">Les caractères spéciaux ne sont pas acceptés.</span><span class="sxs-lookup"><span data-stu-id="c1943-144">Special characters are not accepted.</span></span>

## <a name="configure-hello-gateway"></a><span data-ttu-id="c1943-145">Configurer la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="c1943-145">Configure hello gateway</span></span>

<span data-ttu-id="c1943-146">La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="c1943-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="c1943-147">les valeurs Hello peuvent être liées configuration de hello tooconstruct ensemble.</span><span class="sxs-lookup"><span data-stu-id="c1943-147">hello values can be tied together tooconstruct hello configuration.</span></span>

<span data-ttu-id="c1943-148">les valeurs Hello sont :</span><span class="sxs-lookup"><span data-stu-id="c1943-148">hello values are:</span></span>

* <span data-ttu-id="c1943-149">**Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-149">**Back-end server pool:** hello list of IP addresses of hello back-end servers.</span></span> <span data-ttu-id="c1943-150">adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="c1943-150">hello IP addresses listed should either belong toohello virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="c1943-151">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="c1943-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c1943-152">Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-152">These settings are tied tooa pool and are applied tooall servers within hello pool.</span></span>
* <span data-ttu-id="c1943-153">**Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-153">**Front-end port:** This port is hello public port that is opened on hello application gateway.</span></span> <span data-ttu-id="c1943-154">Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="c1943-154">Traffic hits this port, and then gets redirected tooone of hello back-end servers.</span></span>
* <span data-ttu-id="c1943-155">**Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).</span><span class="sxs-lookup"><span data-stu-id="c1943-155">**Listener:** hello listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and hello SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="c1943-156">**La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.</span><span class="sxs-lookup"><span data-stu-id="c1943-156">**Rule:** hello rule binds hello listener and hello back-end server pool and defines which back-end server pool hello traffic should be directed toowhen it hits a particular listener.</span></span> <span data-ttu-id="c1943-157">Actuellement, seuls hello *base* règle est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c1943-157">Currently, only hello *basic* rule is supported.</span></span> <span data-ttu-id="c1943-158">Hello *base* règle est la distribution de la charge de tourniquet.</span><span class="sxs-lookup"><span data-stu-id="c1943-158">hello *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="c1943-159">**Notes de configuration supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="c1943-159">**Additional configuration notes**</span></span>

<span data-ttu-id="c1943-160">Pour configurer des certificats SSL, hello protocole dans **HttpListener** doit également modifier*Https* (sensible à la casse).</span><span class="sxs-lookup"><span data-stu-id="c1943-160">For SSL certificates configuration, hello protocol in **HttpListener** should change too*Https* (case sensitive).</span></span> <span data-ttu-id="c1943-161">Hello **SslCert** l’élément est ajouté trop**HttpListener** avec hello valeur toohello même nom que celui de téléchargement hello de la précédente section de certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="c1943-161">hello **SslCert** element is added too**HttpListener** with hello value set toohello same name as used in hello upload of preceding SSL certificates section.</span></span> <span data-ttu-id="c1943-162">le port frontal Hello doit être too443 mis à jour.</span><span class="sxs-lookup"><span data-stu-id="c1943-162">hello front-end port should be updated too443.</span></span>

<span data-ttu-id="c1943-163">**affinité basé sur cookie de tooenable**: une passerelle d’application peut être configurée tooensure qu’une demande à partir d’une session cliente est toujours dirigée toohello même machine virtuelle dans la batterie de serveurs web hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-163">**tooenable cookie-based affinity**: An application gateway can be configured tooensure that a request from a client session is always directed toohello same VM in hello web farm.</span></span> <span data-ttu-id="c1943-164">Ce scénario est effectué par injection d’un cookie de session qui autorise le trafic toodirect de passerelle de hello de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="c1943-164">This scenario is done by injection of a session cookie that allows hello gateway toodirect traffic appropriately.</span></span> <span data-ttu-id="c1943-165">l’affinité basé sur cookie tooenable, définie **CookieBasedAffinity** trop*activé* Bonjour **paramètres** élément.</span><span class="sxs-lookup"><span data-stu-id="c1943-165">tooenable cookie-based affinity, set **CookieBasedAffinity** too*Enabled* in hello **BackendHttpSettings** element.</span></span>

<span data-ttu-id="c1943-166">Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="c1943-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="c1943-167">tooconstruct votre configuration à l’aide d’une configuration de fichier XML, utilisez hello suivants exemple :</span><span class="sxs-lookup"><span data-stu-id="c1943-167">tooconstruct your configuration by using a configuration XML file, use hello following sample:</span></span>

<span data-ttu-id="c1943-168">**Exemple de configuration XML**</span><span class="sxs-lookup"><span data-stu-id="c1943-168">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-hello-gateway-configuration"></a><span data-ttu-id="c1943-169">Jeu de configuration de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="c1943-169">Set hello gateway configuration</span></span>

<span data-ttu-id="c1943-170">Ensuite, vous définissez la passerelle d’application hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-170">Next, you set hello application gateway.</span></span> <span data-ttu-id="c1943-171">Vous pouvez utiliser hello `Set-AzureApplicationGatewayConfig` applet de commande avec un objet de configuration ou un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="c1943-171">You can use hello `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-hello-gateway"></a><span data-ttu-id="c1943-172">Démarrer hello passerelle</span><span class="sxs-lookup"><span data-stu-id="c1943-172">Start hello gateway</span></span>

<span data-ttu-id="c1943-173">Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande.</span><span class="sxs-lookup"><span data-stu-id="c1943-173">Once hello gateway has been configured, use hello `Start-AzureApplicationGateway` cmdlet toostart hello gateway.</span></span> <span data-ttu-id="c1943-174">Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré.</span><span class="sxs-lookup"><span data-stu-id="c1943-174">Billing for an application gateway begins after hello gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="c1943-175">Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toofinish too15 à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="c1943-175">hello `Start-AzureApplicationGateway` cmdlet might take up too15-20 minutes toofinish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a><span data-ttu-id="c1943-176">Vérifiez l’état de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="c1943-176">Verify hello gateway status</span></span>

<span data-ttu-id="c1943-177">Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="c1943-177">Use hello `Get-AzureApplicationGateway` cmdlet toocheck hello status of hello gateway.</span></span> <span data-ttu-id="c1943-178">Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, *état* doit être en cours d’exécution, et *présence* et *DnsName* doit avoir des entrées valides.</span><span class="sxs-lookup"><span data-stu-id="c1943-178">If `Start-AzureApplicationGateway` succeeded in hello previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="c1943-179">Cet exemple montre une passerelle d’application, en cours d’exécution, et le trafic de tootake prêt.</span><span class="sxs-lookup"><span data-stu-id="c1943-179">This sample shows an application gateway that is up, running, and is ready tootake traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="c1943-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1943-180">Next steps</span></span>

<span data-ttu-id="c1943-181">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="c1943-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="c1943-182">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="c1943-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="c1943-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c1943-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

