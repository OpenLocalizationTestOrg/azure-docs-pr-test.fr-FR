---
title: "aaaUse file d’attente Azure storage toomonitor Media Services notifications du travail avec .NET | Documents Microsoft"
description: "Découvrez comment toomonitor de stockage toouse file d’attente Azure Media Services de notifications de la tâche. exemple de code Hello est écrite en c# et utilise hello Media Services SDK pour .NET."
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
ms.openlocfilehash: e4068621ada00d763133dc0d01cfc666b53f8b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-queue-storage-toomonitor-media-services-job-notifications-with-net"></a><span data-ttu-id="61278-104">Utiliser des notifications de travaux de file d’attente Azure storage toomonitor Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="61278-104">Use Azure Queue storage toomonitor Media Services job notifications with .NET</span></span>
<span data-ttu-id="61278-105">Lorsque vous exécutez des tâches d’encodage, vous nécessitent souvent une progression du travail tootrack moyen.</span><span class="sxs-lookup"><span data-stu-id="61278-105">When you run encoding jobs, you often require a way tootrack job progress.</span></span> <span data-ttu-id="61278-106">Vous pouvez configurer des notifications de Media Services toodeliver trop[stockage de file d’attente Azure](../storage/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="61278-106">You can configure Media Services toodeliver notifications too[Azure Queue storage](../storage/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="61278-107">Vous pouvez surveiller la progression du travail par les notifications de mise en route de hello stockage de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="61278-107">You can monitor job progress by getting notifications from hello Queue storage.</span></span> 

<span data-ttu-id="61278-108">Messages remis tooQueue stockage est accessible à partir de n’importe où dans Bonjour.</span><span class="sxs-lookup"><span data-stu-id="61278-108">Messages delivered tooQueue storage can be accessed from anywhere in hello world.</span></span> <span data-ttu-id="61278-109">Hello architecture de messagerie de stockage de file d’attente est fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="61278-109">hello Queue storage messaging architecture is reliable and highly scalable.</span></span> <span data-ttu-id="61278-110">L’interrogation du Stockage File d’attente pour les messages est préférable aux autres méthodes.</span><span class="sxs-lookup"><span data-stu-id="61278-110">Polling Queue storage for messages is recommended over using other methods.</span></span>

<span data-ttu-id="61278-111">Un scénario courant pour les notifications de Services tooMedia écoute est si vous développez un système de gestion de contenu qui doit tooperform certaines tâches supplémentaires après un travail d’encodage se termine (par exemple, l’étape suivante de tootrigger hello dans un flux de travail, ou toopublish contenu).</span><span class="sxs-lookup"><span data-stu-id="61278-111">One common scenario for listening tooMedia Services notifications is if you are developing a content management system that needs tooperform some additional task after an encoding job completes (for example, tootrigger hello next step in a workflow, or toopublish content).</span></span>

<span data-ttu-id="61278-112">Cette rubrique montre comment les messages de notification de tooget à partir du stockage de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="61278-112">This topic shows how tooget notification messages from Queue storage.</span></span>  

## <a name="considerations"></a><span data-ttu-id="61278-113">Considérations</span><span class="sxs-lookup"><span data-stu-id="61278-113">Considerations</span></span>
<span data-ttu-id="61278-114">Considérez les éléments suivants de hello lors du développement d’applications de Media Services qui utilisent le stockage de file d’attente :</span><span class="sxs-lookup"><span data-stu-id="61278-114">Consider hello following when developing Media Services applications that use Queue storage:</span></span>

* <span data-ttu-id="61278-115">Le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée (FIFO).</span><span class="sxs-lookup"><span data-stu-id="61278-115">Queue storage does not provide a guarantee of first-in-first-out (FIFO) ordered delivery.</span></span> <span data-ttu-id="61278-116">Pour plus d'informations, consultez [Files d'attente Azure et files d'attente Azure Service Bus - comparaison et différences](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span><span class="sxs-lookup"><span data-stu-id="61278-116">For more information, see [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://msdn.microsoft.com/library/azure/hh767287.aspx).</span></span>
* <span data-ttu-id="61278-117">Le Stockage File d’attente n’est pas un service push.</span><span class="sxs-lookup"><span data-stu-id="61278-117">Queue storage is not a push service.</span></span> <span data-ttu-id="61278-118">Vous avez la file d’attente de toopoll hello.</span><span class="sxs-lookup"><span data-stu-id="61278-118">You have toopoll hello queue.</span></span>
* <span data-ttu-id="61278-119">Le nombre de files d’attente est illimité.</span><span class="sxs-lookup"><span data-stu-id="61278-119">You can have any number of queues.</span></span> <span data-ttu-id="61278-120">Pour plus d'informations, consultez [API REST du service de file d'attente](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span><span class="sxs-lookup"><span data-stu-id="61278-120">For more information, see [Queue Service REST API](https://docs.microsoft.com/rest/api/storageservices/Queue-Service-REST-API).</span></span>
* <span data-ttu-id="61278-121">Stockage de file d’attente a certaines limites et certaines toobe spécificités prenant en charge de.</span><span class="sxs-lookup"><span data-stu-id="61278-121">Queue storage has some limitations and specifics toobe aware of.</span></span> <span data-ttu-id="61278-122">Celles-ci sont décrites dans [Files d’attente Azure et files d’attente Azure Service Bus - comparaison et différences](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span><span class="sxs-lookup"><span data-stu-id="61278-122">These are described in [Azure Queues and Azure Service Bus Queues Compared and Contrasted](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted).</span></span>

## <a name="net-code-example"></a><span data-ttu-id="61278-123">Exemple de code .NET</span><span class="sxs-lookup"><span data-stu-id="61278-123">.NET code example</span></span>

<span data-ttu-id="61278-124">exemple de code Hello dans cette section hello suivant :</span><span class="sxs-lookup"><span data-stu-id="61278-124">hello code example in this section does hello following:</span></span>

1. <span data-ttu-id="61278-125">Définit hello **EncodingJobMessage** classe qui mappe le format de message de notification toohello.</span><span class="sxs-lookup"><span data-stu-id="61278-125">Defines hello **EncodingJobMessage** class that maps toohello notification message format.</span></span> <span data-ttu-id="61278-126">code de Hello désérialise les messages reçus à partir de la file d’attente hello dans les objets de hello **EncodingJobMessage** type.</span><span class="sxs-lookup"><span data-stu-id="61278-126">hello code deserializes messages received from hello queue into objects of hello **EncodingJobMessage** type.</span></span>
2. <span data-ttu-id="61278-127">Charges hello Media Services et les informations de compte de stockage du fichier app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="61278-127">Loads hello Media Services and Storage account information from hello app.config file.</span></span> <span data-ttu-id="61278-128">exemple de code Hello utilise cette hello de toocreate informations **CloudMediaContext** et **CloudQueue** objets.</span><span class="sxs-lookup"><span data-stu-id="61278-128">hello code example uses this information toocreate hello **CloudMediaContext** and **CloudQueue** objects.</span></span>
3. <span data-ttu-id="61278-129">Crée une file d’attente hello qui reçoit les messages de notification sur hello travail d’encodage.</span><span class="sxs-lookup"><span data-stu-id="61278-129">Creates hello queue that receives notification messages about hello encoding job.</span></span>
4. <span data-ttu-id="61278-130">Crée la notification hello point de terminaison qui est mappé à la file d’attente de toohello.</span><span class="sxs-lookup"><span data-stu-id="61278-130">Creates hello notification end point that is mapped toohello queue.</span></span>
5. <span data-ttu-id="61278-131">Attache le travail de toohello de point de terminaison de notification hello et soumet le travail d’encodage hello.</span><span class="sxs-lookup"><span data-stu-id="61278-131">Attaches hello notification end point toohello job and submits hello encoding job.</span></span> <span data-ttu-id="61278-132">Vous pouvez avoir plusieurs notification des points de terminaison attachés tooa travail.</span><span class="sxs-lookup"><span data-stu-id="61278-132">You can have multiple notification end points attached tooa job.</span></span>
6. <span data-ttu-id="61278-133">Passe **NotificationJobState.FinalStatesOnly** toohello **AddNew** (méthode).</span><span class="sxs-lookup"><span data-stu-id="61278-133">Passes **NotificationJobState.FinalStatesOnly** toohello **AddNew** method.</span></span> <span data-ttu-id="61278-134">(Dans cet exemple, nous intéresse uniquement les États finaux de traitement hello.)</span><span class="sxs-lookup"><span data-stu-id="61278-134">(In this example, we are only interested in final states of hello job processing.)</span></span>

        job.JobNotificationSubscriptions.AddNew(NotificationJobState.FinalStatesOnly, _notificationEndPoint);
7. <span data-ttu-id="61278-135">Si vous passez **NotificationJobState.All**, vous obtenez tous hello suivant des notifications de changement d’état : en file d’attente, planifié, le traitement et terminé.</span><span class="sxs-lookup"><span data-stu-id="61278-135">If you pass **NotificationJobState.All**, you get all of hello following state change notifications: queued, scheduled, processing, and finished.</span></span> <span data-ttu-id="61278-136">Toutefois, comme indiqué précédemment, le Stockage File d’attente ne garantit pas une remise dans l’ordre d’arrivée.</span><span class="sxs-lookup"><span data-stu-id="61278-136">However, as noted earlier, Queue storage does not guarantee ordered delivery.</span></span> <span data-ttu-id="61278-137">les messages tooorder, utilisez hello **Timestamp** propriété (définie sur hello **EncodingJobMessage** type dans l’exemple hello ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="61278-137">tooorder messages, use hello **Timestamp** property (defined on hello **EncodingJobMessage** type in hello example below).</span></span> <span data-ttu-id="61278-138">Les messages en double sont possibles.</span><span class="sxs-lookup"><span data-stu-id="61278-138">Duplicate messages are possible.</span></span> <span data-ttu-id="61278-139">toocheck les doublons, utilisez hello **propriété ETag** (défini sur hello **EncodingJobMessage** type).</span><span class="sxs-lookup"><span data-stu-id="61278-139">toocheck for duplicates, use hello **ETag property** (defined on hello **EncodingJobMessage** type).</span></span> <span data-ttu-id="61278-140">Il se peut également que certaines notifications de modification d’état soient ignorées.</span><span class="sxs-lookup"><span data-stu-id="61278-140">It is also possible that some state change notifications get skipped.</span></span>
8. <span data-ttu-id="61278-141">Attend que hello travail tooget toohello terminé état par la vérification de la file d’attente hello toutes les 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="61278-141">Waits for hello job tooget toohello finished state by checking hello queue every 10 seconds.</span></span> <span data-ttu-id="61278-142">Supprimer les messages une fois qu’ils ont été traités.</span><span class="sxs-lookup"><span data-stu-id="61278-142">Deletes messages after they have been processed.</span></span>
9. <span data-ttu-id="61278-143">Supprime la file d’attente hello et le point de terminaison de notification hello.</span><span class="sxs-lookup"><span data-stu-id="61278-143">Deletes hello queue and hello notification end point.</span></span>

> [!NOTE]
> <span data-ttu-id="61278-144">Bonjour toomonitor recommandé pour que l’état d’un travail est en écoute les messages toonotification, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="61278-144">hello recommended way toomonitor a job’s state is by listening toonotification messages, as shown in hello following example.</span></span>
>
> <span data-ttu-id="61278-145">Vous pourriez également vérifier sur l’état d’un travail à l’aide de hello **IJob.State** propriété.</span><span class="sxs-lookup"><span data-stu-id="61278-145">Alternatively, you could check on a job’s state by using hello **IJob.State** property.</span></span>  <span data-ttu-id="61278-146">Un message de notification sur l’achèvement d’une tâche peut arrivent avant d’état de hello sur **IJob** est défini trop**terminé**.</span><span class="sxs-lookup"><span data-stu-id="61278-146">A notification message about a job’s completion may arrive before hello state on **IJob** is set too**Finished**.</span></span> <span data-ttu-id="61278-147">Hello **IJob.State** propriété reflète état précis de hello avec un léger retard.</span><span class="sxs-lookup"><span data-stu-id="61278-147">hello **IJob.State**  property reflects hello accurate state with a slight delay.</span></span>
>
>

### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="61278-148">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61278-148">Create and configure a Visual Studio project</span></span>

1. <span data-ttu-id="61278-149">Configurer votre environnement de développement et de remplir le fichier app.config de hello avec les informations de connexion, comme décrit dans [développement Media Services avec .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="61278-149">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 
2. <span data-ttu-id="61278-150">Créer un nouveau dossier (dossier peut être n’importe où sur votre disque local) et copiez le fichier .mp4 que vous voulez tooencode et flux de données ou téléchargez progressivement.</span><span class="sxs-lookup"><span data-stu-id="61278-150">Create a new folder (folder can be anywhere on your local drive) and copy an .mp4 file that you want tooencode and stream or progressively download.</span></span> <span data-ttu-id="61278-151">Dans cet exemple, le chemin d’accès de hello « C:\Media » est utilisé.</span><span class="sxs-lookup"><span data-stu-id="61278-151">In this example, hello "C:\Media" path is used.</span></span>

### <a name="code"></a><span data-ttu-id="61278-152">Code</span><span class="sxs-lookup"><span data-stu-id="61278-152">Code</span></span>

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

        // Type of hello event. Valid values are
        // JobStateChange and NotificationEndpointRegistration.
        public String EventType { get; set; }

        // ETag is used toohelp hello customer detect if
        // hello message is a duplicate of another message previously sent.
        public String ETag { get; set; }

        // Time of occurrence of hello event.
        public String TimeStamp { get; set; }

        // Collection of values specific toohello event.

        // For hello JobStateChange event hello values are:
        //     JobId - Id of hello Job that triggered hello notification.
        //     NewState- hello new state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished
        //     OldState- hello old state of hello Job. Valid values are:
        //          Scheduled, Processing, Canceling, Cancelled, Error, Finished

        // For hello NotificationEndpointRegistration event hello values are:
        //     NotificationEndpointId- Id of hello NotificationEndpoint
        //          that triggered hello notification.
        //     State- hello state of hello Endpoint.
        //          Valid values are: Registered and Unregistered.

        public IDictionary<string, object> Properties { get; set; }
    }

    class Program
    {

        // Read values from hello App.config file.
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

            // Create hello context.
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Create hello queue that will be receiving hello notification messages.
            _queue = CreateQueue(_StorageConnectionString, endPointAddress);

            // Create hello notification point that is mapped toohello queue.
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

            // Create hello queue client
            CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

            // Retrieve a reference tooa queue
            CloudQueue queue = queueClient.GetQueueReference(endPointAddress);

            // Create hello queue if it doesn't already exist
            queue.CreateIfNotExists();

            return queue;
        }


        public static IJob SubmitEncodingJobWithNotificationEndPoint(string inputMediaFilePath)
        {
            // Declare a new job.
            IJob job = _context.Jobs.Create("My MP4 tooSmooth Streaming encoding job");

            //Create an encrypted asset and upload hello mp4.
            IAsset asset = CreateAssetAndUploadSingleFile(AssetCreationOptions.StorageEncrypted,
                inputMediaFilePath);

            // Get a media processor reference, and pass tooit hello name of the
            // processor toouse for hello specific task.
            IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Standard");

            // Create a task with hello conversion details, using a configuration file.
            ITask task = job.Tasks.AddNew("My encoding Task",
                processor,
                "Adaptive Streaming",
                Microsoft.WindowsAzure.MediaServices.Client.TaskOptions.None);

            // Specify hello input asset toobe encoded.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("Output asset",
                AssetCreationOptions.None);

            // Add a notification point toohello job. You can add multiple notification points.  
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
                // Specify how often you want tooget messages from hello queue.
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

                        // Display hello message information.
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
                    // Delete hello message after we've read it.
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
<span data-ttu-id="61278-153">Bonjour précédent exemple produit hello suivant de sortie.</span><span class="sxs-lookup"><span data-stu-id="61278-153">hello preceding example produced hello following output.</span></span> <span data-ttu-id="61278-154">Vos valeurs varieront.</span><span class="sxs-lookup"><span data-stu-id="61278-154">Your values will vary.</span></span>

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
        JobName: My MP4 tooSmooth Streaming encoding job
        NewState: Finished
        OldState: Processing
        AccountName: westeuropewamsaccount
    job with Id: nb:jid:UUID:526291de-f166-be47-b62a-11ffe6d4be54 reached expected
    State: Finished


## <a name="next-step"></a><span data-ttu-id="61278-155">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="61278-155">Next step</span></span>
<span data-ttu-id="61278-156">Consultez les parcours d’apprentissage de Media Services.</span><span class="sxs-lookup"><span data-stu-id="61278-156">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61278-157">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="61278-157">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
