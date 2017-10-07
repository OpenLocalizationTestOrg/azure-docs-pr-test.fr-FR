---
title: "le chiffrement côté aaaClient avec Python pour Microsoft Azure Storage | Documents Microsoft"
description: "Hello bibliothèque cliente de stockage Azure pour Python prend en charge le chiffrement côté client pour une sécurité maximale pour vos applications de stockage Azure."
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: d2e943977322b97b777369508b957a1b2cbaa4e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Chiffrement côté client avec Python pour Microsoft Azure Storage
[!INCLUDE [storage-selector-client-side-encryption-include](../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Vue d'ensemble
Hello [bibliothèque cliente de stockage Azure pour Python](https://pypi.python.org/pypi/azure-storage) prend en charge le chiffrement des données dans les applications clientes avant chargement tooAzure stockage et le déchiffrement des données lors du téléchargement de toohello client.

> [!NOTE]
> bibliothèque de Python de stockage Azure Hello est en version préliminaire.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Chiffrement et déchiffrement via la technique d’enveloppe hello
processus de Hello de chiffrement et déchiffrement suivent technique d’enveloppe hello.

### <a name="encryption-via-hello-envelope-technique"></a>Chiffrement via la technique d’enveloppe hello
Le chiffrement via la technique d’enveloppe hello fonctionne Bonjour de configuration suivant :

1. bibliothèque cliente de stockage Azure Hello génère une clé de chiffrement de contenu (CEK), qui est une clé symétrique usage unique.
2. Les données utilisateur sont chiffrées à l'aide de cette clé de chiffrement de contenu.
3. Hello CEK est ensuite encapsulée (chiffré) à l’aide de la clé de chiffrement à clé hello (KEK). Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique, qui est gérée localement.
   bibliothèque cliente de stockage Hello lui-même n’a jamais accès tooKEK. bibliothèque de Hello appelle clé hello algorithme est fourni par hello veillent d’habillage. Les utilisateurs peuvent choisir de toouse des fournisseurs personnalisés pour l’habillage/désencapsuler une clé si vous le souhaitez.
4. Hello données chiffrées seront ensuite téléchargé toohello le service Azure Storage. clé encapsulée de Hello, ainsi que des métadonnées de chiffrement supplémentaire est stockée en tant que métadonnées (sur un objet blob) ou interpolée avec des données hello chiffré (messages de la file d’attente et les entités de table).

### <a name="decryption-via-hello-envelope-technique"></a>Déchiffrement via la technique d’enveloppe hello
Déchiffrement via la technique d’enveloppe hello fonctionne Bonjour de configuration suivant :

1. bibliothèque du client Hello suppose que l’utilisateur hello est la gestion de clé de chiffrement à clé hello (KEK) localement. utilisateur de Hello ne nécessite pas de clé spécifique tooknow hello qui a été utilisé pour le chiffrement. Au lieu de cela, vous pouvez définir un programme de résolution de clé, qui résout les identificateurs de clé différentes tookeys, et l’utiliser.
2. bibliothèque cliente de Hello télécharge des données de hello chiffrée, ainsi que tout le matériel de chiffrement qui est stocké sur le service de hello.
3. clé de chiffrement de contenu encapsulée Hello (CEK) est désencapsulé (déchiffrés) avec hello clé de chiffrement de clés (KEK). Ici encore, hello client bibliothèque n’a pas accès tooKEK. Il appelle simplement algorithme de désencapsuler du fournisseur personnalisé hello.
4. Hello contenu de la clé de chiffrement (CEK) est ensuite utilisé données toodecrypt hello chiffré de l’utilisateur.

## <a name="encryption-mechanism"></a>Mécanisme de chiffrement
bibliothèque cliente de stockage Hello utilise [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) dans l’ordre tooencrypt utilisateur. Plus précisément, le mode [CBC (Cipher Block Chaining)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) avec AES. Chaque service fonctionnant un peu différemment, nous allons les étudier un par un ici.

### <a name="blobs"></a>Objets blob
bibliothèque cliente de Hello prend actuellement en charge le chiffrement des objets BLOB entier uniquement. Plus précisément, le chiffrement est pris en charge lorsque les utilisateurs utilisent hello **créer*** méthodes. Les téléchargements complets et les téléchargements de plages sont pris en charge, et la parallélisation du chargement et du téléchargement est disponible.

Au cours du chiffrement, bibliothèque cliente de hello génère un vecteur d’initialisation aléatoire (IV) de 16 octets, avec une clé de chiffrement aléatoire de contenu (CEK) de 32 octets et effectuer le chiffrement d’enveloppe de données d’objet blob hello à l’aide de ces informations. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaire sont ensuite stockées comme métadonnées ainsi que de l’objet blob chiffré de hello sur le service de hello d’objets blob.

> [!WARNING]
> Si vous modifiez ou téléchargez vos propres métadonnées pour l’objet blob de hello, vous devez tooensure que ces métadonnées sont conservée. Si vous téléchargez les nouvelles métadonnées sans ces métadonnées, hello CEK encapsulé, vecteur d’initialisation et d’autres métadonnées sont perdues et le contenu blob hello ne sera jamais récupérable à nouveau.
> 
> 

Téléchargement d’un objet blob chiffré implique la récupération de contenu hello d’objet blob entier hello à l’aide de hello **obtenir*** méthodes pratiques. Hello encapsulé est désencapsulé et la clé utilisée avec le vecteur d’initialisation hello (stocké en tant que métadonnées de l’objet blob dans ce cas) tooreturn hello déchiffré données toohello utilisateurs.

Télécharger une plage aléatoire (**obtenir*** méthodes avec des paramètres de la plage passé) Bonjour blob chiffré implique l’ajustement de plage hello fournie par les utilisateurs dans l’ordre tooget une petite quantité de données supplémentaires qui peuvent être utilisées toosuccessfully decrypt hello a demandé la plage.

Les objets blob de blocs et les objets blob de pages peuvent être chiffrés/déchiffrés à l’aide de ce schéma. Il n’existe actuellement aucune prise en charge pour le chiffrement des objets blob d’ajout.

### <a name="queues"></a>Files d’attente
Étant donné que les messages de la file d’attente peuvent être de n’importe quel format, bibliothèque cliente de hello définit un format personnalisé qui inclut hello vecteur d’initialisation (IV) et clé de chiffrement de contenu chiffré hello (CEK) dans le texte du message hello.

Au cours du chiffrement, la bibliothèque cliente de hello génère un vecteur d’initialisation aléatoire de 16 octets avec une clé aléatoire de 32 octets et effectue le chiffrement d’enveloppe du texte de message hello file d’attente à l’aide de ces informations. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaires sont ajoutés puis message chiffré de file d’attente de toohello. Ce message modifié (voir ci-dessous) est stocké sur le service de hello.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Au cours du déchiffrement, clé encapsulée de hello est extrait du message de file d’attente hello et désencapsulé. Hello IV est également extrait du message de file d’attente hello et utilisée avec les données de message hello désencapsulé toodecrypt clé hello file d’attente. Notez que les métadonnées chiffrement hello sont faible (sous 500 octets), alors que cela compte limite de 64 Ko hello pour un message de la file d’attente, impact de hello doit donc être facile à gérer.

### <a name="tables"></a>Tables
Hello client bibliothèque prend en charge le chiffrement des propriétés d’entité pour l’insertion d’opérations et de remplacement.

> [!NOTE]
> La fusion n’est pas prise en charge pour le moment. Dans la mesure où un sous-ensemble de propriétés aient été crypté précédemment à l’aide d’une autre clé, simplement la fusion de nouvelles propriétés de hello et mise à jour des métadonnées de hello entraîne une perte de données. La fusion soit nécessite un service supplémentaire appels entité de tooread hello existant à partir du service de hello, ou à l’aide d’une nouvelle clé par propriété, qui ne conviennent pas pour des raisons de performances.
> 
> 

Le chiffrement des données d’une table fonctionne de la manière suivante :

1. Les utilisateurs spécifient hello propriétés toobe est chiffré.
2. bibliothèque cliente de Hello génère un vecteur d’initialisation aléatoire (IV) de 16 octets avec une clé de chiffrement aléatoire de contenu (CEK) de 32 octets pour chaque entité et effectue le chiffrement d’enveloppe sur toobe de propriétés individuelles hello chiffré en dérivant d’un nouveau vecteur d’initialisation par propriété. propriété de Hello chiffrée est stockée en tant que données binaires.
3. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaire sont ensuite stockées en tant que deux propriétés réservées supplémentaires. Hello réservé tout d’abord la propriété (\_ClientEncryptionMetadata1) est une propriété de chaîne qui conserve des informations de hello sur IV, version et la clé encapsulée. Hello propriété deuxième réservée (\_ClientEncryptionMetadata2) est une propriété binaire qui conserve des informations de hello sur les propriétés de hello sont chiffrés. Hello les informations contenues dans cette seconde propriété (\_ClientEncryptionMetadata2) est elle-même chiffrée.
4. En raison de propriétés réservées supplémentaires toothese obligatoire pour le chiffrement, les utilisateurs peuvent désormais avoir uniquement 250 propriétés personnalisées au lieu de 252. taille totale de Hello d’entité de hello doit être inférieure à 1 Mo.
   
   Notez que seules les propriétés de type chaîne peuvent être chiffrées. Si les autres types de propriétés sont toobe chiffrée, ils doivent être toostrings converti. chaînes de Hello chiffrée sont stockées sur le service de hello en tant que propriétés binaires, et elles sont converties en arrière toostrings (chaînes brutes, non EntityProperties avec type EdmType.STRING) après le déchiffrement.
   
   Pour les tables, en outre toohello de stratégie de chiffrement, les utilisateurs doivent spécifier hello propriétés toobe est chiffré. Cela est possible à stocker ces propriétés dans les objets TableEntity avec tooEdmType.STRING de jeu de type hello et chiffrer l’ensemble tootrue ou paramètre hello encryption_resolver_function sur l’objet de tableservice hello. Un programme de résolution de chiffrement est une fonction qui prend une clé de partition, une clé de ligne et un nom de propriété, puis renvoie une valeur booléenne indiquant si cette propriété doit être chiffrée. Au cours du chiffrement, bibliothèque cliente de hello utilisera cette toodecide informations si une propriété doit être chiffrée lors de l’écriture toohello câble. délégué de Hello prévoit également de la possibilité de hello de logique autour de la façon dont les propriétés sont cryptées. (Par exemple, si X, alors chiffrer la propriété A ; sinon chiffrer les propriétés A et B.) Notez qu’il est tooprovide n’est pas nécessaire de ces informations lors de la lecture ou l’interrogation des entités.

### <a name="batch-operations"></a>Opérations de traitement par lots
Une stratégie de chiffrement s’applique tooall des lignes dans le lot de hello. bibliothèque cliente de Hello en interne génère un nouveau vecteur d’initialisation aléatoire et une clé aléatoire par ligne dans le lot de hello. Les utilisateurs peuvent également choisir tooencrypt des propriétés différentes pour chaque opération dans le lot de hello en définissant ce comportement dans le programme de résolution de chiffrement hello.
Si un lot est créé comme un gestionnaire de contexte via la méthode de batch() tableservice hello, stratégie de chiffrement de hello tableservice sera automatiquement appliqué toohello lot. Si un lot est créé explicitement en appelant le constructeur de hello, stratégie de chiffrement hello doit être passé comme paramètre et gauche non modifié pour la durée de vie hello du lot de hello.
Notez que les entités soient chiffrées qu’elles sont insérées dans le lot de hello à l’aide de la stratégie de chiffrement du lot hello (entités ne sont pas chiffrées au moment de hello de la validation de lot de hello à l’aide de la stratégie de chiffrement de tableservice hello).

### <a name="queries"></a>Requêtes
opérations de requête tooperform, vous devez spécifier un programme de résolution de clé qui est en mesure de tooresolve tous hello clés dans le jeu de résultats hello. Si une entité contenue dans le résultat de la requête hello ne peut pas être résolu tooa fournisseur, la bibliothèque cliente de hello génère une erreur. Pour toute requête qui effectue des projections côté serveur, bibliothèque cliente de hello ajoutera des propriétés de métadonnées de chiffrement spéciaux hello (\_ClientEncryptionMetadata1 et \_ClientEncryptionMetadata2) par défaut toohello les colonnes sélectionnées .

> [!IMPORTANT]
> Tenez compte des points importants suivants quand vous utilisez le chiffrement côté client :
> 
> * Quand tooan de lecture ou écriture chiffrées blob, utilisez les commandes de téléchargement blob entier et commandes de téléchargement d’objets blob plage/entier. Évitez d’écrire tooan objet blob chiffré à l’aide du protocole opérations telles que mettre le bloc, placez la liste de blocs, écrire les Pages ou désactivez Pages ; dans le cas contraire, vous pouvez endommager l’objet blob chiffré de hello et rendre illisible.
> * Pour les tables, une contrainte similaire existe. Propriétés de mise à jour chiffrée toonot prudent sans mettre à jour les métadonnées de chiffrement hello être.
> * Si vous définissez des métadonnées sur l’objet blob chiffré de hello, vous pouvez remplacer hello des métadonnées relatives au chiffrement requises pour le déchiffrement, car la définition des métadonnées n’est pas additif. Cela est également vrai pour les instantanés : évitez de spécifier des métadonnées lors de la création d’un instantané d’objet blob chiffré. Si les métadonnées doivent être définies, être vraiment toocall hello **get_blob_metadata** tooget de première méthode hello des métadonnées de chiffrement en cours et d’éviter les écritures simultanées lors de la définition de métadonnées.
> * Activer hello **require_encryption** indicateur sur l’objet de service hello pour les utilisateurs qui doivent utiliser uniquement les données chiffrées. Pour plus d’informations, consultez la section ci-dessous.
> 
> 

bibliothèque cliente de stockage Hello attend hello fourni veillent et résolveur clé hello tooimplement suivant l’interface. [d’d’Azure Key Vault](https://azure.microsoft.com/services/key-vault/) pour la gestion de la clé de chiffrement de clés (KEK) Python est en attente et sera intégrée ultérieurement à cette bibliothèque.

## <a name="client-api--interface"></a>API/Interface cliente
Après avoir créé un objet de service de stockage (c'est-à-dire blockblobservice), hello utilisateur peut attribuer des valeurs des champs toohello qui constituent une stratégie de chiffrement : key_encryption_key, key_resolver_function et require_encryption. Les utilisateurs peuvent fournir uniquement une KEK, uniquement un programme de résolution ou les deux. key_encryption_key est hello base type de clé qui est identifié à l’aide d’un identificateur de clé et qui fournit une logique de hello pour la Désencapsulation / l’habillage. key_resolver_function est tooresolve utilisé une clé pendant le processus de déchiffrement hello. Elle retourne une KEK valide avec un identificateur de clé. Cela fournit aux utilisateurs hello capacité toochoose entre plusieurs clés qui sont gérés dans plusieurs emplacements.

Hello veillent doit implémenter suivant de hello méthodes toosuccessfully chiffrer les données :

* wrap_key(cek) : enveloppe hello spécifié CEK (octets) à l’aide d’un algorithme de choix de l’utilisateur hello. Hello de retourne encapsulée clé.
* get_key_wrap_algorithm() : retourne hello l’algorithme utilisé toowrap clés.
* get_kid() : retourne hello chaîne id de clé pour cette KEK.
  Hello veillent doit implémenter hello méthodes toosuccessfully decrypt données suivantes :
* unwrap_key (cek, algorithme) : retourne hello désencapsulé Hello spécifiée clé CEK à l’aide d’algorithme de chaîne spécifiée hello.
* get_kid() : retourne un ID de clé de type chaîne pour cette KEK.

programme de résolution clé Hello doit implémenter au moins une méthode renvoyant, étant donné un id de la clé, hello veillent implémentation hello interface correspondante ci-dessus. Seulement cette méthode est toobe affectée propriété key_resolver_function de toohello sur l’objet de service hello.

* Pour le chiffrement, clé de hello est toujours utilisé et absence hello d’une clé entraîne une erreur.
* Pour le déchiffrement :
  
  * programme de résolution clé Hello est appelée si spécifié tooget hello clé. Si le programme de résolution hello est spécifié mais n’a pas d’un mappage pour l’identificateur de clé hello, une erreur est générée.
  * Si le programme de résolution n’est pas spécifié, mais une clé est spécifiée, clé de hello est utilisée si son identificateur correspond à l’identificateur de clé hello requis. Si l’identificateur de hello ne correspond pas, une erreur est générée.
    
    Hello d’exemples de chiffrement dans azure.storage.samples <fix URL>illustrent un scénario de bout en bout plus détaillé pour les objets BLOB, les files d’attente et les tables.
      Exemples d’implémentation de hello de clés et de programme de résolution de clé sont fournies dans les fichiers d’exemple hello en tant que KeyWrapper et KeyResolver respectivement.

### <a name="requireencryption-mode"></a>Mode RequireEncryption
Les utilisateurs peuvent éventuellement activer un mode de fonctionnement dans lequel tous les chargements et téléchargements doivent être chiffrés. Dans ce mode, les tentatives des données de tooupload sans un chiffrement stratégie ou téléchargement de données qui ne sont pas chiffrées sur le service de hello échoue sur le client de hello. Hello **require_encryption** indicateur sur des contrôles d’objet hello service ce comportement.

### <a name="blob-service-encryption"></a>Chiffrement du service BLOB
Définir des champs de stratégie de chiffrement hello sur l’objet de blockblobservice hello. Tout le reste sera gérée par la bibliothèque cliente de hello en interne.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Chiffrement du service de File d’attente
Définir des champs de stratégie de chiffrement hello sur l’objet de queueservice hello. Tout le reste sera gérée par la bibliothèque cliente de hello en interne.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Chiffrement du service de Table
En outre toocreating une stratégie de chiffrement et en le définissant sur les options de requête, vous devez spécifier soit un **encryption_resolver_function** sur hello **tableservice**, ou hello du jeu de chiffrement de l’attribut sur Hello EntityProperty.

### <a name="using-hello-resolver"></a>À l’aide du programme de résolution hello

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Utilisation des attributs
Comme indiqué ci-dessus, une propriété peut être marquée pour le chiffrement en les stockant dans un objet EntityProperty et paramètre hello de chiffrer le champ.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Chiffrement et performances
Notez que le chiffrement de vos données de stockage affecte les performances. Hello contenu clé et vecteur d’initialisation doivent être générée, contenu hello lui-même doit être chiffré, et des métadonnées supplémentaires doivent être mis en forme et téléchargée. Cette surcharge varie en fonction de la quantité de hello de données en cours de chiffrement. Nous recommandons de tester systématiquement les performances des applications au cours du développement.

## <a name="next-steps"></a>Étapes suivantes
* Télécharger hello [bibliothèque cliente de stockage Azure pour Java PyPi package](https://pypi.python.org/pypi/azure-storage)
* Télécharger hello [bibliothèque cliente de stockage Azure pour Python le Code Source à partir de GitHub](https://github.com/Azure/azure-storage-python)
