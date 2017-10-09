---
title: "AAA » télécharger des fichiers dans un compte de service de média à l’aide de hello portail Azure | Documents Microsoft »"
description: "Ce didacticiel vous guide à travers les étapes de hello de téléchargement de fichiers dans un compte de service de média à l’aide de hello portail Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="95062-103">Télécharger des fichiers dans un compte de service de média à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="95062-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95062-104">Portail</span><span class="sxs-lookup"><span data-stu-id="95062-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="95062-105">.NET</span><span class="sxs-lookup"><span data-stu-id="95062-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="95062-106">REST</span><span class="sxs-lookup"><span data-stu-id="95062-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="95062-107">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="95062-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="95062-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="95062-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="95062-109">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="95062-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="95062-110">Hello actif peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.) Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="95062-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="95062-111">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="95062-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="95062-112">Il existe une taille de fichier maximale toohello limite pris en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="95062-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="95062-113">Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="95062-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="95062-114">Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="95062-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="95062-115">Sur hello **paramètres** panneau, cliquez sur **actifs**.</span><span class="sxs-lookup"><span data-stu-id="95062-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="95062-117">Cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="95062-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="95062-118">Hello **télécharger un élément multimédia vidéo** fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="95062-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="95062-119">Il n’existe aucune limite de taille de fichier.</span><span class="sxs-lookup"><span data-stu-id="95062-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="95062-120">Parcourir vidéo toohello souhaité sur votre ordinateur, sélectionnez-le, puis appuyez sur OK.</span><span class="sxs-lookup"><span data-stu-id="95062-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="95062-121">téléchargement de Hello démarre et vous pouvez voir la progression hello sous le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="95062-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="95062-122">Une fois le téléchargement de hello terminé, vous verrez hello un nouveau composant répertorié dans hello **actifs** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="95062-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="95062-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95062-123">Next steps</span></span>
<span data-ttu-id="95062-124">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="95062-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="95062-125">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="95062-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="95062-126">Vous pouvez également utiliser les fonctions Azure tootrigger un travail d’encodage basé sur un fichier qui arrivent dans le conteneur de hello configuré.</span><span class="sxs-lookup"><span data-stu-id="95062-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="95062-127">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="95062-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="95062-128">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="95062-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="95062-129">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="95062-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

