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
# <a name="connect-tooazure-stack"></a>Se connecter tooAzure pile

toomanage des ressources, vous devez vous connecter toohello Kit de développement de pile Azure. Cette rubrique détaille hello les mesures requises kit de développement tooconnect toohello. Vous pouvez utiliser une des hello suivant les options de connexion :

* [Bureau à distance](#connect-with-remote-desktop): permet à un seul utilisateur simultané rapidement vous connecter à partir du kit de développement hello.
* [Réseau privé virtuel (VPN, Virtual Private Network)](#connect-with-vpn): vous permet de connectent de plusieurs utilisateurs simultanément à partir de clients en dehors de l’infrastructure de pile de Azure hello (requiert une configuration).

## <a name="connect-tooazure-stack-with-remote-desktop"></a>Se connecter tooAzure pile avec le Bureau à distance
Avec une connexion Bureau à distance, un seul utilisateur simultané peut travailler avec des ressources toomanage portail hello.

1. Ouvrez une connexion Bureau à distance et se connecter du kit de développement toohello. Entrez **AzureStack\AzureStackAdmin** en tant que nom d’utilisateur hello et hello administratif un mot de passe que vous avez fourni pendant l’installation de la pile de Azure.  

2. À partir de l’ordinateur de kit de développement hello, ouvrez le Gestionnaire de serveur, cliquez sur **serveur Local**, désactivez la sécurité renforcée d’Internet Explorer, puis fermez le Gestionnaire de serveur.

3. utilisateur de hello tooopen [portal](azure-stack-key-features.md#portal), accédez trop (https://portal.local.azurestack.external/) et connectez-vous en utilisant les informations d’identification de l’utilisateur. administrateur de hello tooopen [portal](azure-stack-key-features.md#portal), accédez trop (https://adminportal.local.azurestack.external/) et connectez-vous à l’aide de hello des informations d’identification Azure Active Directory spécifiées pendant l’installation.

## <a name="connect-tooazure-stack-with-vpn"></a>Rejoignez tooAzure pile VPN

Vous pouvez établir un réseau privé virtuel (VPN) de fractionnement tunnel connexion tooan Kit de développement de pile Azure. Via hello connexion VPN, vous pourrez accéder au portail d’administration hello, portail de l’utilisateur et installé localement des outils tels que Visual Studio et les ressources de pile d’Azure PowerShell toomanage. La connectivité VPN est prise en charge dans les déploiements Azure Active Directory (AAD) et Active Directory Federation Services (AD FS). Connexions VPN permettent à plusieurs clients tooconnect tooAzure pile à hello même temps. 

> [!NOTE] 
> Cette connexion VPN ne fournit pas d’infrastructure de pile tooAzure connexion machines virtuelles. 

### <a name="prerequisites"></a>Composants requis

* Installez [Azure PowerShell pour Azure Stack](azure-stack-powershell-install.md) sur votre ordinateur local.  
* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md). 

### <a name="configure-vpn-connectivity"></a>Configurer la connectivité VPN

toocreate un kit de développement toohello de connexion VPN, ouvrez une session PowerShell avec élévation de privilèges à partir de votre ordinateur Windows local et l’exécution hello script (Assurez-vous que tooupdate hello hello IP adresse et le mot de passe valeurs pour votre environnement) suivant :

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

Si hello configurer réussit, vous devez voir **azurestack** dans la liste des connexions VPN.

![Connexions réseau](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a>Se connecter tooAzure pile

Connecter l’instance d’Azure pile toohello à l’aide d’une des deux méthodes suivantes de hello :  

* À l’aide de hello `Connect-AzsVpn ` commande : 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  Lorsque vous y êtes invité, approuver l’hôte de pile de Azure hello et installer le certificat hello à partir de **AzureStackCertificateAuthority** sur le magasin de certificats de votre ordinateur local. (invite de hello peut s’afficher derrière la fenêtre de session PowerShell hello). 

* Sur votre ordinateur local, ouvrez **Paramètres réseau** > **VPN** > cliquez sur **azurestack** > **Se connecter**. À hello connectez-vous invite, entrez le nom d’utilisateur de hello (AzureStack\AzureStackAdmin) et un mot de passe hello.

### <a name="test-hello-vpn-connectivity"></a>Hello de test connectivité VPN

tootest hello connexion avec le portail, ouvrez un navigateur Internet et accédez de portail de l’utilisateur hello tooeither (https://portal.local.azurestack.external/) ou le portail d’administration hello (https://adminportal.local.azurestack.external/), connectez-vous, puis créer ressources.  

## <a name="next-steps"></a>Étapes suivantes

[Rendre tooyour disponible des ordinateurs virtuels aux utilisateurs de pile de Azure](azure-stack-tutorial-tenant-vm.md)

