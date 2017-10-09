---
title: "Se connecter à un réseau virtuel Azure à l’aide de Point-to-Site de tooan ordinateur et l’authentification des certificats : PowerShell | Documents Microsoft"
description: "Connectez-vous en toute sécurité un réseau virtuel d’ordinateurs tooyour en créant une connexion de passerelle VPN Point à Site à l’aide de l’authentification par certificat. Cet article s’applique le modèle de déploiement du Gestionnaire de ressources toohello et utilise PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="968ca-104">Configurer un tooa de connexion de Point-to-Site réseau virtuel à l’aide de l’authentification par certificat : PowerShell</span><span class="sxs-lookup"><span data-stu-id="968ca-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="968ca-105">Cet article vous explique comment toocreate un réseau virtuel avec une connexion Point à Site dans le déploiement du Gestionnaire de ressources hello modèle à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="968ca-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="968ca-106">Cette configuration utilise hello tooauthenticate de certificats client se connecte.</span><span class="sxs-lookup"><span data-stu-id="968ca-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="968ca-107">Vous pouvez également créer cette configuration à l’aide d’un outil de déploiement différentes ou d’un modèle de déploiement en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="968ca-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="968ca-108">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="968ca-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="968ca-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="968ca-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="968ca-110">Portail Azure (classique)</span><span class="sxs-lookup"><span data-stu-id="968ca-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="968ca-111">Une passerelle VPN de Point-to-Site (P2S) vous permet de créer un réseau virtuel tooyour de connexion sécurisée à partir d’un ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="968ca-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="968ca-112">Connexions de point-to-Site VPN sont utiles lorsque vous souhaitez tooconnect tooyour réseau virtuel à partir d’un emplacement distant, par exemple lorsque vous sont télétravailleurs d’accueil ou d’une conférence.</span><span class="sxs-lookup"><span data-stu-id="968ca-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="968ca-113">Un VPN P2S est également un toouse solution utile au lieu d’un VPN de Site à Site lorsque vous avez seulement quelques clients nécessitant tooconnect tooa réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="968ca-114">P2S utilise hello Tunneling protocole SSTP (Secure Socket), qui est un protocole de VPN basée sur le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="968ca-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="968ca-115">Un réseau VPN P2S est établie en le démarrant à partir de l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Se connecter à un réseau virtuel Azure - diagramme de connexions de Point-to-Site de tooan ordinateur](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="968ca-117">Connexions d’authentification de certificat de point-to-Site exiger les éléments de hello :</span><span class="sxs-lookup"><span data-stu-id="968ca-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="968ca-118">Une passerelle VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="968ca-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="968ca-119">Hello clé publique (fichier .cer) pour un certificat racine, qui est téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="968ca-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="968ca-120">Une fois que le certificat de hello est téléchargé, il est considéré comme un certificat approuvé et est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="968ca-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="968ca-121">Un certificat de client qui est généré à partir du certificat racine de hello et installé sur chaque ordinateur client qui se connectera toohello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="968ca-122">Ce certificat est utilisé pour l’authentification du client.</span><span class="sxs-lookup"><span data-stu-id="968ca-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="968ca-123">Un package de configuration du client VPN.</span><span class="sxs-lookup"><span data-stu-id="968ca-123">A VPN client configuration package.</span></span> <span data-ttu-id="968ca-124">package de configuration de client VPN Hello contient des informations nécessaires de hello pour hello client tooconnect toohello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="968ca-125">Hello configure hello VPN client existant est natif toohello système d’exploitation Windows.</span><span class="sxs-lookup"><span data-stu-id="968ca-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="968ca-126">Chaque client qui se connecte doit être configuré à l’aide du package de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="968ca-127">Les connexions point à site ne nécessitent pas de périphérique VPN ou d’adresse IP publique locale.</span><span class="sxs-lookup"><span data-stu-id="968ca-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="968ca-128">Hello connexion VPN est créée sur SSTP (Secure Socket Tunneling Protocol).</span><span class="sxs-lookup"><span data-stu-id="968ca-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="968ca-129">Sur le côté du serveur hello, nous prenons en charge les versions 1.0, 1.1 et 1.2 de SSTP.</span><span class="sxs-lookup"><span data-stu-id="968ca-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="968ca-130">client de Hello décide quelle toouse de version.</span><span class="sxs-lookup"><span data-stu-id="968ca-130">hello client decides which version toouse.</span></span> <span data-ttu-id="968ca-131">Pour Windows 8.1 et supérieur, SSTP utilise la version 1.2 par défaut.</span><span class="sxs-lookup"><span data-stu-id="968ca-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="968ca-132">Pour plus d’informations sur les connexions de Point-to-Site, consultez hello [Point-to-Site FAQ](#faq) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="968ca-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="968ca-133">Avant tout chose</span><span class="sxs-lookup"><span data-stu-id="968ca-133">Before beginning</span></span>

* <span data-ttu-id="968ca-134">Assurez-vous de disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="968ca-135">Si vous ne disposez pas déjà d’un abonnement Azure, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou créer un [compte gratuit](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="968ca-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="968ca-136">Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="968ca-137">Pour plus d’informations sur l’installation des applets de commande PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="968ca-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="968ca-138"><a name="example"></a>Exemples de valeurs</span><span class="sxs-lookup"><span data-stu-id="968ca-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="968ca-139">Vous pouvez utiliser toocreate de valeurs d’exemple hello un environnement de test, ou consultez les valeurs toothese toobetter comprendre les exemples hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="968ca-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="968ca-140">Nous avons défini les variables hello dans la section [1](#declare) de l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="968ca-141">Vous pouvez utiliser les étapes de hello comme une procédure pas à pas et utilisez les valeurs hello sans les modifier ou les modifier tooreflect votre environnement.</span><span class="sxs-lookup"><span data-stu-id="968ca-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="968ca-142">**Nom : VNet1**</span><span class="sxs-lookup"><span data-stu-id="968ca-142">**Name: VNet1**</span></span>
* <span data-ttu-id="968ca-143">**Espace d’adressage :192.168.0.0/16** et **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="968ca-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="968ca-144">Pour cet exemple, nous utilisons plusieurs tooillustrate espace adresse que cette configuration fonctionne avec plusieurs espaces d’adressage.</span><span class="sxs-lookup"><span data-stu-id="968ca-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="968ca-145">Toutefois, plusieurs espaces d’adressage ne sont pas nécessaires pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="968ca-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="968ca-146">**Nom du sous-réseau : FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="968ca-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="968ca-147">**Plage d’adresses de sous-réseau : 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="968ca-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="968ca-148">**Nom du sous-réseau : BackEnd**</span><span class="sxs-lookup"><span data-stu-id="968ca-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="968ca-149">**Plage d’adresses de sous-réseau : 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="968ca-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="968ca-150">**Nom du sous-réseau : GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="968ca-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="968ca-151">nom du sous-réseau Hello *GatewaySubnet* est obligatoire pour toowork de passerelle VPN hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="968ca-152">**Plage d’adresses de GatewaySubnet : 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="968ca-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="968ca-153">**Pool d’adresses des clients VPN : 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="968ca-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="968ca-154">Clients VPN qui se connectent toohello virtuel à l’aide de cette connexion Point-to-Site recevront une adresse IP à partir de hello pool d’adresses VPN client.</span><span class="sxs-lookup"><span data-stu-id="968ca-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="968ca-155">**L’abonnement :** si vous avez plusieurs abonnements, vérifiez que vous utilisez hello correct.</span><span class="sxs-lookup"><span data-stu-id="968ca-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="968ca-156">**Groupe de ressources : TestRG**</span><span class="sxs-lookup"><span data-stu-id="968ca-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="968ca-157">**Emplacement : États-Unis de l’Est**</span><span class="sxs-lookup"><span data-stu-id="968ca-157">**Location: East US**</span></span>
* <span data-ttu-id="968ca-158">**Serveur DNS : Adresse IP** du serveur DNS de hello que vous souhaitez toouse pour la résolution de nom.</span><span class="sxs-lookup"><span data-stu-id="968ca-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="968ca-159">**Nom de passerelle : Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="968ca-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="968ca-160">**Nom d’adresse IP publique : VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="968ca-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="968ca-161">**Type de VPN : RouteBased**</span><span class="sxs-lookup"><span data-stu-id="968ca-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="968ca-162"><a name="declare"></a>1. Connexion et définition des variables</span><span class="sxs-lookup"><span data-stu-id="968ca-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="968ca-163">Dans cette section, vous connectez et déclarez les valeurs hello utilisées pour cette configuration.</span><span class="sxs-lookup"><span data-stu-id="968ca-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="968ca-164">Hello déclaré valeurs sont utilisées dans les exemples de scripts hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="968ca-165">Modifier hello valeurs tooreflect votre propre environnement.</span><span class="sxs-lookup"><span data-stu-id="968ca-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="968ca-166">Ou bien, vous pouvez utiliser hello déclaré de valeurs et suivez les étapes de hello en guise d’exercice.</span><span class="sxs-lookup"><span data-stu-id="968ca-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="968ca-167">Ouvrez la console PowerShell avec des privilèges élevés, puis connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="968ca-168">Cette applet de commande vous invite à entrer les informations d’identification de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="968ca-169">Une fois connecté, il télécharge les paramètres de votre compte afin qu’ils soient disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="968ca-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="968ca-170">Obtenez la liste de vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="968ca-171">Spécifiez un abonnement hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="968ca-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="968ca-172">Déclarez les variables hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="968ca-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="968ca-173">Utilisez hello suivant l’exemple, en remplaçant les valeurs hello pour votre propre lorsque cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="968ca-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="968ca-174"><a name="ConfigureVNet"></a>2. Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="968ca-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="968ca-175">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="968ca-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="968ca-176">Créer des configurations de sous-réseau de réseau virtuel hello, nommant hello *frontal*, *principal*, et *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="968ca-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="968ca-177">Ces préfixes doivent faire partie de hello espace d’adressage de réseau virtuel que vous avez déclaré.</span><span class="sxs-lookup"><span data-stu-id="968ca-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="968ca-178">Créer un réseau virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-178">Create hello virtual network.</span></span>

  <span data-ttu-id="968ca-179">Dans cet exemple, le serveur DNS de hello est facultative.</span><span class="sxs-lookup"><span data-stu-id="968ca-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="968ca-180">La définition d’une valeur n’entraîne pas la création de serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="968ca-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="968ca-181">Hello adresse IP du serveur DNS que vous spécifiez doit être un serveur DNS peut résoudre les noms de hello pour les ressources hello que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="968ca-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="968ca-182">Pour cet exemple, nous avons utilisé une adresse IP privée, mais il est probable qu’il ne s’agit pas d’adresse IP de hello de votre serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="968ca-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="968ca-183">Être toouse que vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="968ca-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="968ca-184">Spécifiez les variables hello pour le réseau virtuel de hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="968ca-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="968ca-185">Une passerelle VPN doit avoir une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="968ca-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="968ca-186">Votre ressource d’adresse IP hello d’abord demander, puis consultez tooit lors de la création de votre passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="968ca-187">adresse IP de Hello est attribué dynamiquement les ressources toohello lors de la création de la passerelle VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="968ca-188">Actuellement, la passerelle VPN prend uniquement en charge l’allocation d’adresses IP publiques *dynamiques*.</span><span class="sxs-lookup"><span data-stu-id="968ca-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="968ca-189">Vous ne pouvez pas demander d’affectation d’adresse IP publique statique.</span><span class="sxs-lookup"><span data-stu-id="968ca-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="968ca-190">Toutefois, cela ne signifie pas que l’adresse IP de hello change après que qu’elle a été affectée passerelle VPN de tooyour.</span><span class="sxs-lookup"><span data-stu-id="968ca-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="968ca-191">Hello seule fois changements d’adresses IP publiques hello est hello lorsque la passerelle est supprimé et recréé.</span><span class="sxs-lookup"><span data-stu-id="968ca-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="968ca-192">Elle n’est pas modifiée lors du redimensionnement, de la réinitialisation ou des autres opérations de maintenance/mise à niveau internes de votre passerelle VPN.</span><span class="sxs-lookup"><span data-stu-id="968ca-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="968ca-193">Demandez une adresse IP publique attribuée dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="968ca-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="968ca-194"><a name="creategateway"></a>3. Créer une passerelle VPN de hello</span><span class="sxs-lookup"><span data-stu-id="968ca-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="968ca-195">Configurez et créez la passerelle de réseau virtuel hello pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="968ca-196">Hello *- le type de passerelle* doit être **Vpn** et hello *- VpnType* doit être **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="968ca-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="968ca-197">Une passerelle VPN peut prendre jusqu'à too45 minutes toocomplete, en fonction de hello [référence (SKU) de passerelle](vpn-gateway-about-vpn-gateway-settings.md) vous sélectionnez.</span><span class="sxs-lookup"><span data-stu-id="968ca-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="968ca-198"><a name="addresspool"></a>4. Ajouter un pool d’adresses client VPN hello</span><span class="sxs-lookup"><span data-stu-id="968ca-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="968ca-199">Passerelle VPN de hello après création, vous pouvez ajouter un pool d’adresses client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="968ca-200">Hello pool d’adresses VPN client est plage hello à partir de laquelle hello clients VPN recevront une adresse IP lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="968ca-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="968ca-201">Utilisez une plage d’adresses IP privées qui ne chevauche pas emplacement hello local auquel vous vous connectez à partir d’ou avec hello réseau virtuel que vous souhaitez tooconnect à.</span><span class="sxs-lookup"><span data-stu-id="968ca-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="968ca-202">Dans cet exemple, hello pool d’adresses VPN client est déclaré comme un [variable](#declare) à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="968ca-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="968ca-203"><a name="Certificates"></a>5. Générer des certificats</span><span class="sxs-lookup"><span data-stu-id="968ca-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="968ca-204">Certificats sont utilisés par les clients VPN tooauthenticate Azure pour Point-to-Site VPN.</span><span class="sxs-lookup"><span data-stu-id="968ca-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="968ca-205">Télécharger des informations de clé publique hello de tooAzure de certificat racine hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="968ca-206">clé publique de Hello est alors considéré comme « approuvé ».</span><span class="sxs-lookup"><span data-stu-id="968ca-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="968ca-207">Les certificats clients doivent être générés à partir du certificat racine approuvé de hello et installés sur chaque ordinateur client dans le magasin de certificats d’utilisateur de certificats-actuel/personnel hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="968ca-208">certificat de Hello est client de hello tooauthenticate utilisée lorsqu’elle initie un toohello de connexion réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="968ca-209">Si vous utilisez des certificats auto-signés, ceux-ci doivent être créés à l’aide de paramètres spécifiques.</span><span class="sxs-lookup"><span data-stu-id="968ca-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="968ca-210">Vous pouvez créer un certificat auto-signé à l’aide d’instructions hello pour [PowerShell et Windows 10](vpn-gateway-certificates-point-to-site.md), ou, si vous n’avez pas Windows 10, vous pouvez utiliser [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="968ca-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="968ca-211">Il est important de suivre les étapes de hello dans les instructions hello lors de la génération des certificats racines auto-signés et les certificats clients.</span><span class="sxs-lookup"><span data-stu-id="968ca-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="968ca-212">Sinon, vous générez des certificats hello ne sera pas compatibles avec les connexions P2S et vous recevrez une erreur de connexion.</span><span class="sxs-lookup"><span data-stu-id="968ca-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="968ca-213"><a name="cer"></a>1. Obtenir le fichier .cer hello pour le certificat racine de hello</span><span class="sxs-lookup"><span data-stu-id="968ca-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="968ca-214"><a name="generate"></a>2. Générer un certificat client</span><span class="sxs-lookup"><span data-stu-id="968ca-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="968ca-215"><a name="upload"></a>6. Télécharger les informations clé publique de certificat racine hello</span><span class="sxs-lookup"><span data-stu-id="968ca-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="968ca-216">Vérifiez que votre passerelle VPN a terminé la création.</span><span class="sxs-lookup"><span data-stu-id="968ca-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="968ca-217">Une fois terminée, vous pouvez télécharger le fichier de .cer hello (qui contient les informations de clé publique hello) pour un tooAzure de certificat racine de confiance.</span><span class="sxs-lookup"><span data-stu-id="968ca-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="968ca-218">Une fois a.cer fichier est téléchargé, Azure peut utiliser tooauthenticate les clients qui ont installé un certificat de client généré à partir du certificat racine approuvé de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="968ca-219">Vous pouvez télécharger les fichiers de certificat racine de confiance supplémentaires - tooa total de 20 - ultérieurement, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="968ca-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="968ca-220">Déclarer la variable hello pour votre nom de certificat, en remplaçant la valeur de hello avec vos propres.</span><span class="sxs-lookup"><span data-stu-id="968ca-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="968ca-221">Remplacez le chemin d’accès du fichier hello avec vos propres, puis exécutez les applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="968ca-222">Téléchargez tooAzure des informations de clé publique hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="968ca-223">Une fois les informations de certificat hello sont téléchargées, Azure considère que cette toobe un certificat racine approuvé.</span><span class="sxs-lookup"><span data-stu-id="968ca-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="968ca-224"><a name="clientconfig"></a>7. Télécharger le package de configuration de client VPN hello</span><span class="sxs-lookup"><span data-stu-id="968ca-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="968ca-225">tooconnect tooa virtuel à l’aide d’un VPN de Point-to-Site, chaque client doit installer un package de configuration de client qui configure le client VPN natif de hello avec des paramètres de hello et les fichiers qui sont le réseau virtuel de toohello tooconnect nécessaire.</span><span class="sxs-lookup"><span data-stu-id="968ca-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="968ca-226">package de configuration de client VPN Hello configure client VPN Windows natif de hello, il n’installe pas un client VPN nouveaux ou différent.</span><span class="sxs-lookup"><span data-stu-id="968ca-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="968ca-227">Vous pouvez utiliser hello même configuration du client VPN le package sur chaque ordinateur client, tant que la version de hello correspond à l’architecture hello pour les clients hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="968ca-228">Pour hello de la liste des systèmes d’exploitation client pris en charge, consultez hello [ForumauxquestionssurlesconnexionsPointàSite](#faq) à fin hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="968ca-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="968ca-229">Une fois la passerelle de hello a été créé, vous pouvez générer et télécharger le package de configuration client hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="968ca-230">Cet exemple télécharge le package de hello pour les clients 64 bits.</span><span class="sxs-lookup"><span data-stu-id="968ca-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="968ca-231">Si vous souhaitez que les clients de toodownload hello 32 bits, remplacez « Amd64 » par « x86 ».</span><span class="sxs-lookup"><span data-stu-id="968ca-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="968ca-232">Vous pouvez également télécharger le client VPN de hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="968ca-233">Copiez et collez le lien hello renvoyé tooa navigateur toodownload hello package web, en prenant soin de guillemets de hello tooremove entourant le lien de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="968ca-234">Téléchargez et installez le package de hello sur l’ordinateur client de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="968ca-235">Si une fenêtre contextuelle SmartScreen s’affiche, cliquez sur **Plus d’infos**, puis sur **Exécuter quand même**.</span><span class="sxs-lookup"><span data-stu-id="968ca-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="968ca-236">Vous pouvez également enregistrer hello package tooinstall sur d’autres ordinateurs client.</span><span class="sxs-lookup"><span data-stu-id="968ca-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="968ca-237">Sur l’ordinateur client de hello, accédez trop**paramètres réseau** et cliquez sur **VPN**.</span><span class="sxs-lookup"><span data-stu-id="968ca-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="968ca-238">Hello connexion VPN affiche le nom hello du réseau virtuel hello auquel il se connecte.</span><span class="sxs-lookup"><span data-stu-id="968ca-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="968ca-239"><a name="clientcertificate"></a>8. Installer un certificat client exporté</span><span class="sxs-lookup"><span data-stu-id="968ca-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="968ca-240">Si vous voulez toocreate un P2S à partir d’un ordinateur client autre que hello celle que vous avez utilisé des certificats de client de hello toogenerate, vous devez tooinstall un certificat client.</span><span class="sxs-lookup"><span data-stu-id="968ca-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="968ca-241">Lorsque vous installez un certificat client, vous avez besoin d’un mot de passe hello créé lors de l’exportation du certificat client hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="968ca-242">En règle générale, il est simplement en double-cliquant sur le certificat de hello et l’installer.</span><span class="sxs-lookup"><span data-stu-id="968ca-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="968ca-243">Assurez-vous que le certificat de client hello a été exporté dans un fichier .pfx, ainsi que la chaîne de certificat entière hello (qui est la valeur par défaut hello).</span><span class="sxs-lookup"><span data-stu-id="968ca-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="968ca-244">Dans le cas contraire, informations relatives au certificat racine hello n’est pas présents sur l’ordinateur client de hello et hello client ne sera pas en mesure de tooauthenticate correctement.</span><span class="sxs-lookup"><span data-stu-id="968ca-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="968ca-245">Pour plus d’informations, consultez la rubrique [Installer un certificat client exporté](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="968ca-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="968ca-246"><a name="connect"></a>9. Se connecter tooAzure</span><span class="sxs-lookup"><span data-stu-id="968ca-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="968ca-247">tooconnect tooyour réseau virtuel, sur l’ordinateur client de hello, accédez tooVPN connexions et trouver la connexion VPN hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="968ca-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="968ca-248">Il est nommé hello même nom que votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="968ca-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="968ca-249">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="968ca-249">Click **Connect**.</span></span> <span data-ttu-id="968ca-250">Un message peut apparaître qui fait référence le certificat de hello toousing.</span><span class="sxs-lookup"><span data-stu-id="968ca-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="968ca-251">Cliquez sur **continuer** toouse des privilèges élevés.</span><span class="sxs-lookup"><span data-stu-id="968ca-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="968ca-252">Sur hello **connexion** page d’état, cliquez sur **Connect** connexion de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="968ca-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="968ca-253">Si vous voyez un **sélectionner un certificat** écran, vérifiez que hello certificat client affiché est hello une que vous souhaitez toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="968ca-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="968ca-254">Si elle n’est pas le cas, utilisez bon certificat hello flèche tooselect hello, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="968ca-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![Client VPN connecte tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="968ca-256">Votre connexion est établie.</span><span class="sxs-lookup"><span data-stu-id="968ca-256">Your connection is established.</span></span>

  ![Connexion établie](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="968ca-258">Résolution des problèmes liés aux connexions P2S</span><span class="sxs-lookup"><span data-stu-id="968ca-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="968ca-259"><a name="verify"></a>10. Vérifier votre connexion</span><span class="sxs-lookup"><span data-stu-id="968ca-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="968ca-260">tooverify que votre connexion VPN est active, ouvrez une invite de commandes avec élévation de privilèges et exécutez *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="968ca-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="968ca-261">Afficher les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-261">View hello results.</span></span> <span data-ttu-id="968ca-262">Notez qu’adresse hello que vous avez reçu est une des adresses hello dans le Pool d’adresses hello Point-to-Site VPN Client que vous avez spécifié dans votre configuration.</span><span class="sxs-lookup"><span data-stu-id="968ca-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="968ca-263">les résultats de Hello sont similaires toothis exemple :</span><span class="sxs-lookup"><span data-stu-id="968ca-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="968ca-264"><a name="connectVM"></a>Connecter l’ordinateur virtuel de tooa</span><span class="sxs-lookup"><span data-stu-id="968ca-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="968ca-265"><a name="addremovecert"></a>Ajouter ou supprimer un certificat racine</span><span class="sxs-lookup"><span data-stu-id="968ca-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="968ca-266">Vous pouvez ajouter et supprimer des certificats racines approuvés à partir d'Azure.</span><span class="sxs-lookup"><span data-stu-id="968ca-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="968ca-267">Lorsque vous supprimez un certificat racine, les clients qui possèdent un certificat généré à partir du certificat racine de hello ne peut pas authentifier et ne pourra plus être en mesure de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="968ca-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="968ca-268">Si vous souhaitez un tooauthenticate client et vous connecter, vous devez tooinstall un nouveau certificat de client généré à partir d’un certificat racine approuvé tooAzure (téléchargé).</span><span class="sxs-lookup"><span data-stu-id="968ca-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="968ca-269"><a name="addtrustedroot"></a>tooadd un certificat racine approuvé</span><span class="sxs-lookup"><span data-stu-id="968ca-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="968ca-270">Vous pouvez ajouter jusqu'à tooAzure de fichiers too20 racine certificat .cer.</span><span class="sxs-lookup"><span data-stu-id="968ca-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="968ca-271">les étapes suivantes de Hello aide vous ajoutez un certificat racine :</span><span class="sxs-lookup"><span data-stu-id="968ca-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="968ca-272"><a name="certmethod1"></a>Méthode 1</span><span class="sxs-lookup"><span data-stu-id="968ca-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="968ca-273">Il s’agit de tooupload de méthode la plus efficace hello un certificat racine.</span><span class="sxs-lookup"><span data-stu-id="968ca-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="968ca-274">Préparer tooupload de fichier .cer hello :</span><span class="sxs-lookup"><span data-stu-id="968ca-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="968ca-275">Téléchargez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-275">Upload hello file.</span></span> <span data-ttu-id="968ca-276">Vous ne pouvez charger qu’un seul fichier à la fois.</span><span class="sxs-lookup"><span data-stu-id="968ca-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="968ca-277">tooverify ce fichier de certificat hello téléchargés :</span><span class="sxs-lookup"><span data-stu-id="968ca-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="968ca-278"><a name="certmethod2"></a>Méthode 2</span><span class="sxs-lookup"><span data-stu-id="968ca-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="968ca-279">Cette méthode est a davantage d’étapes que la méthode 1, mais a hello même résultat.</span><span class="sxs-lookup"><span data-stu-id="968ca-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="968ca-280">Il est inclus en cas de besoin des données du certificat tooview hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="968ca-281">Créer et préparer hello nouvelle racine certificat tooadd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="968ca-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="968ca-282">Exporter la clé publique de hello comme Base-64 encodé X.509 (. CER) et ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="968ca-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="968ca-283">Copiez les valeurs hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="968ca-283">Copy hello values, as shown in hello following example:</span></span>

  ![certificat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="968ca-285">Lors de la copie des données de certificat hello, assurez-vous que vous copiez le texte hello ligne continue sans les retours chariot ou les sauts de ligne.</span><span class="sxs-lookup"><span data-stu-id="968ca-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="968ca-286">Vous devrez peut-être toomodify votre affichage dans too'Show de l’éditeur de texte hello symbole/Afficher chariot de tous les caractères toosee hello retourne et sauts de ligne.</span><span class="sxs-lookup"><span data-stu-id="968ca-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="968ca-287">Spécifiez le nom du certificat hello et les informations de clé en tant que variable.</span><span class="sxs-lookup"><span data-stu-id="968ca-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="968ca-288">Remplacez les informations de hello avec vos propres, comme indiqué dans hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="968ca-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="968ca-289">Ajouter un nouveau certificat racine de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-289">Add hello new root certificate.</span></span> <span data-ttu-id="968ca-290">Vous ne pouvez ajouter qu’un seul certificat à la fois.</span><span class="sxs-lookup"><span data-stu-id="968ca-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="968ca-291">Vous pouvez vérifier qu’hello un nouveau certificat a été ajouté correctement à l’aide de hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="968ca-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="968ca-292"><a name="removerootcert"></a>tooremove un certificat racine</span><span class="sxs-lookup"><span data-stu-id="968ca-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="968ca-293">Déclarer des variables de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="968ca-294">Supprimer le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="968ca-295">Hello utilisation suivant tooverify exemple qui hello certificat a été correctement supprimé.</span><span class="sxs-lookup"><span data-stu-id="968ca-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="968ca-296"><a name="revoke"></a>Révocation d'un certificat client</span><span class="sxs-lookup"><span data-stu-id="968ca-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="968ca-297">Vous pouvez révoquer des certificats clients.</span><span class="sxs-lookup"><span data-stu-id="968ca-297">You can revoke client certificates.</span></span> <span data-ttu-id="968ca-298">certificat Hello liste de révocation vous permet de tooselectively refuser la connectivité de Point à Site basée sur des certificats clients individuels.</span><span class="sxs-lookup"><span data-stu-id="968ca-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="968ca-299">Cela est différent de la suppression d’un certificat racine approuvé.</span><span class="sxs-lookup"><span data-stu-id="968ca-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="968ca-300">Si vous supprimez un .cer du certificat racine approuvé à partir d’Azure, il révoque l’accès de hello pour tous les certificats du client généré/signé par le certificat racine révoqués de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="968ca-301">Révoquer un certificat client, au lieu de certificat racine hello permet hello autres certificats générés à partir de hello racine certificat toocontinue toobe utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="968ca-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="968ca-302">courant Hello est toouse hello racine certificat toomanage l’accès aux niveaux d’équipe ou organisation, lors de l’utilisation des certificats clients révoqués de contrôle d’accès précis sur les utilisateurs individuels.</span><span class="sxs-lookup"><span data-stu-id="968ca-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="968ca-303"><a name="revokeclientcert"></a>toorevoke un certificat client</span><span class="sxs-lookup"><span data-stu-id="968ca-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="968ca-304">Récupérer l’empreinte de certificat client hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="968ca-305">Pour plus d’informations, consultez [comment tooretrieve hello empreinte d’un certificat](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="968ca-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="968ca-306">Éditeur de texte hello informations tooa de copie et supprimer tous les espaces afin qu’il soit une chaîne continue.</span><span class="sxs-lookup"><span data-stu-id="968ca-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="968ca-307">Cette chaîne est déclarée en tant que variable dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="968ca-308">Déclarer des variables de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-308">Declare hello variables.</span></span> <span data-ttu-id="968ca-309">Vérifiez l’empreinte numérique de hello toodeclare que vous avez récupéré à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="968ca-310">Ajoutez hello empreinte toohello liste de certificats révoqués.</span><span class="sxs-lookup"><span data-stu-id="968ca-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="968ca-311">Vous voyez « Réussi » lorsque l’empreinte numérique hello a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="968ca-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="968ca-312">Vérifiez que l’empreinte numérique hello a été ajouté toohello liste de révocation de certificats.</span><span class="sxs-lookup"><span data-stu-id="968ca-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="968ca-313">Après avoir ajouté l’empreinte numérique hello, certificat de hello ne peut plus être utilisé tooconnect.</span><span class="sxs-lookup"><span data-stu-id="968ca-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="968ca-314">Les clients qui tentent de tooconnect à l’aide de ce certificat recevoir un message indiquant que ce certificat hello n’est plus valide.</span><span class="sxs-lookup"><span data-stu-id="968ca-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="968ca-315"><a name="reinstateclientcert"></a>tooreinstate un certificat client</span><span class="sxs-lookup"><span data-stu-id="968ca-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="968ca-316">Vous pouvez le rétablir sous un certificat client en supprimant l’empreinte numérique hello à partir de la liste de hello des certificats clients révoqués.</span><span class="sxs-lookup"><span data-stu-id="968ca-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="968ca-317">Déclarer des variables de hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-317">Declare hello variables.</span></span> <span data-ttu-id="968ca-318">Assurez-vous que vous déclarez hello correct l’empreinte numérique hello certificat que vous souhaitez tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="968ca-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="968ca-319">Supprimer l’empreinte numérique du certificat hello à partir de la liste de révocation de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="968ca-320">Vérifiez si l’empreinte numérique hello est supprimée à partir de la liste de révocation hello.</span><span class="sxs-lookup"><span data-stu-id="968ca-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="968ca-321"><a name="faq"></a>Forum Aux Questions sur les connexions point à site</span><span class="sxs-lookup"><span data-stu-id="968ca-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="968ca-322">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="968ca-322">Next steps</span></span>
<span data-ttu-id="968ca-323">Une fois que votre connexion est terminée, vous pouvez ajouter des machines virtuelles tooyour des réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="968ca-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="968ca-324">Pour plus d’informations, consultez [Machines virtuelles](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="968ca-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="968ca-325">toounderstand en savoir plus sur la mise en réseau et les machines virtuelles, consultez [vue d’ensemble du réseau Azure et Linux VM](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="968ca-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
