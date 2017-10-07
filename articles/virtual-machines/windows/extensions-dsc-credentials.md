---
title: "informations d’identification d’aaaPassing tooAzure à l’aide de DSC | Documents Microsoft"
description: "Vue d’ensemble sur le passage en toute sécurité les informations d’identification virtuels tooAzure à l’aide de la Configuration d’état souhaité PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>Passer des informations d’identification toohello Azure Gestionnaire d’extensions DSC
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Cet article traite l’extension de Configuration d’état souhaité hello pour Azure. Vous trouverez une vue d’ensemble du Gestionnaire d’extensions hello DSC à [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="passing-in-credentials"></a>Passage d’informations d’identification
Dans le cadre du processus de configuration hello, vous devrez peut-être tooset des comptes d’utilisateurs, accéder aux services ou installer un programme dans un contexte utilisateur. toodo ces éléments, vous avez besoin des informations d’identification tooprovide. 

DSC permet des configurations paramétrables dans laquelle les informations d’identification sont passées dans la configuration de hello et stockées en toute sécurité dans les fichiers MOF. Hello Gestionnaire d’extensions Azure simplifie la gestion des informations d’identification en fournissant une gestion automatique de certificats. 

Tenez compte des hello script de configuration DSC qui crée un compte d’utilisateur local avec le mot de passe spécifié hello suivant :

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

Il est important tooinclude *nœud localhost* dans le cadre de la configuration de hello. Si cette instruction est manquante, hello étapes suivantes ne fonctionnent pas comme gestionnaire d’extensions hello recherche plus particulièrement d’instruction de localhost nœud hello. Il est également important de conversion de type hello de tooinclude *[PsCredential]*, comme ce type spécifique déclenche les informations d’identification de hello extension tooencrypt hello. 

Publier ce stockage tooblob de script :

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

Définir une extension de configuration DSC Azure hello et fournir des informations d’identification hello :

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>Sécurisation des informations d’identification
L’exécution de ce code invite à entrer les informations d’identification. Une fois celles-ci fournies, elles sont stockées en mémoire brièvement. Lorsqu’il est publié avec `Set-AzureVmDscExtension` applet de commande, il est transmis via HTTPS toohello machine virtuelle, où Azure stocke chiffrées sur le disque, à l’aide de certificats d’ordinateur virtuel local hello. Il est brièvement déchiffrée en mémoire et re-chiffrée toopass il tooDSC.

Ce comportement est différent de celui [à l’aide de configurations sécurisées sans le Gestionnaire d’extensions hello](https://msdn.microsoft.com/powershell/dsc/securemof). Hello environnement Azure offre un moyen tootransmit configuration de données en toute sécurité via les certificats. Lorsque vous utilisez le Gestionnaire d’extensions hello DSC, il n’existe aucun tooprovide besoin $CertificatePath ou un $CertificateID / entrée $Thumbprint dans ConfigurationData.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Examinez hello [modèle Azure Resource Manager pour l’extension de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Vous pouvez gérer avec PowerShell DSC, des fonctionnalités supplémentaires toofind [parcourir la galerie PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) pour plus de ressources DSC.

