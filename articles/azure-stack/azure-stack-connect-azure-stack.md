---
title: "Se connecter à Azure Stack | Microsoft Docs"
description: "Découvrez comment vous connecter à Azure Stack"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 44b167972ceffc8de48ae7560b85009a96378144
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="4bda4-103">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4bda4-103">Connect to Azure Stack</span></span>

<span data-ttu-id="4bda4-104">Pour pouvoir gérer des ressources, vous devez vous connecter au Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="4bda4-104">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="4bda4-105">Cette rubrique explique en détail les étapes à suivre pour vous connecter à ce kit de développement.</span><span class="sxs-lookup"><span data-stu-id="4bda4-105">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="4bda4-106">Vous avez le choix entre ces deux options de connexion :</span><span class="sxs-lookup"><span data-stu-id="4bda4-106">You can use either of the following connection options:</span></span>

* <span data-ttu-id="4bda4-107">[Bureau à distance](#connect-with-remote-desktop) : permet à un seul utilisateur à la fois de se connecter rapidement à partir du kit de développement.</span><span class="sxs-lookup"><span data-stu-id="4bda4-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="4bda4-108">[Réseau privé virtuel (VPN)](#connect-with-vpn) : permet à plusieurs utilisateurs de se connecter simultanément à partir de clients extérieurs à l’infrastructure Azure Stack (nécessite une configuration particulière).</span><span class="sxs-lookup"><span data-stu-id="4bda4-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="4bda4-109">Se connecter à Azure Stack avec l’option Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="4bda4-109">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="4bda4-110">Avec une connexion Bureau à distance, un seul utilisateur à la fois peut se connecter au portail pour gérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="4bda4-110">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="4bda4-111">Ouvrez une connexion Bureau à distance et connectez-vous au kit de développement.</span><span class="sxs-lookup"><span data-stu-id="4bda4-111">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="4bda4-112">Entrez **AzureStack\AzureStackAdmin** en tant que le nom d’utilisateur et le mot de passe d’administration que vous avez fourni pendant l’installation de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bda4-112">Enter **AzureStack\AzureStackAdmin** as the username, and the administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="4bda4-113">À partir de l’ordinateur du kit de développement, ouvrez le Gestionnaire de serveur, cliquez sur **Serveur local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.</span><span class="sxs-lookup"><span data-stu-id="4bda4-113">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="4bda4-114">Pour ouvrir le [portail](azure-stack-key-features.md#portal) de l’utilisateur, accédez à https://portal.local.azurestack.external/ et connectez-vous à l’aide des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4bda4-114">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="4bda4-115">Pour ouvrir l’administrateur [portal](azure-stack-key-features.md#portal), accédez au (https://adminportal.local.azurestack.external/) et connectez-vous avec les informations d’identification Azure Active Directory spécifiées pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="4bda4-115">To open the administrator [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="4bda4-116">Se connecter à Azure Stack avec l’option VPN</span><span class="sxs-lookup"><span data-stu-id="4bda4-116">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="4bda4-117">Vous pouvez établir une connexion VPN avec tunneling fractionné à un Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="4bda4-117">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="4bda4-118">Via la connexion VPN, vous pouvez accéder au portail d’administrateur, portail de l’utilisateur et installé localement des outils tels que Visual Studio et PowerShell pour gérer les ressources de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="4bda4-118">Through the VPN connection, you can access the administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="4bda4-119">La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="4bda4-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="4bda4-120">Les connexions VPN permettent à plusieurs clients de se connecter à Azure Stack en même temps.</span><span class="sxs-lookup"><span data-stu-id="4bda4-120">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4bda4-121">Cette connexion VPN ne fournit pas de connectivité aux machines virtuelles de l’infrastructure Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="4bda4-121">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="4bda4-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4bda4-122">Prerequisites</span></span>

* <span data-ttu-id="4bda4-123">Installez [Azure PowerShell pour Azure Stack](azure-stack-powershell-install.md) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="4bda4-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="4bda4-124">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="4bda4-124">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="4bda4-125">Configurer la connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="4bda4-125">Configure VPN connectivity</span></span>

<span data-ttu-id="4bda4-126">Pour créer une connexion VPN au kit de développement, ouvrez une session PowerShell avec des privilèges élevés à partir de votre ordinateur Windows local, puis exécutez le script suivant (après avoir changé l’adresse IP et le mot de passe de manière appropriée pour votre environnement) :</span><span class="sxs-lookup"><span data-stu-id="4bda4-126">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for the local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="4bda4-127">Si vous avez correctement configuré la connexion, vous devez voir **azurestack** dans votre liste de connexions VPN.</span><span class="sxs-lookup"><span data-stu-id="4bda4-127">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Connexions réseau](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="4bda4-129">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4bda4-129">Connect to Azure Stack</span></span>

<span data-ttu-id="4bda4-130">Connectez-vous à l’instance Azure Stack à l’aide d’une des deux méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4bda4-130">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="4bda4-131">Utilisez la commande `Connect-AzsVpn ` :</span><span class="sxs-lookup"><span data-stu-id="4bda4-131">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="4bda4-132">Quand vous y êtes invité, approuvez l’hôte Azure Stack et installez le certificat fourni par **AzureStackCertificateAuthority** dans le magasin de certificats de votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="4bda4-132">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="4bda4-133">(l’invite s’affiche parfois derrière la fenêtre de session PowerShell).</span><span class="sxs-lookup"><span data-stu-id="4bda4-133">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="4bda4-134">Sur votre ordinateur local, ouvrez **Paramètres réseau** > **VPN** > cliquez sur **azurestack** > **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="4bda4-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="4bda4-135">À l’invite de connexion, entrez le nom d’utilisateur (AzureStack\AzureStackAdmin) et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4bda4-135">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="4bda4-136">Tester la connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="4bda4-136">Test the VPN connectivity</span></span>

<span data-ttu-id="4bda4-137">Pour tester la connexion avec le portail, ouvrez un navigateur Internet et accédez au portail de l’utilisateur (https://portal.local.azurestack.external/) ou sur le portail d’administration (https://adminportal.local.azurestack.external/), se connecter et créer des ressources.</span><span class="sxs-lookup"><span data-stu-id="4bda4-137">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="4bda4-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4bda4-138">Next steps</span></span>

[<span data-ttu-id="4bda4-139">Mettre des machines virtuelles à la disposition de vos utilisateurs Azure Stack</span><span class="sxs-lookup"><span data-stu-id="4bda4-139">Make virtual machines available to your Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

