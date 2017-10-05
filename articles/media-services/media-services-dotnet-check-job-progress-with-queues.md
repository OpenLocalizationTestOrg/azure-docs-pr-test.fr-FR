---
title: Utiliser Azure Queue Storage pour surveiller les notifications de travaux Media Services avec .NET | Microsoft Docs
description: "Découvrez comment utiliser Azure Queue Storage pour surveiller les notifications de travaux Media Services. L’exemple de code est écrit en C# et utilise le Kit de développement logiciel (SDK) Media Services pour .NET."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: f535d0b5-f86c-465f-81c6-177f4f490987
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/14/2017
ms.author: juliako
ms.openlocfilehash: 5ee89d0ae4c3c56d164aff4e321ee99f015ba4fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-queue-storage-to-monitor-media-services-job-notifications-with-net"></a><span data-ttu-id="4ad24-104">Utiliser Azure Queue Storage pour surveiller les notifications de travaux Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="4ad24-104">Use Azure Queue storage to monitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="4ad24-105">Lorsque vous exécutez des travaux d’encodage, vous avez généralement besoin de faire appel à une méthode de suivi de la progression du travail.</span><span class="sxs-lookup"><span data-stu-id="4ad24-105">When you run encoding jobs, you often require a way to track job progress.</span></span> <span data-ttu-id="4ad24-106">Vous pouvez configurer Media Services pour transmettre des notifications à [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="4ad24-106">You can configure Media Services to deliver notifications to [Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="4ad24-107">Vous pouvez vérifier la progression des tâches en obtenant des notifications à partir de Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="4ad24-107">You can monitor job progress by getting notifications from the Queue storage.</span></span> 

<span data-ttu-id="4ad24-108">Les messages transmis au stockage de files d’attente sont accessibles n’importe où dans le monde.</span><span class="sxs-lookup"><span data-stu-id="4ad24-108">Messages delivered to Queue storage can be accessed from anywhere in the world.</span></span> <span data-ttu-id="4ad24-109">L’architecture de messagerie de Stockage File d’attente est hautement évolutive.</span><span class="sxs-lookup"><span data-stu-id="4ad24-109">The Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="4ad24-110">L’interrogation du Stockage File d’attente pour les messages est préférable aux autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="4ad24-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="4ad24-111">Un scénario courant pour écouter les notifications Media Services se présente si vous développez un système de gestion de contenu qui doit exécuter une tâche supplémentaire une fois un travail d’encodage terminé (par exemple, déclencher l’étape suivante d’un flux de travail ou publier du contenu).</span><span class="sxs-lookup"><span data-stu-id="4ad24-111">One common scenario for listening to Media Services notifications is if you are developing a content management system that needs to perform some additional task after an encoding job completes (for example, to trigger the next step in a workflow, or to publish content).</span></span>

<span data-ttu-id="4ad24-112">Cette rubrique explique comment obtenir des messages de notification à partir de Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="4ad24-112">This topic shows how to get notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="4ad24-113">Considérations</span><span class="sxs-lookup"><span data-stu-id="4ad24-113">Considerations</span></span>
<span data-ttu-id="4ad24-114">Considérez les éléments suivants lors du développement d’applications Media Services qui utilisent le Stockage File d’attente :</span><span class="sxs-lookup"><span data-stu-id="4ad24-114">Consider the following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="4ad24-115">Le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée (FIFO).</span><span class="sxs-lookup"><span data-stu-id="4ad24-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="4ad24-116">Pour plus d'informations, consultez [Files d'attente Azure et files d'attente Azure Service Bus - comparaison et différences](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="4ad24-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="4ad24-117">Le Stockage File d’attente n’est pas un service push.</span><span class="sxs-lookup"><span data-stu-id="4ad24-117">Queue storage is not a push service.</span></span> <span data-ttu-id="4ad24-118">Vous devez interroger la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4ad24-118">You have to poll the queue.</span></span>
* <span data-ttu-id="4ad24-119">Le nombre de files d’attente est illimité.</span><span class="sxs-lookup"><span data-stu-id="4ad24-119">You can have any number of queues.</span></span> <span data-ttu-id="4ad24-120">Pour plus d'informations, consultez [API REST du service de file d'attente](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="4ad24-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="4ad24-121">Le Stockage File d’attente a certaines limitations et spécificités que vous devez connaître.</span><span class="sxs-lookup"><span data-stu-id="4ad24-121">Queue storage has some limitations and specifics to be aware of.</span></span> <span data-ttu-id="4ad24-122">Celles-ci sont décrites dans [Files d’attente Azure et files d’attente Azure Service Bus - comparaison et différences](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="4ad24-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="4ad24-123">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="4ad24-123">.NET code example</span></span>

<span data-ttu-id="4ad24-124">L’exemple de code de cette section permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4ad24-124">The code example in this section does the following:</span></span>

1. <span data-ttu-id="4ad24-125">Définir la classe **EncodingJobMessage** qui assure le mappage au format des messages de notification.</span><span class="sxs-lookup"><span data-stu-id="4ad24-125">Defines the **EncodingJobMessage** class that maps to the notification message format.</span></span> <span data-ttu-id="4ad24-126">Le code désérialise les messages reçus à partir de la file d'attente en objets du type **EncodingJobMessage** .</span><span class="sxs-lookup"><span data-stu-id="4ad24-126">The code deserializes messages received from the queue into objects of the **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="4ad24-127">Charger les informations de compte Media Services et Storage à partir du fichier app.config.</span><span class="sxs-lookup"><span data-stu-id="4ad24-127">Loads the Media Services and Storage account information from the app.config file.</span></span> <span data-ttu-id="4ad24-128">L’exemple de code utilise ces informations pour créer les objets **CloudMediaContext** et **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="4ad24-128">The code example uses this information to create the **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="4ad24-129">Créer la file d’attente qui reçoit les messages de notification concernant le travail d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4ad24-129">Creates the queue that receives notification messages about the encoding job.</span></span>
4. <span data-ttu-id="4ad24-130">Créer le point de terminaison de notification mappé à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="4ad24-130">Creates the notification end point that is mapped to the queue.</span></span>
5. <span data-ttu-id="4ad24-131">Associer le point de terminaison de notification à la tâche et soumettre la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="4ad24-131">Attaches the notification end point to the job and submits the encoding job.</span></span> <span data-ttu-id="4ad24-132">Vous pouvez avoir plusieurs points de terminaison de notification associés à une tâche.</span><span class="sxs-lookup"><span data-stu-id="4ad24-132">You can have multiple notification end points attached to a job.</span></span>
6. <span data-ttu-id="4ad24-133">Transmettre **NotificationJobState.FinalStatesOnly** à la méthode **AddNew**.</span><span class="sxs-lookup"><span data-stu-id="4ad24-133">Passes **NotificationJobState.FinalStatesOnly** to the **AddNew** method.</span></span> <span data-ttu-id="4ad24-134">(Dans cet exemple, nous nous intéressons uniquement aux derniers états du traitement du travail.)</span><span class="sxs-lookup"><span data-stu-id="4ad24-134">(In this example, we are only interested in final states of the job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="4ad24-135">Si vous transmettez **NotificationJobState.All**, vous obtenez toutes les notifications de modification des états suivantes : en attente, planifié, traitement en cours et terminé.</span><span class="sxs-lookup"><span data-stu-id="4ad24-135">If you pass **NotificationJobState.All**, you get all of the following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="4ad24-136">Toutefois, comme indiqué précédemment, le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée.</span><span class="sxs-lookup"><span data-stu-id="4ad24-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="4ad24-137">Vous pouvez utiliser la propriété **Timestamp** (définie sur le type **EncodingJobMessage** dans l’exemple ci-dessous) pour ordonner les messages.</span><span class="sxs-lookup"><span data-stu-id="4ad24-137">To order messages, use the **Timestamp** property (defined on the **EncodingJobMessage** type in the example below).</span></span> <span data-ttu-id="4ad24-138">Les messages en double sont possibles.</span><span class="sxs-lookup"><span data-stu-id="4ad24-138">Duplicate messages are possible.</span></span> <span data-ttu-id="4ad24-139">Utilisez la **propriété ETag** (définie sur le type **EncodingJobMessage**) pour rechercher les éventuels doublons.</span><span class="sxs-lookup"><span data-stu-id="4ad24-139">To check for duplicates, use the **ETag property** (defined on the **EncodingJobMessage** type).</span></span> <span data-ttu-id="4ad24-140">Il se peut également que certaines notifications de modification d’état soient ignorées.</span><span class="sxs-lookup"><span data-stu-id="4ad24-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="4ad24-141">Attendre que la tâche atteigne l’état Terminé en vérifiant la file d’attente toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="4ad24-141">Waits for the job to get to the finished state by checking the queue every 10 seconds.</span></span> <span data-ttu-id="4ad24-142">Supprimer les messages une fois qu’ils ont été traités.</span><span class="sxs-lookup"><span data-stu-id="4ad24-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="4ad24-143">Supprimer la file d’attente et le point de terminaison de notification.</span><span class="sxs-lookup"><span data-stu-id="4ad24-143">Deletes the queue and the notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="4ad24-144">La méthode recommandée pour surveiller l’état d’une tâche consiste à écouter les messages de notification, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4ad24-144">The recommended way to monitor a job’s state is by listening to notification messages, as shown in the following example.</span></span>
>
> <span data-ttu-id="4ad24-145">Vous pouvez également contrôler l'état d'une tâche à l'aide de la propriété **IJob.State** .</span><span class="sxs-lookup"><span data-stu-id="4ad24-145">Alternatively, you could check on a job’s state by using the **IJob.State** property.</span></span>  <span data-ttu-id="4ad24-146">Il se peut qu’un message de notification annonçant la fin d’un travail arrive avant que l’état sur **IJob** soit défini sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="4ad24-146">A notification message about a job’s completion may arrive before the state on **IJob** is set to **Finished**.</span></span> <span data-ttu-id="4ad24-147">La propriété **IJob.State** reflète l’état correct avec un léger retard.</span><span class="sxs-lookup"><span data-stu-id="4ad24-147">The **IJob.State**  property reflects the accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="4ad24-148">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ad24-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="4ad24-149">Configurez votre environnement de développement et ajoutez des informations de connexion au fichier app.config selon la procédure décrite dans l’article [Développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="4ad24-149">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="4ad24-150">Créez un dossier (à tout emplacement sur votre disque local) et copiez-y le fichier .mp4 à encoder et à diffuser en continu ou à télécharger.</span><span class="sxs-lookup"><span data-stu-id="4ad24-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want to encode and stream or progressively download.</span></span> <span data-ttu-id="4ad24-151">Dans cet exemple, le chemin d'accès « C:\Media » est utilisé.</span><span class="sxs-lookup"><span data-stu-id="4ad24-151">In this example, the "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="4ad24-152">Code</span><span class="sxs-lookup"><span data-stu-id="4ad24-152">Code</span></span>

```
using System;
using System.Linq;
using System.Configuration;
using System.IO;
using System.Threading;
using System.Collections.Generic;
using Microsoft.WindowsAzure.MediaServices.Client;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Queue;
using System.Runtime.Serialization.Json;

namespace JobNotification
{
    public class EncodingJobMessage
    {
        // MessageVersion is used for version control.
        public String MessageVersion { get; set; }

        // Type of the event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used to help the customer detect if
        // the message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of the event.
        public String TimeStamp { get; set; }

        // Collection of values specific to the event.

        // For the JobStateChange event the values are:
        //     JobId - Id of the Job that triggered the notification.
        //     NewState- The new state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- The old state of the Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For the NotificationEndpointRegistration event the values are:
        //     NotificationEndpointId- Id of the NotificationEndpoint
        //          that triggered the notification.
        //     State- The state of the Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from the App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
        private static readonly string _StorageConnectionString = 
            ConfigurationManager.AppSettings["StorageConnectionString"];

        private static CloudMediaContext _context = null;
        private static CloudQueue _queue = null;
        private static INotificationEndPoint _notificationEndPoint = null;

        private static readonly string _singleInputMp4Path =
            Path.GetFullPath(@"C:\Media\BigBuckBunny.mp4");

        static void Main(string[] args)
        {
            string endPointAddress = Guid.NewGuid().ToString();

            // Create the context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create the queue that will be receiving the notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create the notification point that is mapped to the queue.
            _notificationEndPoint =
                    _context.NotificationEndPoints.Create(
                    Guid.NewGuid().ToString(), NotificationEndPointType.AzureQueue, endPointAddress);


            if (_notificationEndPoint != null)
            {
                IJob job = SubmitEncodingJobWithNotificationEndPoint(_singleInputMp4Path);
                WaitForJobToReachedFinishedState(job.Id);
            }

            // Clean up.
            _queue.Delete();
            _notificationEndPoint.Delete();
        }


        static public CloudQueue CreateQueue(string storageAccountConnectionString, string endPointAddress)
        {
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageAccountConnectionString);

            // Create the queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference to a queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create the queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 to Smooth Streaming encoding job");

            //Create an encrypted asset and upload the mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass to it the name of the
            // processor to use for the specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with the conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify the input asset to be encoded.
            task.InputAssets.Add(asset);

            // Add an output asset to contain the results of the job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point to the job. You can add multiple notification points.  
            job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly,
                _notificationEndPoint);

            job.Submit();

            return job;
        }

        public static void WaitForJobToReachedFinishedState(string jobId)
        {
            int expectedState = (int)JobState.Finished;
            int timeOutInSeconds = 600;

            bool jobReachedExpectedState = false;
            DateTime startTime = DateTime.Now;
            int jobState = -1;

            while (!jobReachedExpectedState)
            {
                // Specify how often you want to get messages from the queue.
                Thread.Sleep(TimeSpan.FromSeconds(10));

                foreach (var message in _queue.GetMessages(10))
                {
                    using (Stream stream = new MemoryStream(message.AsBytes))
                    {
                        DataContractJsonSerializerSettings settings = new DataContractJsonSerializerSettings();
                        settings.UseSimpleDictionaryFormat = true;
                        DataContractJsonSerializer ser = new DataContractJsonSerializer(typeof(EncodingJobMessage), settings);
                        EncodingJobMessage encodingJobMsg = (EncodingJobMessage)ser.ReadObject(stream);

                        Console.WriteLine();

                        // Display the message information.
                        Console.WriteLine("EventType: {0}", encodingJobMsg.EventType);
                        Console.WriteLine("MessageVersion: {0}", encodingJobMsg.MessageVersion);
                        Console.WriteLine("ETag: {0}", encodingJobMsg.ETag);
                        Console.WriteLine("TimeStamp: {0}", encodingJobMsg.TimeStamp);
                        foreach (var property in encodingJobMsg.Properties)
                        {
                            Console.WriteLine("    {0}: {1}", property.Key, property.Value);
                        }

                        // We are only interested in messages
                        // where EventType is "JobStateChange".
                        if (encodingJobMsg.EventType == "JobStateChange")
                        {
                            string JobId = (String)encodingJobMsg.Properties.Where(j => j.Key == "JobId").FirstOrDefault().Value;
                            if (JobId == jobId)
                            {
                                string oldJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "OldState").FirstOrDefault().Value;
                                string newJobStateStr = (String)encodingJobMsg.Properties.
                                                            Where(j => j.Key == "NewState").FirstOrDefault().Value;

                                JobState oldJobState = (JobState)Enum.Parse(typeof(JobState), oldJobStateStr);
                                JobState newJobState = (JobState)Enum.Parse(typeof(JobState), newJobStateStr);

                                if (newJobState == (JobState)expectedState)
                                {
                                    Console.WriteLine("job with Id: {0} reached expected state: {1}",
                                        jobId, newJobState);
                                    jobReachedExpectedState = true;
                                    break;
                                }
                            }
                        }
                    }
                    // Delete the message after we've read it.
                    _queue.DeleteMessage(message);
                }

                // Wait until timeout
                TimeSpan timeDiff = DateTime.Now - startTime;
                bool timedOut = (timeDiff.TotalSeconds > timeOutInSeconds);
                if (timedOut)
                {
                    Console.WriteLine(@"Timeout for checking job notification messages,
                                        latest found state ='{0}', wait time = {1} secs",
                        jobState,
                        timeDiff.TotalSeconds);

                    throw new TimeoutException();
                }
            }
        }

        static private IAsset CreateAssetAndUploadSingleFile(AssetCreationOptions assetCreationOptions, string singleFilePath)
        {
            var asset = _context.Assets.Create("UploadSingleFile_" + DateTime.UtcNow.ToString(),
                assetCreationOptions);

            var fileName = Path.GetFileName(singleFilePath);

            var assetFile = asset.AssetFiles.Create(fileName);

            Console.WriteLine("Created assetFile {0}", assetFile.Name);
            Console.WriteLine("Upload {0}", assetFile.Name);

            assetFile.Upload(singleFilePath);
            Console.WriteLine("Done uploading of {0}", assetFile.Name);

            return asset;
        }

        static private IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors.Where(p => p.Name == mediaProcessorName).
                ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();

            if (processor == null)
                throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));

            return processor;
        }
    }
}
```
<span data-ttu-id="4ad24-153">L’exemple ci-dessus produit le résultat suivant.</span><span class="sxs-lookup"><span data-stu-id="4ad24-153">The preceding example produced the following output.</span></span> <span data-ttu-id="4ad24-154">Vos valeurs varieront.</span><span class="sxs-lookup"><span data-stu-id="4ad24-154">Your values will vary.</span></span>

    Created assetFile BigBuckBunny.mp4
    Upload BigBuckBunny.mp4
    Done uploading of BigBuckBunny.mp4

    EventType: NotificationEndPointRegistration
    MessageVersion: 1.0
    ETag: e0238957a9b25bdf3351a88e57978d6a81a84527fad03bc23861dbe28ab293f6
    TimeStamp: 2013-05-14T20:22:37
        NotificationEndPointId: nb:nepid:UUID:d6af9412-2488-45b2-ba1f-6e0ade6dbc27
        State: Registered
        Name: dde957b2-006e-41f2-9869-a978870ac620
        Created: 2013-05-14T20:22:35

    EventType: JobStateChange
    MessageVersion: 1.0
    ETag: 4e381f37c2d844bde06ace650310284d6928b1e50101d82d1b56220cfcb6076c
    TimeStamp: 2013-05-14T20:24:40
        JobId: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54
        JobName: My MP4 to Smooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="4ad24-155">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="4ad24-155">Next step</span></span>
<span data-ttu-id="4ad24-156">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="4ad24-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4ad24-157">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4ad24-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
