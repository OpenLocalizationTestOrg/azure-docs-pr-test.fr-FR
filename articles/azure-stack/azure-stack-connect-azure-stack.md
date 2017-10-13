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
ms.date: 09/25/2017
ms.author: sngun
ms.openlocfilehash: 09c626e97832821009ce2da360ceea2b54273ffa
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="connect-to-azure-stack"></a><span data-ttu-id="aa3d2-103">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="aa3d2-103">Connect to Azure Stack</span></span>

<span data-ttu-id="aa3d2-104">*S’applique à : Kit de développement Azure Stack*</span><span class="sxs-lookup"><span data-stu-id="aa3d2-104">*Applies to: Azure Stack Development Kit*</span></span>

<span data-ttu-id="aa3d2-105">Pour pouvoir gérer des ressources, vous devez vous connecter au Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-105">To manage resources, you must connect to the Azure Stack Development Kit.</span></span> <span data-ttu-id="aa3d2-106">Cette rubrique explique en détail les étapes à suivre pour vous connecter à ce kit de développement.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-106">This topic details the steps required to connect to the development kit.</span></span> <span data-ttu-id="aa3d2-107">Vous avez le choix entre ces deux options de connexion :</span><span class="sxs-lookup"><span data-stu-id="aa3d2-107">You can use either of the following connection options:</span></span>

* <span data-ttu-id="aa3d2-108">[Bureau à distance](#connect-with-remote-desktop) : permet à un seul utilisateur à la fois de se connecter rapidement à partir du kit de développement.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-108">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from the development kit.</span></span>
* <span data-ttu-id="aa3d2-109">[Réseau privé virtuel (VPN)](#connect-with-vpn) : permet à plusieurs utilisateurs de se connecter simultanément à partir de clients extérieurs à l’infrastructure Azure Stack (nécessite une configuration particulière).</span><span class="sxs-lookup"><span data-stu-id="aa3d2-109">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of the Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-to-azure-stack-with-remote-desktop"></a><span data-ttu-id="aa3d2-110">Se connecter à Azure Stack avec l’option Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="aa3d2-110">Connect to Azure Stack with Remote Desktop</span></span>
<span data-ttu-id="aa3d2-111">Avec une connexion Bureau à distance, un seul utilisateur à la fois peut se connecter au portail pour gérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-111">With a Remote Desktop connection, a single concurrent user can work with the portal to manage resources.</span></span>

1. <span data-ttu-id="aa3d2-112">Ouvrez une connexion Bureau à distance et connectez-vous au kit de développement.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-112">Open a Remote Desktop Connection and connect to the development kit.</span></span> <span data-ttu-id="aa3d2-113">Entrez le nom d’utilisateur **AzureStack\AzureStackAdmin**, ainsi que le mot de passe de l’opérateur que vous avez fourni au moment de l’installation d’Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-113">Enter **AzureStack\AzureStackAdmin** as the username, and the operator's password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="aa3d2-114">À partir de l’ordinateur du kit de développement, ouvrez le Gestionnaire de serveur, cliquez sur **Serveur local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-114">From the development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="aa3d2-115">Pour ouvrir le [portail](azure-stack-key-features.md#portal) de l’utilisateur, accédez à https://portal.local.azurestack.external/ et connectez-vous à l’aide des informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-115">To open the user [portal](azure-stack-key-features.md#portal), navigate to (https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="aa3d2-116">Pour ouvrir le [portail](azure-stack-key-features.md#portal) de l’opérateur Azure Stack, accédez à https://adminportal.local.azurestack.external/ et connectez-vous à l’aide des informations d’identification Azure Active Directory spécifiées pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-116">To open the Azure Stack operator's [portal](azure-stack-key-features.md#portal), navigate to (https://adminportal.local.azurestack.external/) and sign in using the Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-to-azure-stack-with-vpn"></a><span data-ttu-id="aa3d2-117">Se connecter à Azure Stack avec l’option VPN</span><span class="sxs-lookup"><span data-stu-id="aa3d2-117">Connect to Azure Stack with VPN</span></span>

<span data-ttu-id="aa3d2-118">Vous pouvez établir une connexion VPN avec tunneling fractionné à un Kit de développement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-118">You can establish a split tunnel Virtual Private Network (VPN) connection to an Azure Stack Development Kit.</span></span> <span data-ttu-id="aa3d2-119">Par le biais de la connexion VPN, vous pouvez ensuite accéder au portail de l’opérateur Azure Stack, au portail de l’utilisateur et à des outils installés localement, tels que Visual Studio et PowerShell, pour gérer des ressources Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-119">Through the VPN connection, you can access the Azure Stack operator's portal, user portal, and locally installed tools such as Visual Studio and PowerShell to manage Azure Stack resources.</span></span> <span data-ttu-id="aa3d2-120">La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="aa3d2-120">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="aa3d2-121">Les connexions VPN permettent à plusieurs clients de se connecter à Azure Stack en même temps.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-121">VPN connections enable multiple clients to connect to Azure Stack at the same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="aa3d2-122">Cette connexion VPN ne fournit pas de connectivité aux machines virtuelles de l’infrastructure Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-122">This VPN connection does not provide connectivity to Azure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="aa3d2-123">Composants requis</span><span class="sxs-lookup"><span data-stu-id="aa3d2-123">Prerequisites</span></span>

* <span data-ttu-id="aa3d2-124">Installez [Azure PowerShell pour Azure Stack](azure-stack-powershell-install.md) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-124">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="aa3d2-125">Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="aa3d2-125">Download the [tools required to work with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="aa3d2-126">Configurer la connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="aa3d2-126">Configure VPN connectivity</span></span>

<span data-ttu-id="aa3d2-127">Pour créer une connexion VPN au kit de développement, ouvrez une session PowerShell avec des privilèges élevés à partir de votre ordinateur Windows local, puis exécutez le script suivant (après avoir changé l’adresse IP et le mot de passe de manière appropriée pour votre environnement) :</span><span class="sxs-lookup"><span data-stu-id="aa3d2-127">To create a VPN connection to the development kit, open an elevated PowerShell session from your local Windows-based computer and run the following script (make sure to update the the IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import the Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add the development kit computer’s host IP address & certificate authority (CA) to the list of trusted hosts. Make sure to update the the IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<operator's password provided when deploying Azure Stack>" `
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

<span data-ttu-id="aa3d2-128">Si vous avez correctement configuré la connexion, vous devez voir **azurestack** dans votre liste de connexions VPN.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-128">If the set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Connexions réseau](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a><span data-ttu-id="aa3d2-130">Se connecter à Azure Stack</span><span class="sxs-lookup"><span data-stu-id="aa3d2-130">Connect to Azure Stack</span></span>

<span data-ttu-id="aa3d2-131">Connectez-vous à l’instance Azure Stack à l’aide d’une des deux méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="aa3d2-131">Connect to the Azure Stack instance by using either of the following two methods:</span></span>  

* <span data-ttu-id="aa3d2-132">Utilisez la commande `Connect-AzsVpn ` :</span><span class="sxs-lookup"><span data-stu-id="aa3d2-132">By using the `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="aa3d2-133">Quand vous y êtes invité, approuvez l’hôte Azure Stack et installez le certificat fourni par **AzureStackCertificateAuthority** dans le magasin de certificats de votre ordinateur local</span><span class="sxs-lookup"><span data-stu-id="aa3d2-133">When prompted, trust the Azure Stack host and install the certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="aa3d2-134">(l’invite s’affiche parfois derrière la fenêtre de session PowerShell).</span><span class="sxs-lookup"><span data-stu-id="aa3d2-134">(the prompt might appear behind the PowerShell session window).</span></span> 

* <span data-ttu-id="aa3d2-135">Sur votre ordinateur local, ouvrez **Paramètres réseau** > **VPN** > cliquez sur **azurestack** > **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-135">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="aa3d2-136">À l’invite de connexion, entrez le nom d’utilisateur (AzureStack\AzureStackAdmin) et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-136">At the sign-in prompt, enter the username (AzureStack\AzureStackAdmin) and the password.</span></span>

### <a name="test-the-vpn-connectivity"></a><span data-ttu-id="aa3d2-137">Tester la connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="aa3d2-137">Test the VPN connectivity</span></span>

<span data-ttu-id="aa3d2-138">Pour tester la connexion au portail, ouvrez un navigateur Internet et accédez au portail de l’utilisateur (https://portal.local.azurestack.external/) ou au portail de l’opérateur (https://adminportal.local.azurestack.external/), connectez-vous et créez des ressources.</span><span class="sxs-lookup"><span data-stu-id="aa3d2-138">To test the portal connection, open an Internet browser and navigate to either the user portal (https://portal.local.azurestack.external/) or the operator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="aa3d2-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aa3d2-139">Next steps</span></span>

[<span data-ttu-id="aa3d2-140">Mettre des machines virtuelles à la disposition de vos utilisateurs Azure Stack</span><span class="sxs-lookup"><span data-stu-id="aa3d2-140">Make virtual machines available to your Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

