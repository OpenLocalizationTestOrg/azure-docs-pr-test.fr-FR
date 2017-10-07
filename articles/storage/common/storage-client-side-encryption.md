---
title: "le chiffrement côté aaaClient avec .NET de Microsoft Azure Storage | Documents Microsoft"
description: "Hello bibliothèque cliente de stockage Azure pour .NET prend en charge le chiffrement côté client et l’intégration avec le coffre de clés Azure pour une sécurité maximale pour vos applications de stockage Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c09246f43801e17aff96ea453182d11ffbf5e420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Vue d'ensemble
Hello [bibliothèque cliente de stockage Azure pour .NET Nuget package](https://www.nuget.org/packages/WindowsAzure.Storage) prend en charge le chiffrement des données dans les applications clientes avant chargement tooAzure stockage et le déchiffrement des données lors du téléchargement de toohello client. bibliothèque de Hello prend également en charge l’intégration avec [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) pour la gestion de clés de compte de stockage.

Pour obtenir un didacticiel qui vous guide tout au long des processus de hello de chiffrement d’objets BLOB à l’aide du chiffrement côté client et le coffre de clés Azure, consultez [chiffrer et déchiffrer des objets BLOB dans Microsoft Azure Storage à l’aide d’Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).

Pour le chiffrement côté client avec Java, consultez la page [Chiffrement côté client avec Java pour Microsoft Azure Storage](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Chiffrement et déchiffrement via la technique d’enveloppe hello
processus de Hello de chiffrement et déchiffrement suivent technique d’enveloppe hello.

### <a name="encryption-via-hello-envelope-technique"></a>Chiffrement via la technique d’enveloppe hello
Le chiffrement via la technique d’enveloppe hello fonctionne Bonjour de configuration suivant :

1. bibliothèque cliente de stockage Azure Hello génère une clé de chiffrement de contenu (CEK), qui est une clé symétrique usage unique.
2. Les données utilisateur sont chiffrées à l'aide de cette clé de chiffrement de contenu.
3. Hello CEK est ensuite encapsulée (chiffré) à l’aide de la clé de chiffrement à clé hello (KEK). Hello veillent est identifié par un identificateur de clé et peut être une paire de clés asymétriques ou une clé symétrique et peut être géré localement ou stockée dans des coffres de clé Azure.
   
    bibliothèque cliente de stockage Hello lui-même n’a jamais accès tooKEK. bibliothèque de Hello appelle algorithme hello encapsulage de clé fourni par le coffre de clés. Les utilisateurs peuvent choisir de toouse des fournisseurs personnalisés pour l’habillage/désencapsuler une clé si vous le souhaitez.

4. Hello données chiffrées seront ensuite téléchargé toohello le service Azure Storage. clé encapsulée de Hello, ainsi que des métadonnées de chiffrement supplémentaire est stockée en tant que métadonnées (sur un objet blob) ou interpolée avec des données hello chiffré (messages de la file d’attente et les entités de table).

### <a name="decryption-via-hello-envelope-technique"></a>Déchiffrement via la technique d’enveloppe hello
Déchiffrement via la technique d’enveloppe hello fonctionne Bonjour de configuration suivant :

1. bibliothèque du client Hello suppose que l’utilisateur hello est la gestion de clé de chiffrement à clé hello (KEK) localement ou dans des coffres de clé Azure. utilisateur de Hello ne nécessite pas de clé spécifique tooknow hello qui a été utilisé pour le chiffrement. Au lieu de cela, vous pouvez définir un programme de résolution de clés qui résout les identificateurs de clé différentes tookeys et l’utiliser.
2. bibliothèque cliente de Hello télécharge des données de hello chiffrée, ainsi que tout le matériel de chiffrement qui est stocké sur le service de hello.
3. clé de chiffrement de contenu encapsulée Hello (CEK) est désencapsulé (déchiffrés) avec hello clé de chiffrement de clés (KEK). Ici encore, hello client bibliothèque n’a pas accès tooKEK. Il appelle simplement hello personnalisé ou l’algorithme de désencapsuler du fournisseur de coffre de clés.
4. Hello contenu de la clé de chiffrement (CEK) est ensuite utilisé données toodecrypt hello chiffré de l’utilisateur.

## <a name="encryption-mechanism"></a>Mécanisme de chiffrement
bibliothèque cliente de stockage Hello utilise [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) dans l’ordre tooencrypt utilisateur. Plus précisément, le mode [CBC (Cipher Block Chaining)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) avec AES. Chaque service fonctionnant un peu différemment, nous allons les étudier un par un ici.

### <a name="blobs"></a>Objets blob
bibliothèque cliente de Hello prend actuellement en charge le chiffrement des objets BLOB entier uniquement. Plus précisément, le chiffrement est pris en charge lorsque les utilisateurs utilisent hello **UploadFrom*** méthodes ou hello **OpenWrite** (méthode). Les téléchargements complets et de plages sont tous deux pris en charge.

Au cours du chiffrement, bibliothèque cliente de hello génère un vecteur d’initialisation aléatoire (IV) de 16 octets, avec une clé de chiffrement aléatoire de contenu (CEK) de 32 octets et effectuer le chiffrement d’enveloppe de données d’objet blob hello à l’aide de ces informations. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaire sont ensuite stockées comme métadonnées ainsi que de l’objet blob chiffré de hello sur le service de hello d’objets blob.

> [!WARNING]
> Si vous modifiez ou téléchargez vos propres métadonnées pour l’objet blob de hello, vous devez tooensure que ces métadonnées sont conservée. Si vous téléchargez les nouvelles métadonnées sans ces métadonnées, hello encapsulée CEK, IV et autres métadonnées sont perdues et le contenu blob hello ne sera jamais récupérable à nouveau.
> 
> 

Téléchargement d’un objet blob chiffré implique la récupération de contenu hello d’objet blob entier hello à l’aide de hello **DownloadTo***/**BlobReadStream** commodité méthodes. Hello encapsulé est désencapsulé et la clé utilisée avec le vecteur d’initialisation hello (stocké en tant que métadonnées de l’objet blob dans ce cas) tooreturn hello déchiffré données toohello utilisateurs.

Télécharger une plage aléatoire (**DownloadRange*** méthodes) Bonjour blob chiffré implique l’ajustement de plage de hello fournies par les utilisateurs dans l’ordre tooget une petite quantité de données supplémentaires qui peuvent être utilisé toosuccessfully déchiffrer hello plage demandée.

Tous les types d’objets blob (objets blob de blocs, objets blob de pages et objets blob d’ajouts) peuvent être chiffrés/déchiffrés à l’aide de ce schéma.

### <a name="queues"></a>Files d’attente
Étant donné que les messages de la file d’attente peuvent être de n’importe quel format, bibliothèque cliente de hello définit un format personnalisé qui inclut hello vecteur d’initialisation (IV) et clé de chiffrement de contenu chiffré hello (CEK) dans le texte du message hello.

Au cours du chiffrement, la bibliothèque cliente de hello génère un vecteur d’initialisation aléatoire de 16 octets avec une clé aléatoire de 32 octets et effectue le chiffrement d’enveloppe du texte de message hello file d’attente à l’aide de ces informations. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaires sont ajoutés puis message chiffré de file d’attente de toohello. Ce message modifié (voir ci-dessous) est stocké sur le service de hello.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

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
3. Hello encapsulée CEK et des métadonnées de chiffrement supplémentaire sont ensuite stockées en tant que deux propriétés réservées supplémentaires. propriété réservée première Hello (_ClientEncryptionMetadata1) est une propriété de chaîne qui conserve des informations de hello sur IV, version et la clé encapsulée. propriété réservée deuxième Hello (_ClientEncryptionMetadata2) est une propriété binaire qui contient des informations de hello sur les propriétés de hello sont chiffrés. informations Hello dans ce deuxième propriété (_ClientEncryptionMetadata2) sont elle-même chiffrée.
4. En raison de propriétés réservées supplémentaires toothese obligatoire pour le chiffrement, les utilisateurs peuvent désormais avoir uniquement 250 propriétés personnalisées au lieu de 252. taille totale de Hello d’entité de hello doit être inférieure à 1 Mo.

Notez que seules les propriétés de type chaîne peuvent être chiffrées. Si les autres types de propriétés sont toobe chiffrée, ils doivent être toostrings converti. chaînes de Hello chiffrée sont stockées sur le service de hello en tant que propriétés binaires, et elles sont converties en arrière toostrings après le déchiffrement.

Pour les tables, en outre toohello de stratégie de chiffrement, les utilisateurs doivent spécifier hello propriétés toobe est chiffré. Pour ce faire, il faut spécifier un attribut EncryptProperty \(pour les entités POCO qui dérivent de TableEntity) ou un programme de résolution de chiffrement dans les options de requête. Un programme de résolution de chiffrement est un délégué qui prend une clé de partition, une clé de ligne et un nom de propriété, puis renvoie une valeur booléenne indiquant si cette propriété doit être chiffrée. Au cours du chiffrement, bibliothèque cliente de hello utilisera cette toodecide informations si une propriété doit être chiffrée lors de l’écriture toohello câble. délégué de Hello prévoit également de la possibilité de hello de logique autour de la façon dont les propriétés sont cryptées. (Par exemple, si X, alors chiffrer la propriété A ; sinon chiffrer les propriétés A et B.) Notez qu’il est tooprovide n’est pas nécessaire de ces informations lors de la lecture ou l’interrogation des entités.

### <a name="batch-operations"></a>Opérations de traitement par lots
Dans les opérations de traitement par lots, hello veillent même est utilisée dans toutes les lignes hello dans cette opération de traitement par lots, car la bibliothèque cliente de hello permet uniquement d’un objet d’options (et par conséquent, une stratégie/KEK) par le traitement par lots. Toutefois, bibliothèque cliente de hello en interne génère un nouveau vecteur d’initialisation aléatoire et une clé aléatoire par ligne dans le lot de hello. Les utilisateurs peuvent également choisir tooencrypt des propriétés différentes pour chaque opération dans le lot de hello en définissant ce comportement dans le programme de résolution de chiffrement hello.

### <a name="queries"></a>Requêtes
opérations de requête tooperform, vous devez spécifier un programme de résolution de clé qui est en mesure de tooresolve tous hello clés dans le jeu de résultats hello. Si une entité contenue dans le résultat de la requête hello ne peut pas être résolu tooa fournisseur, la bibliothèque cliente de hello génère une erreur. Pour une requête qui effectue des projections côté serveur, bibliothèque cliente de hello ajoutera hello spécial de chiffrement des propriétés de métadonnées (_ClientEncryptionMetadata1 et _ClientEncryptionMetadata2) par les colonnes de toohello sélectionné par défaut.

## <a name="azure-key-vault"></a>coffre de clés Azure
Azure Key Vault permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud. En utilisant Azure Key Vault, les utilisateurs peuvent chiffrer les clés et secrets (tels que les clés d’authentification, les clés de compte de stockage, les clés de chiffrement de données, les fichiers .PFX et les mots de passe) à l’aide de clés protégées par des modules de sécurité matériels (HSM). Pour plus d’informations, consultez la page [Qu’est-ce qu’Azure Key Vault ?](../../key-vault/key-vault-whatis.md)

bibliothèque cliente de stockage Hello utilise la bibliothèque de noyaux hello coffre de clés dans l’ordre tooprovide une infrastructure commune sur Azure pour la gestion des clés. Les utilisateurs obtiennent également hello autre avantage d’à l’aide de la bibliothèque d’extensions hello coffre de clés. bibliothèque d’extensions Hello fournit des fonctionnalités utiles autour simple et transparente symétrique/RSA local et les fournisseurs de clé de cloud, ainsi qu’avec la mise en cache et d’agrégation.

### <a name="interface-and-dependencies"></a>Interfaces et dépendances
Il existe trois packages de coffre de clés :

* Microsoft.Azure.KeyVault.Core contient hello IKey et IKeyResolver. Il s’agit d’un petit package sans dépendances. bibliothèque cliente de stockage Hello pour .NET définit en tant que dépendance.
* Microsoft.Azure.KeyVault contient le client REST de coffre de clé de hello.
* Microsoft.Azure.KeyVault.Extensions contient le code d’extension qui inclut des implémentations d’algorithmes de chiffrement, RSAKey et SymmetricKey. Il dépend des espaces de noms principal et KeyVault hello et fournit des fonctionnalités toodefine un résolveur d’agrégation (lorsque les utilisateurs souhaitent toouse plusieurs fournisseurs de clés) et un programme de résolution de clé mise en cache. Bien que la bibliothèque cliente de stockage hello ne dépend pas directement ce package, si les utilisateurs souhaitent leurs clés ou les toouse Bonjour le coffre de clés extensions tooconsume Bonjour toouse Azure Key Vault toostore local et les fournisseurs de services de chiffrement de cloud, ils auront besoin de ce package.

Le coffre de clés est conçu pour les clés principales de valeur élevée et les seuils de limitation par coffre de clés sont définies avec cela à l’esprit. Lorsque vous effectuez le chiffrement côté client avec le coffre de clés, le modèle par défaut de hello est toouse maître des clés symétriques stockées en tant que clés secrètes dans le coffre de clés et mis en cache localement. Les utilisateurs doivent opérer suivant de hello :

1. Créer une clé secrète en mode hors connexion et le télécharger tooKey coffre.
2. Utilisez l’identificateur de base du secret hello comme un tooresolve paramètre hello version actuelle du secret hello pour le chiffrement et mettre en cache ces informations localement. Utilisez CachingKeyResolver pour la mise en cache ; les utilisateurs est tooimplement attendu pas leur propre mise en cache logique.
3. Utilisez le résolveur de mise en cache de hello en tant qu’entrée lors de la création de stratégie de chiffrement hello.

Vous trouverez plus d’informations sur l’utilisation du coffre de clés Bonjour [exemples de code de chiffrement](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>Meilleures pratiques
Prise en charge le chiffrement est disponible uniquement dans la bibliothèque cliente de stockage hello pour .NET. Windows Phone et Windows Runtime ne prennent pas en charge le chiffrement pour le moment.

> [!IMPORTANT]
> Tenez compte des points importants suivants quand vous utilisez le chiffrement côté client :
> 
> * Quand tooan de lecture ou écriture chiffrées blob, utilisez les commandes de téléchargement blob entier et commandes de téléchargement d’objets blob plage/entier. Évitez d’écrire tooan objet blob chiffré à l’aide d’opérations de protocole tels que Put bloc, placer la liste de blocs, écrire les Pages, effacer des Pages ou ajouter un bloc ; dans le cas contraire, vous pouvez endommager l’objet blob chiffré de hello et rendre illisible.
> * Pour les tables, une contrainte similaire existe. Propriétés de mise à jour chiffrée toonot prudent sans mettre à jour les métadonnées de chiffrement hello être.
> * Si vous définissez des métadonnées sur l’objet blob chiffré de hello, vous pouvez remplacer hello des métadonnées relatives au chiffrement requises pour le déchiffrement, car la définition des métadonnées n’est pas additif. Cela est également vrai pour les instantanés : évitez de spécifier des métadonnées lors de la création d’un instantané d’objet blob chiffré. Si les métadonnées doivent être définies, être vraiment toocall hello **FetchAttributes** tooget de première méthode hello des métadonnées de chiffrement en cours et d’éviter les écritures simultanées lors de la définition de métadonnées.
> * Activer hello **RequireEncryption** propriété dans les options de requête par défaut hello pour les utilisateurs qui doivent fonctionner uniquement avec les données chiffrées. Pour plus d’informations, consultez la section ci-dessous.
> 
> 

## <a name="client-api--interface"></a>API/Interface cliente
Lors de la création d’un objet EncryptionPolicy, les utilisateurs peuvent fournir une clé seulement (implémentation de IKey), un programme de résolution seulement (implémentation de IKeyResolver), ou les deux. IKey est hello base type de clé qui est identifié à l’aide d’un identificateur de clé et qui fournit une logique de hello pour la Désencapsulation / l’habillage. IKeyResolver est tooresolve utilisé une clé pendant le processus de déchiffrement hello. Il définit une méthode ResolveKey qui renvoie un IKey avec un identificateur de clé. Cela fournit aux utilisateurs hello capacité toochoose entre plusieurs clés qui sont gérés dans plusieurs emplacements.

* Pour le chiffrement, clé de hello est toujours utilisé et absence hello d’une clé entraîne une erreur.
* Pour le déchiffrement :
  * programme de résolution clé Hello est appelée si spécifié tooget hello clé. Si le programme de résolution hello est spécifié mais n’a pas d’un mappage pour l’identificateur de clé hello, une erreur est générée.
  * Si le programme de résolution n’est pas spécifié, mais une clé est spécifiée, clé de hello est utilisée si son identificateur correspond à l’identificateur de clé hello requis. Si l’identificateur de hello ne correspond pas, une erreur est générée.

Hello [exemples de chiffrement](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) illustrent un scénario de bout en bout plus détaillé pour les objets BLOB, les files d’attente et les tables, ainsi qu’avec l’intégration du coffre de clés.

### <a name="requireencryption-mode"></a>Mode RequireEncryption
Les utilisateurs peuvent éventuellement activer un mode de fonctionnement dans lequel tous les chargements et téléchargements doivent être chiffrés. Dans ce mode, les tentatives des données de tooupload sans un chiffrement stratégie ou téléchargement de données qui ne sont pas chiffrées sur le service de hello échoue sur le client de hello. Hello **RequireEncryption** propriété d’objet d’options de demande hello contrôle ce comportement. Si votre application chiffre tous les objets stockés dans le stockage Azure, vous pouvez définir hello **RequireEncryption** propriété sur les options de requête hello par défaut pour l’objet de client de service hello. Par exemple, définissez **CloudBlobClient.DefaultRequestOptions.RequireEncryption** trop**true** toorequire le chiffrement pour toutes les opérations de l’objet blob effectué par le biais de cet objet client.

### <a name="blob-service-encryption"></a>Chiffrement du service BLOB
Créer un **BlobEncryptionPolicy** de l’objet et la définir dans les options de demande hello (par l’API ou à un niveau de client à l’aide de **DefaultRequestOptions**). Tout le reste sera gérée par la bibliothèque cliente de hello en interne.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Chiffrement du service de File d’attente
Créer un **QueueEncryptionPolicy** de l’objet et la définir dans les options de demande hello (par l’API ou à un niveau de client à l’aide de **DefaultRequestOptions**). Tout le reste sera gérée par la bibliothèque cliente de hello en interne.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Chiffrement du service de Table
En outre toocreating une stratégie de chiffrement et en le définissant sur les options de requête, vous devez spécifier soit un **EncryptionResolver** dans **TableRequestOptions**, ou définissez l’attribut sur hello [EncryptProperty] entité de Hello.

#### <a name="using-hello-resolver"></a>À l’aide du programme de résolution hello

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Utilisation des attributs
Comme indiqué ci-dessus, si l’entité de hello implémente TableEntity, propriétés de hello peuvent être décorées avec l’attribut hello [EncryptProperty] au lieu de spécifier hello **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Chiffrement et performances
Notez que le chiffrement de vos données de stockage affecte les performances. Hello contenu clé et vecteur d’initialisation doivent être générée, contenu hello lui-même doit être chiffré, et des métadonnées supplémentaires doivent être mis en forme et téléchargées. Cette surcharge varie en fonction de la quantité de hello de données en cours de chiffrement. Nous recommandons de tester systématiquement les performances des applications au cours du développement.

## <a name="next-steps"></a>Étapes suivantes
* [Didacticiel : Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l'aide d'Azure Key Vault](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* Télécharger hello [bibliothèque cliente de stockage Azure pour le package NuGet de .NET](https://www.nuget.org/packages/WindowsAzure.Storage)
* Télécharger hello Azure Key Vault NuGet [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [Client](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), et [Extensions](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) packages  
* Visitez hello [documentation relative à Azure Key Vault](../../key-vault/key-vault-whatis.md)
