---
title: "modèles d’aaaDeploy avec PowerShell dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment toodeploy un ordinateur virtuel à l’aide d’un modèle de gestionnaire de ressources et de PowerShell."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 12fe32d7-0a1a-4c02-835d-7b97f151ed0f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: fb0d4b190e058b3c5c1273b6c91fc3d72dedeb1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-powershell"></a><span data-ttu-id="11316-103">Déployer des modèles dans Azure Stack à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="11316-103">Deploy templates in Azure Stack using PowerShell</span></span>
<span data-ttu-id="11316-104">Utilisez PowerShell toodeploy Azure Resource Manager modèles toohello Kit de développement de pile Azure.</span><span class="sxs-lookup"><span data-stu-id="11316-104">Use PowerShell toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span>  <span data-ttu-id="11316-105">Les modèles Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.</span><span class="sxs-lookup"><span data-stu-id="11316-105">Resource Manager templates deploy and provision all resources for your application in a single, coordinated operation.</span></span>

## <a name="run-azurerm-powershell-cmdlets"></a><span data-ttu-id="11316-106">Exécuter les applets de commande AzureRM PowerShell</span><span class="sxs-lookup"><span data-stu-id="11316-106">Run AzureRM PowerShell cmdlets</span></span>
<span data-ttu-id="11316-107">Dans cet exemple, vous exécutez un script toodeploy un tooAzure de l’ordinateur virtuel à l’aide d’un modèle de gestionnaire de ressources du Kit de développement de pile.</span><span class="sxs-lookup"><span data-stu-id="11316-107">In this example, you run a script toodeploy a virtual machine tooAzure Stack Development Kit using a Resource Manager template.</span></span>  <span data-ttu-id="11316-108">Avant de continuer, vérifiez que vous avez [configuré PowerShell](azure-stack-powershell-configure-user.md)</span><span class="sxs-lookup"><span data-stu-id="11316-108">Before proceeding, ensure you have [configured PowerShell](azure-stack-powershell-configure-user.md)</span></span>  

<span data-ttu-id="11316-109">Hello disque dur virtuel utilisé dans cet exemple de modèle est Windows Server 2012 R2 centres.</span><span class="sxs-lookup"><span data-stu-id="11316-109">hello VHD used in this example template is WindowsServer-2012-R2-Datacenter.</span></span>

1. <span data-ttu-id="11316-110">Accédez trop<http://aka.ms/AzureStackGitHub>, recherchez hello **101-simple-windows-vm** modèle et enregistrez-le toohello l’emplacement suivant : c :\\modèles\\ azuredeploy-101-simple-windows-vm.json.</span><span class="sxs-lookup"><span data-stu-id="11316-110">Go too<http://aka.ms/AzureStackGitHub>, search for hello **101-simple-windows-vm** template, and save it toohello following location: c:\\templates\\azuredeploy-101-simple-windows-vm.json.</span></span>
2. <span data-ttu-id="11316-111">Dans PowerShell, exécutez hello suivant du script de déploiement.</span><span class="sxs-lookup"><span data-stu-id="11316-111">In PowerShell, run hello following deployment script.</span></span> <span data-ttu-id="11316-112">Remplacez *username* et *password* par votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="11316-112">Replace *username* and *password* with your username and password.</span></span> <span data-ttu-id="11316-113">Lors des utilisations ultérieures, incrémenter la valeur hello pour hello *$myNum* tooprevent paramètre remplacer votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="11316-113">On subsequent uses, increment hello value for hello *$myNum* parameter tooprevent overwriting your deployment.</span></span>
   
   ```PowerShell
       # Set Deployment Variables
       $myNum = "001" #Modify this per deployment
       $RGName = "myRG$myNum"
       $myLocation = "local"
   
       # Create Resource Group for Template Deployment
       New-AzureRmResourceGroup -Name $RGName -Location $myLocation
   
       # Deploy Simple IaaS Template
       New-AzureRmResourceGroupDeployment `
           -Name myDeployment$myNum `
           -ResourceGroupName $RGName `
           -TemplateFile c:\templates\azuredeploy-101-simple-windows-vm.json `
           -NewStorageAccountName mystorage$myNum `
           -DnsNameForPublicIP mydns$myNum `
           -AdminUsername <username> `
           -AdminPassword ("<password>" | ConvertTo-SecureString -AsPlainText -Force) `
           -VmName myVM$myNum `
           -WindowsOSVersion 2012-R2-Datacenter
   ```
3. <span data-ttu-id="11316-114">Ouvrez hello Azure pile portail, sur **Parcourir**, cliquez sur **virtuels**et recherchez votre nouvelle machine virtuelle (*myDeployment001*).</span><span class="sxs-lookup"><span data-stu-id="11316-114">Open hello Azure Stack portal, click **Browse**, click **Virtual machines**, and look for your new virtual machine (*myDeployment001*).</span></span>


## <a name="next-steps"></a><span data-ttu-id="11316-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11316-115">Next steps</span></span>
[<span data-ttu-id="11316-116">Déployer des modèles avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11316-116">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

