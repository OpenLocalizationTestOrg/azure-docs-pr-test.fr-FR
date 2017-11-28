---
title: "Gérer les points de terminaison de streaming avec le SDK .NET. | Microsoft Docs"
description: "Cette rubrique montre comment gérer les points de terminaison de streaming avec le Portail Azure."
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
ms.openlocfilehash: 2f4f464f8604b6f453d6b50b736c6a3a889a3408
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-net-sdk"></a><span data-ttu-id="10fcb-104">Gérer les points de terminaison de streaming avec le SDK .NET</span><span class="sxs-lookup"><span data-stu-id="10fcb-104">Manage streaming endpoints with .NET SDK</span></span>

>[!NOTE]
><span data-ttu-id="10fcb-105">Consultez la rubrique de [présentation](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10fcb-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> <span data-ttu-id="10fcb-106">Consultez aussi [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="10fcb-106">Also, review [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="10fcb-107">Le code de cette rubrique montre comment effectuer les tâches suivantes à l’aide du Kit de développement logiciel (SDK) Azure Media Services .NET :</span><span class="sxs-lookup"><span data-stu-id="10fcb-107">The code in this topic shows how to do the following tasks using the Azure Media Services .NET SDK:</span></span>

- <span data-ttu-id="10fcb-108">Examinez le point de terminaison de streaming par défaut.</span><span class="sxs-lookup"><span data-stu-id="10fcb-108">Examine the default streaming endpoint.</span></span>
- <span data-ttu-id="10fcb-109">Créez/ajoutez un nouveau point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="10fcb-109">Create/add new streaming endpoint.</span></span>

    <span data-ttu-id="10fcb-110">Vous pouvez également disposer de plusieurs points de terminaison de streaming si vous prévoyez d’avoir différents CDN ou bien un CDN et un accès direct.</span><span class="sxs-lookup"><span data-stu-id="10fcb-110">You might want to have multiple streaming endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10fcb-111">Vous êtes facturé uniquement lorsque votre point de terminaison de streaming est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="10fcb-111">You are only billed when your Streaming Endpoint is in running state.</span></span>
    
- <span data-ttu-id="10fcb-112">Mettez à jour le point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="10fcb-112">Update the streaming endpoint.</span></span>
    
    <span data-ttu-id="10fcb-113">Appelez la fonction Update().</span><span class="sxs-lookup"><span data-stu-id="10fcb-113">Make sure to call the Update() function.</span></span>

- <span data-ttu-id="10fcb-114">Supprimez le point de terminaison de streaming.</span><span class="sxs-lookup"><span data-stu-id="10fcb-114">Delete the streaming endpoint.</span></span>

    >[!NOTE]
    ><span data-ttu-id="10fcb-115">Il n’est pas possible de supprimer le point de terminaison de streaming par défaut.</span><span class="sxs-lookup"><span data-stu-id="10fcb-115">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="10fcb-116">Pour plus d’informations sur la mise à l’échelle du point de terminaison de streaming, consultez [cette](media-services-portal-scale-streaming-endpoints.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="10fcb-116">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="10fcb-117">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10fcb-117">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="10fcb-118">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="10fcb-118">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="add-code-that-manages-streaming-endpoints"></a><span data-ttu-id="10fcb-119">Ajouter le code qui gère les points de terminaison de streaming</span><span class="sxs-lookup"><span data-stu-id="10fcb-119">Add code that manages streaming endpoints</span></span>
    
<span data-ttu-id="10fcb-120">Remplacez le contenu de Program.cs par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="10fcb-120">Replace the code in the Program.cs with the following code:</span></span>

    using System;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using Microsoft.WindowsAzure.MediaServices.Client.Live;

    namespace AMSStreamingEndpoint
    {
        class Program
        {
        // Read values from the App.config file.
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


## <a name="next-steps"></a><span data-ttu-id="10fcb-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10fcb-121">Next steps</span></span>
<span data-ttu-id="10fcb-122">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="10fcb-122">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="10fcb-123">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="10fcb-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

