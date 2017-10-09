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
# <a name="deploy-templates-in-azure-stack-using-powershell"></a>Déployer des modèles dans Azure Stack à l’aide de PowerShell
Utilisez PowerShell toodeploy Azure Resource Manager modèles toohello Kit de développement de pile Azure.  Les modèles Resource Manager déploient et approvisionnent toutes les ressources de l’application en une seule opération coordonnée.

## <a name="run-azurerm-powershell-cmdlets"></a>Exécuter les applets de commande AzureRM PowerShell
Dans cet exemple, vous exécutez un script toodeploy un tooAzure de l’ordinateur virtuel à l’aide d’un modèle de gestionnaire de ressources du Kit de développement de pile.  Avant de continuer, vérifiez que vous avez [configuré PowerShell](azure-stack-powershell-configure-user.md)  

Hello disque dur virtuel utilisé dans cet exemple de modèle est Windows Server 2012 R2 centres.

1. Accédez trop<http://aka.ms/AzureStackGitHub>, recherchez hello **101-simple-windows-vm** modèle et enregistrez-le toohello l’emplacement suivant : c :\\modèles\\ azuredeploy-101-simple-windows-vm.json.
2. Dans PowerShell, exécutez hello suivant du script de déploiement. Remplacez *username* et *password* par votre nom d’utilisateur et votre mot de passe. Lors des utilisations ultérieures, incrémenter la valeur hello pour hello *$myNum* tooprevent paramètre remplacer votre déploiement.
   
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
3. Ouvrez hello Azure pile portail, sur **Parcourir**, cliquez sur **virtuels**et recherchez votre nouvelle machine virtuelle (*myDeployment001*).


## <a name="next-steps"></a>Étapes suivantes
[Déployer des modèles avec Visual Studio](azure-stack-deploy-template-visual-studio.md)

