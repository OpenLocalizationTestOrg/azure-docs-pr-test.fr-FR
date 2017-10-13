---
title: "Ajouter une image de machine virtuelle à Azure Stack | Microsoft Docs"
description: "Ajouter une image de machine virtuelle Windows ou Linux personnalisée de votre organisation à utiliser par les locataires"
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
ms.date: 09/25/2017
ms.author: sngun
ms.openlocfilehash: de8540397b63093457382cf427a65ea0e48b93e0
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>Mettre une image de machine virtuelle personnalisée à la disposition des utilisateurs dans Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

Azure Stack permet aux opérateurs de mettre des images de machine virtuelle personnalisées à la disposition de leurs utilisateurs. Ces images peuvent être référencées par des modèles Azure Resource Manager ou être ajoutées à l’interface utilisateur de la Place de marché Azure au moment de la création d’un élément sur la Place de marché. 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a>Ajouter une image de machine virtuelle sur la Place de marché à l’aide de PowerShell

Effectuez les étapes prérequises suivantes à partir du [kit de développement](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), ou à partir d’un client externe Windows si vous êtes [connecté par le biais d’un VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).  

* Téléchargez les [outils nécessaires pour utiliser Azure Stack](azure-stack-powershell-download.md).  

* Préparez une image de disque dur virtuel du système d’exploitation Windows ou Linux au format VHD (et non VHDX).
   
   * Pour les images Windows, suivez les instructions sur la préparation des images fournies dans l’article [Charger une image de machine virtuelle Windows dans Azure pour des déploiements Resource Manager](../virtual-machines/windows/upload-generalized-managed.md), à la section **Préparer le disque VHD pour le chargement**.
   * Pour les images Linux, suivez les étapes décrites dans l’article [Déployer des machines virtuelles Linux dans Azure Stack](azure-stack-linux.md) pour préparer l’image ou utiliser une image Linux existante dans Azure Stack.  

Effectuez maintenant les étapes suivantes pour ajouter l’image sur la Place de marché Azure Stack :

1. Importez les modules Connect et ComputeAdmin :
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. Connectez-vous à votre environnement Azure Stack. Exécutez le script suivant en fonction du type de déploiement de votre environnement Azure Stack : AAD ou AD FS (veillez à remplacer les valeurs tenantName AAD, le point de terminaison GraphAudience et la valeur ArmEndpoint conformément à la configuration de votre environnement) : 

   a. Pour **AAD**, utilisez l’applet de commande suivante :

   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.windows.net/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   #Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience $GraphAudience

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. Pour **AD FS**, utilisez l’applet de commande suivante :
    
   ```PowerShell
   # For Azure Stack development kit, this value is set to https://adminmanagement.local.azurestack.external. To get this value for Azure Stack integrated systems, contact your service provider.
   $ArmEndpoint = "<Resource Manager endpoint for your environment>"

   # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. To get this value for Azure Stack integrated systems, contact your service provider.
   $GraphAudience = "<GraphAuidence endpoint for your environment>"

   # Create the Azure Stack operator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint $ArmEndpoint

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience $GraphAudience `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. Ajoutez l’image de machine virtuelle en appelant l’applet de commande `Add-AzsVMImage`. Dans l’applet de commande Add-AzsVMImage, spécifiez Windows ou Linux comme valeur du paramètre « osType ». Indiquez l’éditeur (« publisher »), l’offre (« offer »), la référence SKU (« sku ») et la version pour l’image de machine virtuelle. Consultez la section [Paramètres](#parameters) pour plus d’informations sur les paramètres autorisés. Ces paramètres sont utilisés par les modèles Azure Resource Manager pour référencer l’image de machine virtuelle. Voici un exemple d’appel du script :
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

La commande exécute les actions suivantes :

* Elle effectue l’authentification auprès de l’environnement Azure Stack.
* Elle charge le disque VHD local dans un nouveau compte de stockage temporaire.
* Elle ajoute l’image de machine virtuelle dans le référentiel d’images de machine virtuelle.
* Elle crée un élément de Place de marché.

Pour vous assurer que la commande s’est correctement exécutée, accédez à la Place de marché dans le portail, puis vérifiez que l’image de machine virtuelle est disponible dans la catégorie **Machines virtuelles**.

![Image de machine virtuelle correctement ajoutée](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>Supprimer une image de machine virtuelle à l’aide de PowerShell

Si vous n’avez plus besoin de l’image de machine virtuelle que vous avez chargée, vous pouvez la supprimer sur la Place de marché à l’aide de l’applet de commande suivante :

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
| **publisher** |Segment du nom de l’éditeur de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image. Exemple : « Microsoft ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **offer** |Segment du nom de l’offre de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image. Exemple : « WindowsServer ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **sku** |Segment du nom de la référence SKU de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image. Exemple : « Datacenter2016 ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **version** |Version de l’image de machine virtuelle que les utilisateurs indiquent pour déployer l’image. La version suit le format *\#.\#.\#*, par exemple, « 1.0.0 ». N’incluez aucun espace ou autre caractère spécial dans ce champ. |
| **osType** |Type d’exploitation de l’image, qui doit être « Windows » ou « Linux ». |
| **osDiskLocalPath** |Chemin d’accès local au disque VHD de système d’exploitation que vous chargez comme image de machine virtuelle dans Azure Stack. |
| **dataDiskLocalPaths** |Tableau facultatif des chemins d’accès locaux des disques de données qui peuvent être chargés comme partie de l’image de machine virtuelle. |
| **CreateGalleryItem** |Indicateur booléen qui détermine s’il faut créer un élément sur la Place de marché. Par défaut, il est défini sur true. |
| **title** |Nom d’affichage de l’élément de la Place de marché. Par défaut, il se compose des segments Éditeur-Offre-SKU de l’image de machine virtuelle. |
| **description** |Description de l’élément de la Place de marché. |
| **location** |Emplacement de publication de l’image de machine virtuelle. Par défaut, cette valeur est définie sur «local ».|
| **osDiskBlobURI** |(Facultatif) Ce script accepte également un URI de stockage Blob pour osDisk. |
| **dataDiskBlobURIs** |(Facultatif) Ce script accepte également un tableau d’URI de stockage Blob pour l’ajout de disques de données à l’image. |

## <a name="add-a-vm-image-through-the-portal"></a>Ajouter une image de machine virtuelle par le biais du portail

> [!NOTE]
> Cette méthode nécessite de créer l’élément de la Place de marché séparément.

L’une des exigences pour les images est de permettre leur référencement par un URI de stockage Blob. Préparez une image de système d’exploitation Windows ou Linux au format VHD (pas VHDX), puis chargez cette image dans un compte de stockage Azure ou Azure Stack. Si votre image est déjà chargée dans le stockage Blob Azure ou Azure Stack, ignorez l’étape 1.

1. [Chargez une image de machine virtuelle Windows dans Azure pour les déploiements Resource Manager ](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) ou, pour une image Linux, suivez les instructions fournies dans l’article [Déployer des machines virtuelles Linux dans Azure Stack](azure-stack-linux.md). Avant de charger l’image, tenez compte des points suivants :

   * Il est préférable de charger une image dans le stockage Blob Azure Stack plutôt que dans le stockage Blob Azure, car la publication d’une image dans le référentiel d’images Azure Stack est plus rapide. 
   
   * Quand vous chargez [l’image de machine virtuelle Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), pensez à substituer l’étape **Se connecter à Azure** par l’étape [Configurer l’environnement PowerShell de l’opérateur Azure Stack](azure-stack-powershell-configure-admin.md).  

   * Notez l’URI du stockage Blob où vous chargez l’image, au format suivant : *&lt;compteStockage&gt;/&lt;conteneurBlob&gt;/&lt;nomVHDCible&gt;*.vhd

   * Pour rendre le stockage Blob accessible de manière anonyme, accédez au conteneur d’objets blob du compte de stockage dans lequel l’image de machine virtuelle VHD a été chargée dans **Blob**, puis sélectionnez **Stratégie d’accès**. Si vous le souhaitez, vous pouvez à la place générer une signature d’accès partagé pour le conteneur et l’inclure dans l’URI de l’objet blob.

   ![Accéder aux objets blob du compte de stockage](./media/azure-stack-add-vm-image/image1.png)

   ![Définir un accès public pour les objets blob](./media/azure-stack-add-vm-image/image2.png)

2. Connectez-vous à Azure Stack en tant qu’opérateur : dans le menu, cliquez sur **Plus de services** > **Fournisseurs de ressources** > sélectionnez **Compute** > **Images de machine virtuelle** > **Ajouter**

3. Dans le panneau **Ajouter une image de machine virtuelle**, entrez l’éditeur, l’offre, la référence SKU et la version de l’image de machine virtuelle. Ces segments de nom référencent l’image de machine virtuelle dans les modèles Resource Manager. Sélectionnez le **type de système d’exploitation** approprié. Dans **URI d’objet blob du disque de système d’exploitation**, entrez l’URI de l’objet blob où l’image a été chargée, puis cliquez sur **Créer** pour démarrer la création de l’image de machine virtuelle.
   
   ![Démarrer la création de l’image](./media/azure-stack-add-vm-image/image4.png)

   Une fois que l’image de machine virtuelle a été créée, son état passe à « Réussi ».

4. Pour rendre une image de machine virtuelle plus rapidement disponible dans l’interface utilisateur, il est préférable de [créer un élément de Place de marché](azure-stack-create-and-publish-marketplace-item.md).

## <a name="next-steps"></a>Étapes suivantes

[Approvisionner une machine virtuelle](azure-stack-provision-vm.md)