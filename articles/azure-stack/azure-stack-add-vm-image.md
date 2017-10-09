---
title: "aaaAdding une machine virtuelle de l’image tooAzure pile | Documents Microsoft"
description: "Ajout Windows ou Linux VM image personnalisée de votre organisation pour les locataires toouse"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>Mettre une image de machine virtuelle personnalisée à la disposition des utilisateurs dans Azure Stack

Les administrateurs toomake machine virtuelle personnalisée images disponibles tootheir utilisateurs du cloud de Azure permet de pile. Ces images peuvent être référencés par les modèles Azure Resource Manager ou ajouté toothe Azure Marketplace UI avec la création d’un élément de Marketplace hello. 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a>Ajouter un toomarketplace d’image de machine virtuelle avec PowerShell

Exécution hello suivant la configuration requise à partir de hello [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe basé sur Windows si vous êtes [connectés via VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).  

* Télécharger hello [toowork requis d’outils avec Azure pile](azure-stack-powershell-download.md).  

* Préparez une image de disque dur virtuel du système d’exploitation Windows ou Linux au format VHD (et non VHDX).
   
   * Pour les images Windows hello article [télécharger un tooAzure d’image de machine virtuelle Windows pour les déploiements de gestionnaire de ressources](../virtual-machines/windows/upload-generalized-managed.md) contient des instructions de préparation d’image Bonjour **hello préparation du disque dur virtuel pour le téléchargement** section.
   * Pour les images de Linux, suivez les étapes de hello pour préparer l’image de hello ou utiliser une image Linux de pile Azure existante comme décrit dans l’article de hello [ordinateurs virtuels Linux de déployer sur Azure pile](azure-stack-linux.md).  

Maintenant, exécutez hello suivant marketplace de la pile de Azure étapes tooadd hello image toohello :

1. Importer des modules de se connecter et ComputeAdmin hello :
   
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
    
3. Ajouter l’image de machine virtuelle hello en appelant hello `Add-AzsVMImage` applet de commande. Dans l’applet de commande Add-AzsVMImage hello, attribuez-leur hello osType Windows ou Linux. Inclure le serveur de publication hello, offre, référence (SKU) et la version pour l’image de machine virtuelle hello. Consultez hello [paramètres](#parameters) section pour plus d’informations sur hello autorisé de paramètres. Ces paramètres sont utilisés par l’image de machine virtuelle Azure Resource Manager modèles tooreference hello. Voici un appel de l’exemple de script de hello :
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

commande Hello hello suivant :

* Authentifie l’environnement de Azure pile toohello
* Télécharge hello tooa de disque dur virtuel local créé le compte de stockage temporaire
* Ajoute le référentiel d’images hello VM image toohello machine virtuelle et
* Elle crée un élément de Place de marché.

tooverify commande hello s’est correctement exécutée, tooMarketplace dans le portail de hello, puis vérifiez cette image de machine virtuelle hello est disponible dans hello **virtuels** catégorie.

![Image de machine virtuelle correctement ajoutée](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>Supprimer une image de machine virtuelle à l’aide de PowerShell

Lorsque vous avez besoin n’est plus hello image de machine virtuelle que vous avez téléchargés précédemment, vous pouvez le supprimer à partir du marketplace de hello à l’aide de hello suivant l’applet de commande :

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a>Paramètres

| Paramètre | Description |
| --- | --- |
| **publisher** |segment de nom Hello Éditeur d’image de machine virtuelle hello que les utilisateurs utilisent lors du déploiement d’image de hello. Exemple : « Microsoft ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **offer** |segment de nom Hello offre de hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello. Exemple : « WindowsServer ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **sku** |segment de nom Hello référence (SKU) de hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello. Exemple : « Datacenter2016 ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **version** |version Hello Hello Image de machine virtuelle que les utilisateurs utilisent lors du déploiement d’image de machine virtuelle hello. Cette version est au format de hello  *\#.\#. \#*. par exemple, « 1.0.0 ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **osType** |osType Hello d’image de hello doit être 'Windows' ou 'Linux'. |
| **osDiskLocalPath** |disque toohello du système d’exploitation du chemin d’accès local de Hello VHD que vous chargez en tant qu’un tooAzure d’image de machine virtuelle pile. |
| **dataDiskLocalPaths** |Tableau facultatif de chemins d’accès local de hello pour les disques de données qui peuvent être téléchargés dans le cadre de l’image de machine virtuelle hello. |
| **CreateGalleryItem** |Indicateur booléen qui détermine si un élément dans le Marketplace de toocreate. Par défaut, elle a la valeur tootrue. |
| **title** |Hello affiche le nom de l’élément du Marketplace. Par défaut, elle a la valeur toohello Publisher-offre-référence (SKU) de l’image de machine virtuelle hello. |
| **description** |description de Hello d’élément du Marketplace hello. |
| **location** |image de machine virtuelle Hello emplacement toowhich hello doit être publié. Par défaut, cette valeur est définie à toolocal.|
| **osDiskBlobURI** |(Facultatif) Ce script accepte également un URI de stockage Blob pour osDisk. |
| **dataDiskBlobURIs** |Si vous le souhaitez, ce script accepte également un tableau de stockage d’objets Blob URI pour l’ajout d’image de toohello de disques de données. |

## <a name="add-a-vm-image-through-hello-portal"></a>Ajouter une image de machine virtuelle via le portail de hello

> [!NOTE]
> Cette méthode requiert la création d’élément du Marketplace hello séparément.

L’une des exigences pour les images est de permettre leur référencement par un URI de stockage Blob. Préparer une image de système d’exploitation Windows ou Linux au format de disque dur virtuel (pas VHDX) et puis télécharger hello image tooa compte de stockage Azure ou de la pile de Azure. Si votre image est déjà téléchargé toohello stockage d’objets Blob dans Azure ou de la pile d’Azure, vous pouvez ignorer l’étape 1.

1. [Télécharger un tooAzure d’image de machine virtuelle Windows pour les déploiements de gestionnaire de ressources](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) ou d’une image Linux, suivez les instructions de hello décrites dans hello [ordinateurs virtuels Linux de déployer sur Azure pile](azure-stack-linux.md) l’article. Vous devez comprendre hello suivant considérations avant de charger hello image :

   * Il est plus efficace tooupload une tooAzure image stockage d’objets Blob de pile à tooAzure stockage d’objets Blob, car il prend moins référentiel d’images temps toopush toohello hello image Azure pile. 
   
   * Lors du téléchargement hello [image de machine virtuelle Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), assurez-vous que toosubstitute hello **connexion tooAzure** étape avec hello [configurer l’environnement PowerShell de l’opérateur de pile de Azure hello](azure-stack-powershell-configure-admin.md)étape.  

   * Prenez note de hello URI où vous téléchargez l’image hello, qui se trouve dans hello format de stockage d’objets Blob :  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd

   * toomake hello accessible de manière anonyme, accédez toohello compte blob conteneur de stockage blob hello VM où l’image disque dur virtuel a été téléchargé trop**Blob,** , puis sélectionnez **la stratégie d’accès**. Si vous le souhaitez, vous pouvez à la place générer une signature d’accès partagé pour le conteneur de hello et inclure dans le cadre de l’URI d’objet blob hello.

   ![Parcourir les objets BLOB du compte toostorage](./media/azure-stack-add-vm-image/image1.png)

   ![Jeu d’objets blob accès toopublic](./media/azure-stack-add-vm-image/image2.png)

2. Connectez-vous à tooAzure pile sous la forme d’un administrateur de cloud > hello menu, cliquez sur **davantage de services** > **fournisseurs de ressources** > sélectionnez **de calcul**  >  **Images de machine virtuelle** > **ajouter**

3. Sur hello **ajouter une Image de machine virtuelle** panneau, entrez le serveur de publication hello, offre, référence (SKU) et la version de l’image de machine virtuelle hello. Ces segments de noms font référence toohello image de machine virtuelle dans les modèles de gestionnaire de ressources. Assurez-vous que tooselect le **osType** correctement. Pour **OD disque Blob URI**, entrez hello URI d’objet Blob où l’image a été téléchargée, cliquez sur **créer** toobegin création de l’Image de machine virtuelle.
   
   ![BEGIN toocreate hello image](./media/azure-stack-add-vm-image/image4.png)

   Lorsque l’image de hello est correctement créé, hello état d’image de machine virtuelle change too'Succeeded'.

4. image de machine virtuelle hello toomake plus facilement disponible pour un utilisateur dans l’interface utilisateur de hello, il est préférable de trop[créer un élément du Marketplace](azure-stack-create-and-publish-marketplace-item.md).

## <a name="next-steps"></a>Étapes suivantes

[Approvisionner une machine virtuelle](azure-stack-provision-vm.md)