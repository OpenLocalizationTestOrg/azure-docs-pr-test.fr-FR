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
# <a name="connect-to-azure-stack"></a>Se connecter à Azure Stack

Pour pouvoir gérer des ressources, vous devez vous connecter au Kit de développement Azure Stack. Cette rubrique explique en détail les étapes à suivre pour vous connecter à ce kit de développement. Vous avez le choix entre ces deux options de connexion :

* [Bureau à distance](#connect-with-remote-desktop) : permet à un seul utilisateur à la fois de se connecter rapidement à partir du kit de développement.
* [Réseau privé virtuel (VPN)](#connect-with-vpn) : permet à plusieurs utilisateurs de se connecter simultanément à partir de clients extérieurs à l’infrastructure Azure Stack (nécessite une configuration particulière).

## <a name="connect-to-azure-stack-with-remote-desktop"></a>Se connecter à Azure Stack avec l’option Bureau à distance
Avec une connexion Bureau à distance, un seul utilisateur à la fois peut se connecter au portail pour gérer des ressources.

1. Ouvrez une connexion Bureau à distance et connectez-vous au kit de développement. Entrez **AzureStack\AzureStackAdmin** en tant que le nom d’utilisateur et le mot de passe d’administration que vous avez fourni pendant l’installation de la pile de Azure.  

2. À partir de l’ordinateur du kit de développement, ouvrez le Gestionnaire de serveur, cliquez sur **Serveur local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.

3. Pour ouvrir le [portail](azure-stack-key-features.md#portal) de l’utilisateur, accédez à https://portal.local.azurestack.external/ et connectez-vous à l’aide des informations d’identification de l’utilisateur. Pour ouvrir l’administrateur [portal](azure-stack-key-features.md#portal), accédez au (https://adminportal.local.azurestack.external/) et connectez-vous avec les informations d’identification Azure Active Directory spécifiées pendant l’installation.

## <a name="connect-to-azure-stack-with-vpn"></a>Se connecter à Azure Stack avec l’option VPN

Vous pouvez établir une connexion VPN avec tunneling fractionné à un Kit de développement Azure Stack. Via la connexion VPN, vous pouvez accéder au portail d’administrateur, portail de l’utilisateur et installé localement des outils tels que Visual Studio et PowerShell pour gérer les ressources de la pile de Azure. La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS). Les connexions VPN permettent à plusieurs clients de se connecter à Azure Stack en même temps. 

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

Pour tester la connexion avec le portail, ouvrez un navigateur Internet et accédez au portail de l’utilisateur (https://portal.local.azurestack.external/) ou sur le portail d’administration (https://adminportal.local.azurestack.external/), se connecter et créer des ressources.  

## <a name="next-steps"></a>Étapes suivantes

[Mettre des machines virtuelles à la disposition de vos utilisateurs Azure Stack](azure-stack-tutorial-tenant-vm.md)

