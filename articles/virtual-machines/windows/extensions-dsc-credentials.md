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
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="38f22-103">Passer des informations d’identification toohello Azure Gestionnaire d’extensions DSC</span><span class="sxs-lookup"><span data-stu-id="38f22-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="38f22-104">Cet article traite l’extension de Configuration d’état souhaité hello pour Azure.</span><span class="sxs-lookup"><span data-stu-id="38f22-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="38f22-105">Vous trouverez une vue d’ensemble du Gestionnaire d’extensions hello DSC à [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38f22-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="38f22-106">Passage d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="38f22-106">Passing in credentials</span></span>
<span data-ttu-id="38f22-107">Dans le cadre du processus de configuration hello, vous devrez peut-être tooset des comptes d’utilisateurs, accéder aux services ou installer un programme dans un contexte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="38f22-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="38f22-108">toodo ces éléments, vous avez besoin des informations d’identification tooprovide.</span><span class="sxs-lookup"><span data-stu-id="38f22-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="38f22-109">DSC permet des configurations paramétrables dans laquelle les informations d’identification sont passées dans la configuration de hello et stockées en toute sécurité dans les fichiers MOF.</span><span class="sxs-lookup"><span data-stu-id="38f22-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="38f22-110">Hello Gestionnaire d’extensions Azure simplifie la gestion des informations d’identification en fournissant une gestion automatique de certificats.</span><span class="sxs-lookup"><span data-stu-id="38f22-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="38f22-111">Tenez compte des hello script de configuration DSC qui crée un compte d’utilisateur local avec le mot de passe spécifié hello suivant :</span><span class="sxs-lookup"><span data-stu-id="38f22-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="38f22-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="38f22-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="38f22-113">Il est important tooinclude *nœud localhost* dans le cadre de la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="38f22-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="38f22-114">Si cette instruction est manquante, hello étapes suivantes ne fonctionnent pas comme gestionnaire d’extensions hello recherche plus particulièrement d’instruction de localhost nœud hello.</span><span class="sxs-lookup"><span data-stu-id="38f22-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="38f22-115">Il est également important de conversion de type hello de tooinclude *[PsCredential]*, comme ce type spécifique déclenche les informations d’identification de hello extension tooencrypt hello.</span><span class="sxs-lookup"><span data-stu-id="38f22-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="38f22-116">Publier ce stockage tooblob de script :</span><span class="sxs-lookup"><span data-stu-id="38f22-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="38f22-117">Définir une extension de configuration DSC Azure hello et fournir des informations d’identification hello :</span><span class="sxs-lookup"><span data-stu-id="38f22-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="38f22-118">Sécurisation des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="38f22-118">How credentials are secured</span></span>
<span data-ttu-id="38f22-119">L’exécution de ce code invite à entrer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="38f22-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="38f22-120">Une fois celles-ci fournies, elles sont stockées en mémoire brièvement.</span><span class="sxs-lookup"><span data-stu-id="38f22-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="38f22-121">Lorsqu’il est publié avec `Set-AzureVmDscExtension` applet de commande, il est transmis via HTTPS toohello machine virtuelle, où Azure stocke chiffrées sur le disque, à l’aide de certificats d’ordinateur virtuel local hello.</span><span class="sxs-lookup"><span data-stu-id="38f22-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="38f22-122">Il est brièvement déchiffrée en mémoire et re-chiffrée toopass il tooDSC.</span><span class="sxs-lookup"><span data-stu-id="38f22-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="38f22-123">Ce comportement est différent de celui [à l’aide de configurations sécurisées sans le Gestionnaire d’extensions hello](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="38f22-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="38f22-124">Hello environnement Azure offre un moyen tootransmit configuration de données en toute sécurité via les certificats.</span><span class="sxs-lookup"><span data-stu-id="38f22-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="38f22-125">Lorsque vous utilisez le Gestionnaire d’extensions hello DSC, il n’existe aucun tooprovide besoin $CertificatePath ou un $CertificateID / entrée $Thumbprint dans ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="38f22-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38f22-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38f22-126">Next steps</span></span>
<span data-ttu-id="38f22-127">Pour plus d’informations sur le Gestionnaire d’extensions Azure DSC hello, consultez [Gestionnaire d’extensions Azure DSC Introduction toohello](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38f22-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="38f22-128">Examinez hello [modèle Azure Resource Manager pour l’extension de hello DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="38f22-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="38f22-129">Pour plus d’informations sur PowerShell DSC, [visitez le centre de documentation PowerShell hello](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="38f22-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="38f22-130">Vous pouvez gérer avec PowerShell DSC, des fonctionnalités supplémentaires toofind [parcourir la galerie PowerShell de hello](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) pour plus de ressources DSC.</span><span class="sxs-lookup"><span data-stu-id="38f22-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

