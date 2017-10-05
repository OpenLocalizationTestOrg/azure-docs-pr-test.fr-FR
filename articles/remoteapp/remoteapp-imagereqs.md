---
title: "Configuration requise pour les images Azure RemoteApp | Microsoft Docs"
description: "En savoir plus sur la configuration requise pour la création d’images à utiliser avec Azure RemoteApp"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="505fb-103">Configuration requise pour les images Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="505fb-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="505fb-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="505fb-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="505fb-105">Pour plus d’informations, lisez [l’annonce](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="505fb-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="505fb-106">Azure RemoteApp utilise une image Windows Server 2012 R2 pour héberger tous les programmes que vous souhaitez partager avec vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="505fb-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="505fb-107">Pour créer une image personnalisée, vous pouvez commencer avec une image existante ou en [créer une](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="505fb-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="505fb-108">Saviez-vous que votre abonnement Azure RemoteApp vous donne accès à une image Windows Server 2012 R2 dans la galerie de machines virtuelles Azure et que vous pouvez l’utiliser pour créer votre propre image de modèle ?</span><span class="sxs-lookup"><span data-stu-id="505fb-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="505fb-109">[Voyez par vous-même](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="505fb-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="505fb-110">Vous trouverez, ci-dessous, les exigences relatives à l’image qui peut être téléchargée en vue d'être utilisée avec Azure RemoteApp :</span><span class="sxs-lookup"><span data-stu-id="505fb-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="505fb-111">Les applications personnalisées ne stockent pas de données localement sur l’image.</span><span class="sxs-lookup"><span data-stu-id="505fb-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="505fb-112">Ces images sont sans état et ne doivent contenir que des applications.</span><span class="sxs-lookup"><span data-stu-id="505fb-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="505fb-113">L’image ne contient pas de données pouvant être perdues.</span><span class="sxs-lookup"><span data-stu-id="505fb-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="505fb-114">La taille de l'image doit être un multiple de Mo.</span><span class="sxs-lookup"><span data-stu-id="505fb-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="505fb-115">Si vous tentez de télécharger une image dont la taille n'est pas un multiple exact de Mo, le téléchargement échouera.</span><span class="sxs-lookup"><span data-stu-id="505fb-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="505fb-116">La taille de l'image doit être de 127 Go ou moins.</span><span class="sxs-lookup"><span data-stu-id="505fb-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="505fb-117">Elle doit se trouver dans un fichier VHD (pour l'instant, les fichiers VHDX ne sont pas pris en charge).</span><span class="sxs-lookup"><span data-stu-id="505fb-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="505fb-118">Le disque dur virtuel ne doit pas être une machine virtuelle de deuxième génération.</span><span class="sxs-lookup"><span data-stu-id="505fb-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="505fb-119">Le disque dur virtuel (VHD) peut être de taille fixe ou dynamique.</span><span class="sxs-lookup"><span data-stu-id="505fb-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="505fb-120">L'utilisation d'un fichier VHD de taille dynamique est recommandée, car le téléchargement sur Azure prend moins de temps qu'un fichier VHD de taille fixe.</span><span class="sxs-lookup"><span data-stu-id="505fb-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="505fb-121">Le disque doit être initialisé à l'aide du type de partitionnement MBR (Enregistrement de démarrage principal).</span><span class="sxs-lookup"><span data-stu-id="505fb-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="505fb-122">Le style de partition GPT (GUID Partition Table) n'est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="505fb-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="505fb-123">Le disque dur virtuel doit contenir une seule installation de Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="505fb-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="505fb-124">Il peut contenir plusieurs volumes, mais un seul contenant une installation de Windows.</span><span class="sxs-lookup"><span data-stu-id="505fb-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="505fb-125">Le rôle RDSH (Hôte de session Bureau à distance) et la fonctionnalité Expérience utilisateur doivent être installés.</span><span class="sxs-lookup"><span data-stu-id="505fb-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="505fb-126">Le rôle de service Broker pour les connexions Bureau à distance ne doit *pas* être installé.</span><span class="sxs-lookup"><span data-stu-id="505fb-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="505fb-127">Le système de fichiers EFS (Encrypting File System) doit être désactivé.</span><span class="sxs-lookup"><span data-stu-id="505fb-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="505fb-128">L'image doit être préparée avec SYSPREP en utilisant les paramètres **/oobe /generalize /shutdown** (n'utilisez PAS le paramètre **/mode:vm**).</span><span class="sxs-lookup"><span data-stu-id="505fb-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="505fb-129">Le téléchargement de votre disque dur virtuel à partir d’une chaîne d’instantanés n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="505fb-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="505fb-130">Consultez [Création d'une image Azure RemoteApp](remoteapp-imageoptions.md) pour plus d'informations sur la création d'images pour Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="505fb-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

