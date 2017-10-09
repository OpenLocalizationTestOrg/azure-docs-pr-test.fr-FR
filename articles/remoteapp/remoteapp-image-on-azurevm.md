---
title: "aaaCreate une image Azure RemoteApp basée sur une machine virtuelle Azure | Documents Microsoft"
description: "Découvrez comment toocreate une image pour Azure RemoteApp en commençant par une machine virtuelle Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Création d’une image Azure RemoteApp basée sur une machine virtuelle Azure
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vous pouvez créer des images d’Azure RemoteApp (qui contiennent des applications de hello que vous partagez dans votre collection) à partir d’une machine virtuelle Azure. Vous pouvez également choisir toouse une image de machine virtuelle que nous avons ajouté la galerie d’images de machine virtuelle Azure toohello qui répond à toutes les exigences d’image Azure RemoteApp hello : vous pouvez utiliser cette image de machine virtuelle comme point de départ pour votre propre machine virtuelle, si vous le souhaitez. Recherchez simplement image de « Windows Server à distance hôte de Session bureau » hello dans la bibliothèque de hello.

Il existe deux étapes toocreate votre propre image basée sur une machine virtuelle Azure - création d’image de hello, puis le télécharger à partir de tooAzure de bibliothèque de machine virtuelle Azure hello RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Créez une image personnalisée basée sur une machine virtuelle Azure
Utilisez ces étapes de toocreate une image basée sur une machine virtuelle Azure.

1. Créez une machine virtuelle Azure. Vous pouvez utiliser hello « Windows Server à distance hôte de Session bureau » ou l’image de « Windows Server à distance Bureau Session hôte avec Microsoft Office 365 ProPlus » hello à partir de la galerie d’images de machine virtuelle Azure de hello. Cette image répond à toutes les exigences d’image de modèle hello Azure RemoteApp.
   
    Pour plus d’informations, consultez la section [Création d’une machine virtuelle exécutant Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Se connecter toohello machine virtuelle et installer et configurer des applications hello que vous souhaitez tooshare via RemoteApp. Assurez-vous que tooperform toutes les configurations Windows supplémentaires requises par vos applications.
   
    Pour plus d’informations, consultez [comment tooLog sur tooa Machine virtuelle exécutant Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. Si vous utilisez une des images hôte de Session Bureau à distance Windows Server de hello, il est un script de validation inclus qui permettra à que votre machine virtuelle répond aux hello RemoteApp pre-reqs. script de toorun, double-cliquez sur **validation** sur le bureau de hello. Assurez-vous que toutes les erreurs signalées par le script de hello sont résolus avant l’étape suivante toohello de continuer.
4. SYSPREP /generalize et capturer l’image de hello. Consultez [comment tooCapture un tooUse de Machine virtuelle Windows en tant que modèle](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) pour obtenir des instructions.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Importer l’image de hello dans la bibliothèque d’images hello Azure RemoteApp
Utilisez ces étapes tooimport hello nouvelle image dans Azure RemoteApp :

1. Bonjour **Images de modèle** onglet :
   
   * Si vous ne disposez pas d’images existantes, cliquez sur **Télécharger ou importer une image de modèle**.
   * Si vous avez déjà au moins une image, cliquez sur  **+**  tooadd une nouvelle image.
2. Sélectionnez **Importer une image à partir de votre bibliothèque de machines virtuelles**, puis cliquez sur **Suivant**.
3. Sur la page suivante de hello, sélectionnez votre image personnalisée à partir de la liste de hello et confirmez que vous avez suivi les étapes de hello répertoriées lorsque vous avez créé votre image. Cliquez sur **Suivant**.
4. Entrez un nom pour la nouvelle image de RemoteApp hello choisissez hello emplacement, puis cliquez sur le processus d’importation hello coche toostart hello.

> [!NOTE]
> Vous pouvez importer des images à partir de n’importe quel emplacement Azure pris en charge par les Machines virtuelles Azure tooany emplacement Azure pris en charge par Azure RemoteApp. Importation de hello peut prendre en fonction des emplacements de hello too25 minutes.
> 
> 

Maintenant vous êtes prêt toocreate votre nouvelle collection, soit une [cloud](remoteapp-create-cloud-deployment.md) collection ou [hybride](remoteapp-create-hybrid-deployment.md), en fonction de vos besoins.

