---
title: "Création d’un processeur multimédia à l’aide du Kit de développement logiciel Azure Media Services pour .NET | Microsoft Docs"
description: "Apprenez à créer un composant processeur multimédia pour encoder, chiffrer ou déchiffrer un contenu multimédia, ou convertir son format pour Azure Media Services. Les exemples de code sont écrits en C# et utilisent le Kit de développement logiciel (SDK) Media Services pour .NET."
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
ms.openlocfilehash: c2cbe41b71afa8acc184f9d7f4cfe94686de783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="d9131-104">Obtention d’une instance de processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="d9131-104">How to: Get a Media Processor Instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9131-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d9131-105">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="d9131-106">REST</span><span class="sxs-lookup"><span data-stu-id="d9131-106">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="d9131-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d9131-107">Overview</span></span>
<span data-ttu-id="d9131-108">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="d9131-108">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="d9131-109">Le plus souvent, vous devez créer un processeur multimédia lorsque vous créez une tâche visant à encoder, à chiffrer ou à convertir le format du contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="d9131-109">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="d9131-110">Processeurs multimédias Azure</span><span class="sxs-lookup"><span data-stu-id="d9131-110">Azure media processors</span></span> 

<span data-ttu-id="d9131-111">La rubrique suivante fournit une liste de processeurs multimédias :</span><span class="sxs-lookup"><span data-stu-id="d9131-111">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="d9131-112">Processeurs multimédias d’encodage</span><span class="sxs-lookup"><span data-stu-id="d9131-112">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="d9131-113">Processeurs multimédias Analytics</span><span class="sxs-lookup"><span data-stu-id="d9131-113">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

## <a name="get-media-processor"></a><span data-ttu-id="d9131-114">Obtention d'un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="d9131-114">Get Media Processor</span></span>

<span data-ttu-id="d9131-115">La méthode suivante montre comment obtenir une instance de processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="d9131-115">The following method shows how to get a media processor instance.</span></span> <span data-ttu-id="d9131-116">L’exemple de code implique l’utilisation d’une variable au niveau du module, nommée **_context**, pour conserver une référence au contexte, tel que décrit dans la section [Comment : se connecter à Media Services par programmation](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d9131-116">The code example assumes the use of a module-level variable named **_context** to reference the server context as described in the section [How to: Connect to Media Services Programmatically](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

    private static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
        ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

        if (processor == null)
        throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

        return processor;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="d9131-117">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d9131-117">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9131-118">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d9131-118">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="d9131-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9131-119">Next Steps</span></span>
<span data-ttu-id="d9131-120">Maintenant que vous savez comment obtenir une instance de processeur multimédia, consultez la rubrique [Encodage d’un élément multimédia](media-services-dotnet-encode-with-media-encoder-standard.md) pour savoir comment utiliser Media Encoder Standard afin d’encoder un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="d9131-120">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-dotnet-encode-with-media-encoder-standard.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

