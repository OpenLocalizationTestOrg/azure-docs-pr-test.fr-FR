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
ms.openlocfilehash: 914f2e5d10aa341cea5eba8c24c7c37610e6b626
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="connect-to-azure-stack"></a>Se connecter à Azure Stack

Pour pouvoir gérer des ressources, vous devez vous connecter au Kit de développement Azure Stack. Cette rubrique explique en détail les étapes à suivre pour vous connecter à ce kit de développement. Vous avez le choix entre ces deux options de connexion :

* [Bureau à distance](#connect-with-remote-desktop) : permet à un seul utilisateur à la fois de se connecter rapidement à partir du kit de développement.
* [Réseau privé virtuel (VPN)](#connect-with-vpn) : permet à plusieurs utilisateurs de se connecter simultanément à partir de clients extérieurs à l’infrastructure Azure Stack (nécessite une configuration particulière).

## <a name="connect-to-azure-stack-with-remote-desktop"></a>Se connecter à Azure Stack avec l’option Bureau à distance
Avec une connexion Bureau à distance, un seul utilisateur à la fois peut se connecter au portail pour gérer des ressources.

1. Ouvrez une connexion Bureau à distance et connectez-vous au kit de développement. Entrez le nom d’utilisateur **AzureStack\AzureStackAdmin**, ainsi que le mot de passe d’administration que vous avez fourni au moment de l’installation d’Azure Stack.  

2. À partir de l’ordinateur du kit de développement, ouvrez le Gestionnaire de serveur, cliquez sur **Serveur local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.

3. Pour ouvrir le portail, accédez à (https://portal.local.azurestack.external/) et connectez-vous à l’aide des informations d’identification de l’utilisateur.


## <a name="connect-to-azure-stack-with-vpn"></a>Se connecter à Azure Stack avec l’option VPN

Vous pouvez établir une connexion VPN avec tunneling fractionné à un Kit de développement Azure Stack. Par le biais de la connexion VPN, vous pouvez accéder au portail de l’administrateur, au portail de l’utilisateur et à des outils installés localement, tels que Visual Studio et PowerShell, pour gérer des ressources Azure Stack. La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS). Les connexions VPN permettent à plusieurs clients de se connecter à Azure Stack en même temps. 

> [!NOTE] 
> Cette connexion VPN ne fournit pas de connectivité aux machines virtuelles de l’infrastructure Azure Stack. 

### <a name="prerequisites"></a>Composants requis

* Installez [Azure PowerShell pour Azure Stack](azure-stack-powershell-install.md) sur votre ordinateur local.  
* Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md). 

### <a name="configure-vpn-connectivity"></a>Configurer la connectivité VPN

Pour créer une connexion VPN au kit de développement, ouvrez une session PowerShell avec des privilèges élevés à partir de votre ordinateur Windows local, puis exécutez le script suivant (après avoir changé l’adresse IP et le mot de passe de manière appropriée pour votre environnement) :

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

Si vous avez correctement configuré la connexion, vous devez voir **azurestack** dans votre liste de connexions VPN.

![Connexions réseau](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-to-azure-stack"></a>Se connecter à Azure Stack

Connectez-vous à l’instance Azure Stack à l’aide d’une des deux méthodes suivantes :  

* Utilisez la commande `Connect-AzsVpn ` : 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  Quand vous y êtes invité, approuvez l’hôte Azure Stack et installez le certificat fourni par **AzureStackCertificateAuthority** dans le magasin de certificats de votre ordinateur local (l’invite s’affiche parfois derrière la fenêtre de session PowerShell). 

* Sur votre ordinateur local, ouvrez **Paramètres réseau** > **VPN** > cliquez sur **azurestack** > **Se connecter**. À l’invite de connexion, entrez le nom d’utilisateur (AzureStack\AzureStackAdmin) et le mot de passe.

### <a name="test-the-vpn-connectivity"></a>Tester la connectivité VPN

Pour tester la connexion au portail, ouvrez un navigateur Internet et accédez au portail de l’utilisateur (https://portal.local.azurestack.external/), connectez-vous et créez des ressources.  

## <a name="next-steps"></a>Étapes suivantes



