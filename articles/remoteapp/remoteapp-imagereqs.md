---
title: "configuration requise d’aaaAzure RemoteApp image | Documents Microsoft"
description: "En savoir plus sur la configuration requise de hello pour créer des toobe d’images utilisé avec Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="23215-103">Configuration requise pour les images Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="23215-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="23215-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="23215-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="23215-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="23215-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="23215-106">Azure RemoteApp utilise un toohost d’image de Windows Server 2012 R2 tous les programmes hello que vous souhaitez tooshare avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="23215-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="23215-107">toocreate une image personnalisée, vous pouvez démarrer avec une image existante ou [créer un nouveau](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="23215-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="23215-108">Saviez-vous que votre Azure RemoteApp abonnement vous donne dans qu'accès image de Windows Server 2012 R2 tooa hello galerie de machine virtuelle Azure que vous pouvez utiliser toocreate votre propre image de modèle ?</span><span class="sxs-lookup"><span data-stu-id="23215-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="23215-109">[Voyez par vous-même](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="23215-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="23215-110">exigences de Hello d’image hello qui peuvent être téléchargés pour une utilisation avec Azure RemoteApp sont :</span><span class="sxs-lookup"><span data-stu-id="23215-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="23215-111">Applications personnalisées ne stockent des données localement sur l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="23215-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="23215-112">Ces images sont sans état et ne doivent contenir que des applications.</span><span class="sxs-lookup"><span data-stu-id="23215-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="23215-113">image de Hello ne contient pas de données qui peuvent être perdues.</span><span class="sxs-lookup"><span data-stu-id="23215-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="23215-114">taille de l’image Hello doit être un multiple de nombre de Mo.</span><span class="sxs-lookup"><span data-stu-id="23215-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="23215-115">Si vous essayez de tooupload une image qui n’est pas un multiple exact, le téléchargement de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="23215-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="23215-116">taille de l’image Hello doit être 127 Go ou plus petit.</span><span class="sxs-lookup"><span data-stu-id="23215-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="23215-117">Elle doit se trouver dans un fichier VHD (pour l'instant, les fichiers VHDX ne sont pas pris en charge).</span><span class="sxs-lookup"><span data-stu-id="23215-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="23215-118">Hello disque dur virtuel ne doit pas être un ordinateur virtuel de génération 2.</span><span class="sxs-lookup"><span data-stu-id="23215-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="23215-119">Hello disque dur virtuel peut être de taille fixe ou expansion dynamique.</span><span class="sxs-lookup"><span data-stu-id="23215-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="23215-120">Un disque dur virtuel de taille dynamique est recommandé, car il prend moins tooAzure tooupload de temps qu’un fichier de disque dur virtuel de taille fixe.</span><span class="sxs-lookup"><span data-stu-id="23215-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="23215-121">disque de Hello doit être initialisé à l’aide du style de partitionnement hello enregistrement de démarrage principal (MBR).</span><span class="sxs-lookup"><span data-stu-id="23215-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="23215-122">Hello style de partition GUID partition GPT (table) n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="23215-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="23215-123">Hello disque dur virtuel doit contenir une seule installation de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="23215-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="23215-124">Il peut contenir plusieurs volumes, mais un seul contenant une installation de Windows.</span><span class="sxs-lookup"><span data-stu-id="23215-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="23215-125">rôle d’ordinateur hôte de Session de bureau à distance (RDSH) Hello et la fonctionnalité expérience utilisateur hello doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="23215-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="23215-126">rôle du service Broker pour les connexions Bureau à distance Hello doit *pas* être installé.</span><span class="sxs-lookup"><span data-stu-id="23215-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="23215-127">Hello EFS (ENCRYPTING file) doit être désactivée.</span><span class="sxs-lookup"><span data-stu-id="23215-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="23215-128">Hello image doit être préparée avec Sysprep à l’aide des paramètres de hello **/oobe /generalize /shutdown** (ne pas utiliser hello **/mode : VM** paramètre).</span><span class="sxs-lookup"><span data-stu-id="23215-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="23215-129">Le téléchargement de votre disque dur virtuel à partir d’une chaîne d’instantanés n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="23215-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="23215-130">Consultez [Création d'une image Azure RemoteApp](remoteapp-imageoptions.md) pour plus d'informations sur la création d'images pour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="23215-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

