---
title: "Obtention d’une instance de processeur multimédia à l’aide de REST | Microsoft Docs"
description: "Apprenez à créer un composant processeur multimédia pour encoder, chiffrer ou déchiffrer un contenu multimédia, ou convertir son format pour Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 4ad90ad979c5bd74fc55155098c88d5c13cb12e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-a-media-processor-instance"></a><span data-ttu-id="edfc3-103">Obtention d’une instance de processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="edfc3-103">How to get a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="edfc3-104">.NET</span><span class="sxs-lookup"><span data-stu-id="edfc3-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="edfc3-105">REST</span><span class="sxs-lookup"><span data-stu-id="edfc3-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="edfc3-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="edfc3-106">Overview</span></span>
<span data-ttu-id="edfc3-107">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="edfc3-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="edfc3-108">Le plus souvent, vous devez créer un processeur multimédia lorsque vous créez une tâche visant à encoder, à chiffrer ou à convertir le format du contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="edfc3-108">You typically create a media processor when you are creating a task to encode, encrypt, or convert the format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="edfc3-109">Processeurs multimédias Azure</span><span class="sxs-lookup"><span data-stu-id="edfc3-109">Azure media processors</span></span> 

<span data-ttu-id="edfc3-110">La rubrique suivante fournit une liste de processeurs multimédias :</span><span class="sxs-lookup"><span data-stu-id="edfc3-110">The following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="edfc3-111">Processeurs multimédias d’encodage</span><span class="sxs-lookup"><span data-stu-id="edfc3-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="edfc3-112">Processeurs multimédias Analytics</span><span class="sxs-lookup"><span data-stu-id="edfc3-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="edfc3-113">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="edfc3-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="edfc3-114">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="edfc3-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="edfc3-115">Connexion à Media Services</span><span class="sxs-lookup"><span data-stu-id="edfc3-115">Connect to Media Services</span></span>

<span data-ttu-id="edfc3-116">Pour savoir comment vous connecter à l’API AMS, consultez [Accéder à l’API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="edfc3-116">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="edfc3-117">Après vous être connecté à https://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI Media Services.</span><span class="sxs-lookup"><span data-stu-id="edfc3-117">After successfully connecting to https://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="edfc3-118">Vous devez faire d’autres appels au nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="edfc3-118">You must make subsequent calls to the new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="edfc3-119">Obtention d’un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="edfc3-119">Get a media processor</span></span>

<span data-ttu-id="edfc3-120">L’appel REST suivant montre comment obtenir une instance de processeur multimédia par nom (dans ce cas, **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="edfc3-120">The following REST call shows how to get a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="edfc3-121">Demande :</span><span class="sxs-lookup"><span data-stu-id="edfc3-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="edfc3-122">Réponse :</span><span class="sxs-lookup"><span data-stu-id="edfc3-122">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="edfc3-123">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="edfc3-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="edfc3-124">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="edfc3-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="edfc3-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edfc3-125">Next Steps</span></span>
<span data-ttu-id="edfc3-126">Maintenant que vous savez comment obtenir une instance de processeur multimédia, consultez la rubrique [Encodage d’un élément multimédia](media-services-rest-get-started.md) pour savoir comment utiliser Media Encoder Standard afin d’encoder un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="edfc3-126">Now that you know how to get a media processor instance, go to the [How to Encode an Asset](media-services-rest-get-started.md) topic which will show you how to use the Media Encoder Standard to encode an asset.</span></span>

