---
title: "aaaOverview de capturer les concentrateurs d’événements Azure | Documents Microsoft"
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
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="3c34e-103">Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="3c34e-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="3c34e-104">Capturer les concentrateurs d’événements Azure vous permet de hello de remise tooautomatically diffusion en continu des données dans des concentrateurs d’événements tooan [le stockage Blob Azure](https://azure.microsoft.com/services/storage/blobs/) ou [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) compte de votre choix, par hello une plus grande flexibilité spécifier un intervalle de temps ou de taille.</span><span class="sxs-lookup"><span data-stu-id="3c34e-104">Azure Event Hubs Capture enables you tooautomatically deliver hello streaming data in Event Hubs tooan [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with hello added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="3c34e-105">Configuration de Capture est rapide, il n’existe aucune toorun les coûts administratifs et il met à l’échelle automatiquement avec les concentrateurs d’événements [unités de débit](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="3c34e-105">Setting up Capture is fast, there are no administrative costs toorun it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="3c34e-106">Capturer des concentrateurs d’événements est tooload moyen plus simple de hello, diffusion en continu des données dans Azure et vous permet de toofocus sur le traitement des données plutôt que sur la capture de données.</span><span class="sxs-lookup"><span data-stu-id="3c34e-106">Event Hubs Capture is hello easiest way tooload streaming data into Azure, and enables you toofocus on data processing rather than on data capture.</span></span>

<span data-ttu-id="3c34e-107">Capturer des concentrateurs d’événements vous permet de tooprocess en temps réel et en fonction de traitement par lots des pipelines sur hello même flux.</span><span class="sxs-lookup"><span data-stu-id="3c34e-107">Event Hubs Capture enables you tooprocess real-time and batch-based pipelines on hello same stream.</span></span> <span data-ttu-id="3c34e-108">Cela vous permet de créer des solutions capables d’évoluer avec vos besoins au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="3c34e-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="3c34e-109">Si vous créez des systèmes lot aujourd'hui avec un œil vers un traitement ultérieur en temps réel ou si vous souhaitez tooadd une solution en temps réel efficace de chemin d’accès à froid tooan existante, capturer des concentrateurs d’événements rend l’utilisation de la diffusion en continu de données plus facilement.</span><span class="sxs-lookup"><span data-stu-id="3c34e-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want tooadd an efficient cold path tooan existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="3c34e-110">Fonctionnement d’Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="3c34e-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="3c34e-111">Event Hubs est une mémoire tampon de rétention de temps durable pour l’entrée de données de télémétrie, journal de distribuées tooa similaire.</span><span class="sxs-lookup"><span data-stu-id="3c34e-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar tooa distributed log.</span></span> <span data-ttu-id="3c34e-112">tooscaling de clé Hello dans les concentrateurs d’événements est hello [modèle de consommateur partitionné](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="3c34e-112">hello key tooscaling in Event Hubs is hello [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="3c34e-113">Chaque partition est un segment de données indépendant, et est utilisée de manière indépendante.</span><span class="sxs-lookup"><span data-stu-id="3c34e-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="3c34e-114">Au fil du temps de que ces données soient hors tension, selon la période de rétention configurable hello.</span><span class="sxs-lookup"><span data-stu-id="3c34e-114">Over time this data ages off, based on hello configurable retention period.</span></span> <span data-ttu-id="3c34e-115">Par conséquent, un hub d’événements donné n’est jamais « saturé ».</span><span class="sxs-lookup"><span data-stu-id="3c34e-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="3c34e-116">Capturer des concentrateurs d’événements permet de vous toospecify votre propre compte de stockage d’objets Blob Azure et un conteneur ou un compte Azure Data Lake Store, qui sont des données hello capturée toostore utilisé.</span><span class="sxs-lookup"><span data-stu-id="3c34e-116">Event Hubs Capture enables you toospecify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used toostore hello captured data.</span></span> <span data-ttu-id="3c34e-117">Ces comptes peuvent être Bonjour même région que votre concentrateur d’événements ou dans une autre région, ajout d’une grande souplesse toohello de fonctionnalité de Capture des concentrateurs d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="3c34e-117">These accounts can be in hello same region as your event hub or in another region, adding toohello flexibility of hello Event Hubs Capture feature.</span></span>

<span data-ttu-id="3c34e-118">Les données capturées sont écrites au format [Apache Avro][Apache Avro] : un format compact, rapide et binaire qui fournit des structures de données riches avec un schéma inclus.</span><span class="sxs-lookup"><span data-stu-id="3c34e-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="3c34e-119">Ce format est largement utilisé dans Azure Data Factory écosystème de Hadoop hello et Analytique de flux de données.</span><span class="sxs-lookup"><span data-stu-id="3c34e-119">This format is widely used in hello Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="3c34e-120">Vous trouverez plus d’informations sur l’utilisation d’Avro plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3c34e-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="3c34e-121">Fenêtrage de Capture</span><span class="sxs-lookup"><span data-stu-id="3c34e-121">Capture windowing</span></span>

<span data-ttu-id="3c34e-122">Vous tooset d’une capture de fenêtre toocontrol permet de capturer des concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="3c34e-122">Event Hubs Capture enables you tooset up a window toocontrol capturing.</span></span> <span data-ttu-id="3c34e-123">Cette fenêtre est une taille minimale et la configuration de l’heure avec une « premier wins stratégie, « ce qui signifie que qui hello les causes première déclencheur a rencontré une opération de capture.</span><span class="sxs-lookup"><span data-stu-id="3c34e-123">This window is a minimum size and time configuration with a "first wins policy," meaning that hello first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="3c34e-124">Si vous avez un quinze minutes, 100 Mo fenêtre de capture et envoyer 1 Mo par seconde, les déclencheurs de fenêtre de taille hello avant la fenêtre de temps hello.</span><span class="sxs-lookup"><span data-stu-id="3c34e-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, hello size window triggers before hello time window.</span></span> <span data-ttu-id="3c34e-125">Chaque partition indépendamment de capture et écrit un objet blob de bloc terminé lors de la capture, hello nommé pour le moment hello à quels hello intervalle de capture a été rencontrée.</span><span class="sxs-lookup"><span data-stu-id="3c34e-125">Each partition captures independently and writes a completed block blob at hello time of capture, named for hello time at which hello capture interval was encountered.</span></span> <span data-ttu-id="3c34e-126">convention d’affectation de noms de stockage Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c34e-126">hello storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a><span data-ttu-id="3c34e-127">Mise à l’échelle des unités de toothroughput</span><span class="sxs-lookup"><span data-stu-id="3c34e-127">Scaling toothroughput units</span></span>

<span data-ttu-id="3c34e-128">Le trafic Event Hubs est contrôlé par les [unités de débit](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="3c34e-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="3c34e-129">Une unité de débit autorise 1 Mo/s ou 1 000 événements par seconde d’entrée et 2 000 événements par seconde de sortie.</span><span class="sxs-lookup"><span data-stu-id="3c34e-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="3c34e-130">Les concentrateurs d’événements Standard peuvent être configurés avec 1 à 20 unités de débit, et vous pouvez en acheter d’autres en soumettant une [demande de support][support request] d’augmentation de quota.</span><span class="sxs-lookup"><span data-stu-id="3c34e-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="3c34e-131">L’utilisation au-delà des unités de débit que vous avez achetées est limitée.</span><span class="sxs-lookup"><span data-stu-id="3c34e-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="3c34e-132">Capturer des concentrateurs d’événements de copie les données directement à partir de stockage de concentrateurs d’événements interne hello, en ignorant les quotas de sortie unité de débit et de l’enregistrement de votre sortie pour les autres lecteurs de traitement, telles que les flux de données Analytique ou Spark.</span><span class="sxs-lookup"><span data-stu-id="3c34e-132">Event Hubs Capture copies data directly from hello internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="3c34e-133">Une fois configuré, Event Hubs Capture s’exécute automatiquement lorsque vous envoyez votre premier événement et continue de s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="3c34e-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="3c34e-134">toomake de votre tooknow de traitement en aval hello processus fonctionne, les concentrateurs d’événements écrit les fichiers vides lorsqu’il n’existe aucune donnée.</span><span class="sxs-lookup"><span data-stu-id="3c34e-134">toomake it easier for your downstream processing tooknow that hello process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="3c34e-135">Ce processus fournit une cadence prévisible et un marqueur qui peuvent alimenter vos processeurs de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="3c34e-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="3c34e-136">Configuration de l’outil Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="3c34e-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="3c34e-137">Vous pouvez configurer la Capture au moment de la création du hub d’événements hello à l’aide de hello [portail Azure](https://portal.azure.com), ou à l’aide de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3c34e-137">You can configure Capture at hello event hub creation time using hello [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="3c34e-138">Pour plus d’informations, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="3c34e-138">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="3c34e-139">Activer la Capture de concentrateurs d’événements à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3c34e-139">Enable Event Hubs Capture using hello Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="3c34e-140">Créer un espace de noms Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3c34e-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a><span data-ttu-id="3c34e-141">Exploration des fichiers de hello capturée et l’utilisation de Avro</span><span class="sxs-lookup"><span data-stu-id="3c34e-141">Exploring hello captured files and working with Avro</span></span>

<span data-ttu-id="3c34e-142">Capturer des concentrateurs d’événements crée des fichiers au format Avro, tel que spécifié dans la fenêtre de temps hello configuré.</span><span class="sxs-lookup"><span data-stu-id="3c34e-142">Event Hubs Capture creates files in Avro format, as specified on hello configured time window.</span></span> <span data-ttu-id="3c34e-143">Vous pouvez afficher ces fichiers à l’aide de n’importe quel outil tel que [l’Explorateur de stockage Azure][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="3c34e-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="3c34e-144">Vous pouvez télécharger hello fichiers localement toowork sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="3c34e-144">You can download hello files locally toowork on them.</span></span>

<span data-ttu-id="3c34e-145">fichiers Hello produites par la Capture des concentrateurs d’événements ont hello suivant du schéma Avro :</span><span class="sxs-lookup"><span data-stu-id="3c34e-145">hello files produced by Event Hubs Capture have hello following Avro schema:</span></span>

![][3]

<span data-ttu-id="3c34e-146">Un moyen simple tooexplore Avro des fichiers est à l’aide de hello [Avro outils] [ Avro Tools] jar d’Apache.</span><span class="sxs-lookup"><span data-stu-id="3c34e-146">An easy way tooexplore Avro files is by using hello [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="3c34e-147">Après avoir téléchargé ce fichier jar, vous pouvez voir le schéma hello d’un fichier Avro spécifique en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3c34e-147">After downloading this jar, you can see hello schema of a specific Avro file by running hello following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="3c34e-148">Cette commande renvoie</span><span class="sxs-lookup"><span data-stu-id="3c34e-148">This command returns</span></span>

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

<span data-ttu-id="3c34e-149">Vous pouvez également utiliser le format tooJSON fichier Avro outils tooconvert hello et effectuer d’autres traitements.</span><span class="sxs-lookup"><span data-stu-id="3c34e-149">You can also use Avro Tools tooconvert hello file tooJSON format and perform other processing.</span></span>

<span data-ttu-id="3c34e-150">tooperform plus avancé du traitement, téléchargement et installer Avro votre choix de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="3c34e-150">tooperform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="3c34e-151">Au moment de hello de rédaction de cet article, les implémentations sont disponibles pour C, C++, C\#, Java, NodeJS, Perl, PHP, Python et Ruby.</span><span class="sxs-lookup"><span data-stu-id="3c34e-151">At hello time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="3c34e-152">Apache Avro propose des guides de mise en route complets pour [Java][Java] et [Python][Python].</span><span class="sxs-lookup"><span data-stu-id="3c34e-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="3c34e-153">Vous pouvez également lire hello [mise en route avec la Capture des concentrateurs d’événements](event-hubs-capture-python.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="3c34e-153">You can also read hello [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="3c34e-154">Chargement d’Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="3c34e-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="3c34e-155">Capturer des concentrateurs d’événements est limitée de même les unités toothroughput : comme un tarif horaire.</span><span class="sxs-lookup"><span data-stu-id="3c34e-155">Event Hubs Capture is metered similarly toothroughput units: as an hourly charge.</span></span> <span data-ttu-id="3c34e-156">frais de Hello sont nombre toohello directement proportionnelle d’unités de débit achetées pour l’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="3c34e-156">hello charge is directly proportional toohello number of throughput units purchased for hello namespace.</span></span> <span data-ttu-id="3c34e-157">Comme unités de débit augmentent et diminuent, compteurs de capturer des concentrateurs d’événements augmentent et diminuent les tooprovide correspondance des performances.</span><span class="sxs-lookup"><span data-stu-id="3c34e-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease tooprovide matching performance.</span></span> <span data-ttu-id="3c34e-158">compteurs de Hello se produisent en tandem.</span><span class="sxs-lookup"><span data-stu-id="3c34e-158">hello meters occur in tandem.</span></span> <span data-ttu-id="3c34e-159">Pour plus d’informations sur les prix appliqués, consultez [Tarification d’Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="3c34e-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3c34e-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c34e-160">Next steps</span></span>

<span data-ttu-id="3c34e-161">Capturer des concentrateurs d’événements est hello plus simple des tooget données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3c34e-161">Event Hubs Capture is hello easiest way tooget data into Azure.</span></span> <span data-ttu-id="3c34e-162">À l’aide d’Azure Data Lake, d’Azure Data Factory et d’Azure HDInsight, vous pouvez effectuer un traitement par lots, ainsi que d’autres analyses en utilisant des outils et des plateformes de votre choix, à l’échelle requise.</span><span class="sxs-lookup"><span data-stu-id="3c34e-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="3c34e-163">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="3c34e-163">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="3c34e-164">Bien démarrer avec l’envoi et la réception d’événements</span><span class="sxs-lookup"><span data-stu-id="3c34e-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="3c34e-165">Un [exemple d'application complet qui utilise des hubs d’événements][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="3c34e-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="3c34e-166">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="3c34e-166">[Event Hubs overview][Event Hubs overview]</span></span>

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
