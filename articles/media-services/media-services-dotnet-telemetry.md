---
title: "aaaConfiguring télémétrie d’Azure Media Services avec .NET | Documents Microsoft"
description: "Cet article vous explique comment toouse hello télémétrie d’Azure Media Services à l’aide du Kit de développement .NET."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f8f55e37-0714-49ea-bf4a-e6c1319bec44
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: 4019fa7d080ca3f8a8709bd1e666f7062b883954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-azure-media-services-telemetry-with-net"></a><span data-ttu-id="4b3b5-103">Configuration de la télémétrie Azure Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="4b3b5-103">Configuring Azure Media Services telemetry with .NET</span></span>

<span data-ttu-id="4b3b5-104">Cette rubrique décrit les étapes générales que vous pouvez entreprendre lors de la configuration de télémétrie d’Azure Media Services (AMS) hello à l’aide du Kit de développement .NET.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-104">This topic describes general steps that you might take when configuring hello Azure Media Services (AMS) telemetry using .NET SDK.</span></span> 

>[!NOTE]
><span data-ttu-id="4b3b5-105">Pour une explication détaillée des éléments hello est données de télémétrie AMS et comment tooconsume, consultez hello [vue d’ensemble](media-services-telemetry-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-105">For hello detailed explanation of what is AMS telemetry and how tooconsume it, see hello [overview](media-services-telemetry-overview.md) topic.</span></span>

<span data-ttu-id="4b3b5-106">Vous pouvez utiliser les données de télémétrie dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="4b3b5-106">You can consume telemetry data in one of hello following ways:</span></span>

- <span data-ttu-id="4b3b5-107">Lire les données directement à partir de stockage de tables Azure (par exemple, à l’aide de hello SDK de stockage).</span><span class="sxs-lookup"><span data-stu-id="4b3b5-107">Read data directly from Azure Table Storage (e.g. using hello Storage SDK).</span></span> <span data-ttu-id="4b3b5-108">Pour la description hello des tables de stockage de données de télémétrie, consultez hello **consommation des informations de télémétrie** dans [cela](https://msdn.microsoft.com/library/mt742089.aspx) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-108">For hello description of telemetry storage tables, see hello **Consuming telemetry information** in [this](https://msdn.microsoft.com/library/mt742089.aspx) topic.</span></span>

<span data-ttu-id="4b3b5-109">Ou</span><span class="sxs-lookup"><span data-stu-id="4b3b5-109">Or</span></span>

- <span data-ttu-id="4b3b5-110">Prise en charge d’utilisation hello Bonjour Media Services .NET SDK pour la lecture des données de stockage.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-110">Use hello support in hello Media Services .NET SDK for reading storage data.</span></span> <span data-ttu-id="4b3b5-111">Cette rubrique montre comment télémétrie tooenable pour hello spécifié compte de AMS et comment les métriques de hello tooquery à l’aide de hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-111">This topic shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

## <a name="configuring-telemetry-for-a-media-services-account"></a><span data-ttu-id="4b3b5-112">Configuration de la télémétrie pour un compte Media Services</span><span class="sxs-lookup"><span data-stu-id="4b3b5-112">Configuring telemetry for a Media Services account</span></span>

<span data-ttu-id="4b3b5-113">Hello étapes suivantes sont nécessaires tooenable télémétrie :</span><span class="sxs-lookup"><span data-stu-id="4b3b5-113">hello following steps are needed tooenable telemetry:</span></span>

- <span data-ttu-id="4b3b5-114">Obtenir des informations d’identification de hello de hello stockage compte lié toohello compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-114">Get hello credentials of hello storage account attached toohello Media Services account.</span></span> 
- <span data-ttu-id="4b3b5-115">Créer un point de terminaison de Notification avec **EndPointType** défini trop**AzureTable** et endPointAddress pointant vers la table de stockage toohello.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-115">Create a Notification Endpoint with **EndPointType** set too**AzureTable** and endPointAddress pointing toohello storage table.</span></span>

        INotificationEndPoint notificationEndPoint = 
                      _context.NotificationEndPoints.Create("monitoring", 
                      NotificationEndPointType.AzureTable,
                      "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/");

- <span data-ttu-id="4b3b5-116">Créer une configuration d’analyse des paramètres pour hello services que vous souhaitez toomonitor.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-116">Create a monitoring configuration settings for hello services you want toomonitor.</span></span> <span data-ttu-id="4b3b5-117">Pas plus d’un paramètre de configuration de la surveillance n’est autorisé.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-117">No more than one monitoring configuration settings is allowed.</span></span> 
  
        IMonitoringConfiguration monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
            new List<ComponentMonitoringSetting>()
            {
                new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)
            });

## <a name="consuming-telemetry-information"></a><span data-ttu-id="4b3b5-118">informations sur l’utilisation de la télémétrie</span><span class="sxs-lookup"><span data-stu-id="4b3b5-118">Consuming telemetry information</span></span>

<span data-ttu-id="4b3b5-119">Pour plus d’informations sur l’utilisation de la télémétrie, consultez [cette](media-services-telemetry-overview.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-119">For information about consuming telemetry information, see [this](media-services-telemetry-overview.md) topic.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4b3b5-120">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b3b5-120">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4b3b5-121">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4b3b5-121">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

2. <span data-ttu-id="4b3b5-122">Ajouter hello suivant élément trop**appSettings** défini dans votre fichier app.config :</span><span class="sxs-lookup"><span data-stu-id="4b3b5-122">Add hello following element too**appSettings** defined in your app.config file:</span></span>

    <add key="StorageAccountName" value="storage_name" />
 
## <a name="example"></a><span data-ttu-id="4b3b5-123">Exemple</span><span class="sxs-lookup"><span data-stu-id="4b3b5-123">Example</span></span>  
    
<span data-ttu-id="4b3b5-124">Bonjour à l’exemple suivant montre comment télémétrie tooenable pour hello spécifié compte de AMS et comment les métriques de hello tooquery à l’aide de hello Azure Media Services .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4b3b5-124">hello following example shows how tooenable telemetry for hello specified AMS account and how tooquery hello metrics using hello Azure Media Services .NET SDK.</span></span>  

    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;

    namespace AMSMetrics
    {
        class Program
        {
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        private static readonly string _mediaServicesStorageAccountName =
            ConfigurationManager.AppSettings["StorageAccountName"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        private static IStreamingEndpoint _streamingEndpoint = null;
        private static IChannel _channel = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            _streamingEndpoint = _context.StreamingEndpoints.FirstOrDefault();
            _channel = _context.Channels.FirstOrDefault();

            var monitoringConfigurations = _context.MonitoringConfigurations;
            IMonitoringConfiguration monitoringConfiguration = null;

            // No more than one monitoring configuration settings is allowed.
            if (monitoringConfigurations.ToArray().Length != 0)
            {
            monitoringConfiguration = _context.MonitoringConfigurations.FirstOrDefault();
            }
            else
            {
            INotificationEndPoint notificationEndPoint =
                      _context.NotificationEndPoints.Create("monitoring",
                      NotificationEndPointType.AzureTable, GetTableEndPoint());

            monitoringConfiguration = _context.MonitoringConfigurations.Create(notificationEndPoint.Id,
                new List<ComponentMonitoringSetting>()
                {
                    new ComponentMonitoringSetting(MonitoringComponent.Channel, MonitoringLevel.Normal),
                    new ComponentMonitoringSetting(MonitoringComponent.StreamingEndpoint, MonitoringLevel.Normal)

                });
            }

            //Print metrics for a Streaming Endpoint.
            PrintStreamingEndpointMetrics();

            Console.ReadLine();
        }

        private static string GetTableEndPoint()
        {
            return "https://" + _mediaServicesStorageAccountName + ".table.core.windows.net/";
        }

        private static void PrintStreamingEndpointMetrics()
        {
            Console.WriteLine(string.Format("Telemetry for streaming endpoint '{0}'", _streamingEndpoint.Name));

            DateTime timerangeEnd = DateTime.UtcNow;
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some streaming endpoint metrics.
            var telemetry = _streamingEndpoint.GetTelemetry();

            var res = telemetry.GetStreamingEndpointRequestLogs(timerangeStart, timerangeEnd);

            Console.Title = "Streaming endpoint metrics:";

            foreach (var log in res)
            {
            Console.WriteLine("AccountId: {0}", log.AccountId);
            Console.WriteLine("BytesSent: {0}", log.BytesSent);
            Console.WriteLine("EndToEndLatency: {0}", log.EndToEndLatency);
            Console.WriteLine("HostName: {0}", log.HostName);
            Console.WriteLine("ObservedTime: {0}", log.ObservedTime);
            Console.WriteLine("PartitionKey: {0}", log.PartitionKey);
            Console.WriteLine("RequestCount: {0}", log.RequestCount);
            Console.WriteLine("ResultCode: {0}", log.ResultCode);
            Console.WriteLine("RowKey: {0}", log.RowKey);
            Console.WriteLine("ServerLatency: {0}", log.ServerLatency);
            Console.WriteLine("StatusCode: {0}", log.StatusCode);
            Console.WriteLine("StreamingEndpointId: {0}", log.StreamingEndpointId);
            Console.WriteLine();
            }

            Console.WriteLine();
        }

        private static void PrintChannelMetrics()
        {
            if (_channel == null)
            {
            Console.WriteLine("There are no channels in this AMS account");
            return;
            }

            Console.WriteLine(string.Format("Telemetry for channel '{0}'", _channel.Name));

            DateTime timerangeEnd = DateTime.UtcNow; 
            DateTime timerangeStart = DateTime.UtcNow.AddHours(-5);

            // Get some channel metrics.
            var telemetry = _channel.GetTelemetry();

            var channelMetrics = telemetry.GetChannelHeartbeats(timerangeStart, timerangeEnd);

            // Print hello channel metrics.
            Console.WriteLine("Channel metrics:");

            foreach (var channelHeartbeat in channelMetrics.OrderBy(x => x.ObservedTime))
            {
            Console.WriteLine(
                "    Observed time: {0}, Last timestamp: {1}, Incoming bitrate: {2}",
                channelHeartbeat.ObservedTime,
                channelHeartbeat.LastTimestamp,
                channelHeartbeat.IncomingBitrate);
            }

            Console.WriteLine();
        }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="4b3b5-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b3b5-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4b3b5-126">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4b3b5-126">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
