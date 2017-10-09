---
title: "AAA comment tooget une instance de processeur multimédia à l’aide de REST | Documents Microsoft"
description: "Découvrez comment toocreate un tooencode de composant de processeur multimédia, convertir le format de chiffrer ou déchiffrer le contenu multimédia pour Azure Media Services."
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
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a><span data-ttu-id="78aa8-103">Comment tooget une instance de processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="78aa8-103">How tooget a Media Processor instance</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78aa8-104">.NET</span><span class="sxs-lookup"><span data-stu-id="78aa8-104">.NET</span></span>](media-services-get-media-processor.md)
> * [<span data-ttu-id="78aa8-105">REST</span><span class="sxs-lookup"><span data-stu-id="78aa8-105">REST</span></span>](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="78aa8-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="78aa8-106">Overview</span></span>
<span data-ttu-id="78aa8-107">Dans Media Services, un processeur multimédia est un composant qui gère une tâche de traitement spécifique, telle que l’encodage, la conversion de format, le chiffrement ou le déchiffrement de contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="78aa8-107">In Media Services a media processor is a component that handles a specific processing task, such as encoding, format conversion, encrypting, or decrypting media content.</span></span> <span data-ttu-id="78aa8-108">Vous généralement créez un processeur multimédia lorsque vous créez une tâche tooencode, chiffrez ou convertissez le format hello du contenu multimédia.</span><span class="sxs-lookup"><span data-stu-id="78aa8-108">You typically create a media processor when you are creating a task tooencode, encrypt, or convert hello format of media content.</span></span>

## <a name="azure-media-processors"></a><span data-ttu-id="78aa8-109">Processeurs multimédias Azure</span><span class="sxs-lookup"><span data-stu-id="78aa8-109">Azure media processors</span></span> 

<span data-ttu-id="78aa8-110">Hello rubrique suivante fournit des listes de processeurs multimédias :</span><span class="sxs-lookup"><span data-stu-id="78aa8-110">hello following topic provides lists of media processors:</span></span>

* [<span data-ttu-id="78aa8-111">Processeurs multimédias d’encodage</span><span class="sxs-lookup"><span data-stu-id="78aa8-111">Encoding media processors</span></span>](scenarios-and-availability.md#encoding-media-processors)
* [<span data-ttu-id="78aa8-112">Processeurs multimédias Analytics</span><span class="sxs-lookup"><span data-stu-id="78aa8-112">Analytics media processors</span></span>](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
><span data-ttu-id="78aa8-113">Lors de l’accès aux entités dans Media Services, vous devez définir les valeurs et les champs d’en-tête spécifiques dans vos requêtes HTTP.</span><span class="sxs-lookup"><span data-stu-id="78aa8-113">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="78aa8-114">Pour plus d'informations, consultez [Installation pour le développement REST API de Media Services](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="78aa8-114">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span>

## <a name="connect-toomedia-services"></a><span data-ttu-id="78aa8-115">Connecter les Services de tooMedia</span><span class="sxs-lookup"><span data-stu-id="78aa8-115">Connect tooMedia Services</span></span>

<span data-ttu-id="78aa8-116">Pour plus d’informations sur la façon dont tooconnect toohello AMS API, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="78aa8-116">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="78aa8-117">Après vous être connecté toohttps://media.windows.net, vous recevrez une redirection 301 spécifiant un autre URI de Media Services.</span><span class="sxs-lookup"><span data-stu-id="78aa8-117">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="78aa8-118">Vous devez effectuer les appels suivants toohello nouvel URI.</span><span class="sxs-lookup"><span data-stu-id="78aa8-118">You must make subsequent calls toohello new URI.</span></span>

## <a name="get-a-media-processor"></a><span data-ttu-id="78aa8-119">Obtention d’un processeur multimédia</span><span class="sxs-lookup"><span data-stu-id="78aa8-119">Get a media processor</span></span>

<span data-ttu-id="78aa8-120">Hello après l’appel REST montre comment tooget un processeur multimédia par nom d’instance (dans ce cas, **Media Encoder Standard**).</span><span class="sxs-lookup"><span data-stu-id="78aa8-120">hello following REST call shows how tooget a media processor instance by name (in this case, **Media Encoder Standard**).</span></span> 

<span data-ttu-id="78aa8-121">Demande :</span><span class="sxs-lookup"><span data-stu-id="78aa8-121">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="78aa8-122">Réponse :</span><span class="sxs-lookup"><span data-stu-id="78aa8-122">Response:</span></span>

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


## <a name="media-services-learning-paths"></a><span data-ttu-id="78aa8-123">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="78aa8-123">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="78aa8-124">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="78aa8-124">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="78aa8-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78aa8-125">Next Steps</span></span>
<span data-ttu-id="78aa8-126">Maintenant que vous savez comment tooget une instance de processeur multimédia, accédez toohello [comment tooEncode un élément multimédia](media-services-rest-get-started.md) rubrique qui vous indique comment toouse hello tooencode Media Encoder Standard, un élément multimédia.</span><span class="sxs-lookup"><span data-stu-id="78aa8-126">Now that you know how tooget a media processor instance, go toohello [How tooEncode an Asset](media-services-rest-get-started.md) topic which will show you how toouse hello Media Encoder Standard tooencode an asset.</span></span>

