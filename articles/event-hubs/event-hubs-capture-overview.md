---
title: "Vue d’ensemble d’Azure Event Hubs Capture | Microsoft Docs"
description: "Capturer les données de télémétrie avec Event Hubs Capture"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="919eb-103">Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="919eb-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="919eb-104">Azure Event Hubs Capture vous permet de fournir automatiquement les données de streaming dans Event Hubs vers un compte [Stockage Blob Azure](https://azure.microsoft.com/services/storage/blobs/) ou [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) de votre choix avec une souplesse accrue permettant de spécifier un intervalle personnalisé de temps ou de taille.</span><span class="sxs-lookup"><span data-stu-id="919eb-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="919eb-105">La configuration de l’outil Capture est rapide : il n’existe aucun coût d’administration pour son exécution et il s’adapte automatiquement à vos [unités de débit](event-hubs-features.md#capacity) Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="919eb-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="919eb-106">Event Hubs Capture représente le moyen le plus simple de charger les données pour la diffusion en continu dans Azure et vous permet de vous concentrer sur le traitement des données plutôt que sur la capture de données.</span><span class="sxs-lookup"><span data-stu-id="919eb-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="919eb-107">Event Hubs Capture vous permet de traiter des pipelines basés sur des lots et en temps réel sur le même flux.</span><span class="sxs-lookup"><span data-stu-id="919eb-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="919eb-108">Cela vous permet de créer des solutions capables d’évoluer avec vos besoins au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="919eb-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="919eb-109">Que vous créiez des systèmes basés sur des lots dès aujourd’hui en pensant au traitement en temps réel à l’avenir, ou que vous souhaitiez ajouter un chemin à froid efficace vers une solution existante en temps réel, Event Hubs Capture facilite la tâche avec les données diffusées en continu.</span><span class="sxs-lookup"><span data-stu-id="919eb-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="919eb-110">Fonctionnement d’Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="919eb-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="919eb-111">Event Hubs est une mémoire tampon durable de rétention temporelle pour l’entrée de télémétrie, similaire à un journal distribué.</span><span class="sxs-lookup"><span data-stu-id="919eb-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="919eb-112">La clé de la mise à l’échelle dans Event Hubs est le [modèle de consommateur partitionné](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="919eb-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="919eb-113">Chaque partition est un segment de données indépendant, et est utilisée de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="919eb-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="919eb-114">Au fil du temps ces données vieillissent, en fonction de la période de rétention configurable.</span><span class="sxs-lookup"><span data-stu-id="919eb-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="919eb-115">Par conséquent, un hub d’événements donné n’est jamais « saturé ».</span><span class="sxs-lookup"><span data-stu-id="919eb-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="919eb-116">Event Hubs Capture vous permet de spécifier votre propre compte Stockage Blob Azure ou Azure Data Lake Store, ainsi qu’un conteneur qui est utilisé pour stocker les données capturées.</span><span class="sxs-lookup"><span data-stu-id="919eb-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="919eb-117">Ces comptes peuvent se trouver dans la même région que votre hub d’événements ou dans une autre région, ce qui ajoute à la flexibilité de la fonctionnalité Event Hubs Capture.</span><span class="sxs-lookup"><span data-stu-id="919eb-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="919eb-118">Les données capturées sont écrites au format [Apache Avro][Apache Avro] : un format compact, rapide et binaire qui fournit des structures de données riches avec un schéma inclus.</span><span class="sxs-lookup"><span data-stu-id="919eb-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="919eb-119">Ce format est largement utilisé dans l’écosystème Hadoop, Stream Analytics et Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="919eb-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="919eb-120">Vous trouverez plus d’informations sur l’utilisation d’Avro plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="919eb-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="919eb-121">Fenêtrage de Capture</span><span class="sxs-lookup"><span data-stu-id="919eb-121">Capture windowing</span></span>

<span data-ttu-id="919eb-122">Event Hubs Capture vous permet de configurer une fenêtre de temps pour le contrôle de la capture.</span><span class="sxs-lookup"><span data-stu-id="919eb-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="919eb-123">Cette fenêtre présente une taille et une configuration temporelle minimales avec une « stratégie de premier gagnant », ce qui signifie que le premier déclencheur rencontré entraîne une opération de capture.</span><span class="sxs-lookup"><span data-stu-id="919eb-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="919eb-124">Si vous avez une fenêtre de capture de quinze minutes et de 100 Mo, et si vous envoyez 1 Mo par seconde, la fenêtre de taille se déclenche avant la fenêtre temporelle.</span><span class="sxs-lookup"><span data-stu-id="919eb-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="919eb-125">Chaque partition capture indépendamment et écrit un objet blob de bloc complet au moment de la capture, nommé d’après l’heure à laquelle l’intervalle de capture a été rencontré.</span><span class="sxs-lookup"><span data-stu-id="919eb-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="919eb-126">La convention d’affectation de noms de stockage est la suivante :</span><span class="sxs-lookup"><span data-stu-id="919eb-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="919eb-127">Mise à l’échelle des unités de débit</span><span class="sxs-lookup"><span data-stu-id="919eb-127">Scaling to throughput units</span></span>

<span data-ttu-id="919eb-128">Le trafic Event Hubs est contrôlé par les [unités de débit](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="919eb-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="919eb-129">Une unité de débit autorise 1 Mo/s ou 1 000 événements par seconde d’entrée et 2 000 événements par seconde de sortie.</span><span class="sxs-lookup"><span data-stu-id="919eb-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="919eb-130">Les concentrateurs d’événements Standard peuvent être configurés avec 1 à 20 unités de débit, et vous pouvez en acheter d’autres en soumettant une [demande de support][support request] d’augmentation de quota.</span><span class="sxs-lookup"><span data-stu-id="919eb-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="919eb-131">L’utilisation au-delà des unités de débit que vous avez achetées est limitée.</span><span class="sxs-lookup"><span data-stu-id="919eb-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="919eb-132">Event Hubs Capture copie les données directement depuis le stockage Event Hubs interne, en contournant les quotas de sortie des unités de débit et en enregistrant votre sortie pour d’autres lecteurs de traitement tels que Stream Analytics ou Spark.</span><span class="sxs-lookup"><span data-stu-id="919eb-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="919eb-133">Une fois configuré, Event Hubs Capture s’exécute automatiquement lorsque vous envoyez votre premier événement et continue de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="919eb-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="919eb-134">Pour que votre traitement en aval sache plus facilement que le processus fonctionne, les Event Hubs écrivent des fichiers vides en l’absence de données.</span><span class="sxs-lookup"><span data-stu-id="919eb-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="919eb-135">Ce processus fournit une cadence prévisible et un marqueur qui peuvent alimenter vos processeurs de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="919eb-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="919eb-136">Configuration de l’outil Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="919eb-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="919eb-137">Vous pouvez configurer la fonctionnalité Capture lors de la création du concentrateur d’événements, à l’aide du [portail Azure](https://portal.azure.com) ou des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="919eb-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="919eb-138">Pour plus d’informations, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="919eb-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="919eb-139">Activer Event Hubs Capture à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="919eb-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="919eb-140">Créer un espace de noms Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="919eb-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="919eb-141">Exploration des fichiers capturés et utilisation d’Avro</span><span class="sxs-lookup"><span data-stu-id="919eb-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="919eb-142">Event Hubs Capture crée des fichiers au format Avro, tel que spécifié dans la fenêtre de temps configurée.</span><span class="sxs-lookup"><span data-stu-id="919eb-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="919eb-143">Vous pouvez afficher ces fichiers à l’aide de n’importe quel outil tel que [l’Explorateur de stockage Azure][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="919eb-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="919eb-144">Vous pouvez télécharger les fichiers localement pour les utiliser.</span><span class="sxs-lookup"><span data-stu-id="919eb-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="919eb-145">Les fichiers générés par Event Hubs Capture présentent le schéma Avro suivant :</span><span class="sxs-lookup"><span data-stu-id="919eb-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="919eb-146">Un moyen facile d’explorer les fichiers Avro consiste à utiliser la boîte à [outils Avro][Avro Tools] d’Apache.</span><span class="sxs-lookup"><span data-stu-id="919eb-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="919eb-147">Après avoir téléchargé cette boîte, vous pouvez voir le schéma d’un fichier Avro spécifique en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="919eb-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="919eb-148">Cette commande renvoie</span><span class="sxs-lookup"><span data-stu-id="919eb-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="919eb-149">Vous pouvez également utiliser les outils Avro pour convertir le fichier au format JSON et effectuer d’autres traitements.</span><span class="sxs-lookup"><span data-stu-id="919eb-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="919eb-150">Pour effectuer un traitement plus avancé, téléchargez et installez Avro pour la plateforme de votre choix.</span><span class="sxs-lookup"><span data-stu-id="919eb-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="919eb-151">Au moment de la rédaction de cet article, les implémentations sont disponibles pour C, C++, C\#, Java, NodeJS, Perl, PHP, Python et Ruby.</span><span class="sxs-lookup"><span data-stu-id="919eb-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="919eb-152">Apache Avro propose des guides de mise en route complets pour [Java][Java] et [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="919eb-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="919eb-153">Vous pouvez également lire l’article [Prise en main d’Event Hubs Capture](event-hubs-capture-python.md).</span><span class="sxs-lookup"><span data-stu-id="919eb-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="919eb-154">Chargement d’Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="919eb-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="919eb-155">Event Hubs Capture est mesuré de la même façon que les unités de débit, au tarif horaire.</span><span class="sxs-lookup"><span data-stu-id="919eb-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="919eb-156">La facturation est directement proportionnelle au nombre d’unités de débit achetées pour l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="919eb-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="919eb-157">En même temps que les unités de débit augmentent et diminuent, Event Hubs Capture augmente et diminue pour fournir des performances adaptées.</span><span class="sxs-lookup"><span data-stu-id="919eb-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="919eb-158">Les compteurs se produisent en même temps.</span><span class="sxs-lookup"><span data-stu-id="919eb-158">The meters occur in tandem.</span></span> <span data-ttu-id="919eb-159">Pour plus d’informations sur les prix appliqués, consultez [Tarification d’Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="919eb-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="919eb-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="919eb-160">Next steps</span></span>

<span data-ttu-id="919eb-161">Event Hubs Capture est la solution la plus simple pour charger des données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="919eb-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="919eb-162">À l’aide d’Azure Data Lake, d’Azure Data Factory et d’Azure HDInsight, vous pouvez effectuer un traitement par lots, ainsi que d’autres analyses en utilisant des outils et des plateformes de votre choix, à l’échelle requise.</span><span class="sxs-lookup"><span data-stu-id="919eb-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="919eb-163">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="919eb-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="919eb-164">Bien démarrer avec l’envoi et la réception d’événements</span><span class="sxs-lookup"><span data-stu-id="919eb-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="919eb-165">Un [exemple d'application complet qui utilise des hubs d’événements][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="919eb-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="919eb-166">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="919eb-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
