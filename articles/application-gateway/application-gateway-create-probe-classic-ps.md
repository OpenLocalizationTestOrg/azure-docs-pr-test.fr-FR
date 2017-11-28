---
title: "Créer une sonde personnalisée - Passerelle Azure Application Gateway - PowerShell classic | Microsoft Docs"
description: "Apprendre à créer une sonde personnalisée pour Application Gateway en utilisant PowerShell dans le modèle de déploiement classique"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: bf190741b10c10e885d927ad21a9f2b25107943f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="c17d5-103">Créer une sonde personnalisée pour Azure Application Gateway (classique) en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="c17d5-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c17d5-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c17d5-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="c17d5-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c17d5-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="c17d5-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="c17d5-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="c17d5-107">Dans cet article, une sonde personnalisée est ajoutée à une passerelle d’application existante à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c17d5-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="c17d5-108">Les sondes personnalisées sont utiles pour les applications qui ont une page de contrôle d’intégrité spécifique ou pour les applications qui ne fournissent pas de réponse correcte dans l’application web par défaut.</span><span class="sxs-lookup"><span data-stu-id="c17d5-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c17d5-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c17d5-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c17d5-110">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="c17d5-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c17d5-111">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c17d5-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c17d5-112">Découvrez comment [effectuer ces étapes à l’aide du modèle Resource Manager](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c17d5-112">Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="c17d5-113">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="c17d5-113">Create an application gateway</span></span>

<span data-ttu-id="c17d5-114">Pour créer une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="c17d5-114">To create an application gateway:</span></span>

1. <span data-ttu-id="c17d5-115">Créez une ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c17d5-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="c17d5-116">Créez un fichier XML de configuration ou un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="c17d5-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="c17d5-117">Validez la configuration de la ressource Application Gateway nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="c17d5-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="c17d5-118">Créer une ressource de passerelle d’application avec une sonde personnalisée</span><span class="sxs-lookup"><span data-stu-id="c17d5-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="c17d5-119">Pour créer la passerelle, utilisez l’applet de commande `New-AzureApplicationGateway` en remplaçant les valeurs par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="c17d5-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="c17d5-120">La facturation de la passerelle ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="c17d5-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="c17d5-121">La facturation commence à une étape ultérieure, lorsque la passerelle a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="c17d5-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="c17d5-122">L’exemple suivant illustre la création d’une nouvelle passerelle d’application avec un réseau virtuel appelé « testvnet1 » et un sous-réseau appelé « subnet-1 ».</span><span class="sxs-lookup"><span data-stu-id="c17d5-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="c17d5-123">Pour valider la création de la passerelle, vous pouvez utiliser l’applet de commande `Get-AzureApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="c17d5-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="c17d5-124">La valeur par défaut pour *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="c17d5-124">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c17d5-125">La valeur par défaut du paramètre *GatewaySize* est Medium.</span><span class="sxs-lookup"><span data-stu-id="c17d5-125">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c17d5-126">Vous avez le choix entre Small, Medium et Large.</span><span class="sxs-lookup"><span data-stu-id="c17d5-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="c17d5-127">Les paramètres *VirtualIPs* et *DnsName* sont sans valeur, car la passerelle n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="c17d5-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="c17d5-128">Ces valeurs seront créées une fois la passerelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c17d5-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="c17d5-129">Configurer une passerelle d’application à l’aide de XML</span><span class="sxs-lookup"><span data-stu-id="c17d5-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="c17d5-130">Dans l’exemple ci-dessous, vous allez utiliser un fichier XML pour configurer tous les paramètres de la passerelle d’application et les valider dans la ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="c17d5-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="c17d5-131">Copiez le texte suivant dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="c17d5-131">Copy the following text to Notepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="c17d5-132">Modifiez les valeurs entre parenthèses pour les éléments de configuration.</span><span class="sxs-lookup"><span data-stu-id="c17d5-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="c17d5-133">Enregistrez le fichier avec l’extension .xml.</span><span class="sxs-lookup"><span data-stu-id="c17d5-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="c17d5-134">L’exemple suivant montre comment utiliser un fichier de configuration pour configurer la passerelle d’application en vue d’équilibrer la charge du trafic HTTP sur le port public 80 et d’orienter le trafic réseau vers le port 80 principal entre deux adresses IP en utilisant une sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c17d5-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c17d5-135">L’élément de protocole Http ou Https est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="c17d5-135">The protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="c17d5-136">Un nouvel élément de configuration \<Probe\> est ajouté pour configurer les sondes personnalisées.</span><span class="sxs-lookup"><span data-stu-id="c17d5-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="c17d5-137">Les paramètres de configuration sont :</span><span class="sxs-lookup"><span data-stu-id="c17d5-137">The configuration parameters are:</span></span>

|<span data-ttu-id="c17d5-138">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c17d5-138">Parameter</span></span>|<span data-ttu-id="c17d5-139">Description</span><span class="sxs-lookup"><span data-stu-id="c17d5-139">Description</span></span>|
|---|---|
|<span data-ttu-id="c17d5-140">**Nom**</span><span class="sxs-lookup"><span data-stu-id="c17d5-140">**Name**</span></span> |<span data-ttu-id="c17d5-141">Nom de référence de la sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c17d5-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="c17d5-142">* **Protocole**</span><span class="sxs-lookup"><span data-stu-id="c17d5-142">* **Protocol**</span></span> | <span data-ttu-id="c17d5-143">Protocole utilisé (les valeurs possibles sont HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="c17d5-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="c17d5-144">**Hôte** et **Chemin**</span><span class="sxs-lookup"><span data-stu-id="c17d5-144">**Host** and **Path**</span></span> | <span data-ttu-id="c17d5-145">Chemin complet de l’URL qui est appelé par la passerelle d’application pour déterminer l’intégrité de l’instance.</span><span class="sxs-lookup"><span data-stu-id="c17d5-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="c17d5-146">Par exemple : avec un site web http://contoso.com/, la sonde personnalisée peut être configurée pour « http://contoso.com/path/custompath.htm » afin que les contrôles de sonde renvoient une réponse HTTP réussie.</span><span class="sxs-lookup"><span data-stu-id="c17d5-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="c17d5-147">**Intervalle**</span><span class="sxs-lookup"><span data-stu-id="c17d5-147">**Interval**</span></span> | <span data-ttu-id="c17d5-148">Configure les vérifications d’intervalle de sonde en secondes.</span><span class="sxs-lookup"><span data-stu-id="c17d5-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="c17d5-149">**Délai d'expiration**</span><span class="sxs-lookup"><span data-stu-id="c17d5-149">**Timeout**</span></span> | <span data-ttu-id="c17d5-150">Définit le délai d’expiration d’un contrôle de réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="c17d5-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="c17d5-151">**Seuil de défaillance sur le plan de l’intégrité**</span><span class="sxs-lookup"><span data-stu-id="c17d5-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="c17d5-152">Le nombre d’échecs de réponses HTTP nécessaires pour marquer l’instance de serveur principal comme *défectueuse*.</span><span class="sxs-lookup"><span data-stu-id="c17d5-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="c17d5-153">Le nom de la sonde est référencé dans la configuration \<BackendHttpSettings\> pour affecter le pool principal qui va utiliser les paramètres de sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c17d5-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="c17d5-154">Ajoute une sonde personnalisée à une passerelle d’application existante</span><span class="sxs-lookup"><span data-stu-id="c17d5-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="c17d5-155">La modification de la configuration actuelle d’une passerelle d’application se fait en trois étapes : obtenez le fichier de configuration XML actuel, modifiez-le de façon à avoir une sonde personnalisée et configurez la passerelle d’application avec les nouveaux paramètres XML.</span><span class="sxs-lookup"><span data-stu-id="c17d5-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="c17d5-156">Obtenir le fichier XML à l’aide de `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="c17d5-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="c17d5-157">L’applet de commande exporte le fichier XML de configuration, afin d’être modifié pour y ajouter un paramètre de sonde.</span><span class="sxs-lookup"><span data-stu-id="c17d5-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="c17d5-158">Ouvrez le fichier XML dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="c17d5-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="c17d5-159">Ajoutez une section `<probe>` après `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="c17d5-159">Add a `<probe>` section after `<frontendport>`.</span></span>

  ```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
  ```

  <span data-ttu-id="c17d5-160">Dans la section backendHttpSettings du fichier XML, ajoutez le nom de la sonde comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c17d5-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

  ```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
  ```

  <span data-ttu-id="c17d5-161">Enregistrez le fichier XML.</span><span class="sxs-lookup"><span data-stu-id="c17d5-161">Save the XML file.</span></span>

1. <span data-ttu-id="c17d5-162">Mettez à jour la configuration de la passerelle d’application avec le nouveau fichier XML avec `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="c17d5-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="c17d5-163">Cette applet de commande met à jour votre passerelle d’application avec cette nouvelle configuration.</span><span class="sxs-lookup"><span data-stu-id="c17d5-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="c17d5-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c17d5-164">Next steps</span></span>

<span data-ttu-id="c17d5-165">Si vous voulez configurer le déchargement SSL (Secure Sockets Layer), consultez [Configuration d’une passerelle Application Gateway pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="c17d5-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="c17d5-166">Si vous voulez configurer une passerelle Application Gateway à utiliser avec l’équilibreur de charge interne, consultez [Création d’une passerelle Application Gateway avec un équilibrage de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="c17d5-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

