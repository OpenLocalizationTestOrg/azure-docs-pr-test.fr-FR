---
title: "codes d’erreur de codage de média aaaAzure | Documents Microsoft"
description: "Cette rubrique répertorie les codes d’erreur qui peut être renvoyés au cas où une erreur est survenue pendant hello encodage d’exécution de la tâche..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="1b405-103">Codes d’erreur d’encodage</span><span class="sxs-lookup"><span data-stu-id="1b405-103">Encoding error codes</span></span>

<span data-ttu-id="1b405-104">Hello tableau suivant répertorie les codes d’erreur qui peut être renvoyés au cas où une erreur est survenue pendant hello exécution de la tâche de codage.</span><span class="sxs-lookup"><span data-stu-id="1b405-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="1b405-105">Détails de l’erreur tooget dans votre code .NET, utilisez hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="1b405-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="1b405-106">Détails de l’erreur tooget dans votre code reste, utilisez hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) API REST.</span><span class="sxs-lookup"><span data-stu-id="1b405-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="1b405-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="1b405-107">ErrorDetail.Code</span></span> | <span data-ttu-id="1b405-108">Causes possibles de l’erreur</span><span class="sxs-lookup"><span data-stu-id="1b405-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="1b405-109">Unknown</span><span class="sxs-lookup"><span data-stu-id="1b405-109">Unknown</span></span> |<span data-ttu-id="1b405-110">Erreur inconnue lors de l’exécution de tâche hello</span><span class="sxs-lookup"><span data-stu-id="1b405-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="1b405-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="1b405-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="1b405-112">Catégorie d’erreurs se produisant lors du téléchargement d’éléments multimédias d’entrée : noms de fichier incorrects, fichiers de longueur nulle, formats incorrects, etc.</span><span class="sxs-lookup"><span data-stu-id="1b405-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="1b405-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="1b405-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="1b405-114">Catégorie d’erreurs qui traite des problèmes sur le côté du service hello - pour les exemples d’erreurs réseau ou de stockage lors du téléchargement.</span><span class="sxs-lookup"><span data-stu-id="1b405-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="1b405-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="1b405-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="1b405-116">Catégorie d’erreurs de tâches où <see cref="MediaTask.PrivateData"/> (configuration) n’est pas valide, par exemple la configuration de hello n’est pas un système valide prédéfini ou il contient du code XML non valide.</span><span class="sxs-lookup"><span data-stu-id="1b405-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="1b405-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="1b405-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="1b405-118">Catégorie d’erreurs lors de l’exécution de hello de tâche hello où problèmes à l’intérieur de hello d’entrée des fichiers multimédias de provoquer un échec.</span><span class="sxs-lookup"><span data-stu-id="1b405-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="1b405-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="1b405-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="1b405-120">Catégorie d’erreurs où processeur multimédia de hello ne peut pas traiter les fichiers hello fournis - format de média non pris en charge ou ne correspond pas à la Configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="1b405-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="1b405-121">Par exemple, la tentative de tooproduce une sortie audio uniquement à partir d’une ressource qui a uniquement les vidéos</span><span class="sxs-lookup"><span data-stu-id="1b405-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="1b405-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="1b405-122">ErrorProcessingTask</span></span> |<span data-ttu-id="1b405-123">Catégorie d’autres erreurs hello processeur multimédia rencontre lors du traitement de hello de tâche hello qui sont toocontent non liée.</span><span class="sxs-lookup"><span data-stu-id="1b405-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="1b405-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="1b405-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="1b405-125">Catégorie d’erreurs lors du chargement de la ressource en sortie hello</span><span class="sxs-lookup"><span data-stu-id="1b405-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="1b405-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="1b405-126">ErrorCancelingTask</span></span> |<span data-ttu-id="1b405-127">Catégorie d’erreurs toocover échecs lors de la tentative de toocancel hello tâche</span><span class="sxs-lookup"><span data-stu-id="1b405-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="1b405-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="1b405-128">TransientError</span></span> |<span data-ttu-id="1b405-129">Catégorie d’erreurs toocover problèmes temporaires (par exemple).</span><span class="sxs-lookup"><span data-stu-id="1b405-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="1b405-130">problèmes réseau temporaires avec Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="1b405-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="1b405-131">aide tooget hello **Media Services** équipe, ouvrez un [ticket de support](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="1b405-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1b405-132">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="1b405-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1b405-133">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="1b405-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="1b405-134">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="1b405-134">Related articles</span></span>
* [<span data-ttu-id="1b405-135">Exécution de tâches d’encodage avancées via la personnalisation des présélections Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="1b405-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="1b405-136">Quotas et limitations</span><span class="sxs-lookup"><span data-stu-id="1b405-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
