---
title: "aaaPolling opérations longues | Documents Microsoft"
description: "Cette rubrique montre comment les opérations de longue toopoll."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="91642-103">Diffusion vidéo en flux continu avec Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="91642-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="91642-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="91642-104">Overview</span></span>

<span data-ttu-id="91642-105">Microsoft Azure Media Services propose des API qui envoient des demandes d’opérations de toostart tooMedia Services (par exemple : créer, Démarrer, arrêter ou supprimer un canal).</span><span class="sxs-lookup"><span data-stu-id="91642-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="91642-106">Ces opérations sont des opérations de longue durée.</span><span class="sxs-lookup"><span data-stu-id="91642-106">These operations are long-running.</span></span>

<span data-ttu-id="91642-107">Hello Media Services .NET SDK fournit des API qui envoie la demande de hello et attendre hello opération toocomplete (en interne, hello API demandent progression de l’opération après certains intervalles).</span><span class="sxs-lookup"><span data-stu-id="91642-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="91642-108">Par exemple, lorsque vous appelez le canal. Start(), méthode hello retourne après le démarrage du canal de hello.</span><span class="sxs-lookup"><span data-stu-id="91642-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="91642-109">Vous pouvez également utiliser la version asynchrone de hello : await de canal. StartAsync() (pour plus d’informations sur le modèle asynchrone basé sur des tâches, consultez [appuyez sur](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="91642-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="91642-110">API d’envoyer une demande d’opération et interroge ensuite pour l’état de hello jusqu'à ce que l’opération hello est terminée sont appelées « méthodes d’interrogation ».</span><span class="sxs-lookup"><span data-stu-id="91642-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="91642-111">Ces méthodes (notamment les version Async hello) sont recommandés pour les applications clientes complètes et/ou les services avec état.</span><span class="sxs-lookup"><span data-stu-id="91642-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="91642-112">Il existe des scénarios dans lesquels une application ne peut pas attendre d’une demande http longue et souhaite que toopoll de progression de l’opération hello manuellement.</span><span class="sxs-lookup"><span data-stu-id="91642-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="91642-113">Un exemple classique serait un navigateur qui interagit avec un service web sans état : lors de la demande de navigateur de hello toocreate un canal, service web de hello initie une opération longue et renvoie hello navigateur de toohello ID opération.</span><span class="sxs-lookup"><span data-stu-id="91642-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="91642-114">Hello navigateur peut alors demander hello web service tooget hello état de l’opération en fonction de hello ID.</span><span class="sxs-lookup"><span data-stu-id="91642-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="91642-115">Hello Media Services .NET SDK fournit des API qui est utiles pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="91642-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="91642-116">Ces API sont appelées « méthodes sans interrogation ».</span><span class="sxs-lookup"><span data-stu-id="91642-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="91642-117">« méthodes sans interrogation » Hello ont hello suivant le modèle d’affectation de noms : envoyer*NomOpération*opération (par exemple, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="91642-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="91642-118">Envoyer*NomOpération*hello de retour des méthodes d’opération **IOperation** objet ; hello objet retourné contient des informations qui peuvent être utilisés tootrack hello opération.</span><span class="sxs-lookup"><span data-stu-id="91642-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="91642-119">Envoi de Hello*NomOpération*OperationAsync méthodes retournent **tâche<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="91642-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="91642-120">Actuellement, hello suivant les méthodes sans interrogation de prise en charge des classes : **canal**, **StreamingEndpoint**, et **programme**.</span><span class="sxs-lookup"><span data-stu-id="91642-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="91642-121">toopoll pour l’état de l’opération hello, utilisez hello **GetOperation** méthode sur hello **OperationBaseCollection** classe.</span><span class="sxs-lookup"><span data-stu-id="91642-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="91642-122">Utilisez hello suivant l’état de l’opération hello intervalles toocheck : pour **canal** et **StreamingEndpoint** opérations, utilisez 30 secondes ; pour **programme** opérations, utilisez 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="91642-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="91642-123">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="91642-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="91642-124">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="91642-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="91642-125">Exemple</span><span class="sxs-lookup"><span data-stu-id="91642-125">Example</span></span>

<span data-ttu-id="91642-126">Hello exemple suivant définit une classe appelée **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="91642-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="91642-127">Cette définition de classe peut constituer un point de départ pour la définition de classe de votre service Web.</span><span class="sxs-lookup"><span data-stu-id="91642-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="91642-128">Par souci de simplicité, hello exemples suivants utilisent les versions non asynchrones hello de méthodes.</span><span class="sxs-lookup"><span data-stu-id="91642-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="91642-129">Hello montre également comment les clients hello peuvent utiliser cette classe.</span><span class="sxs-lookup"><span data-stu-id="91642-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="91642-130">Définition de la classe ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="91642-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="91642-131">code client Hello</span><span class="sxs-lookup"><span data-stu-id="91642-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="91642-132">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="91642-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="91642-133">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="91642-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

