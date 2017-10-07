---
title: "aaaHow toouse le stockage Blob Azure (stockage d’objets) à partir de Python | Documents Microsoft"
description: "Stocker des données non structurées dans le cloud hello avec le stockage d’objets Blob Azure (stockage d’objets)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Comment toouse le stockage Blob Azure à partir de Python
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Vue d'ensemble
Stockage d’objets Blob Azure est un service qui stocke des données non structurées dans le cloud de hello en tant qu’objets/BLOB. Ce service peut stocker tout type de données texte ou binaires, par exemple, un document, un fichier multimédia ou un programme d’installation d’application. Stockage d’objets BLOB est également référencé tooas stockage d’objets.

Cet article vous indiquent comment les scénarios courants tooperform à l’aide du stockage d’objets Blob. exemples de Hello sont écrites dans Python et utiliser hello [le stockage Microsoft Azure SDK pour Python]. les scénarios de Hello couvertes incluent le téléchargement, liste, le téléchargement et suppression d’objets BLOB.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Créez un conteneur.
En fonction de type hello d’objet blob vous aimeriez toouse, créez un **BlockBlobService**, **AppendBlobService**, ou **PageBlobService** objet. code Hello suivant utilise un **BlockBlobService** objet. Ajoutez les éléments suivants de hello haut hello de n’importe quel fichier Python dans lequel vous souhaitez tooprogrammatically accès stockage d’objets Blob Azure bloc.

```python
from azure.storage.blob import BlockBlobService
```

Hello de code suivant crée un **BlockBlobService** objet à l’aide de la clé de compte et le nom du compte de stockage hello.  Remplacez « myaccount » et « mykey » par le nom et la clé réels de votre compte.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Bonjour exemple de code suivant, vous pouvez utiliser un **BlockBlobService** le conteneur objet toocreate hello si elle n’existe pas.

```python
block_blob_service.create_container('mycontainer')
```

Par défaut, le nouveau conteneur de hello est privé, vous devez spécifier votre clé d’accès (comme précédemment) BLOB toodownload à partir de ce conteneur. Si vous souhaitez que les objets BLOB toomake hello tooeveryone disponibles du conteneur hello, vous pouvez créer un conteneur de hello et passer le niveau d’accès public hello à l’aide de hello suivant de code.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Ou bien, vous pouvez modifier un conteneur une fois que vous avez créé à l’aide de hello suivant de code.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Après cette modification, toute personne sur Internet de hello peut voir les objets BLOB dans un conteneur public, mais vous pouvez uniquement modifier ou les supprimer.

## <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
toocreate un objet blob de blocs et les données de téléchargement, utilisez hello **créer\_blob\_de\_chemin d’accès**, **créer\_blob\_de\_flux**, **créer\_blob\_de\_octets** ou **créer\_blob\_de\_texte** méthodes. Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.

**créer\_blob\_de\_chemin d’accès** téléchargements hello le contenu d’un fichier à partir du chemin d’accès spécifié hello, et **créer\_blob\_de\_flux** téléchargements hello contenu à partir d’un flux de fichier/déjà ouvert. **créer\_blob\_de\_octets** télécharge un tableau d’octets, et **créer\_blob\_de\_texte** télécharge hello spécifié valeur de texte à l’aide de hello spécifié d’encodage (valeurs par défaut tooUTF-8).

exemple Hello télécharge contenu hello Hello **sunset.png** fichier hello **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur
objets BLOB de hello toolist dans un conteneur, utilisez hello **liste\_BLOB** (méthode). Cette méthode retourne un générateur. Hello de code suivant génère hello **nom** de chaque objet blob dans une console toohello de conteneur.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Télécharger des objets blob
toodownload des données à partir d’un objet blob, utilisez **obtenir\_blob\_à\_chemin d’accès**, **obtenir\_blob\_à\_flux**, **obtenir\_blob\_à\_octets**, ou **obtenir\_blob\_à\_texte**. Ce sont des méthodes de haut niveau qui effectuent la segmentation nécessaire hello lorsque la taille de hello de données de hello dépasse 64 Mo.

Hello exemple suivant montre comment utiliser **obtenir\_blob\_à\_chemin d’accès** contenu de hello toodownload Hello **myblob** d’objets blob et le stocker toohello **hors-sunset.png** fichier.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Supprimer un objet blob
Enfin, toodelete un objet blob, appelez **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Écriture tooan ajouter des objets blob
Il est optimisé pour les opérations d’ajout, telles que la journalisation. Comme un objet blob de blocs, un objet blob d’ajout est constitué de blocs, mais lorsque vous ajoutez un nouvel objet blob bloc tooan append, il est toujours ajouté toohello de fin de l’objet blob de hello. Vous ne pouvez pas mettre à jour ou supprimer un bloc dans un objet blob d’ajout. ID de bloc Hello pour un objet blob d’ajout ne sont pas exposés à ceux d’un objet blob de blocs.

Chaque bloc dans un objet blob d’ajout peut avoir une taille différente, les tooa au maximum de 4 Mo, et un objet blob d’ajout peut inclure un maximum de 50 000 blocs. Hello taille maximale d’un objet blob d’ajout est par conséquent légèrement supérieur à 195 Go (4 Mo X avec 50 000 blocs).

exemple Hello ci-dessous crée un nouvel objet blob d’ajout et ajoute certaines tooit de données, en simulant une opération de journalisation simple.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello du stockage Blob, suivez ces liens de toolearn plus.

* [Centre de développement Python](https://azure.microsoft.com/develop/python/)
* [API REST des services d’Azure Storage](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog de l'équipe Azure Storage]
* [le stockage Microsoft Azure SDK pour Python]

[Blog de l'équipe Azure Storage]: http://blogs.msdn.com/b/windowsazurestorage/
[le stockage Microsoft Azure SDK pour Python]: https://github.com/Azure/azure-storage-python
