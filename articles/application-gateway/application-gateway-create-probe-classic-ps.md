---
title: "aaaCreate un classique de PowerShell sonde personnalisée - passerelle d’Application Azure - | Documents Microsoft"
description: "Découvrez comment toocreate personnalisé sondage pour la passerelle d’Application à l’aide de PowerShell dans le modèle de déploiement classique de hello"
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
ms.openlocfilehash: 68332367c99328bd6456b0c339923765637be986
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="d3bc3-103">Créer une sonde personnalisée pour Azure Application Gateway (classique) en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3bc3-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3bc3-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d3bc3-104">Azure portal</span></span>](application-gateway-create-probe-portal.md)
> * [<span data-ttu-id="d3bc3-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3bc3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-probe-ps.md)
> * [<span data-ttu-id="d3bc3-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3bc3-106">Azure Classic PowerShell</span></span>](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="d3bc3-107">Dans cet article, vous ajoutez une passerelle existante d’application sonde personnalisée tooan avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-107">In this article, you add a custom probe tooan existing application gateway with PowerShell.</span></span> <span data-ttu-id="d3bc3-108">Les sondes personnalisés sont utiles pour les applications qui ont une page de vérification d’intégrité spécifique ou pour les applications qui ne fournissent pas une réponse correcte sur l’application web de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on hello default web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3bc3-109">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3bc3-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d3bc3-110">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d3bc3-111">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d3bc3-112">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](application-gateway-create-probe-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d3bc3-112">Learn how too[perform these steps using hello Resource Manager model](application-gateway-create-probe-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="d3bc3-113">Créer une passerelle Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d3bc3-113">Create an application gateway</span></span>

<span data-ttu-id="d3bc3-114">toocreate une passerelle d’application :</span><span class="sxs-lookup"><span data-stu-id="d3bc3-114">toocreate an application gateway:</span></span>

1. <span data-ttu-id="d3bc3-115">Créez une ressource Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="d3bc3-116">Créez un fichier XML de configuration ou un objet de configuration.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="d3bc3-117">Valider hello toohello de configuration qui vient d’être créé ressource passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-117">Commit hello configuration toohello newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="d3bc3-118">Créer une ressource de passerelle d’application avec une sonde personnalisée</span><span class="sxs-lookup"><span data-stu-id="d3bc3-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="d3bc3-119">passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-119">toocreate hello gateway, use hello `New-AzureApplicationGateway` cmdlet, replacing hello values with your own.</span></span> <span data-ttu-id="d3bc3-120">La facturation pour la passerelle de hello ne démarre pas à ce stade.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-120">Billing for hello gateway does not start at this point.</span></span> <span data-ttu-id="d3bc3-121">La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-121">Billing begins in a later step, when hello gateway is successfully started.</span></span>

<span data-ttu-id="d3bc3-122">Hello exemple suivant crée une passerelle d’application à l’aide d’un réseau virtuel appelé « testvnet1 » et un sous-réseau nommé « sous-réseau-1 ».</span><span class="sxs-lookup"><span data-stu-id="d3bc3-122">hello following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="d3bc3-123">toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-123">toovalidate that hello gateway was created, you can use hello `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> <span data-ttu-id="d3bc3-124">Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-124">hello default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="d3bc3-125">Hello la valeur par défaut de *GatewaySize* est moyenne.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-125">hello default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="d3bc3-126">Vous avez le choix entre Small, Medium et Large.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-126">You can choose between Small, Medium, and Large.</span></span>
> 
> 

<span data-ttu-id="d3bc3-127">*Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-127">*VirtualIPs* and *DnsName* are shown as blank because hello gateway has not started yet.</span></span> <span data-ttu-id="d3bc3-128">Ces valeurs sont créés une fois la passerelle de hello en hello état en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-128">These values are created once hello gateway is in hello running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="d3bc3-129">Configurer une passerelle d’application à l’aide de XML</span><span class="sxs-lookup"><span data-stu-id="d3bc3-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="d3bc3-130">Bonjour l’exemple suivant, un tooconfigure de fichier XML tous les paramètres de passerelle d’application et de les valider toohello ressource de passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-130">In hello following example, you use an XML file tooconfigure all application gateway settings and commit them toohello application gateway resource.</span></span>  

<span data-ttu-id="d3bc3-131">Copiez hello suivant tooNotepad de texte.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-131">Copy hello following text tooNotepad.</span></span>

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

<span data-ttu-id="d3bc3-132">Modifier les valeurs hello entre parenthèses hello pour les éléments de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-132">Edit hello values between hello parentheses for hello configuration items.</span></span> <span data-ttu-id="d3bc3-133">Hello enregistrez-le avec l’extension .xml.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-133">Save hello file with extension .xml.</span></span>

<span data-ttu-id="d3bc3-134">Hello suivant montre comment toouse un tooset du fichier de configuration des tooload de passerelle d’application hello équilibrer le trafic HTTP sur le port public 80 et envoyer le trafic réseau tooback-end port80 entre deux adresses IP à l’aide d’une sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-134">hello following example shows how toouse a configuration file tooset up hello application gateway tooload balance HTTP traffic on public port 80 and send network traffic tooback-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3bc3-135">l’élément Hello protocole Http ou Https est sensible à la casse.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-135">hello protocol item Http or Https is case-sensitive.</span></span>

<span data-ttu-id="d3bc3-136">Un élément de configuration \<sonde\> est ajouté tooconfigure les sondes personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-136">A new configuration item \<Probe\> is added tooconfigure custom probes.</span></span>

<span data-ttu-id="d3bc3-137">les paramètres de configuration de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="d3bc3-137">hello configuration parameters are:</span></span>

|<span data-ttu-id="d3bc3-138">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d3bc3-138">Parameter</span></span>|<span data-ttu-id="d3bc3-139">Description</span><span class="sxs-lookup"><span data-stu-id="d3bc3-139">Description</span></span>|
|---|---|
|<span data-ttu-id="d3bc3-140">**Nom**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-140">**Name**</span></span> |<span data-ttu-id="d3bc3-141">Nom de référence de la sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="d3bc3-142">* **Protocole**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-142">* **Protocol**</span></span> | <span data-ttu-id="d3bc3-143">Protocole utilisé (les valeurs possibles sont HTTP ou HTTPS).</span><span class="sxs-lookup"><span data-stu-id="d3bc3-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="d3bc3-144">**Hôte** et **Chemin**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-144">**Host** and **Path**</span></span> | <span data-ttu-id="d3bc3-145">URL du chemin d’accès complet qui est appelée par hello application passerelle toodetermine hello d’intégrité de l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-145">Complete URL path that is invoked by hello application gateway toodetermine hello health of hello instance.</span></span> <span data-ttu-id="d3bc3-146">Par exemple, si vous avez un site Web http://contoso.com/, sonde personnalisée de hello peut être configurée pour « http://contoso.com/path/custompath.htm » pour la sonde vérifie toohave une réponse HTTP correcte.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-146">For example, if you have a website http://contoso.com/, then hello custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks toohave a successful HTTP response.</span></span>|
| <span data-ttu-id="d3bc3-147">**Intervalle**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-147">**Interval**</span></span> | <span data-ttu-id="d3bc3-148">Configure les vérifications d’intervalle hello sondage en secondes.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-148">Configures hello probe interval checks in seconds.</span></span>|
| <span data-ttu-id="d3bc3-149">**Délai d'expiration**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-149">**Timeout**</span></span> | <span data-ttu-id="d3bc3-150">Définit le délai d’attente de la sonde hello pour une vérification de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-150">Defines hello probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="d3bc3-151">**Seuil de défaillance sur le plan de l’intégrité**</span><span class="sxs-lookup"><span data-stu-id="d3bc3-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="d3bc3-152">Hello nombre d’échecs de réponse HTTP nécessaires de l’instance tooflag hello principal en tant que *défectueux*.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-152">hello number of failed HTTP responses needed tooflag hello back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="d3bc3-153">nom de la sonde Hello est référencé dans hello \<paramètres\> tooassign configuration quel pool principal utilise des paramètres de sonde personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-153">hello probe name is referenced in hello \<BackendHttpSettings\> configuration tooassign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-tooan-existing-application-gateway"></a><span data-ttu-id="d3bc3-154">Ajouter une passerelle d’application existant du tooan sonde personnalisée</span><span class="sxs-lookup"><span data-stu-id="d3bc3-154">Add a custom probe tooan existing application gateway</span></span>

<span data-ttu-id="d3bc3-155">La modification de configuration actuel hello d’une passerelle d’application nécessite trois étapes : obtenir le fichier de configuration XML actuel hello, modifier toohave une sonde personnalisée et configurer la passerelle d’application hello avec de nouveaux paramètres de XML hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-155">Changing hello current configuration of an application gateway requires three steps: Get hello current XML configuration file, modify toohave a custom probe, and configure hello application gateway with hello new XML settings.</span></span>

1. <span data-ttu-id="d3bc3-156">Obtenir le fichier XML de hello à l’aide de `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-156">Get hello XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="d3bc3-157">Cette toobe XML de configuration applet de commande exporte hello modifié tooadd un paramètre de sonde.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-157">This cmdlet exports hello configuration XML toobe modified tooadd a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path toofile>"
  ```

1. <span data-ttu-id="d3bc3-158">Ouvrez le fichier XML de hello dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-158">Open hello XML file in a text editor.</span></span> <span data-ttu-id="d3bc3-159">Ajoutez une section `<probe>` après `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="d3bc3-160">Dans la section Paramètres de hello Hello XML, ajoutez les nom de la sonde hello comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d3bc3-160">In hello backendHttpSettings section of hello XML, add hello probe name as shown in hello following example:</span></span>

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

  <span data-ttu-id="d3bc3-161">Enregistrez le fichier XML de hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-161">Save hello XML file.</span></span>

1. <span data-ttu-id="d3bc3-162">Configuration de passerelle l’application hello mise à jour avec hello fichier XML à l’aide de `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-162">Update hello application gateway configuration with hello new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="d3bc3-163">Cette applet de commande met à jour votre passerelle d’application avec la nouvelle configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="d3bc3-163">This cmdlet updates your application gateway with hello new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path toofile>"
```

## <a name="next-steps"></a><span data-ttu-id="d3bc3-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3bc3-164">Next steps</span></span>

<span data-ttu-id="d3bc3-165">Si vous souhaitez tooconfigure décharger de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="d3bc3-165">If you want tooconfigure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="d3bc3-166">Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="d3bc3-166">If you want tooconfigure an application gateway toouse with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

