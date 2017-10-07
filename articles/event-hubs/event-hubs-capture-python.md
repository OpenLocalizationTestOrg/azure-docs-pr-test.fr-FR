---
title: "procédure pas à pas capturer des concentrateurs d’événements aaaAzure | Documents Microsoft"
description: "Exemple qui utilise toodemonstrate du Kit de développement logiciel Azure Python hello à l’aide de la fonctionnalité de Capture des concentrateurs d’événements hello."
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
ms.openlocfilehash: 1737dcca283711d863aa970db0e80ae71814e666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-capture-walkthrough-python"></a>Procédure pas à pas d’Event Hubs Capture : Python

Capturer des concentrateurs d’événements est une fonctionnalité des concentrateurs d’événements qui vous permet de vous tooautomatically remettre hello de diffusion en continu des données dans votre tooan de concentrateur d’événements compte de stockage d’objets Blob Azure de votre choix. Cette fonctionnalité rend facile tooperform traitement par lots sur des données de diffusion en continu en temps réel. Cet article décrit comment capturer les concentrateurs d’événements toouse avec Python. Pour plus d’informations sur la Capture de concentrateurs d’événements, consultez hello [l’article de vue d’ensemble](event-hubs-archive-overview.md).

Cet exemple utilise hello [Azure Python SDK](https://azure.microsoft.com/develop/python/) toodemonstrate la fonctionnalité de Capture hello. programme de sender.py Hello envoie les tooEvent concentrateurs de télémétrie de l’environnement simulé au format JSON. Hello concentrateur d’événements est configuré toouse hello Capture fonctionnalité toowrite ce stockage tooblob des données dans des lots. Hello capturereader.py application lit ces objets BLOB et crée un fichier append par périphérique, puis écrit les données de hello dans les fichiers .csv.

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer

1. Créer un compte de stockage d’objets Blob Azure et un conteneur d’objets blob qu’il contient, à l’aide de hello portail Azure.
2. Créer un espace de noms de concentrateur d’événements à l’aide de hello portail Azure.
3. Créer un concentrateur d’événements avec la fonctionnalité de Capture hello activée, à l’aide de hello portail Azure.
4. Envoyer un concentrateur d’événements toohello données avec un script Python.
5. Lire les fichiers à partir de hello hello capturent et de les traitent avec un autre script Python.

## <a name="prerequisites"></a>Composants requis

- Python 2.7x
- Un abonnement Azure
- Un [espace de noms Event Hubs et un concentrateur d’événements actifs.](event-hubs-create.md)

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="create-an-azure-storage-account"></a>Création d'un compte Azure Storage
1. Ouvrez une session sur toohello [portail Azure][Azure portal].
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **stockage**, puis cliquez sur **compte de stockage**.
3. Renseignez les champs hello dans le panneau de compte de stockage hello et puis cliquez sur **créer**.
   
   ![][1]
4. Une fois que vous consultez hello **déploiements a réussi** , cliquez sur le nom hello du nouveau compte de stockage hello et Bonjour **Essentials** panneau, cliquez sur **BLOB**. Hello lorsque **service Blob** panneau s’ouvre, cliquez sur **+ conteneur** haut hello. Conteneur de hello nom **capture**, puis fermez hello **service Blob** panneau.
5. Cliquez sur **clés d’accès** dans hello gauche lame et copie hello le nom du compte de stockage hello et valeur hello **key1**. Enregistrez ces tooNotepad de valeurs ou un autre emplacement temporaire.

## <a name="create-a-python-script-toosend-events-tooyour-event-hub"></a>Créez un hub d’événements Python script toosend événements tooyour
1. Ouvrez votre éditeur Python favori, tel que [Visual Studio Code][Visual Studio Code].
2. Créez un script appelé **sender.py**. Ce script envoie le concentrateur d’événements tooyour 200 événements. Ce sont de simples lectures environnementales envoyées au format JSON.
3. Collez hello après le code dans sender.py :
   
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
4. Mettre à jour hello précédant toouse de code de votre espace de noms, la valeur de clé et le nom de hub d’événements que vous avez obtenue lors de la création d’espace de noms hello concentrateurs d’événements.

## <a name="create-a-python-script-tooread-your-capture-files"></a>Créer un tooread de script Python vos fichiers de Capture

1. Remplir le panneau de hello et cliquez sur **créer**.
2. Créez un script appelé **capturereader.py**. Ce script lit hello capture les fichiers et crée un fichier de données de périphérique toowrite hello par uniquement pour cet appareil.
3. Collez hello après le code dans capturereader.py :
   
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
4. Être toopaste que les valeurs hello appropriées pour votre nom de compte de stockage et de la clé dans hello appel trop`startProcessing`.

## <a name="run-hello-scripts"></a>Exécuter des scripts de hello
1. Ouvrez une invite de commandes qui a les Python dans son chemin d’accès, puis d’exécuter les packages de composants requis de Python tooinstall ces commandes :
   
  ```
  pip install azure-storage
  pip install azure-servicebus
  pip install avro
  ```
   
  Si vous avez une version antérieure de stockage azure ou azure, vous devrez peut-être toouse hello **--mise à niveau** option
   
  Vous devrez peut-être également suivant de hello toorun (sauf sur la plupart des systèmes) :
   
  ```
  pip install cryptography
  ```
2. Modifier votre toowherever de répertoire que vous avez enregistré sender.py et capturereader.py et exécutez la commande suivante :
   
  ```
  start python sender.py
  ```
   
  Cette commande démarre un nouvelle Python processus toorun hello expéditeur.
3. Maintenant, patientez quelques minutes pour hello capture toorun. Puis tapez Bonjour commande suivante dans votre fenêtre de commande d’origine :
   
   ```
   python capturereader.py
   ```

   Ce processeur capture utilise toodownload de répertoire local hello tous les objets BLOB de hello à partir du compte de stockage hello/conteneur. Il traite tous ceux qui ne sont pas vides et écrit les résultats de hello en tant que fichiers .csv dans le répertoire local de hello.

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Présentation d’Event Hubs Capture][Overview of Event Hubs Capture]
* Un [exemple d'application complet qui utilise des hubs d’événements][sample application that uses Event Hubs].
* Hello [montée en charge le traitement des événements avec des concentrateurs d’événements] [ Scale out Event Processing with Event Hubs] exemple.
* [Vue d’ensemble des hubs d’événements][Event Hubs overview]

[Azure portal]: https://portal.azure.com/
[Overview of Event Hubs Capture]: event-hubs-archive-overview.md
[1]: ./media/event-hubs-archive-python/event-hubs-python1.png
[About Azure storage accounts]:../storage/common/storage-create-storage-account.md
[Visual Studio Code]: https://code.visualstudio.com/
[Event Hubs overview]: event-hubs-overview.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
