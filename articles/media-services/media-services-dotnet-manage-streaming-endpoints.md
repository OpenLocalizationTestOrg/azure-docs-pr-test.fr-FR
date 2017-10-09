---
title: "aaaManage de diffusion en continu des points de terminaison avec le Kit de développement .NET. | Microsoft Docs"
description: Cette rubrique montre comment les points de terminaison de diffusion en continu toomanage avec hello portail Azure.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: 0da34a97-f36c-48d0-8ea2-ec12584a2215
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 30c092a8ebf4e2b2902392f4cf98f46d812ccdbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="56161-104">Gérer les points de terminaison de streaming avec le SDK .NET</span><span class="sxs-lookup"><span data-stu-id="56161-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="56161-105">Assurez-vous que tooreview hello [vue d’ensemble](media-services-streaming-endpoints-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="56161-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="56161-106">Consultez aussi [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="56161-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="56161-107">code Hello dans cette rubrique montre comment hello toodo à l’aide des tâches suivantes hello Azure Media Services .NET SDK :</span><span class="sxs-lookup"><span data-stu-id="56161-107">hello code in this topic shows how toodo hello following tasks using hello Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="56161-108">Examinez le point de terminaison de diffusion en continu de la valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="56161-108">Examine hello default streaming endpoint.</span></span>
- <span data-ttu-id="56161-109">Créez/ajoutez un nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="56161-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="56161-110">Vous pourriez toohave plusieurs points de terminaison de diffusion en continu si vous envisagez de toohave CDN différents ou un CDN et un accès direct.</span><span class="sxs-lookup"><span data-stu-id="56161-110">You might want toohave multiple streaming endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="56161-111">Vous êtes facturé uniquement lorsque votre point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56161-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="56161-112">Mettre à jour hello point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="56161-112">Update hello streaming endpoint.</span></span>
    
    <span data-ttu-id="56161-113">Vérifiez que hello toocall fonction Update().</span><span class="sxs-lookup"><span data-stu-id="56161-113">Make sure toocall hello Update() function.</span></span>

- <span data-ttu-id="56161-114">Supprimer hello point de terminaison de diffusion en continu.</span><span class="sxs-lookup"><span data-stu-id="56161-114">Delete hello streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="56161-115">point de terminaison de diffusion en continu de la valeur par défaut Hello ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="56161-115">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="56161-116">Pour plus d’informations sur la façon dont tooscale hello point de terminaison de diffusion en continu, consultez [cela](media-services-portal-scale-streaming-endpoints.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="56161-116">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="56161-117">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="56161-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="56161-118">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="56161-118">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="56161-119">Ajouter le code qui gère les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="56161-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="56161-120">Remplacez le code hello hello Program.cs par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="56161-120">Replace hello code in hello Program.cs with hello following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
        ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
        ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            var defaultStreamingEndpoint = _context.StreamingEndpoints.Where(s => s.Name.Contains("default")).FirstOrDefault();
            ExamineStreamingEndpoint(defaultStreamingEndpoint);

            IStreamingEndpoint newStreamingEndpoint = AddStreamingEndpoint();
            UpdateStreamingEndpoint(newStreamingEndpoint);
            DeleteStreamingEndpoint(newStreamingEndpoint);
        }

        static public void ExamineStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            Console.WriteLine(streamingEndpoint.Name);
            Console.WriteLine(streamingEndpoint.StreamingEndpointVersion);
            Console.WriteLine(streamingEndpoint.FreeTrialEndTime);
            Console.WriteLine(streamingEndpoint.ScaleUnits);
            Console.WriteLine(streamingEndpoint.CdnProvider);
            Console.WriteLine(streamingEndpoint.CdnProfile);
            Console.WriteLine(streamingEndpoint.CdnEnabled);
        }

        static public IStreamingEndpoint AddStreamingEndpoint()
        {
            var name = "StreamingEndpoint" + DateTime.UtcNow.ToString("hhmmss");
            var option = new StreamingEndpointCreationOptions(name, 1)
            {
            StreamingEndpointVersion = new Version("2.0"),
            CdnEnabled = true,
            CdnProfile = "CdnProfile",
            CdnProvider = CdnProviderType.PremiumVerizon
            };

            var streamingEndpoint = _context.StreamingEndpoints.Create(option);

            return streamingEndpoint;
        }

        static public void UpdateStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            if (streamingEndpoint.StreamingEndpointVersion == "1.0")
            streamingEndpoint.StreamingEndpointVersion = "2.0";

            streamingEndpoint.CdnEnabled = false;
            streamingEndpoint.Update();
        }

        static public void DeleteStreamingEndpoint(IStreamingEndpoint streamingEndpoint)
        {
            streamingEndpoint.Delete();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="56161-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56161-121">Next steps</span></span>
<span data-ttu-id="56161-122">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="56161-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="56161-123">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="56161-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

