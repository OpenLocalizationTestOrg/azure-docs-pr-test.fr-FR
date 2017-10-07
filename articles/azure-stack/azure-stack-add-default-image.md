---
title: "marketplace Azure pile toohello de la machine virtuelle par défaut aaaAdd hello image | Documents Microsoft"
description: "Ajoutez le marketplace de la pile de Azure hello machine virtuelle de Windows Server 2016 par défaut image toohello."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a>Ajouter le marketplace Azure pile toohello hello Windows Server 2016 VM image

Par défaut, il ne sont pas toutes les images de machine virtuelle disponibles dans le marketplace d’Azure pile hello. administrateur du cloud Azure pile Hello doit ajouter un marketplace toohello d’image avant que les utilisateurs peuvent les utiliser. Vous pouvez ajouter le marketplace d’Azure pile hello Windows Server 2016 image toohello à l’aide d’une des deux méthodes suivantes de hello :

* [Ajouter l’image de hello en le téléchargeant à partir d’Azure Marketplace de hello](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -Utilisez cette option si vous opérez dans un scénario connecté et si vous avez enregistré votre instance de la pile d’Azure avec Azure.

* [Ajouter l’image de hello à l’aide de PowerShell](#add-the-image-by-using-powershell) -Utilisez cette option si vous avez déployé Azure pile dans un scénario déconnecté ou dans des scénarios avec une connectivité limitée.

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a>Ajouter l’image de hello en le téléchargeant à partir de hello Azure Marketplace

1. Après avoir déployé la pile d’Azure, connectez-vous tooyour Kit de développement de pile Azure.

2. Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure** 

3. Rechercher ou pour hello **Windows Server Datacenter 2016 – Eval** image > cliquez sur **télécharger**

   ![Télécharger l’image à partir d’Azure](media/azure-stack-add-default-image/download-image.png)

Une fois le téléchargement de hello terminé, hello image ajoutée toohello **Marketplace gestion** lame et il est également accessible à partir de hello **virtuels** panneau.

## <a name="add-hello-image-by-using-powershell"></a>Ajouter l’image de hello à l’aide de PowerShell

### <a name="prerequisites"></a>Composants requis 

Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Installez les [modules Azure PowerShell compatibles avec Azure Stack](azure-stack-powershell-install.md).  

* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).  

* Accédez toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 et télécharger version d’évaluation de Windows Server 2016 de hello. Lorsque vous y êtes invité, sélectionnez hello **ISO** version du téléchargement de hello. Toohello de chemin d’accès d’enregistrement hello téléchargement, qui est utilisé ultérieurement dans cette procédure. Cette étape nécessite une connectivité Internet.  

Maintenant, exécutez hello suivant marketplace de la pile de Azure étapes tooadd hello image toohello :
   
1. Importez les modules Azure Connect de pile et ComputeAdmin hello à l’aide de hello suivant de commandes :

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. Se connecter tooyour environnement Azure pile. De script suivante d’exécution hello selon si votre environnement Azure pile est déployé à l’aide d’AAD ou ADFS (Assurez-vous que tooreplace hello AAD nom_client) :  

   a. **Azure Active Directory**, utilisez hello suivant l’applet de commande :

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Active Directory Federation Services**, utilisez hello suivant l’applet de commande :
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. Ajouter le marketplace d’Azure pile hello Windows Server 2016 image toohello (Assurez-vous que tooreplace hello *Path_to_ISO* avec le chemin d’accès de hello toohello ISO WS2016 vous avez téléchargé) :

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

tooensure qui hello image de machine virtuelle de Windows Server 2016 a hello dernière mise à jour cumulative, inclure hello `IncludeLatestCU` paramètre lors de l’exécution hello `New-AzsServer2016VMImage` applet de commande. Consultez hello [paramètres](#parameters) section pour plus d’informations sur les paramètres autorisés pour hello `New-AzsServer2016VMImage` applet de commande. Cela prend environ un marketplace d’Azure pile toohello image heure toopublish hello. 

## <a name="parameters"></a>Paramètres

|Paramètres New-AzsServer2016VMImage|Requis ?|Description|
|-----|-----|------|
|ISOPath|Oui|Hello toohello de chemin d’accès complet de télécharger Windows Server 2016 ISO.|
|Net35|Non|Ce paramètre vous permet de runtime de .NET 3.5 hello tooinstall sur l’image de Windows Server 2016 hello. Par défaut, cette valeur est définie à tootrue. Il est obligatoire de que cette image hello contient hello .NET 3.5 runtime tooinstall hello SQL et MYSQL fournisseurs de ressources. |
|Version|Non|Ce paramètre vous permet de toochoose si tooadd un **Core** ou **complète** ou **les deux** les images Windows Server 2016. Par défaut, cette valeur est définie trop « Full ».|
|VHDSizeInMB|Non|Hello taille taille (en Mo) de hello VHD image toobe ajouté environnement de Azure pile tooyour. Par défaut, cette valeur est définie à too40960 Mo.|
|CreateGalleryItem|Non|Spécifie si un élément du Marketplace doit être créé pour l’image de hello Windows Server 2016. Par défaut, cette valeur est définie à tootrue.|
|location |Non |Spécifie l’image de Windows Server 2016 hello emplacement toowhich hello doit être publiée.|
|IncludeLatestCU|Non|Définissez cette toohello mise à jour cumulative de Windows Server 2016 plus récente de commutateur tooapply hello nouveau disque dur virtuel.|
|CUUri |Non |Définissez cette mise à jour cumulative valeur toochoose hello Windows Server 2016 à partir d’un URI spécifique. |
|CUPath |Non |Définissez cette mise à jour cumulative valeur toochoose hello Windows Server 2016 à partir d’un chemin d’accès local. Cette option est utile si vous avez déployé instance d’Azure pile hello dans un environnement déconnecté.|

## <a name="next-steps"></a>Étapes suivantes

[Approvisionner une machine virtuelle](azure-stack-provision-vm.md)
