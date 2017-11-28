---
title: fichiers aaaUpload dans un compte Azure Media Services, Azure StorSimple | Documents Microsoft
description: "Cet article donne une brève vue d’ensemble d’Azure StorSimple Data Manager. article de Hello contient également des liens tootutorials qui vous montrent comment les données tooextract de StorSimple et le télécharger en tant que ressources tooan compte Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="a85be-104">Charger des fichiers dans un compte Azure Media Services à partir d’Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="a85be-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="a85be-105">Cet article donne une brève vue d’ensemble d’Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="a85be-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="a85be-106">article de Hello contient également des liens tootutorials qui vous montrent comment les données tooextract de StorSimple et charger ces données en tant que ressources tooan compte d’Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="a85be-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="a85be-107">Azure StorSimple Data Manager est actuellement disponible en version préliminaire privée.</span><span class="sxs-lookup"><span data-stu-id="a85be-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="a85be-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a85be-108">Overview</span></span>

<span data-ttu-id="a85be-109">Dans Media Services, vous téléchargez vos fichiers numériques dans une ressource.</span><span class="sxs-lookup"><span data-stu-id="a85be-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="a85be-110">Hello actif peut contenir vidéo, audio, images, collections de miniatures, texte assure le suivi et sous-titres fichiers (et les métadonnées hello sur ces fichiers.) Une fois que les fichiers hello sont téléchargés, votre contenu est stocké en toute sécurité dans le cloud hello pour le traitement et la diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="a85be-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="a85be-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) utilise le stockage cloud comme une extension de hello solution locale et reconnaît automatiquement les données sur un stockage local hello et de stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="a85be-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="a85be-112">l’appareil StorSimple Hello dedupes et compresse les données avant de les envoyer cloud toohello rend très efficace pour l’envoi de cloud de toohello des fichiers volumineux.</span><span class="sxs-lookup"><span data-stu-id="a85be-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="a85be-113">Hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service fournit des API que vous tooextract les données à partir de StorSimple et de les présentent comme des ressources AMS.</span><span class="sxs-lookup"><span data-stu-id="a85be-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="a85be-114">Prise en main</span><span class="sxs-lookup"><span data-stu-id="a85be-114">Get started</span></span>

1. <span data-ttu-id="a85be-115">[Créer un compte Media Services](media-services-portal-create-account.md) dans lequel vous souhaitez actifs de hello tootransfer.</span><span class="sxs-lookup"><span data-stu-id="a85be-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="a85be-116">S’inscrire pour l’aperçu du Gestionnaire de données, comme décrit dans hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="a85be-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="a85be-117">Créez un compte StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="a85be-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="a85be-118">Créez un travail de transformation de données qui extrait des données d’un appareil StorSimple et les transfère vers un compte AMS en tant que ressources.</span><span class="sxs-lookup"><span data-stu-id="a85be-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="a85be-119">Lors de la tâche de hello commence à s’exécuter, une file d’attente de stockage est créé.</span><span class="sxs-lookup"><span data-stu-id="a85be-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="a85be-120">Cette file d’attente est renseignée avec des messages sur les objets blob transformés, au fur et à mesure de leur mise à disposition.</span><span class="sxs-lookup"><span data-stu-id="a85be-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="a85be-121">nom de Hello de cette file d’attente est hello identique au nom de la définition de la tâche hello hello.</span><span class="sxs-lookup"><span data-stu-id="a85be-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="a85be-122">Vous pouvez utiliser cette toodetermine de file d’attente lorsque comme élément multimédia est prêt et appeler votre toorun d’opération Media Services souhaitée sur celle-ci.</span><span class="sxs-lookup"><span data-stu-id="a85be-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="a85be-123">Par exemple, vous pouvez utiliser cette tootrigger de file d’attente une fonction d’Azure qui contient du code de Media Services nécessaire hello qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="a85be-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="a85be-124">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a85be-124">See also</span></span>

[<span data-ttu-id="a85be-125">Utilisez hello .net SDK travaux tootrigger Bonjour Data Manager</span><span class="sxs-lookup"><span data-stu-id="a85be-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="a85be-126">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="a85be-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a85be-127">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="a85be-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a85be-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a85be-128">Next steps</span></span>

<span data-ttu-id="a85be-129">Vous pouvez désormais encoder vos éléments multimédias téléchargés.</span><span class="sxs-lookup"><span data-stu-id="a85be-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="a85be-130">Pour plus d'informations, consultez [Encode an asset using Media Encoder Standard with the Azure portal (Encoder un élément multimédia à l’aide de Media Encoder Standard avec le portail Azure)](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="a85be-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
