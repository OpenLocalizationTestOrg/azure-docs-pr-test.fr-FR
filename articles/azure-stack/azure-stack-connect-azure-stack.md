---
title: aaaConnect tooAzure pile | Documents Microsoft
description: "Découvrez comment tooconnect Azure de la pile"
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
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a><span data-ttu-id="e2c40-103">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="e2c40-103">Connect tooAzure Stack</span></span>

<span data-ttu-id="e2c40-104">toomanage des ressources, vous devez vous connecter toohello Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="e2c40-104">toomanage resources, you must connect toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="e2c40-105">Cette rubrique détaille hello les mesures requises kit de développement tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="e2c40-105">This topic details hello steps required tooconnect toohello development kit.</span></span> <span data-ttu-id="e2c40-106">Vous pouvez utiliser une des hello suivant les options de connexion :</span><span class="sxs-lookup"><span data-stu-id="e2c40-106">You can use either of hello following connection options:</span></span>

* <span data-ttu-id="e2c40-107">[Bureau à distance](#connect-with-remote-desktop): permet à un seul utilisateur simultané rapidement vous connecter à partir du kit de développement hello.</span><span class="sxs-lookup"><span data-stu-id="e2c40-107">[Remote Desktop](#connect-with-remote-desktop): lets a single concurrent user quickly connect from hello development kit.</span></span>
* <span data-ttu-id="e2c40-108">[Réseau privé virtuel (VPN, Virtual Private Network)](#connect-with-vpn): vous permet de connectent de plusieurs utilisateurs simultanément à partir de clients en dehors de l’infrastructure de pile de Azure hello (requiert une configuration).</span><span class="sxs-lookup"><span data-stu-id="e2c40-108">[Virtual Private Network (VPN)](#connect-with-vpn): lets multiple concurrent users connect from clients outside of hello Azure Stack infrastructure (requires configuration).</span></span>

## <a name="connect-tooazure-stack-with-remote-desktop"></a><span data-ttu-id="e2c40-109">Se connecter tooAzure pile avec le Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="e2c40-109">Connect tooAzure Stack with Remote Desktop</span></span>
<span data-ttu-id="e2c40-110">Avec une connexion Bureau à distance, un seul utilisateur simultané peut travailler avec des ressources toomanage portail hello.</span><span class="sxs-lookup"><span data-stu-id="e2c40-110">With a Remote Desktop connection, a single concurrent user can work with hello portal toomanage resources.</span></span>

1. <span data-ttu-id="e2c40-111">Ouvrez une connexion Bureau à distance et se connecter du kit de développement toohello.</span><span class="sxs-lookup"><span data-stu-id="e2c40-111">Open a Remote Desktop Connection and connect toohello development kit.</span></span> <span data-ttu-id="e2c40-112">Entrez **AzureStack\AzureStackAdmin** en tant que nom d’utilisateur hello et hello administratif un mot de passe que vous avez fourni pendant l’installation de la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="e2c40-112">Enter **AzureStack\AzureStackAdmin** as hello username, and hello administrative password that you provided during Azure Stack setup.</span></span>  

2. <span data-ttu-id="e2c40-113">À partir de l’ordinateur de kit de développement hello, ouvrez le Gestionnaire de serveur, cliquez sur **serveur Local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.</span><span class="sxs-lookup"><span data-stu-id="e2c40-113">From hello development kit computer, open Server Manager, click **Local Server**, turn off Internet Explorer Enhanced Security, and then close Server Manager.</span></span>

3. <span data-ttu-id="e2c40-114">utilisateur de hello tooopen [portal](azure-stack-key-features.md#portal), accédez trop (https://portal.local.azurestack.external/) et connectez-vous en utilisant les informations d’identification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2c40-114">tooopen hello user [portal](azure-stack-key-features.md#portal), navigate too(https://portal.local.azurestack.external/) and sign in using user credentials.</span></span> <span data-ttu-id="e2c40-115">administrateur de hello tooopen [portal](azure-stack-key-features.md#portal), accédez trop (https://adminportal.local.azurestack.external/) et connectez-vous à l’aide de hello des informations d’identification Azure Active Directory spécifiées pendant l’installation.</span><span class="sxs-lookup"><span data-stu-id="e2c40-115">tooopen hello administrator [portal](azure-stack-key-features.md#portal), navigate too(https://adminportal.local.azurestack.external/) and sign in using hello Azure Active Directory credentials specified during installation.</span></span>

## <a name="connect-tooazure-stack-with-vpn"></a><span data-ttu-id="e2c40-116">Rejoignez tooAzure pile VPN</span><span class="sxs-lookup"><span data-stu-id="e2c40-116">Connect tooAzure Stack with VPN</span></span>

<span data-ttu-id="e2c40-117">Vous pouvez établir un réseau privé virtuel (VPN) de fractionnement tunnel connexion tooan Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="e2c40-117">You can establish a split tunnel Virtual Private Network (VPN) connection tooan Azure Stack Development Kit.</span></span> <span data-ttu-id="e2c40-118">Via hello connexion VPN, vous pourrez accéder au portail d’administration hello, portail de l’utilisateur et installé localement des outils tels que Visual Studio et les ressources de pile d’Azure PowerShell toomanage.</span><span class="sxs-lookup"><span data-stu-id="e2c40-118">Through hello VPN connection, you can access hello administrator portal, user portal, and locally installed tools such as Visual Studio and PowerShell toomanage Azure Stack resources.</span></span> <span data-ttu-id="e2c40-119">La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS).</span><span class="sxs-lookup"><span data-stu-id="e2c40-119">VPN connectivity is supported in both Azure Active Directory(AAD) and Active Directory Federation Services(AD FS) based deployments.</span></span> <span data-ttu-id="e2c40-120">Connexions VPN permettent à plusieurs clients tooconnect tooAzure pile à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="e2c40-120">VPN connections enable multiple clients tooconnect tooAzure Stack at hello same time.</span></span> 

> [!NOTE] 
> <span data-ttu-id="e2c40-121">Cette connexion VPN ne fournit pas d’infrastructure de pile tooAzure connexion machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e2c40-121">This VPN connection does not provide connectivity tooAzure Stack infrastructure VMs.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="e2c40-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2c40-122">Prerequisites</span></span>

* <span data-ttu-id="e2c40-123">Installez [Azure PowerShell pour Azure Stack](azure-stack-powershell-install.md) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e2c40-123">Install [Azure Stack compatible Azure PowerShell](azure-stack-powershell-install.md) on your local computer.</span></span>  
* <span data-ttu-id="e2c40-124">Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).</span><span class="sxs-lookup"><span data-stu-id="e2c40-124">Download hello [tools required toowork with Azure Stack](azure-stack-powershell-download.md).</span></span> 

### <a name="configure-vpn-connectivity"></a><span data-ttu-id="e2c40-125">Configurer la connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="e2c40-125">Configure VPN connectivity</span></span>

<span data-ttu-id="e2c40-126">toocreate un kit de développement toohello de connexion VPN, ouvrez une session PowerShell avec élévation de privilèges à partir de votre ordinateur Windows local et l’exécution hello script (Assurez-vous que tooupdate hello hello IP adresse et le mot de passe valeurs pour votre environnement) suivant :</span><span class="sxs-lookup"><span data-stu-id="e2c40-126">toocreate a VPN connection toohello development kit, open an elevated PowerShell session from your local Windows-based computer and run hello following script (make sure tooupdate hello hello IP address and password values for your environment):</span></span>

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

<span data-ttu-id="e2c40-127">Si hello configurer réussit, vous devez voir **azurestack** dans la liste des connexions VPN.</span><span class="sxs-lookup"><span data-stu-id="e2c40-127">If hello set up succeeds, you should see **azurestack** in your list of VPN connections.</span></span>

![Connexions réseau](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a><span data-ttu-id="e2c40-129">Se connecter tooAzure pile</span><span class="sxs-lookup"><span data-stu-id="e2c40-129">Connect tooAzure Stack</span></span>

<span data-ttu-id="e2c40-130">Connecter l’instance d’Azure pile toohello à l’aide d’une des deux méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="e2c40-130">Connect toohello Azure Stack instance by using either of hello following two methods:</span></span>  

* <span data-ttu-id="e2c40-131">À l’aide de hello `Connect-AzsVpn ` commande :</span><span class="sxs-lookup"><span data-stu-id="e2c40-131">By using hello `Connect-AzsVpn ` command:</span></span> 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  <span data-ttu-id="e2c40-132">Lorsque vous y êtes invité, approuver l’hôte de pile de Azure hello et installer le certificat hello à partir de **AzureStackCertificateAuthority** sur le magasin de certificats de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e2c40-132">When prompted, trust hello Azure Stack host and install hello certificate from **AzureStackCertificateAuthority** onto your local computer’s certificate store.</span></span> <span data-ttu-id="e2c40-133">(invite de hello peut s’afficher derrière la fenêtre de session PowerShell hello).</span><span class="sxs-lookup"><span data-stu-id="e2c40-133">(hello prompt might appear behind hello PowerShell session window).</span></span> 

* <span data-ttu-id="e2c40-134">Sur votre ordinateur local, ouvrez **Paramètres réseau** > **VPN** > cliquez sur **azurestack** > **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="e2c40-134">Open your local computer’s **Network Settings** > **VPN** > click **azurestack** > **connect**.</span></span> <span data-ttu-id="e2c40-135">À hello connectez-vous invite, entrez le nom d’utilisateur de hello (AzureStack\AzureStackAdmin) et un mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="e2c40-135">At hello sign-in prompt, enter hello username (AzureStack\AzureStackAdmin) and hello password.</span></span>

### <a name="test-hello-vpn-connectivity"></a><span data-ttu-id="e2c40-136">Hello de test connectivité VPN</span><span class="sxs-lookup"><span data-stu-id="e2c40-136">Test hello VPN connectivity</span></span>

<span data-ttu-id="e2c40-137">tootest hello connexion avec le portail, ouvrez un navigateur Internet et accédez de portail de l’utilisateur hello tooeither (https://portal.local.azurestack.external/) ou le portail d’administration hello (https://adminportal.local.azurestack.external/), connectez-vous, puis créer ressources.</span><span class="sxs-lookup"><span data-stu-id="e2c40-137">tootest hello portal connection, open an Internet browser and navigate tooeither hello user portal (https://portal.local.azurestack.external/) or hello administrator portal (https://adminportal.local.azurestack.external/), sign in and create resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e2c40-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2c40-138">Next steps</span></span>

[<span data-ttu-id="e2c40-139">Rendre tooyour disponible des ordinateurs virtuels aux utilisateurs de pile de Azure</span><span class="sxs-lookup"><span data-stu-id="e2c40-139">Make virtual machines available tooyour Azure Stack users</span></span>](azure-stack-tutorial-tenant-vm.md)

