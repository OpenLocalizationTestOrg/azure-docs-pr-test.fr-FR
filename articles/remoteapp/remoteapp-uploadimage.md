---
title: "aaaUpload une image personnalisée pour Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooupload personnalisé d’images pour Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="873fa-103">Téléchargement d'une image personnalisée pour Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="873fa-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="873fa-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="873fa-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="873fa-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="873fa-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="873fa-106">Maintenant que vous avez créé votre image de modèle personnalisé ou que vous avez mis à jour avec les modifications, vous devez tooupload cette bibliothèque d’images tooyour image Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="873fa-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="873fa-107">Suivez ces étapes.</span><span class="sxs-lookup"><span data-stu-id="873fa-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="873fa-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="873fa-108">Before you start</span></span>
1. <span data-ttu-id="873fa-109">Vérifiez que votre image personnalisée répond à hello [spécifications de l’image](remoteapp-imagereqs.md) et [configuration requise pour application](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="873fa-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="873fa-110">Installer hello [module Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="873fa-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="873fa-111">Étape par étape sur l’image personnalisée de tooupload</span><span class="sxs-lookup"><span data-stu-id="873fa-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="873fa-112">Ouvrez le portail de gestion Azure et accédez toohello RemoteApp page.</span><span class="sxs-lookup"><span data-stu-id="873fa-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="873fa-113">Sur hello **images de modèle** , cliquez sur **télécharger** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="873fa-114">Entrez un nom convivial pour votre image et spécifier l’emplacement du compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="873fa-115">Vérifiez hello trouve hello même emplacement que votre collection RemoteApp ou un emplacement où vous voulez toocreate un.</span><span class="sxs-lookup"><span data-stu-id="873fa-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="873fa-116">Lorsque vous y êtes invité, télécharger hello script tooyour PC local.</span><span class="sxs-lookup"><span data-stu-id="873fa-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="873fa-117">Copier les paramètres de commande hello dans le Presse-papiers de tooyour de zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="873fa-118">Ouvrez une fenêtre Windows PowerShell avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="873fa-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="873fa-119">À partir de hello élevés fenêtre Windows PowerShell, accédez toohello même répertoire où vous avez téléchargé le script de hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="873fa-120">Hello de coller copier la commande et appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="873fa-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="873fa-121">processus de téléchargement Hello commence et durée dépendent de nombreux facteurs, notamment votre vitesse du réseau et la taille d’image de hello</span><span class="sxs-lookup"><span data-stu-id="873fa-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="873fa-122">Si votre téléchargement ne réussit pas à cause d’interruption du réseau ou les choses comme cela, vous pouvez toujours reprendre les processus de téléchargement hello que vous a commencé.</span><span class="sxs-lookup"><span data-stu-id="873fa-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="873fa-123">tooresume un téléchargement, exécuter le script hello en utilisant hello même ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="873fa-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="873fa-124">Ne modifiez jamais de script de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-124">Never modify hello upload script.</span></span> <span data-ttu-id="873fa-125">Vérifications spécifiques ont été implémentée tooensure qui hello image répond aux exigences de l’image hello et exigences de l’application.</span><span class="sxs-lookup"><span data-stu-id="873fa-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="873fa-126">Problèmes courants</span><span class="sxs-lookup"><span data-stu-id="873fa-126">Common problems</span></span>
* <span data-ttu-id="873fa-127">Veillez à utiliser Windows PowerShell, et non Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="873fa-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="873fa-128">Vous devez le module Azure PowerShell de hello tooinstall, car certains modules sont nécessaires au cours du processus de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="873fa-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="873fa-129">Script de hello ne modifient jamais, sont les validations de commodité.</span><span class="sxs-lookup"><span data-stu-id="873fa-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="873fa-130">Si le fichier de disque dur virtuel hello obtient verrouillé pendant le téléchargement, copiez le fichier de hello ou déplacez-le tooa nouveau emplacement et la tentative de téléchargement à nouveau.</span><span class="sxs-lookup"><span data-stu-id="873fa-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="873fa-131">Un processus Windows peut empêcher le téléchargement.</span><span class="sxs-lookup"><span data-stu-id="873fa-131">There might be some Windows process that is preventing upload.</span></span>  

