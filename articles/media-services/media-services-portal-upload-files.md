---
title: " Téléchargement de fichiers dans un compte Media Services à l’aide du portail Azure | Microsoft Docs"
description: "Ce didacticiel vous guide à travers les étapes de téléchargement de fichiers dans un compte Media Services à l’aide du portail Azure."
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
ms.openlocfilehash: 3a1dd7470f940da839687478b636464d930d8ab7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-azure-portal"></a><span data-ttu-id="c9a01-103">Téléchargement de fichiers dans un compte Media Services à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c9a01-103">Upload files into a Media Services account using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9a01-104">Portail</span><span class="sxs-lookup"><span data-stu-id="c9a01-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="c9a01-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c9a01-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="c9a01-106">REST</span><span class="sxs-lookup"><span data-stu-id="c9a01-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="c9a01-107">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c9a01-107">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c9a01-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9a01-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="c9a01-109">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="c9a01-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="c9a01-110">L’élément multimédia peut contenir des fichiers vidéo, des fichiers audio, des images, des collections de miniatures, des pistes textuelles et des légendes (ainsi que les métadonnées concernant ces fichiers). Une fois les fichiers téléchargés, votre contenu est stocké en toute sécurité dans le cloud et peut faire l’objet d’un traitement et d’une diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="c9a01-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="c9a01-111">Charger des fichiers</span><span class="sxs-lookup"><span data-stu-id="c9a01-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="c9a01-112">Une limite est appliquée à la taille maximale des fichiers pris en charge pour le traitement dans Media Services.</span><span class="sxs-lookup"><span data-stu-id="c9a01-112">There is a limit to the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="c9a01-113">Consultez [cette rubrique](media-services-quotas-and-limitations.md) pour en savoir plus sur les limites de taille des fichiers.</span><span class="sxs-lookup"><span data-stu-id="c9a01-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

1. <span data-ttu-id="c9a01-114">Dans le [portail Azure](https://portal.azure.com/), sélectionnez votre compte Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="c9a01-114">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c9a01-115">Dans le panneau **Paramètres**, cliquez sur **Éléments multimédias**.</span><span class="sxs-lookup"><span data-stu-id="c9a01-115">On the **Settings** blade, click **Assets**.</span></span>
   
    ![Charger des fichiers](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="c9a01-117">Cliquez sur le bouton **Télécharger** .</span><span class="sxs-lookup"><span data-stu-id="c9a01-117">Click the **Upload** button.</span></span>
   
    <span data-ttu-id="c9a01-118">La fenêtre **Upload a video asset** (Charger un élément multimédia vidéo) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c9a01-118">The **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c9a01-119">Il n’existe aucune limite de taille de fichier.</span><span class="sxs-lookup"><span data-stu-id="c9a01-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="c9a01-120">Accédez à la vidéo de votre choix sur votre ordinateur, sélectionnez-la, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="c9a01-120">Browse to the desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="c9a01-121">Le chargement démarre ; vous pouvez en voir la progression sous le nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="c9a01-121">The upload starts and you can see the progress under the file name.</span></span>  

<span data-ttu-id="c9a01-122">Une fois le téléchargement terminé, le nouvel élément multimédia s’affiche dans la fenêtre **Éléments multimédias** .</span><span class="sxs-lookup"><span data-stu-id="c9a01-122">Once the upload completes, you will see the new asset listed in the **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c9a01-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9a01-123">Next steps</span></span>
<span data-ttu-id="c9a01-124">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="c9a01-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="c9a01-125">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="c9a01-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="c9a01-126">Vous pouvez également utiliser les fonctions Azure pour déclencher une tâche de codage à partir d’un fichier entrant dans le conteneur configuré.</span><span class="sxs-lookup"><span data-stu-id="c9a01-126">You can also use Azure Functions to trigger an encoding job based on a file arriving in the configured container.</span></span> <span data-ttu-id="c9a01-127">Pour plus d’informations, consultez [cet exemple](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="c9a01-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="c9a01-128">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="c9a01-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c9a01-129">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="c9a01-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

