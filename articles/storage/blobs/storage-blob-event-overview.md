---
title: "Réagir aux événements de stockage Blob Azure (version préliminaire) | Microsoft Docs"
description: "Utilisez Azure Event Grid pour vous abonner à des événements de stockage Blob."
services: storage,event-grid
keywords: 
author: cbrooksmsft
ms.author: cbrooks
ms.date: 08/25/2017
ms.topic: article
ms.service: storage
ms.openlocfilehash: a56e6026ed0c2c873030625fa7a9b35b92faf930
ms.sourcegitcommit: e38120a5575ed35ebe7dccd4daf8d5673534626c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2017
---
# <a name="reacting-to-blob-storage-events-preview"></a>Réagir aux événements de stockage d’objets Blob (version préliminaire)

Les événements de stockage Blob Azure permettent aux applications de réagir à la création et la suppression d’objets Blob avec des architectures sans serveur modernes et sans nécessiter de code complexe ou de services d’interrogation coûteux et inefficaces.  Au lieu de cela, les événements sont envoyés via [Azure Event Grid](https://azure.microsoft.com/services/event-grid/) aux abonnés, comme [Azure Functions](https://azure.microsoft.com/services/functions/), [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/), ou même à votre propre écouteur http personnalisé, et vous payez seulement pour ce que vous utilisez.

Les scénarios d’événements de stockage d’objets Blob courants incluent le traitement d’images ou de vidéos, l’indexation pour la recherche ou n’importe quel flux de travail orienté fichier.  Les téléchargements de fichier asynchrones sont parfaitement adaptés aux événements.  Lorsque les modifications sont peu fréquentes, mais que votre scénario requiert une réactivité immédiate, une architecture basée sur des événements peut être particulièrement efficace.

La préversion d’Event Grid est actuellement disponible pour les comptes situés dans les régions ***États-Unis Centre-Ouest*** ou ***États-Unis de l’Ouest 2***.  Examinons [Acheminer des événements de stockage Blob Azure vers un point de terminaison Web personnalisé ](storage-blob-event-quickstart.md) pour obtenir un exemple rapide.

![Modèle de Event Grid](./media/storage-blob-event-overview/event-grid-functional-model.png)

## <a name="blob-storage-accounts"></a>Comptes de stockage d’objets blob
Les événements de stockage d’objets Blob sont disponibles dans [Comptes de stockage d’objets Blob](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#blob-storage-accounts) (et non dans les comptes de stockage à usage général).  Un compte de stockage d’objets blob est un compte de stockage spécialisé pour le stockage des données non structurées en tant qu’objets blob dans Azure Storage. Les comptes de stockage d’objets blob sont comme vos comptes de stockage à usage général existants et offrent les excellents niveaux de durabilité, disponibilité, évolutivité et performances dont vous bénéficiez aujourd’hui. Ils assurent notamment la cohérence d’API à 100 % pour les objets blob de blocs et d’ajout. Pour les applications qui requièrent uniquement le stockage d’objets blob de blocs ou d’objets blob d’ajout, nous recommandons d’utiliser des comptes de stockage d’objets blob.

## <a name="available-blob-storage-events"></a>Événements de stockage Blob disponibles
Event Grid utilise les [abonnements aux événements](../../event-grid/concepts.md#event-subscriptions) pour acheminer les messages d’événements vers les abonnés.  Les abonnements aux événements de stockage Blob peuvent inclure deux types d’événements :  

> |Nom de l'événement|Description|
> |----------|-----------|
> |`Microsoft.Storage.BlobCreated`|Déclenché lorsqu’un objet Blob est créé ou remplacé par le biais des opérations `PutBlob`, `PutBlockList` ou `CopyBlob`|
> |`Microsoft.Storage.BlobDeleted`|Déclenché lorsqu’un objet Blob est supprimé via une opération `DeleteBlob`|

## <a name="event-schema"></a>Schéma d’événement
Les événements de stockage d’objets Blob contiennent toutes les informations dont vous avez besoin pour répondre aux modifications de vos données.  Vous pouvez identifier un événement de stockage d’objets Blob, car la propriété eventType commence par « Microsoft.Storage ».  
Plus d’informations sur l’utilisation des propriétés d’événement Event Grid sont documentées dans [schéma d’événement Event Grid](../../event-grid/event-schema.md).  

> |Propriété|Type|Description|
> |-------------------|------------------------|-----------------------------------------------------------------------|
> |rubrique|string|ID Azure Resource Manager complet du compte de stockage qui émet l’événement.|
> |subject|string|Le chemin d’accès de la ressource relative à l’objet qui est le sujet de l’événement, avec le même format Azure Resource Manager étendu que nous utilisons pour décrire les comptes de stockage, les services et mes conteneurs pour Azure RBAC.  Ce format comprend un nom d’objet blob en conservant la casse.|
> |eventTime|string|La date et l’heure de l’événement sont générées au format ISO 8601|
> |eventType|string|« Microsoft.Storage.BlobCreated » ou « Microsoft.Storage.BlobDeleted »|
> |Id|string|Identificateur unique si cet événement|
> |données|objet|Collection de données d’événement spécifiques au stockage d’objets Blob|
> |data.contentType|string|Le type de contenu de l’objet Blob, comme renvoyé dans l’en-tête Content-Type, serait retourné à partir de l’objet Blob|
> |data.contentLength|number|La taille de l’objet blob comme entier représentant un nombre d’octets, comme dans l’en-tête Content-Length serait retourné à partir de l’objet Blob.  Envoyé avec l’événement BlobCreated, mais pas avec BlobDeleted.|
> |data.url|string|L’URL de l’objet qui est le sujet de l’événement|
> |data.eTag|string|L’etag de l’objet lorsque cet événement est déclenché.  Non disponible pour l’événement BlobDeleted.|
> |data.api|string|Le nom de l’opération d’API qui a déclenché cet événement.  Pour les événements BlobCreated, cette valeur est « PutBlob », « PutBlockList » ou « CopyBlob ».  Pour les événements BlobDeleted, cette valeur est « DeleteBlob ».  Ces valeurs sont les mêmes noms d’API que ceux présents dans les journaux de diagnostic de stockage Azure.  Consultez [Opérations journalisées et messages d’état](https://docs.microsoft.com/rest/api/storageservices/storage-analytics-logged-operations-and-status-messages).|
> |data.sequencer|string|Une valeur de chaîne opaque représentant l’ordre logique des événements pour n’importe quel nom d’objet Blob particulier.  Les utilisateurs peuvent utiliser la comparaison de chaînes standard pour comprendre l’ordre relatif de deux événements sur le même nom d’objet Blob.|
> |data.requestId|string|L’ID de requête de service généré pour l’opération de l’API de stockage.  Peut être utilisé pour mettre en corrélation les journaux de diagnostic de stockage Azure en utilisant le champ « request-id-header » dans les journaux et est retourné lors de l’initialisation de l’appel d’API dans l’en-tête 'x-ms-request-id'. Consultez [Format de journal](https://docs.microsoft.com/rest/api/storageservices/storage-analytics-log-format).|
> |data.clientRequestId|string|L’ID de requête fourni par le client pour l’opération de l’API de stockage.  Peut être utilisé pour mettre en corrélation les journaux de diagnostic de stockage Azure en utilisant le champ « client-request-id » dans les journaux et peut être fourni dans les demandes du client à l’aide de l’en-tête « x-ms-client-request-id ». Consultez [Format de journal](https://docs.microsoft.com/rest/api/storageservices/storage-analytics-log-format).|
> |data.storageDiagnostics|objet|Des données de diagnostic occasionnellement incluses par le service de stockage Azure.  Elles doivent, le cas échéant, être ignorées par les consommateurs d’événements.|

Voici un exemple d’événement BlobCreated :
```json
[{
  "topic": "/subscriptions/319a9601-1ec0-0000-aebc-8fe82724c81e/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/file1.txt",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2017-08-16T01:57:26.005121Z",
  "id": "602a88ef-0001-00e6-1233-1646070610ea",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "799304a4-bbc5-45b6-9849-ec2c66be800a",
    "requestId": "602a88ef-0001-00e6-1233-164607000000",
    "eTag": "0x8D4E44A24ABE7F1",
    "contentType": "text/plain",
    "contentLength": 447,
    "blobType": "BlockBlob",
    "url": "https://myaccount.blob.core.windows.net/testcontainer/file1.txt",
    "sequencer": "00000000000000EB000000000000C65A",
  }
}]

```

Pour plus d’informations, consultez [Schéma des événements de stockage Blob](../../event-grid/event-schema-blob-storage.md).

## <a name="filtering-events"></a>Filtrage des événements
Les abonnements aux événements d’objet Blob peuvent être filtrés en fonction du type d’événement et par le nom du conteneur et le nom de l’objet blob de l’objet qui a été créé ou supprimé.  Les filtres d’objet dans Event Grid reposent sur les correspondances « commence par » et « se termine par », afin que les événements dont l’objet correspond soient remis à l’abonné.
Le sujet des événements de stockage d’objets Blob utilise le format suivant :
```json
/blobServices/default/containers/<containername>/blobs/<blobname>
```
Pour faire correspondre tous les événements pour un compte de stockage, vous pouvez laisser les filtres de sujet vides.

Pour faire correspondre les événements à partir d’objets Blob créés dans un ensemble de conteneurs partageant un préfixe, utilisez un filtre `subjectBeginsWith`, comme :
```json
/blobServices/default/containers/containerprefix
```
Pour faire correspondre les événements d’objet Blob créés dans un conteneur spécifique, utilisez un filtre `subjectBeginsWith`, comme :
```json
/blobServices/default/containers/containername/
```
Pour faire correspondre les événements d’objet Blob créés dans un conteneur spécifique partageant un préfixe de nom d’objet Blob, utilisez un filtre `subjectBeginsWith`, comme :
```json
/blobServices/default/containers/containername/blobs/blobprefix
```

Pour faire correspondre les événements d’objet Blob créés dans un conteneur spécifique partageant un suffixe d’objet Blob, utilisez un filtre `subjectEndsWith`, comme « .log » ou « .jpg »

Pour plus d’informations, consultez [Concepts d’Event Grid](../../event-grid/concepts.md#filters).

## <a name="practices-for-consuming-events"></a>Pratiques pour la consommation d’événements
Les applications qui gèrent des événements de stockage d’objets Blob doivent suivre certaines pratiques recommandées :
> [!div class="checklist"]
> * Comme plusieurs abonnements peuvent être configurés pour acheminer les événements vers le même gestionnaire d’événements, il est important de ne pas considérer que les événements proviennent d’une source particulière, mais de vérifier le sujet du message pour vous assurer qu’il provient d’un compte de stockage que vous attendez.
> * De même, vérifiez que vous êtes prêt à traiter son eventType, et ne supposez pas que tous les événements reçus seront aux types que vous attendez.
> * Les messages pouvant arriver en désordre et après un certain temps, utilisez les champs etag pour comprendre si vos informations sur les objets sont toujours à jour.  En outre, utilisez les champs de séquence pour comprendre l’ordre des événements sur un objet particulier.
> * Utilisez le champ blobType pour comprendre le type d’opération autorisé sur l’objet Blob, et les types de bibliothèque client que vous devez utiliser pour accéder à l’objet Blob.
> * Utilisez le champ URL avec les constructeurs `CloudBlockBlob` et `CloudAppendBlob` pour accéder à l’objet Blob.
> * Ignorez les champs que vous ne comprenez pas.  Cette pratique vous aidera à prendre en charge les nouvelles fonctionnalités qui peuvent être ajoutées à l’avenir.


## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur Event Grid et essayer les événements de stockage d’objets Blob :

- [Event Grid](../../event-grid/overview.md)
- [Acheminer des événements de stockage Blob Azure vers un point de terminaison Web personnalisé ](storage-blob-event-quickstart.md)
