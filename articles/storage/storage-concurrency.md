---
title: "aaaManaging d’accès concurrentiel dans Microsoft Azure Storage"
description: "La concurrence d’accès à toomanage hello services Blob, file d’attente, Table et fichier"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Gestion de l’accès concurrentiel dans Microsoft Azure Storage
## <a name="overview"></a>Vue d'ensemble
Dans les applications Internet modernes, les données sont généralement consultées et mises à jour par plusieurs utilisateurs à la fois. Cela nécessite toothink de développeurs d’application avec soin sur comment tooprovide un prédictible rencontrer les utilisateurs finaux de tootheir, en particulier pour les scénarios où plusieurs utilisateurs peuvent mettre à jour hello même données. Les développeurs prennent généralement en compte trois grandes stratégies d'accès concurrentiel aux données :  

1. L’accès concurrentiel optimiste : une application exécute qu'une mise à jour dans le cadre de sa mise à jour vérifie si les données de salutation a changé depuis l’application hello dernière lecture de ces données. Par exemple, si deux utilisateurs affichage d’une page wiki effectuent une mise à jour toohello même page, plateforme de wiki hello doit garantir de que cette mise à jour deuxième hello n’écrase pas hello première mise à jour, et que les deux utilisateurs comprennent si leur mise à jour a réussi ou non. Cette stratégie est la plus souvent utilisée dans les applications web.
2. L’accès simultané pessimiste : une application recherche tooperform une mise à jour prendre un verrou sur un objet empêche d’autres utilisateurs de mettre à jour les données de salutation jusqu'à ce que la libération du verrou hello. Par exemple, dans un scénario de réplication de données maître/esclave où seul maître hello effectue les mises à jour principale de hello généralement contiendra un verrou exclusif pour une période prolongée sur hello données tooensure, aucune autre personne peut le mettre à jour.
3. Dernier à écrire gagne – une approche qui permet de n’importe quel tooproceed d’opérations de mise à jour sans vérifier si une autre application a mis à jour les données de salutation depuis l’application hello lire tout d’abord les données de salutation. Cette stratégie (ou l’absence d’une stratégie formelle) est généralement utilisé lorsque les données sont partitionnées de manière à ce qu’il n’existe pas de risque que plusieurs utilisateurs n’accèdent hello mêmes données. Elle peut également être utile lors du traitement de flux de données à durée de vie limitée.  

Cet article fournit une vue d’ensemble de la plate-forme de stockage Azure hello simplifie le développement en fournissant la prise en charge de première classe pour les trois de ces stratégies d’accès concurrentiel.  

## <a name="azure-storage--simplifies-cloud-development"></a>Azure Storage – Simplification du développement dans le cloud
Hello service de stockage Azure prend en charge tous les trois stratégies, bien qu’il soit dans sa capacité tooprovide prise en charge complète d’accès concurrentiel optimiste et pessimiste car elle était tooembrace conçu un modèle de cohérence forte, ce qui garantit que quand Bonjour les validations de service de stockage insérer ou mettre à jour d’opération, toutes les autres données de toothat accès verront hello de mise à jour de données. Plateformes de stockage qui utilisent un modèle de cohérence éventuelle ont un décalage entre lorsqu’une opération d’écriture est exécutée par un utilisateur et lorsque hello mis à jour les données sont visibles par d’autres utilisateurs, par conséquent, ce qui complique le développement d’applications clientes des incohérences tooprevent de commande à partir de affecter des utilisateurs finaux.  

En outre tooselecting les développeurs de stratégie d’accès concurrentiel approprié doivent également être conscient de la façon dont une plate-forme de stockage isole les modifications – en particulier les toohello modifications même d’objets entre les transactions. Hello service de stockage Azure utilise tooallow de d’isolation d’instantané lire toohappen opérations en même temps que les opérations d’écriture dans une même partition. Contrairement à d’autres niveaux d’isolation, l’isolement d’instantané garantit que toutes les lectures voient un instantané cohérent des données de salutation même pendant que les mises à jour sont en cours – essentiellement en retournant des valeurs de validée dernière hello pendant le traitement d’une transaction de mise à jour.  

## <a name="managing-concurrency-in-blob-storage"></a>Gestion de l’accès concurrentiel dans Blob Storage
Vous pouvez choisir toouse toomanage accès tooblobs des modèles de concurrence optimiste ou pessimiste et de conteneurs dans hello service blob. Si vous ne spécifiez pas explicitement une stratégie dernière écritures wins par défaut de hello.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Accès concurrentiel optimiste pour les objets blob et les conteneurs
Hello service de stockage affecte un objet de tooevery identificateur stocké. Cet identificateur est mis à jour à chaque fois qu'une mise à jour est effectuée sur un objet. identificateur de Hello est retournée client toohello dans le cadre d’une réponse HTTP GET à l’aide d’en-tête ETag (balise d’entité) hello qui est défini dans le protocole de hello HTTP. Un utilisateur en effectuant une mise à jour sur un tel objet peut envoyer dans hello ETag d’origine avec une tooensure en-tête conditionnel qui une mise à jour se produit uniquement si une certaine condition a été remplie – dans ce cas la condition de hello est un en-tête « If-Match » qui requiert hello stockage Valeur de type hello tooensure de service de hello ETag spécifié dans la demande de mise à jour hello est hello même que celui stocké dans le Service de stockage de hello.  

structure de Hello de ce processus est la suivante :  

1. Récupérer un objet blob à partir du service de stockage hello, réponse de hello inclut une valeur d’en-tête ETag de HTTP qui identifie la version actuelle de hello d’objet hello dans le service de stockage hello.
2. Lorsque vous mettez à jour les blob hello, inclure la valeur d’ETag de hello obtenu à l’étape 1 Bonjour **If-Match** en-tête conditionnel de demande hello vous envoyez toohello service.
3. service de Hello compare la valeur d’ETag hello dans la demande hello avec la valeur ETag actuelle de hello d’objet blob de hello.
4. Si la valeur ETag actuelle de hello d’objet blob de hello est une version différente que hello ETag Bonjour **If-Match** en-tête conditionnel dans la demande hello, service de hello retourne un client de toohello 412 erreur. Cela indique client toohello qu’un autre processus a mis à jour les blob hello étant donné que le client de hello extrait.
5. Si hello actuel ETag est de valeur d’objet blob de hello hello la même version que hello ETag Bonjour **If-Match** en-tête conditionnel dans la demande hello, service de hello effectue hello a demandé l’opération et les mises à jour hello valeur ETag actuelle de l’objet blob de hello tooshow qu’il a créé une nouvelle version.  

Hello (à l’aide de la bibliothèque cliente de stockage 4.2.0 de hello) c# extrait suivant montre un exemple simple de tooconstruct un **If-Match AccessCondition** selon hello valeur ETag qui est accessible à partir des propriétés hello d’un objet blob qui a été précédemment soit récupéré ou insérées. Il utilise ensuite hello **AccessCondition** objet quand il mise à jour des objets blob de hello : hello **AccessCondition** objet ajoute hello **If-Match** demande de toohello d’en-tête. Si un autre processus a mis à jour l’objet blob de hello, le service d’objets blob hello renvoie un message d’état HTTP 412 (Échec de la précondition). Vous pouvez télécharger ici hello exemple complète : [concurrence de la gestion à l’aide d’Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Hello Service de stockage prend également en charge des en-têtes conditionnels comme **If-Modified-Since**, **If-Unmodified-Since** et **If-None-Match** ainsi que combinaison. Pour plus d'informations, consultez la rubrique [Spécification des en-têtes conditionnels pour les opérations du service BLOB](http://msdn.microsoft.com/library/azure/dd179371.aspx) sur MSDN.  

Hello tableau suivant récapitule les opérations de conteneur hello qui acceptent comme des en-têtes conditionnels **If-Match** dans la demande de hello et qui retournent une valeur d’ETag dans la réponse de hello.  

| Opération | Renvoie une valeur ETag de conteneur | Accepte les en-têtes conditionnels |
|:--- |:--- |:--- |
| Create Container |Oui |Non |
| Get Container Properties |Oui |Non |
| Get Container Metadata |Oui |Non |
| Set Container Metadata |Oui |Oui |
| Get Container ACL |Oui |Non |
| Set Container ACL |Oui |Oui (*) |
| Delete Container |Non |Oui |
| Lease Container |Oui |Oui |
| List Blobs |Non |Non |

(*) hello autorisations définies par SetContainerACL sont mis en cache et les mises à jour des autorisations toothese prennent 30 secondes toopropagate période pendant laquelle les mises à jour ne sont pas garanties toobe cohérent.  

Hello tableau suivant récapitule les opérations d’objet blob hello qui acceptent comme des en-têtes conditionnels **If-Match** dans la demande de hello et qui retournent une valeur d’ETag dans la réponse de hello.

| Opération | Renvoie une valeur ETag | Accepte les en-têtes conditionnels |
|:--- |:--- |:--- |
| Put Blob |Oui |Oui |
| Get Blob |Oui |Oui |
| Get Blob Properties |Oui |Oui |
| Set Blob Properties |Oui |Oui |
| Get Blob Metadata |Oui |Oui |
| Set Blob Metadata |Oui |Oui |
| Lease Blob (*) |Oui |Oui |
| Snapshot Blob |Oui |Oui |
| Copie d'un objet blob |Oui |Oui (pour les objets blob source et de destination) |
| Abort Copy Blob |Non |Non |
| Delete Blob |Non |Oui |
| Put Block |Non |Non |
| Put Block List |Oui |Oui |
| Get Block List |Oui |Non |
| Put Page |Oui |Oui |
| Get Page Ranges |Oui |Oui |

(*) Objet Blob de bail ne change pas hello ETag sur un objet blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Accès concurrentiel pessimiste pour les objets blob
un objet blob pour une utilisation exclusive de toolock, vous pouvez acquérir un [bail](http://msdn.microsoft.com/library/azure/ee691972.aspx) dessus. Lorsque vous achetez un bail, vous spécifiez pour la durée pendant laquelle vous devez hello bail : il peut s’agir d’entre 15 secondes too60 ou infinie le verrou exclusif tooan de quantités. Vous pouvez renouveler un tooextend bail finie et vous pouvez libérer un bail lorsque vous avez terminé avec lui. service d’objets blob Hello libère automatiquement les baux finies à leur expiration.  

Baux d’activer la synchronisation différentes stratégies toobe pris en charge, y compris écriture exclusif / partagé en lecture, exclusif écriture / exclusif en lecture et partagé d’écriture / lecture d’exclusif. Lorsqu’un bail service de stockage hello applique exclusif écritures (put, définir et les opérations de suppression) toutefois vous être assuré d’exclusivité pour les opérations de lecture requiert tooensure de développeur hello toutes les applications clientes d’utiliser un ID de bail et qu’un seul client à la fois a un ID de bail valide. Les opérations de lecture sans identificateur de bail entraînent l’application d’une stratégie de lecture partagée.  

Hello c# extrait de code suivant montre un exemple de l’acquisition d’un bail exclusif pendant 30 secondes sur un objet blob, la mise à jour le contenu de l’objet blob de hello hello, puis relâchez le bail de hello. S’il existe déjà un bail valid sur l’objet blob de hello lorsque vous essayez de tooacquire un nouveau bail, le service d’objets blob hello retourne un résultat d’état « HTTP (409) conflit ». extrait de code Hello ci-dessous utilise un **AccessCondition** rend un objet blob de demande tooupdate hello dans le service de stockage hello l’objet d’informations de bail tooencapsulate hello.  Vous pouvez télécharger ici hello exemple complète : [concurrence de la gestion à l’aide d’Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Si vous tentez une opération d’écriture sur un objet blob loué sans passer l’ID de bail hello, demande de hello échoue avec une erreur 412. Notez que si hello bail expire avant d’appeler hello **UploadText** (méthode), mais vous toujours passez des ID de bail hello, demande de hello échoue également avec un **412** erreur. Pour plus d’informations sur la gestion des délais d’expiration de bail et ID de bail, consultez hello [Lease Blob](http://msdn.microsoft.com/library/azure/ee691972.aspx) documentation de REST.  

Hello opérations blob suivantes permettent d’accès concurrentiel pessimiste de baux toomanage :  

* Put Blob
* Get Blob
* Get Blob Properties
* Set Blob Properties
* Get Blob Metadata
* Set Blob Metadata
* Delete Blob
* Put Block
* Put Block List
* Get Block List
* Put Page
* Get Page Ranges
* Snapshot Blob - identificateur de bail en option s'il existe un bail
* Copie d’objets Blob - ID de bail requis s’il existe un bail sur l’objet blob de destination hello
* Abort Copy Blob - ID de bail requis s’il existe un bail infini sur l’objet blob de destination hello
* Lease Blob  

### <a name="pessimistic-concurrency-for-containers"></a>Accès concurrentiel pessimiste pour les conteneurs
Baux sur les conteneurs activer hello même toobe de stratégies de synchronisation pris en charge sur les objets BLOB (exclusif d’écriture et partagé en lecture, exclusif écriture / exclusif en lecture et partagé d’écriture / lecture d’exclusif) toutefois à la différence des objets BLOB de service de stockage hello applique uniquement exclusivité sur les opérations de suppression. toodelete un conteneur avec un bail actif, un client doit inclure des ID de bail actif hello avec la demande de suppression hello. Toutes les autres opérations de conteneur réussissent sur un conteneur loué sans inclure l’ID de bail hello auquel cas ils sont partagés des opérations. Si l'exclusivité est requise pour les opérations de mise à jour (Put ou Set) ou de lecture, les développeurs doivent veiller à ce que tous les clients utilisent un identificateur de bail et à ce que seul un client à la fois dispose d'un identificateur de bail valable.  

Hello opérations conteneur suivantes permettent d’accès concurrentiel pessimiste de baux toomanage :  

* Delete Container
* Get Container Properties
* Get Container Metadata
* Set Container Metadata
* Get Container ACL
* Set Container ACL
* Lease Container  

Pour plus d’informations, consultez les pages suivantes :  

* [Spécification des en-têtes conditionnels pour les opérations du service BLOB](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Lease Container](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Lease Blob ](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Gérer l’accès concurrentiel dans hello Service de Table
service de table Hello utilise optimiste de contrôle d’accès concurrentiel hello comportement par défaut lorsque vous travaillez avec des entités, contrairement au service d’objets blob hello où vous devez choisir explicitement de vérifications d’accès concurrentiel optimiste tooperform. Bonjour autre différence entre les services de table et blob hello est que vous pouvez uniquement gérer le comportement de concurrence hello des entités alors que le service d’objets blob hello vous pouvez de gérer d’accès concurrentiel hello de conteneurs et objets BLOB.  

l’accès concurrentiel optimiste toouse et toocheck si un autre processus a modifié une entité, car l’extraction de service de stockage de table hello, vous pouvez utiliser la valeur d’ETag hello que lorsque le service de table hello retourne une entité. structure de Hello de ce processus est la suivante :  

1. Récupérer une entité de service de stockage de table hello, réponse de hello inclut une valeur ETag qui identifie l’identificateur de hello actuel associé à cette entité dans le service de stockage hello.
2. Lorsque vous mettez à jour les entités hello, inclure la valeur d’ETag de hello obtenu à l’étape 1 Bonjour obligatoire **If-Match** en-tête de demande hello vous envoyez toohello service.
3. service de Hello compare hello ETag valeur demande de hello avec hello valeur ETag actuelle d’entité de hello.
4. Si hello valeur ETag actuelle d’entité de hello est différente de celle hello ETag Bonjour obligatoire **If-Match** en-tête dans la demande hello, service de hello renvoie un client de toohello 412 erreur. Cela indique client toohello qu’un autre processus a mis à jour les entités hello étant donné que le client de hello extrait.
5. Si la valeur ETag actuelle de hello d’entité de hello est hello identique hello ETag Bonjour obligatoire **If-Match** en-tête dans la demande de hello ou hello **If-Match** en-tête contient le caractère générique de hello (*), service de hello effectue hello a demandé l’opération et les mises à jour hello valeur ETag actuelle de tooshow d’entité hello qu’il a été mis à jour.  

Notez que, contrairement au service d’objets blob hello, service de table hello requiert hello client tooinclude un **If-Match** en-tête dans les demandes de mise à jour. Toutefois, il est possible de tooforce un inconditionnel (dernière stratégie wins de writer) de mettre à jour et d’ignorer les contrôles d’accès concurrentiel si le client de hello définit hello **If-Match** en-tête toohello caractère (*) dans la demande hello.  

Hello suivant extrait de code c# montre une entité client soit créée précédemment ou récupérées avec leur adresse de messagerie mis à jour. Insérer Hello initial ou récupérer la valeur d’ETag opération magasins hello dans l’objet de client hello et parce que l’exemple hello utilise hello même instance d’objet lorsqu’il exécute hello opération de remplacement, il envoie automatiquement hello ETag valeur arrière toohello service de table l’activation de toocheck de service hello violations d’accès concurrentiel. Si un autre processus a mis à jour l’entité hello dans le stockage table, le service de hello retourne un message d’état HTTP 412 (Échec de la précondition).  Vous pouvez télécharger ici hello exemple complète : [concurrence de la gestion à l’aide d’Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly désactiver le contrôle d’accès concurrentiel de hello, vous devez définir hello **ETag** propriété Hello **employé** trop de l’objet « * » avant d’exécuter d’opération de remplacement hello.  

```csharp
customer.ETag = "*";  
```

Hello tableau suivant résume comment les opérations d’entité de table de hello utilisent les valeurs ETag :

| Opération | Renvoie une valeur ETag | Nécessite l'en-tête de demande If-Match |
|:--- |:--- |:--- |
| Query Entities |Oui |Non |
| Insert Entity |Oui |Non |
| Update Entity |Oui |Oui |
| Merge Entity |Oui |Oui |
| Delete Entity |Non |Oui |
| Insert or Replace Entity |Oui |Non |
| Insert or Merge Entity |Oui |Non |

Notez que hello **insérer ou remplacer une entité** et **insérer ou fusionner une entité** opérations *pas* procède à aucune vérification d’accès concurrentiel, car ils n’envoient pas d’un toohello de valeur ETag service de table.  

Les développeurs utilisant des tables doivent généralement s'appuyer sur l'accès concurrentiel optimiste lors du développement d'applications extensibles. Si le verrouillage pessimiste est nécessaire, les développeurs d’une approche peuvent se lors de l’accès aux Tables tooassign un blob désigné pour chaque table et essayez tootake un bail sur l’objet blob de hello avant d’utiliser la table de hello. Cette méthode nécessite hello application tooensure tout accès aux données toooperating préalable de bail hello sur la table de hello obtenir les chemins d’accès. Notez également que durée du bail minimale hello est 15 secondes, ce qui nécessite une attention particulière pour l’évolutivité.  

Pour plus d’informations, consultez les pages suivantes :  

* [Opérations sur les entités](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Gérer l’accès concurrentiel dans hello Service file d’attente
Un scénario que qui concurrence d’accès est un problème dans le service de file d’attente hello est où plusieurs clients sont la récupération des messages à partir d’une file d’attente. Lorsqu’un message est récupéré à partir de la file d’attente hello, réponse de hello inclut message de type hello et une valeur de l’accusé de réception pop, qui est le message de type hello toodelete requis. message de type Hello n’est pas automatiquement supprimé de la file d’attente hello, mais après que qu’il a été récupéré, il n’est pas visible tooother clients hello intervalle de temps spécifié par le paramètre de visibilitytimeout hello. client Hello qui Récupère le message de type hello est le message de type hello toodelete attendu après qu’elle a été traitée et hello avant le délai spécifié par hello élément TimeNextVisible de hello réponse, qui est calculée en fonction de la valeur hello hello visibilitytimeout paramètre. valeur Hello visibilitytimeout est ajouté au temps toohello à quels hello message est récupéré valeur hello toodetermine TimeNextVisible.  

service de file d’attente Hello n’a pas de prise en charge pour l’accès concurrentiel optimiste ou pessimiste et pour cela les clients de raison du traitement des messages récupérés à partir d’une file d’attente doivent s’assurer messages sont traités de manière idempotente. La règle de Thomas est utilisée pour les opérations de mise à jour telles que SetQueueServiceProperties, SetQueueMetaData, SetQueueACL et UpdateMessage.  

Pour plus d’informations, consultez les pages suivantes :  

* [API REST du service de File d’attente](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Get Messages](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Gérer l’accès concurrentiel dans hello Service de fichiers
service de fichier Hello est accessible à l’aide de points de terminaison autre protocole deux-SMB et REST. Hello service REST n’a pas de prise en charge pour le verrouillage optimiste ou verrouillage pessimiste et les mises à jour suivent une dernière stratégie de wins writer. Les clients qui montent des partages de fichiers peuvent tirer parti de verrouillage mécanismes toomanage accès tooshared fichiers du système, y compris hello capacité tooperform le verrouillage pessimiste. Lorsqu’un client SMB ouvre un fichier, il spécifie un accès de fichier hello et partage de mode. Définition d’une option d’accès au fichier de « Écriture » ou « En lecture/écriture » avec un mode de partage de fichiers « None » entraîne fichier hello verrouillé par un client SMB jusqu'à ce que le fichier de hello est fermé. Si l’opération REST est tentée sur un fichier dans lequel un client SMB a verrouillé du fichier hello hello service REST renvoie le code d’état 409 (conflit) avec le code d’erreur SharingViolation.  

Lorsqu’un client SMB ouvre un fichier à supprimer, il marque les fichiers hello comme en attente de suppression jusqu'à ce que tous les autres clients SMB handles ouverts sur ce fichier sont fermées. Lorsqu'un fichier est marqué comme étant en attente de suppression, toutes les opérations REST effectuées sur le fichier renvoient un code d'état 409 (Conflit) avec le code d'erreur SMBDeletePending. Code d’état 404 (introuvable) n’est pas renvoyé dans la mesure où il est possible pour hello SMB tooremove messages hello du client en attente de fichier de suppression indicateur tooclosing préalable hello. En d’autres termes, code d’état 404 (introuvable) est uniquement attendu lorsque hello a été supprimé. Notez que lorsque le fichier est dans un SMB delete état d’attente, il figurera pas Bonjour que liste des fichiers de résultats. Notez que les opérations REST supprimer le fichier et de supprimer le répertoire reste hello sont validées automatiquement et n’entraînent pas en attente supprimez également un état.  

Pour plus d’informations, consultez les pages suivantes :  

* [Gestion des verrouillages de fichiers](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Résumé et étapes suivantes
Hello Microsoft Azure Storage service a été conçu toomeet les besoins de hello d’applications en ligne plus complexes de hello sans obliger les développeurs toocompromise ou repenser clé hypothèses de conception telles que la cohérence d’accès concurrentiel et les données qu’ils proviennent tootake pour reçoivent.  

Pourquoi effectuer exemple d’application référencé dans ce billet de blog :  

* [Gestion de l’accès concurrentiel avec Azure Storage - Exemple d’application](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Pour plus d’informations concernant Azure Storage, consultez la page :  

* [Page d’accueil de Microsoft Azure Storage](https://azure.microsoft.com/services/storage/)
* [Introduction tooAzure stockage](storage-introduction.md)
* Prise en main du Stockage [Blob](storage-dotnet-how-to-use-blobs.md), [Table](storage-dotnet-how-to-use-tables.md), [File d’attente](storage-dotnet-how-to-use-queues.md) et [Fichier](storage-dotnet-how-to-use-files.md)
* Architecture de stockage – [Stockage Azure : service de stockage cloud à haute disponibilité et à forte cohérence](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

