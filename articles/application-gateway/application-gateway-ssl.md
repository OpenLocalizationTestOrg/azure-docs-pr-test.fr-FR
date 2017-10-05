---
title: "Configurer le déchargement SSL - Passerelle Azure Application Gateway - PowerShell classic | Microsoft Docs"
description: "Cet article fournit des instructions pour créer une passerelle d’application avec le déchargement SSL en utilisant le modèle de déploiement classique Azure."
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
ms.openlocfilehash: 2eba6fb24c11add12ac16d04d3445e19a3486216
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="40401-103">Configurer une passerelle d’application pour le déchargement SSL en utilisant le modèle de déploiement classique</span><span class="sxs-lookup"><span data-stu-id="40401-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="40401-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="40401-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="40401-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="40401-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="40401-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="40401-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="40401-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40401-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="40401-108">Il est possible de configurer Azure Application Gateway de façon à mettre fin à la session SSL (Secure Sockets Layer) sur la passerelle pour éviter les tâches de déchiffrement SSL coûteuses au niveau de la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="40401-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="40401-109">Le déchargement SSL simplifie aussi la configuration de serveur principal et la gestion de l’application web.</span><span class="sxs-lookup"><span data-stu-id="40401-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="40401-110">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="40401-110">Before you begin</span></span>

1. <span data-ttu-id="40401-111">Installez la dernière version des applets de commande Azure PowerShell à l’aide de Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="40401-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="40401-112">Vous pouvez télécharger et installer la dernière version à partir de la section **Windows PowerShell** de la [page Téléchargements](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="40401-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="40401-113">Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.</span><span class="sxs-lookup"><span data-stu-id="40401-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="40401-114">Assurez-vous qu’aucun ordinateur virtuel ou déploiement cloud n’utilise le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="40401-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="40401-115">La passerelle Application Gateway doit être seule sur un sous-réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="40401-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="40401-116">Les serveurs que vous configurez pour utiliser la passerelle Application Gateway doivent exister ou vous devez créer leurs points de terminaison sur le réseau virtuel ou avec une adresse IP/VIP publique affectée.</span><span class="sxs-lookup"><span data-stu-id="40401-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="40401-117">Pour configurer le déchargement SSL sur une passerelle d’application, exécutez les étapes suivantes dans l’ordre indiqué.</span><span class="sxs-lookup"><span data-stu-id="40401-117">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="40401-118">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="40401-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="40401-119">Télécharger des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="40401-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="40401-120">Configurer la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="40401-121">Définir la configuration de la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="40401-122">Démarrer la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="40401-123">Vérifier l'état de la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="40401-124">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="40401-124">Create an application gateway</span></span>

<span data-ttu-id="40401-125">Pour créer la passerelle, utilisez l’applet de commande `New-AzureApplicationGateway` en remplaçant les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="40401-125">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="40401-126">La facturation de la passerelle ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="40401-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="40401-127">La facturation commence à une étape ultérieure, lorsque la passerelle a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="40401-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="40401-128">Pour valider la création de la passerelle, vous pouvez utiliser l’applet de commande `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="40401-128">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="40401-129">Dans l’exemple, *Description*, *InstanceCount* et *GatewaySize* sont des paramètres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="40401-129">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="40401-130">La valeur par défaut pour *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="40401-130">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="40401-131">La valeur par défaut pour *GatewaySize* est Medium.</span><span class="sxs-lookup"><span data-stu-id="40401-131">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="40401-132">Les autres valeurs disponibles sont Small et Large.</span><span class="sxs-lookup"><span data-stu-id="40401-132">Small and Large are other available values.</span></span> <span data-ttu-id="40401-133">Les paramètres *VirtualIPs* et *DnsName* sont sans valeur, car la passerelle n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="40401-133">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="40401-134">Ces valeurs seront créées une fois la passerelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="40401-134">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="40401-135">Télécharger des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="40401-135">Upload SSL certificates</span></span>

<span data-ttu-id="40401-136">Utilisez `Add-AzureApplicationGatewaySslCertificate` pour charger le certificat de serveur au format *pfx* dans la passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="40401-136">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="40401-137">Le nom du certificat est choisi par l'utilisateur et doit être unique au sein de la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="40401-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="40401-138">Ce certificat est identifié par ce nom dans toutes les opérations de gestion de certificat sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="40401-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="40401-139">L’exemple suivant illustre l’applet de commande. Remplacez les valeurs utilisées ici par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="40401-139">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="40401-140">Ensuite, validez le téléchargement du certificat.</span><span class="sxs-lookup"><span data-stu-id="40401-140">Next, validate the certificate upload.</span></span> <span data-ttu-id="40401-141">Utilisez l’applet de commande `Get-AzureApplicationGatewayCertificate` .</span><span class="sxs-lookup"><span data-stu-id="40401-141">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="40401-142">Cet exemple montre l'applet de commande sur la première ligne, suivie de la sortie.</span><span class="sxs-lookup"><span data-stu-id="40401-142">This sample shows the cmdlet on the first line, followed by the output.</span></span>

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
> <span data-ttu-id="40401-143">Le mot de passe du certificat doit comprendre entre 4 et 12 caractères, lettres ou chiffres.</span><span class="sxs-lookup"><span data-stu-id="40401-143">The certificate password has to be between 4 to 12 characters, letters, or numbers.</span></span> <span data-ttu-id="40401-144">Les caractères spéciaux ne sont pas acceptés.</span><span class="sxs-lookup"><span data-stu-id="40401-144">Special characters are not accepted.</span></span>

## <a name="configure-the-gateway"></a><span data-ttu-id="40401-145">Configurer la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-145">Configure the gateway</span></span>

<span data-ttu-id="40401-146">La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs.</span><span class="sxs-lookup"><span data-stu-id="40401-146">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="40401-147">Les valeurs peuvent être liées ensemble pour construire la configuration.</span><span class="sxs-lookup"><span data-stu-id="40401-147">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="40401-148">Les valeurs sont :</span><span class="sxs-lookup"><span data-stu-id="40401-148">The values are:</span></span>

* <span data-ttu-id="40401-149">**Pool de serveurs principaux :** liste des adresses IP des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="40401-149">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="40401-150">Les adresses IP répertoriées doivent appartenir au sous-réseau de réseau virtuel ou doivent correspondre à une adresse IP/VIP publique.</span><span class="sxs-lookup"><span data-stu-id="40401-150">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="40401-151">**Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies.</span><span class="sxs-lookup"><span data-stu-id="40401-151">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="40401-152">Ces paramètres sont liés à un pool et sont appliqués à tous les serveurs du pool.</span><span class="sxs-lookup"><span data-stu-id="40401-152">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="40401-153">**Port frontal :** il s’agit du port public ouvert sur la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="40401-153">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="40401-154">Le trafic atteint ce port, puis il est redirigé vers l’un des serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="40401-154">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="40401-155">**Écouteur :** l’écouteur a un port frontal, un protocole (Http ou Https, avec respect de la casse) et le nom du certificat SSL (en cas de configuration du déchargement SSL).</span><span class="sxs-lookup"><span data-stu-id="40401-155">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="40401-156">**Règle :** la règle lie l’écouteur et le pool de serveurs principaux et définit vers quel pool de serveurs principaux le trafic doit être dirigé quand il atteint un écouteur spécifique.</span><span class="sxs-lookup"><span data-stu-id="40401-156">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="40401-157">Actuellement, seule la règle *de base* est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="40401-157">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="40401-158">La règle de *base* est la distribution de charge par tourniquet.</span><span class="sxs-lookup"><span data-stu-id="40401-158">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="40401-159">**Notes de configuration supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="40401-159">**Additional configuration notes**</span></span>

<span data-ttu-id="40401-160">Pour configurer des certificats SSL, le protocole dans **HttpListener** doit passer à *Https* (sensible à la casse).</span><span class="sxs-lookup"><span data-stu-id="40401-160">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="40401-161">L’élément **SslCert** est ajouté à **HttpListener** avec le même nom que celui utilisé pour le chargement des certificats SSL dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="40401-161">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="40401-162">Le port du serveur frontal doit être mis à jour sur 443.</span><span class="sxs-lookup"><span data-stu-id="40401-162">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="40401-163">**Pour activer l’affinité basée sur les cookies**: une passerelle Application Gateway peut être configurée pour garantir qu’une requête d’une session client est toujours dirigée vers la même machine virtuelle dans la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="40401-163">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="40401-164">Ce scénario est réalisé par l’injection d’un cookie de session, qui permet à la passerelle de diriger le trafic de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="40401-164">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="40401-165">Pour activer l’affinité basée sur les cookies, définissez **CookieBasedAffinity** sur *Activé* dans l’élément **BackendHttpSettings**.</span><span class="sxs-lookup"><span data-stu-id="40401-165">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="40401-166">Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="40401-166">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="40401-167">Pour construire votre configuration à l’aide d’un fichier XML de configuration, utilisez l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="40401-167">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="40401-168">**Exemple de configuration XML**</span><span class="sxs-lookup"><span data-stu-id="40401-168">**Configuration XML sample**</span></span>

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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="40401-169">Définir la configuration de la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-169">Set the gateway configuration</span></span>

<span data-ttu-id="40401-170">Ensuite, vous définissez la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="40401-170">Next, you set the application gateway.</span></span> <span data-ttu-id="40401-171">Vous pouvez utiliser l’applet de commande `Set-AzureApplicationGatewayConfig` avec un objet de configuration ou un fichier XML de configuration.</span><span class="sxs-lookup"><span data-stu-id="40401-171">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="40401-172">Démarrer la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-172">Start the gateway</span></span>

<span data-ttu-id="40401-173">Une fois la passerelle configurée, utilisez l’applet de commande `Start-AzureApplicationGateway` pour démarrer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="40401-173">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="40401-174">La facturation pour une passerelle Application Gateway commence une fois la passerelle démarrée avec succès.</span><span class="sxs-lookup"><span data-stu-id="40401-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> <span data-ttu-id="40401-175">La règle `Start-AzureApplicationGateway` peut prendre jusqu’à 15 à 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="40401-175">The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.</span></span>
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="40401-176">Vérifier l'état de la passerelle</span><span class="sxs-lookup"><span data-stu-id="40401-176">Verify the gateway status</span></span>

<span data-ttu-id="40401-177">Utilisez l’applet de commande `Get-AzureApplicationGateway` pour vérifier l’état de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="40401-177">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="40401-178">Si `Start-AzureApplicationGateway` a réussi à l’étape précédente, *l’état* doit être En cours d’exécution, et les paramètres *VirtualIPs* et *DnsName* doivent posséder des entrées valides.</span><span class="sxs-lookup"><span data-stu-id="40401-178">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="40401-179">Cet exemple montre une passerelle d’application en état de s’exécuter et d’accepter du trafic.</span><span class="sxs-lookup"><span data-stu-id="40401-179">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="40401-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="40401-180">Next steps</span></span>

<span data-ttu-id="40401-181">Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :</span><span class="sxs-lookup"><span data-stu-id="40401-181">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="40401-182">Équilibrage de charge Azure</span><span class="sxs-lookup"><span data-stu-id="40401-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="40401-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="40401-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

