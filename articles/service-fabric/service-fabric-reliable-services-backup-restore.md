---
title: "aaaService sauvegarde de l’infrastructure et de restauration | Documents Microsoft"
description: "Documentation conceptuelle relative à la sauvegarde et à la restauration de Service Fabric"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: subramar,jessebenson
ms.assetid: 91ea6ca4-cc2a-4155-9823-dcbd0b996349
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: mcoskun
ms.openlocfilehash: e502b59c84999c3fe825167383f00a5ebd70c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-restore-reliable-services-and-reliable-actors"></a>Sauvegarder et restaurer Reliable Services et Reliable Actors
Azure Service Fabric est une plateforme haute disponibilité qui réplique des état de hello dans plusieurs nœuds toomaintain cette haute disponibilité.  Par conséquent, même si un nœud de cluster de hello échoue, les services hello continuent toobe disponible. Cette redondance intégrée fournie par la plateforme de hello peut être suffisante pour certains, dans certains cas, il est souhaitable pour tooback de service hello des données (tooan un magasin externe).

> [!NOTE]
> Il est critique toobackup et restaurer vos données (et vérifiez qu’elle fonctionne comme prévu) afin que vous pouvez récupérer à partir de la perte de données.
> 
> 

Par exemple, un service souhaite que tooback les données de tooprotect de commande à partir de hello les scénarios suivants :

- Dans l’événement hello de perte définitive de hello d’ensemble d’un cluster Service Fabric.
- Perte permanente d’une majorité des réplicas hello d’une partition de service
- Erreurs d’administration : état de hello accidentellement obtient supprimée ou endommagée. Par exemple, cela peut se produire si un administrateur doté de privilèges suffisants supprime de façon erronée le service de hello.
- Bogues dans le service hello qui entraînent une altération des données. Par exemple, cela peut se produire lorsqu’une mise à niveau du code de service commence à écrire des données erronées tooa Collection fiable. Dans ce cas, les deux hello code et les données de salutation peut-être toobe tooan de restaurer l’état précédemment.
- Traitement des données hors connexion. Il peut être pratique toohave traitement en mode hors connexion de données business intelligence qui s’effectue séparément à partir du service hello qui génère des données hello.

la fonctionnalité de sauvegarde/restauration Hello permet aux services reposant sur les sauvegardes de toocreate et de restauration de l’API des Services fiables hello. Hello sauvegarde API fournies par la plateforme de hello autoriser ou les sauvegardes de l’état d’une partition de service, sans blocage de lecture ou d’opérations d’écriture. Bonjour restauration Qu'api permettent de toobe d’état d’une partition de service restauré à partir d’une sauvegarde choisie.

## <a name="types-of-backup"></a>Types de sauvegarde
Il existe deux options de sauvegarde : complète et incrémentielle.
Une sauvegarde complète est une sauvegarde qui contient tous les hello requis toorecreate hello état des données de réplica de hello : points de contrôle et tous les enregistrements de journal.
Car il possède des points de contrôle hello et journal de hello, une sauvegarde complète peut être restaurée par lui-même.

problème de Hello avec les sauvegardes complètes survient lorsque les points de contrôle hello sont grands.
Par exemple, un réplica qui dispose de 16 Go de l’état aura des points de contrôle qui s’ajoutent environ too16 go.
Si nous avons un objectif de Point de récupération de cinq minutes, le réplica de hello a besoin toobe sauvegardé toutes les cinq minutes.
Chaque fois qu’il sauvegarde, il doit toocopy 16 Go de points de contrôle en outre too50 Mo (configurable à l’aide `CheckpointThresholdInMB`) équivalent de journaux.

![Exemple de sauvegarde complète.](media/service-fabric-reliable-services-backup-restore/FullBackupExample.PNG)

problème de toothis solution Hello est les sauvegardes incrémentielles, où sauvegarde contient uniquement les enregistrements de journal hello changé depuis la dernière sauvegarde de hello.

![Exemple de sauvegarde incrémentielle.](media/service-fabric-reliable-services-backup-restore/IncrementalBackupExample.PNG)

Étant donné que les sauvegardes incrémentielles sont les seules les modifications apportées depuis hello dernière sauvegarde (n’inclut pas de points de contrôle hello), ils ont tendance toobe plus rapidement, mais ils ne peuvent pas être restaurés sur leurs propres.
toorestore une sauvegarde incrémentielle, la chaîne de sauvegarde entière hello est requise.
Une chaîne de sauvegarde est une chaîne de sauvegardes qui commence par une sauvegarde complète, suivie d’un nombre de sauvegardes incrémentielles contigües.

## <a name="backup-reliable-services"></a>Sauvegarder Reliable Services
Hello auteur du service a le contrôle total de situations dans lesquelles les sauvegardes toomake et l’emplacement de stockage des sauvegardes.

toostart une sauvegarde, service de hello a besoin de fonction de membre tooinvoke hello héritée `BackupAsync`.  
Les sauvegardes peuvent être effectuées uniquement à partir des réplicas principaux et ils nécessitent toobe de statut d’écriture accordé.

Comme indiqué ci-dessous, `BackupAsync` prend un `BackupDescription` objet, où on peut spécifier une sauvegarde complète ou incrémentielle, ainsi que d’une fonction de rappel, `Func<< BackupInfo, CancellationToken, Task<bool>>>` qui est appelé lorsque le dossier de sauvegarde hello a été créée localement et est prêt toobe déplacée de toosome stockage externe.

```csharp

BackupDescription myBackupDescription = new BackupDescription(backupOption.Incremental,this.BackupCallbackAsync);

await this.BackupAsync(myBackupDescription);

```

Tootake demande une sauvegarde incrémentielle peut échouer avec `FabricMissingFullBackupException`. Cette exception indique qu’un des hello suivant choses se produit :

- réplica de Hello n’ait jamais une sauvegarde complète, car il est devenu principal,
- hello certains enregistrements du journal depuis la dernière sauvegarde de hello a été tronqué ou
- réplica passé hello `MaxAccumulatedBackupLogSizeInMB` limite.

Les utilisateurs peuvent augmenter la probabilité de hello d’être en mesure de toodo les sauvegardes incrémentielles en configurant `MinLogSizeInMB` ou `TruncationThresholdFactor`.
Notez que ces valeurs d’augmenter hello par l’utilisation de disque de réplica.
Pour plus d’informations, consultez [Configuration de Reliable Services](service-fabric-reliable-services-configuration.md).

`BackupInfo`Fournit des informations concernant la sauvegarde hello, y compris l’emplacement hello du dossier hello où hello runtime enregistré la sauvegarde de hello (`BackupInfo.Directory`). fonction de rappel Hello peut déplacer hello `BackupInfo.Directory` tooan magasin externe ou un autre emplacement.  Cette fonction retourne également une valeur booléenne qui indique s’il s’agit d’emplacement du dossier de sauvegarde tooits cible pour toosuccessfully en mesure de déplacement hello.

Hello de code suivant montre comment hello `BackupCallbackAsync` méthode peut être utilisé tooupload hello tooAzure sauvegarde stockage :

```csharp
private async Task<bool> BackupCallbackAsync(BackupInfo backupInfo, CancellationToken cancellationToken)
{
    var backupId = Guid.NewGuid();

    await externalBackupStore.UploadBackupFolderAsync(backupInfo.Directory, backupId, cancellationToken);

    return true;
}
```

Dans l’exemple précédent de hello, `ExternalBackupStore` est classe exemple hello toointerface utilisé avec le stockage d’objets Blob Azure, et `UploadBackupFolderAsync` est la méthode hello qui compresse le dossier de hello et le place dans le magasin d’objets Blob Azure hello.

Notez les points suivants :

  - Il ne peut y avoir qu’une seule opération de sauvegarde en cours par réplica à un moment donné. Plusieurs `BackupAsync` appel à la fois lève `FabricBackupInProgressException` toolimit séquentiels sauvegardes tooone.
  - Si un réplica bascule alors qu’une sauvegarde est en cours d’exécution, sauvegarde de hello n’est peut-être pas été terminée. Une fois le basculement de hello se termine, il est donc hello de responsabilité toorestart hello sauvegarde en appelant `BackupAsync` selon les besoins.

## <a name="restore-reliable-services"></a>Restaurer Reliable Services
En général, les cas de hello lorsque vous devrez peut-être tooperform une opération de restauration se répartissent dans ces catégories :

  - service de Hello partitionner les données perdues. Par exemple, disque hello pour deux des trois des réplicas pour une partition (y compris le réplica principal de hello) Obtient endommagé ou réinitialisé. nouveau réplica principal de Hello peut-être toorestore des données à partir d’une sauvegarde.
  - ensemble de service Hello est perdue. Par exemple, un administrateur supprime l’ensemble du service hello et service de hello et les données de salutation devez donc toobe restaurée.
  - service de Hello répliqué des données d’application endommagé (par exemple, en raison d’un bogue dans l’application). Dans ce cas, service de hello a toobe mis à niveau ou restaurée tooremove hello provoqué la corruption de hello et non endommagé des données a toobe restaurée.

Alors que de nombreuses approches sont possibles, nous proposons des exemples sur l’utilisation de `RestoreAsync` toorecover de hello au-dessus de scénarios.

## <a name="partition-data-loss-in-reliable-services"></a>Perte de données de partition dans Reliable Services
Dans ce cas, hello runtime automatiquement détecte une perte de données hello et appeler hello `OnDataLossAsync` API.

auteur du service Hello doit hello tooperform suivant toorecover :

  - Substituez la méthode de classe de base virtuelle hello `OnDataLossAsync`.
  - Recherche hello dernière sauvegarde dans un emplacement externe hello contenant les sauvegardes du service hello.
  - Télécharger la dernière sauvegarde de hello (et décompressez les sauvegarde hello dans le dossier de sauvegarde hello s’il était compressé).
  - Hello `OnDataLossAsync` méthode fournit un `RestoreContext`. Appelez hello `RestoreAsync` API sur hello fourni `RestoreContext`.
  - Renvoie la valeur true si la restauration de hello a réussi.

Voici un exemple d’implémentation de hello `OnDataLossAsync` méthode :

```csharp
protected override async Task<bool> OnDataLossAsync(RestoreContext restoreCtx, CancellationToken cancellationToken)
{
    var backupFolder = await this.externalBackupStore.DownloadLastBackupAsync(cancellationToken);

    var restoreDescription = new RestoreDescription(backupFolder);

    await restoreCtx.RestoreAsync(restoreDescription);

    return true;
}
```

`RestoreDescription`passé dans toohello `RestoreContext.RestoreAsync` appel contient un membre appelé `BackupFolderPath`.
Lorsque vous restaurez une sauvegarde complète unique, cela `BackupFolderPath` doit être défini toohello un chemin d’accès local du dossier hello qui contient votre sauvegarde complète.
Lorsque vous restaurez une sauvegarde complète et un nombre de sauvegardes incrémentielles, `BackupFolderPath` doit être défini toohello un chemin d’accès local du dossier hello qui contient non seulement la sauvegarde complète de hello, mais également toutes les sauvegardes incrémentielles hello.
`RestoreAsync`appel peut lever `FabricMissingFullBackupException` si hello `BackupFolderPath` fourni ne contient pas d’une sauvegarde complète.
Il peut également lever `ArgumentException` si `BackupFolderPath` a une chaîne interrompue de sauvegardes incrémentielles.
Par exemple, s’il contient une sauvegarde complète de hello, hello tout d’abord incrémentielle et hello troisième sauvegarde incrémentielle, mais aucune sauvegarde incrémentielle de hello deuxième.

> [!NOTE]
> Hello RestorePolicy a la valeur tooSafe par défaut.  Cela signifie que hello `RestoreAsync` API échoue avec ArgumentException s’il détecte ce dossier de sauvegarde hello contient un état qui est l’état toohello antérieure à ou égal contenue dans ce réplica.  `RestorePolicy.Force`peut être utilisé tooskip cette vérification de sécurité. comme le spécifie `RestoreDescription`.
> 

## <a name="deleted-or-lost-service"></a>Service supprimé ou perdu
Si un service est supprimé, vous devez tout d’abord recréer les service hello avant la restauration de données de salutation.  Il est service hello toocreate important hello même configuration, par exemple, le schéma, de partitionnement afin que hello données peut être restaurée en toute transparence.  Une fois le service de hello, hello des données d’API toorestore (`OnDataLossAsync` au-dessus) a toobe appelée sur chaque partition de ce service. Pour cela, vous pouvez utiliser `[FabricClient.TestManagementClient.StartPartitionDataLossAsync](https://msdn.microsoft.com/library/mt693569.aspx)` sur chaque partition.  

À partir de ce point de mise en œuvre est hello identique hello au-dessus de scénario. Chaque partition doit toorestore hello dernière pertinentes sauvegarde à partir du magasin externe de hello. L’inconvénient est que partition hello QU'ID peut-être maintenant changé, depuis hello runtime crée dynamiquement les ID de partition. Service de hello doit donc informations de partition approprié toostore hello et service nom tooidentify hello correct dernière sauvegarde toorestore à partir de chaque partition.

> [!NOTE]
> Il n’est pas recommandé toouse `FabricClient.ServiceManager.InvokeDataLossAsync` sur chaque partition toorestore hello service entier, étant donné que qui peut altérer l’état de votre cluster.
> 

## <a name="replication-of-corrupt-application-data"></a>Réplication des données d’application endommagées
Mise à niveau des applications hello nouvellement déployé comporte un bogue, qui peut provoquer une altération des données. Par exemple, une mise à niveau de l’application peut démarrer tooupdate chaque enregistrement de numéro de téléphone d’un dictionnaire fiable avec un code de région non valide.  Dans ce cas, les numéros de téléphone non valide de hello seront répliquées depuis le Service Fabric n’est pas informé de la nature hello de données hello qui sont stockées.

Hello première toodo une fois que vous détectez cet monumentale un bogue qui entraîne une altération des données est toofreeze hello service au niveau de l’application hello et, si possible, mettez à niveau de version toohello hello de code d’application n’a pas de bogue de hello.  Toutefois, même après que le code de service hello est fixe, hello données peuvent toujours être endommagées et par conséquent, les données pouvant nécessiter toobe restaurée.  Dans ce cas, il peut-être pas suffisamment toorestore hello sauvegarde la plus récente, étant donné que les sauvegardes plus récentes hello peuvent également être endommagés.  Par conséquent, vous avez toofind hello dernière sauvegarde effectuée avant les données de salutation sont endommagées.

Si vous n’êtes pas sûr de laquelle les sauvegardes sont endommagés, vous pouvez déployer un cluster Service Fabric et restaurer les sauvegardes de hello de partitions affectées comme hello au-dessus de « Deleted ou perte de service » scénario.  Pour chaque partition, démarrer la restauration des sauvegardes de hello de toohello plus récente de hello moins. Une fois que vous trouvez une sauvegarde qui n’a pas de corruption de hello, déplacer/supprimer toutes les sauvegardes qui ont été plus récents (que cette sauvegarde) de cette partition. Répétez ce processus pour chaque partition. Désormais, lorsque `OnDataLossAsync` est appelée sur une partition hello dans le cluster de production hello, dernière sauvegarde de hello trouvé dans hello externe magasin sera hello une sélectionnées par hello au-dessus de processus.

Maintenant, hello étapes Bonjour « Deleted ou perte de service » section peut être utilisé d’état de hello toorestore des hello service toohello avant un code bogué hello endommagé l’état de hello.

Notez les points suivants :

  - Lorsque vous restaurez, il est en cours d’un risque que hello sauvegarde restaurée est antérieure à état hello de partition de hello avant que les données de salutation a été perdues. Pour cette raison, vous devez restaurer uniquement comme un toorecover recours dernière autant de données que possible.
  - Hello de chaîne qui représente le chemin d’accès du dossier de sauvegarde hello et hello chemins d’accès des fichiers à l’intérieur du dossier de sauvegarde hello peuvent être supérieurs à 255 caractères, selon le chemin d’accès de hello FabricDataRoot et la longueur du nom du Type d’Application. Cela peut entraîner certaines méthodes .NET, tel que `Directory.Move`, toothrow hello `PathTooLongException` exception. Une solution de contournement est toodirectly appeler les API kernel32, comme `CopyFile`.

## <a name="backup-and-restore-reliable-actors"></a>Sauvegarder et restaurer Reliable Actors


L’infrastructure Reliable Actors est basée sur Reliable Services. Hello ActorService qui héberge hello actor(s) est un service fiable sans état. Par conséquent, tous hello sauvegarde et restauration des fonctionnalités disponibles dans les Services fiables sont également acteurs tooReliable disponibles (à l’exception des comportements qui sont le fournisseur d’état spécifique). Étant donné que les sauvegardes sont effectuées par partition, les états de tous les acteurs de cette partition sont sauvegardés (et la restauration se fait de façon similaire, par partition). tooperform sauvegarde/restauration, propriétaire du service hello doit créer une classe de service d’acteur personnalisée qui dérive de la classe de ActorService et puis de sauvegarde/restauration similaire tooReliable Services comme décrit ci-dessus dans les sections précédentes.

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo)
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Lorsque vous créez une classe de service d’acteur personnalisé, vous devez tooregister ainsi que lors de l’inscription d’acteur de hello.

```csharp
ActorRuntime.RegisterActorAsync<MyActor>(
   (context, typeInfo) => new MyCustomActorService(context, typeInfo)).GetAwaiter().GetResult();
```

fournisseur d’état par défaut Hello pour Reliable Actors est `KvsActorStateProvider`. La sauvegarde incrémentielle n’est pas activée par défaut pour `KvsActorStateProvider`. Vous pouvez activer la sauvegarde incrémentielle en créant `KvsActorStateProvider` avec hello approprié à la définition dans son constructeur et transmettez-lui tooActorService constructeur comme indiqué dans l’extrait de code suivant :

```csharp
class MyCustomActorService : ActorService
{
     public MyCustomActorService(StatefulServiceContext context, ActorTypeInformation actorTypeInfo)
            : base(context, actorTypeInfo, null, null, new KvsActorStateProvider(true)) // Enable incremental backup
     {                  
     }
    
    //
   // Method overrides and other code.
    //
}
```

Une fois la sauvegarde incrémentielle a été activée, effectuer une sauvegarde incrémentielle peut échouer avec FabricMissingFullBackupException pour l’une des raisons suivantes, et vous devez tootake une sauvegarde complète avant d’effectuer des sauvegardes incrémentielles d’objets :

  - réplica de Hello n’ait jamais une sauvegarde complète, car il est devenu principal.
  - Certains des enregistrements de journal hello a été tronqués, car la dernière sauvegarde a été effectuée.

Lorsque la sauvegarde incrémentielle est activée, `KvsActorStateProvider` n’utilise pas de mémoire tampon circulaire toomanage son journal enregistre et tronque régulièrement. Si aucune sauvegarde n’est effectuée par l’utilisateur pour une période de 45 minutes, le système de hello tronque automatiquement les enregistrements de journal hello. Cet intervalle peut être configuré en spécifiant `logTrunctationIntervalInMinutes` dans `KvsActorStateProvider` constructeur (toowhen similaire à l’activation de la sauvegarde incrémentielle). enregistrements de journal Hello peuvent également obtenir tronqués si le réplica principal doivent toobuild un autre réplica en envoyant toutes ses données.

Lors de la restauration à partir d’une chaîne de sauvegarde, les Services tooReliable similaires, hello BackupFolderPath doit contenir des sous-répertoires avec un sous-répertoire contenant une sauvegarde complète et autres sous-répertoires contenant l’ou les sauvegardes incrémentielles. API de restauration Hello lèvera FabricException avec le message d’erreur approprié si la validation de chaîne de sauvegarde hello échoue. 

> [!NOTE]
> `KvsActorStateProvider`actuellement ignore l’option hello RestorePolicy.Safe. La prise en charge de cette fonctionnalité est prévue dans une prochaine version.
> 

## <a name="testing-backup-and-restore"></a>Test de la sauvegarde et de la restauration
Il est important tooensure qui sont en cours de sauvegarde des données critiques et peuvent être restaurées à partir de. Cela est possible en appelant hello `Start-ServiceFabricPartitionDataLoss` applet de commande PowerShell qui est susceptible d’entraîner une perte de données dans une partition particulière de tootest si les données de salutation et de restauration pour votre service fonctionne comme prévu.  Il est également possible de tooprogrammatically appeler une perte de données et de restaurer à partir, ainsi que l’événement.

> [!NOTE]
> Vous pouvez trouver un exemple d’implémentation de la sauvegarde et restaurer la fonctionnalité dans hello référence de l’application Web sur GitHub. Regardez hello `Inventory.Service` service pour plus d’informations.
> 
> 

## <a name="under-hello-hood-more-details-on-backup-and-restore"></a>Dans les coulisses de hello : plus d’informations sur la sauvegarde et restauration
Voici des détails supplémentaires sur la sauvegarde et la restauration.

### <a name="backup"></a>Sauvegarde
Hello fiable Gestionnaire d’état fournit hello capacité toocreate des sauvegardes cohérentes sans bloquer les lire ou écrire des opérations. toodo par conséquent, il utilise un mécanisme de persistance de point de contrôle et de journal.  Hello fiable Gestionnaire d’état prend floues (légers) des points de contrôle à certaine points toorelieve la pression à partir du journal des transactions hello et améliorer les temps de récupération.  Lorsque `BackupAsync` est appelée, hello Gestionnaire d’état fiable fait en sorte que tous les objets fiable toocopy leur dernier point de contrôle fichiers tooa dossier de sauvegarde local.  Ensuite, hello Gestionnaire d’état fiable copie tous les enregistrements de journal à partir hello « démarrer le pointeur » toohello dernier enregistrement du journal dans le dossier de sauvegarde hello.  Étant donné que tous les enregistrements de journal hello toohello dernier enregistrement de journal sont inclus dans la sauvegarde de hello et hello fiable Gestionnaire d’état conserve la journalisation WAL, hello fiable Gestionnaire d’état qui garantit que toutes les transactions qui sont validées (`CommitAsync` a retourné avec succès) sont inclus dans la sauvegarde de hello.

Une transaction est validée après `BackupAsync` a été appelée peut ou ne peut pas être dans la sauvegarde de hello.  Une fois que le dossier de sauvegarde local hello a été remplie par la plateforme de hello (par exemple, la sauvegarde locale est terminée par hello runtime), rappel de sauvegarde du service hello est appelé.  Ce rappel est chargé de déplacer l’emplacement externe tooan dossier de sauvegarde hello tels que le stockage Azure.

### <a name="restore"></a>Restauration
Hello fiable Gestionnaire d’état fournit hello capacité toorestore à partir d’une sauvegarde à l’aide de hello `RestoreAsync` API.  
Hello `RestoreAsync` méthode sur `RestoreContext` peut être appelée uniquement à l’intérieur de hello `OnDataLossAsync` (méthode).
Hello bool retourné par `OnDataLossAsync` indique si le service de hello restaurée son état à partir d’une source externe.
Si hello `OnDataLossAsync` retourne la valeur true, l’infrastructure de Service permet de reconstruire tous les autres réplicas à partir de ce serveur principal. Service Fabric garantit que les réplicas qui recevront `OnDataLossAsync` appeler le premier rôle principal toohello de transition, mais ne sont pas accordées lus état ou écrire l’état.
Pour les responsables de l’implémentation de StatefulService, cela implique que la méthode `RunAsync` n’est pas appelée tant que l’exécution de la méthode `OnDataLossAsync` ne s’est pas terminée correctement.
Ensuite, `OnDataLossAsync` sera appelée sur le nouveau réplica principal de hello.
Jusqu'à ce qu’un service termine cette API correctement (en retournant true ou false) et termine une reconfiguration pertinentes hello, hello API sera conserver qui est appelée à la fois.

`RestoreAsync`tout d’abord supprime tous les États existant dans le réplica principal hello qui il a été appelé sur.  
Hello fiable Gestionnaire d’état crée ensuite tous les objets fiable hello qui existent dans le dossier de sauvegarde hello.  
Ensuite, les objets fiable hello sont toorestore demandé à partir de leurs points de contrôle dans le dossier de sauvegarde hello.  
Enfin, hello Gestionnaire d’état fiable récupère son propre état à partir des enregistrements de journal hello dans le dossier de sauvegarde hello et effectue la récupération.  
Dans le cadre du processus de récupération hello, les opérations à partir de hello « point de départ » qui ont des enregistrements de journal de validation dans le dossier de sauvegarde hello sont des objets de fiable toohello relue.  
Cette étape garantit que hello état récupéré est cohérent.

## <a name="next-steps"></a>Étapes suivantes
  - [Collections fiables](service-fabric-work-with-reliable-collections.md)
  - [Démarrage rapide de Reliable Services](service-fabric-reliable-services-quick-start.md)
  - [Notifications Reliable Services](service-fabric-reliable-services-notifications.md)
  - [Configuration de Reliable Services](service-fabric-reliable-services-configuration.md)
  - [Référence du développeur pour les Collections fiables](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

