---
title: "Procédure détaillée d’Azure Event Hubs Capture | Microsoft Docs"
description: "Exemple qui utilise le Kit de développement logiciel (SDK) Azure Python pour illustrer l’utilisation de la fonctionnalité Event Hubs Capture."
services: event-hubs
documentationcenter: 
author: djrosanova
manager: timlt
editor: 
ms.assetid: bdff820c-5b38-4054-a06a-d1de207f01f6
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: darosa;sethm
ms.openlocfilehash: a764a116755c20f60e92e553bd7c896425272b85
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a><span data-ttu-id="8809e-103">Procédure pas à pas d’Event Hubs Capture : Python</span><span class="sxs-lookup"><span data-stu-id="8809e-103">Event Hubs Capture walkthrough: Python</span></span>

<span data-ttu-id="8809e-104">Event Hubs Capture est une fonctionnalité d’Event Hubs qui vous permet de fournir automatiquement les données de diffusion en continu de votre concentrateur d’événements à un compte de stockage Blob Azure de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8809e-104">Event Hubs Capture is a feature of Event Hubs that enables you to automatically deliver the streaming data in your event hub to an Azure Blob storage account of your choice.</span></span> <span data-ttu-id="8809e-105">Cette fonctionnalité facilite le traitement par lots des données de flux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="8809e-105">This capability makes it easy to perform batch processing on real-time streaming data.</span></span> <span data-ttu-id="8809e-106">Cet article décrit comment utiliser Event Hubs Capture avec Python.</span><span class="sxs-lookup"><span data-stu-id="8809e-106">This article describes how to use Event Hubs Capture with Python.</span></span> <span data-ttu-id="8809e-107">Pour plus d’informations sur Event Hubs Capture, consultez [l’article sur la vue d’ensemble](event-hubs-archive-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8809e-107">For more information about Event Hubs Capture, see the [overview article](event-hubs-archive-overview.md).</span></span>

<span data-ttu-id="8809e-108">Cet exemple utilise le [Kit de développement logiciel (SDK) Azure Python](https://azure.microsoft.com/develop/python/) pour illustrer la fonctionnalité Capture.</span><span class="sxs-lookup"><span data-stu-id="8809e-108">This sample uses the [Azure Python SDK](https://azure.microsoft.com/develop/python/) to demonstrate the Capture feature.</span></span> <span data-ttu-id="8809e-109">Le programme sender.py envoie la télémétrie de l’environnement simulé à Event Hubs au format JSON.</span><span class="sxs-lookup"><span data-stu-id="8809e-109">The sender.py program sends simulated environmental telemetry to Event Hubs in JSON format.</span></span> <span data-ttu-id="8809e-110">Le concentrateur d’événements est configuré pour utiliser la fonctionnalité Capture afin d’écrire ces données dans le stockage Blob en lots.</span><span class="sxs-lookup"><span data-stu-id="8809e-110">The event hub is configured to use the Capture feature to write this data to blob storage in batches.</span></span> <span data-ttu-id="8809e-111">L’application capturereader.py lit ensuite ces objets blob et crée un fichier Append par appareil, puis écrit les données dans des fichiers .csv.</span><span class="sxs-lookup"><span data-stu-id="8809e-111">The capturereader.py app then reads these blobs and creates an append file per device, then writes the data into .csv files.</span></span>

## <a name="what-will-be-accomplished"></a><span data-ttu-id="8809e-112">Les opérations que nous allons effectuer</span><span class="sxs-lookup"><span data-stu-id="8809e-112">What will be accomplished</span></span>

1. <span data-ttu-id="8809e-113">Créer un compte de Stockage Blob Azure et un conteneur d’objets blob dans celui-ci à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8809e-113">Create an Azure Blob Storage account and a blob container within it, using the Azure portal.</span></span>
2. <span data-ttu-id="8809e-114">Créer un espace de noms Event Hub à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8809e-114">Create an Event Hub namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="8809e-115">Créer un concentrateur d’événements avec la fonctionnalité Capture activée à l’aide du Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8809e-115">Create an event hub with the Capture feature enabled, using the Azure portal.</span></span>
4. <span data-ttu-id="8809e-116">Envoyer des données au concentrateur d’événements avec un script Python.</span><span class="sxs-lookup"><span data-stu-id="8809e-116">Send data to the event hub with a Python script.</span></span>
5. <span data-ttu-id="8809e-117">Lire les fichiers de la capture et les traiter avec un autre script Python.</span><span class="sxs-lookup"><span data-stu-id="8809e-117">Read the files from the capture and process them with another Python script.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8809e-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8809e-118">Prerequisites</span></span>

- <span data-ttu-id="8809e-119">Python 2.7x</span><span class="sxs-lookup"><span data-stu-id="8809e-119">Python 2.7.x</span></span>
- <span data-ttu-id="8809e-120">Un abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="8809e-120">An Azure subscription</span></span>
- <span data-ttu-id="8809e-121">Un [espace de noms Event Hubs et un concentrateur d’événements actifs.](event-hubs-create.md)</span><span class="sxs-lookup"><span data-stu-id="8809e-121">An active [Event Hubs namespace and event hub.](event-hubs-create.md)</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="8809e-122">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="8809e-122">Create an Azure Storage account</span></span>
1. <span data-ttu-id="8809e-123">Connectez-vous au [portail Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="8809e-123">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="8809e-124">Dans le panneau de navigation gauche du portail, cliquez sur **Nouveau**, puis sur **Données** et sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="8809e-124">In the left navigation pane of the portal, click **New**, then click **Storage**, and then click **Storage Account**.</span></span>
3. <span data-ttu-id="8809e-125">Renseignez les champs dans le panneau de compte de stockage, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8809e-125">Complete the fields in the storage account blade and then click **Create**.</span></span>
   
   ![][1]
4. <span data-ttu-id="8809e-126">Après l’affichage du message**Déploiements réussis**, cliquez sur le nom du nouveau compte de stockage et, dans le panneau **Bases**, cliquez sur **Objets blob**.</span><span class="sxs-lookup"><span data-stu-id="8809e-126">After you see the **Deployments Succeeded** message, click the name of the new storage account and in the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="8809e-127">Quand le panneau **Service Blob** s’ouvre, cliquez sur **+ Conteneur** en haut.</span><span class="sxs-lookup"><span data-stu-id="8809e-127">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="8809e-128">Nommez la **capture** de conteneur, puis fermez le panneau **Service Blob**.</span><span class="sxs-lookup"><span data-stu-id="8809e-128">Name the container **capture**, then close the **Blob service** blade.</span></span>
5. <span data-ttu-id="8809e-129">Cliquez sur **Clés d’accès** dans le panneau de gauche et copiez le nom du compte de stockage et la valeur de **key1**.</span><span class="sxs-lookup"><span data-stu-id="8809e-129">Click **Access keys** in the left blade and copy the name of the storage account and the value of **key1**.</span></span> <span data-ttu-id="8809e-130">Enregistrez ces valeurs dans le Bloc-notes ou un autre emplacement temporaire.</span><span class="sxs-lookup"><span data-stu-id="8809e-130">Save these values to Notepad or some other temporary location.</span></span>

## <a name="create-a-python-script-to-send-events-to-your-event-hub"></a><span data-ttu-id="8809e-131">Créer un script Python pour envoyer des événements à votre concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="8809e-131">Create a Python script to send events to your event hub</span></span>
1. <span data-ttu-id="8809e-132">Ouvrez votre éditeur Python favori, tel que [Visual Studio Code][Visual Studio Code].</span><span class="sxs-lookup"><span data-stu-id="8809e-132">Open your favorite Python editor, such as [Visual Studio Code][Visual Studio Code].</span></span>
2. <span data-ttu-id="8809e-133">Créez un script appelé **sender.py**.</span><span class="sxs-lookup"><span data-stu-id="8809e-133">Create a script called **sender.py**.</span></span> <span data-ttu-id="8809e-134">Ce script envoie 200 événements à votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="8809e-134">This script sends 200 events to your event hub.</span></span> <span data-ttu-id="8809e-135">Ce sont de simples lectures environnementales envoyées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="8809e-135">They are simple environmental readings sent in JSON.</span></span>
3. <span data-ttu-id="8809e-136">Collez le code suivant dans sender.py :</span><span class="sxs-lookup"><span data-stu-id="8809e-136">Paste the following code into sender.py:</span></span>
   
  ```python
  import uuid
  import datetime
  import random
  import json
  from azure.servicebus import ServiceBusService
   
  sbs = ServiceBusService(service_namespace='INSERT YOUR NAMESPACE NAME', shared_access_key_name='RootManageSharedAccessKey', shared_access_key_value='INSERT YOUR KEY')
  devices = []
  for x in range(0, 10):
      devices.append(str(uuid.uuid4()))
   
  for y in range(0,20):
      for dev in devices:
          reading = {'id': dev, 'timestamp': str(datetime.datetime.utcnow()), 'uv': random.random(), 'temperature': random.randint(70, 100), 'humidity': random.randint(70, 100)}
          s = json.dumps(reading)
          sbs.send_event('INSERT YOUR EVENT HUB NAME', s)
      print y
  ```
4. <span data-ttu-id="8809e-137">Mettez à jour le code précédent pour utiliser votre nom d’espace de noms, vos valeurs de clé et votre nom de concentrateur d’événements obtenus lors de la création de l’espace de noms Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="8809e-137">Update the preceding code to use your namespace name, key value, and event hub name that you obtained when you created the Event Hubs namespace.</span></span>

## <a name="create-a-python-script-to-read-your-capture-files"></a><span data-ttu-id="8809e-138">Créer un script Python pour lire vos fichiers Capture</span><span class="sxs-lookup"><span data-stu-id="8809e-138">Create a Python script to read your Capture files</span></span>

1. <span data-ttu-id="8809e-139">Remplissez les champs du panneau et cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8809e-139">Fill out the blade and click **Create**.</span></span>
2. <span data-ttu-id="8809e-140">Créez un script appelé **capturereader.py**.</span><span class="sxs-lookup"><span data-stu-id="8809e-140">Create a script called **capturereader.py**.</span></span> <span data-ttu-id="8809e-141">Ce script lit les fichiers capturés et crée un fichier par appareil pour écrire les données uniquement pour cet appareil.</span><span class="sxs-lookup"><span data-stu-id="8809e-141">This script reads the captured files and creates a file per device to write the data only for that device.</span></span>
3. <span data-ttu-id="8809e-142">Collez le code suivant dans capturereader.py :</span><span class="sxs-lookup"><span data-stu-id="8809e-142">Paste the following code into capturereader.py:</span></span>
   
  ```python
  import os
  import string
  import json
  import avro.schema
  from avro.datafile import DataFileReader, DataFileWriter
  from avro.io import DatumReader, DatumWriter
  from azure.storage.blob import BlockBlobService
   
  def processBlob(filename):
      reader = DataFileReader(open(filename, 'rb'), DatumReader())
      dict = {}
      for reading in reader:
          parsed_json = json.loads(reading["Body"])
          if not 'id' in parsed_json:
              return
          if not dict.has_key(parsed_json['id']):
              list = []
              dict[parsed_json['id']] = list
          else:
              list = dict[parsed_json['id']]
              list.append(parsed_json)
      reader.close()
      for device in dict.keys():
          deviceFile = open(device + '.csv', "a")
          for r in dict[device]:
              deviceFile.write(", ".join([str(r[x]) for x in r.keys()])+'\n')
   
  def startProcessing(accountName, key, container):
      print 'Processor started using path: ' + os.getcwd()
      block_blob_service = BlockBlobService(account_name=accountName, account_key=key)
      generator = block_blob_service.list_blobs(container)
      for blob in generator:
          if blob.properties.content_length != 0:
              print('Downloaded a non empty blob: ' + blob.name)
              cleanName = string.replace(blob.name, '/', '_')
              block_blob_service.get_blob_to_path(container, blob.name, cleanName)
              processBlob(cleanName)
              os.remove(cleanName)
          block_blob_service.delete_blob(container, blob.name)
  startProcessing('YOUR STORAGE ACCOUNT NAME', 'YOUR KEY', 'capture')
  ```
4. <span data-ttu-id="8809e-143">Veillez à coller les valeurs appropriées pour votre nom de compte de stockage et la clé dans l’appel à `startProcessing`.</span><span class="sxs-lookup"><span data-stu-id="8809e-143">Be sure to paste the appropriate values for your storage account name and key in the call to `startProcessing`.</span></span>

## <a name="run-the-scripts"></a><span data-ttu-id="8809e-144">Exécuter les scripts</span><span class="sxs-lookup"><span data-stu-id="8809e-144">Run the scripts</span></span>
1. <span data-ttu-id="8809e-145">Ouvrez une invite de commandes comprenant Python dans son chemin d’accès, puis exécutez ces commandes pour installer les packages de configuration requise Python :</span><span class="sxs-lookup"><span data-stu-id="8809e-145">Open a command prompt that has Python in its path, and then run these commands to install Python prerequisite packages:</span></span>
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  <span data-ttu-id="8809e-146">Si vous disposez d’une version antérieure de Stockage Azure ou d’Azure, vous devrez peut-être utiliser l’option **--mise à niveau**.</span><span class="sxs-lookup"><span data-stu-id="8809e-146">If you have an earlier version of either azure-storage or azure, you may need to use the **--upgrade** option</span></span>
   
  <span data-ttu-id="8809e-147">Vous devrez peut-être également exécuter les éléments suivants (cela n’est pas nécessaire sur la plupart des systèmes) :</span><span class="sxs-lookup"><span data-stu-id="8809e-147">You might also need to run the following (not necessary on most systems):</span></span>
   
  ```
  pip install cryptography
  ```
2. <span data-ttu-id="8809e-148">Remplacez votre répertoire par celui dans lequel vous avez enregistré sender.py et capturereader.py, puis exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="8809e-148">Change your directory to wherever you saved sender.py and capturereader.py, and run this command:</span></span>
   
  ```
  start python sender.py
  ```
   
  <span data-ttu-id="8809e-149">Cette commande démarre un nouveau processus Python pour exécuter l’expéditeur.</span><span class="sxs-lookup"><span data-stu-id="8809e-149">This command starts a new Python process to run the sender.</span></span>
3. <span data-ttu-id="8809e-150">Attendez quelques minutes pour que la capture s’exécute.</span><span class="sxs-lookup"><span data-stu-id="8809e-150">Now wait a few minutes for the capture to run.</span></span> <span data-ttu-id="8809e-151">Puis tapez la commande suivante dans la fenêtre de commande d’origine :</span><span class="sxs-lookup"><span data-stu-id="8809e-151">Then type the following command into your original command window:</span></span>
   
   ```
   python capturereader.py
   ```

   <span data-ttu-id="8809e-152">Ce processeur de capture utilise le répertoire local pour télécharger tous les objets blob à partir du compte de stockage / conteneur.</span><span class="sxs-lookup"><span data-stu-id="8809e-152">This capture processor uses the local directory to download all the blobs from the storage account/container.</span></span> <span data-ttu-id="8809e-153">Il traite tous ceux qui ne sont pas vides et écrit les résultats sous la forme de fichiers .csv dans le répertoire local.</span><span class="sxs-lookup"><span data-stu-id="8809e-153">It processes any that are not empty, and writes the results as .csv files into the local directory.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8809e-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8809e-154">Next steps</span></span>

<span data-ttu-id="8809e-155">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="8809e-155">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="8809e-156">[Présentation d’Event Hubs Capture][Overview of Event Hubs Capture]</span><span class="sxs-lookup"><span data-stu-id="8809e-156">[Overview of Event Hubs Capture][Overview of Event Hubs Capture]</span></span>
* <span data-ttu-id="8809e-157">Un [exemple d'application complet qui utilise des hubs d’événements][sample application that uses Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="8809e-157">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs].</span></span>
* <span data-ttu-id="8809e-158">L’exemple de [montée en puissance du traitement des événements avec Event Hubs][Scale out Event Processing with Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="8809e-158">The [Scale out Event Processing with Event Hubs][Scale out Event Processing with Event Hubs] sample.</span></span>
* <span data-ttu-id="8809e-159">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="8809e-159">[Event Hubs overview][Event Hubs overview]</span></span>

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
