---
title: "Transfert des informations d’identification à Azure à l’aide de DSC | Microsoft Docs"
description: "Vue d’ensemble du transfert sécurisé des informations d’identification aux machines virtuelles Azure à l’aide de la Configuration de l’état souhaité PowerShell"
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
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="68647-103">Transfert des informations d’identification au gestionnaire de l’extension de Configuration de l’état souhaité (DSC) Azure</span><span class="sxs-lookup"><span data-stu-id="68647-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="68647-104">Cet article traite de l’extension de Configuration de l’état souhaité pour Azure.</span><span class="sxs-lookup"><span data-stu-id="68647-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="68647-105">Vous trouverez une vue d’ensemble du gestionnaire de l’extension DSC dans [Présentation du gestionnaire de l’extension de Configuration de l’état souhaité Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68647-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="68647-106">Passage d’informations d’identification</span><span class="sxs-lookup"><span data-stu-id="68647-106">Passing in credentials</span></span>
<span data-ttu-id="68647-107">Dans le cadre du processus de configuration, vous devrez peut-être configurer des comptes d’utilisateur, accéder aux services ou installer un programme dans un contexte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68647-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="68647-108">Pour effectuer ces opérations, vous devez fournir les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="68647-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="68647-109">DSC permet d’effectuer des configurations paramétrables dans lesquelles les informations d’identification sont transmises à la configuration et stockées en toute sécurité dans les fichiers MOF.</span><span class="sxs-lookup"><span data-stu-id="68647-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="68647-110">Le Gestionnaire d’extensions Azure simplifie la gestion des informations d’identification en fournissant une gestion automatique des certificats.</span><span class="sxs-lookup"><span data-stu-id="68647-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="68647-111">Examinez le script de configuration DSC suivant qui crée un compte d’utilisateur local avec le mot de passe spécifié :</span><span class="sxs-lookup"><span data-stu-id="68647-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="68647-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="68647-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="68647-113">Il est important d’inclure l’ *hôte local du nœud* dans le cadre de la configuration.</span><span class="sxs-lookup"><span data-stu-id="68647-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="68647-114">Si cette instruction est manquante, les étapes suivantes ne fonctionnent pas, car le gestionnaire d’extensions recherche spécifiquement l’instruction relative à l’hôte local du nœud.</span><span class="sxs-lookup"><span data-stu-id="68647-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="68647-115">Il est également important d’inclure le caractère *[PsCredential]*, car ce type spécifique déclenche l’extension pour chiffrer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="68647-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="68647-116">Publiez ce script sur le stockage d’objets blob :</span><span class="sxs-lookup"><span data-stu-id="68647-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="68647-117">Définissez l’extension DSC Azure et fournissez les informations d’identification :</span><span class="sxs-lookup"><span data-stu-id="68647-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="68647-118">Sécurisation des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="68647-118">How credentials are secured</span></span>
<span data-ttu-id="68647-119">L’exécution de ce code invite à entrer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="68647-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="68647-120">Une fois celles-ci fournies, elles sont stockées en mémoire brièvement.</span><span class="sxs-lookup"><span data-stu-id="68647-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="68647-121">Lorsqu’elles sont publiées avec l’applet de commande `Set-AzureVmDscExtension` , elles sont transmises via le protocole HTTPS à la machine virtuelle, où elles sont stockées de manière chiffrée sur le disque par Azure, à l’aide du certificat local de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68647-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="68647-122">Elles sont ensuite déchiffrées brièvement en mémoire, puis rechiffrées pour leur transfert à DSC.</span><span class="sxs-lookup"><span data-stu-id="68647-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="68647-123">Ce comportement diffère de l’ [utilisation de configurations sécurisées sans le gestionnaire d’extensions](https://msdn.microsoft.com/powershell/dsc/securemof).</span><span class="sxs-lookup"><span data-stu-id="68647-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="68647-124">L’environnement Windows Azure permet de transmettre des données de configuration en toute sécurité via des certificats.</span><span class="sxs-lookup"><span data-stu-id="68647-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="68647-125">Lors de l’utilisation du gestionnaire d’extensions DSC, il est inutile de fournir une entrée $CertificatePath ou $CertificateID/$Thumbprint dans ConfigurationData.</span><span class="sxs-lookup"><span data-stu-id="68647-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="68647-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="68647-126">Next steps</span></span>
<span data-ttu-id="68647-127">Pour plus d’informations sur le gestionnaire d’extensions DSC Azure, voir [Présentation du gestionnaire d’extensions de configuration d’état souhaité Microsoft Azure](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68647-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="68647-128">Examinez le [modèle Azure Resource Manager pour l’extension DSC](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="68647-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="68647-129">Pour plus informations sur DSC PowerShell, [voir le centre de documentation PowerShell](https://msdn.microsoft.com/powershell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="68647-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="68647-130">Pour accéder aux fonctionnalités supplémentaires que vous pouvez gérer avec DSC PowerShell, [parcourez PowerShell Gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) pour voir des ressources DSC supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="68647-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

