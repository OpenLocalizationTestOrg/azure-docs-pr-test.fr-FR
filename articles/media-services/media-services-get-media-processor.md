---
title: "tooCreate aaaHow un processeur multimédia à l’aide hello Azure Media Services SDK pour .NET | Documents Microsoft"
description: "Découvrez comment toocreate un tooencode de composant de processeur multimédia, convertir le format de chiffrer ou déchiffrer le contenu multimédia pour Azure Media Services. Exemples de code sont écrits en c# et utilisent hello Media Services SDK pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: dbf9496f-c6f0-42a7-aa36-70f89dcb8ea2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: f133565cc1321d366013f17302adc8bc7585b251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="2fb50-104">Obtention d’une instance de processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="2fb50-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2fb50-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2fb50-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="2fb50-106">REST</span><span class="sxs-lookup"><span data-stu-id="2fb50-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="2fb50-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2fb50-107">Overview</span></span>
<span data-ttu-id="2fb50-108">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="2fb50-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="2fb50-109">Vous généralement créez un processeur multimédia lorsque vous créez une tâche tooencode, chiffrez ou convertissez le format hello du contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="2fb50-109">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="2fb50-110">Processeurs multimédias Azure</span><span class="sxs-lookup"><span data-stu-id="2fb50-110">Azure media processors</span></span> 

<span data-ttu-id="2fb50-111">Hello rubrique suivante fournit des listes de processeurs multimédias :</span><span class="sxs-lookup"><span data-stu-id="2fb50-111">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="2fb50-112">Processeurs multimédias d’encodage</span><span class="sxs-lookup"><span data-stu-id="2fb50-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="2fb50-113">Processeurs multimédias Analytics</span><span class="sxs-lookup"><span data-stu-id="2fb50-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="2fb50-114">Obtention d'un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="2fb50-114">Get Media Processor</span></span>

<span data-ttu-id="2fb50-115">Hello suivant de méthode montre comment tooget une instance de processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="2fb50-115">hello following method shows how tooget a media processor instance.</span></span> <span data-ttu-id="2fb50-116">exemple de code Hello suppose l’utilisation de hello d’une variable au niveau du module nommée **contexte _de_données** tooreference contexte hello du serveur comme décrit dans la section de hello [Comment : se connecter tooMedia Services par programmation](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="2fb50-116">hello code example assumes hello use of a module-level variable named **_context** tooreference hello server context as described in hello section [How to: Connect tooMedia Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="2fb50-117">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="2fb50-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2fb50-118">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="2fb50-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2fb50-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2fb50-119">Next Steps</span></span>
<span data-ttu-id="2fb50-120">Maintenant que vous savez comment tooget une instance de processeur multimédia, accédez toohello [comment tooEncode un élément multimédia](media-services-dotnet-encode-with-media-encoder-standard.md) rubrique qui vous indique comment toouse hello tooencode Media Encoder Standard, un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="2fb50-120">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

