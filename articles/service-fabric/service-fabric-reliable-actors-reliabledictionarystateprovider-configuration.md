---
title: "paramètres ReliableDictionaryActorStateProvider aaaChange microservices Azure | Documents Microsoft"
description: "Découvrez comment configurer les acteurs avec état Azure Service Fabric de type ReliableDictionaryActorStateProvider."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: 
ms.assetid: 79b48ffa-2474-4f1c-a857-3471f9590ded
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 44c85a41c90a17669ba874401d7921c94e7be9ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-reliable-actors--reliabledictionaryactorstateprovider"></a>Configuration de Reliable Actors - ReliableDictionaryActorStateProvider
Vous pouvez modifier la configuration par défaut de hello de ReliableDictionaryActorStateProvider en modifiant le fichier settings.xml de hello généré dans la racine du package Visual Studio hello dans le dossier de configuration hello pour l’acteur spécifiés de hello.

Bonjour Azure Service Fabric runtime recherche des noms de section prédéfinie dans le fichier settings.xml de hello et consomme les valeurs de configuration hello lors de la création de hello sous-jacent des composants d’exécution.

> [!NOTE]
> Faire **pas** supprimer ou modifier les noms de section hello Hello suivant des configurations dans le fichier settings.xml hello généré Bonjour solution Visual Studio.
> 
> 

Il existe également des paramètres globaux qui affectent la configuration hello de ReliableDictionaryActorStateProvider.

## <a name="global-configuration"></a>Configuration globale
configuration globale de Hello est spécifiée dans le manifeste du cluster pour le cluster hello sous hello KtlLogger section hello. Il permet de configurer hello partagé limites du journal d’emplacement et taille plus hello mémoire globale utilisée par l’enregistreur d’événements hello. Notez que les modifications dans le manifeste du cluster hello affectent tous les services qui utilisent ReliableDictionaryActorStateProvider et des services fiables avec état.

manifeste du cluster Hello est un fichier XML qui contient les paramètres et les configurations qui s’appliquent tooall nœuds et les services de cluster de hello. fichier de Hello est généralement appelée ClusterManifest.xml. Vous pouvez voir le manifeste de cluster hello pour votre cluster à l’aide de la commande powershell de hello Get-ServiceFabricClusterManifest.

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Ko |8388608 |Nombre minimal de tooallocate Ko en mode noyau pour l’enregistreur d’événements hello pool de mémoire tampon d’écriture. Ce pool de mémoire est utilisé pour la mise en cache des informations d’état avant d’écrire toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Ko |Aucune limite |Pool de mémoire tampon de taille maximale toowhich hello enregistreur d’événements écriture peut atteindre. |
| SharedLogId |GUID |"" |Spécifie un toouse GUID unique pour identifier le fichier journal partagé par défaut hello utilisé par tous les services fiables sur tous les nœuds de cluster de hello qui ne spécifient pas hello SharedLogId dans leur configuration de service spécifique. Si SharedLogId est spécifié, SharedLogPath doit l’être aussi. |
| SharedLogPath |Nom de chemin complet |"" |Spécifie le chemin d’accès qualifié complet hello où hello partagé de fichier journal utilisé par tous les services fiables sur tous les nœuds de cluster de hello qui ne spécifient pas hello SharedLogPath dans leur configuration de service spécifique. Toutefois, si SharedLogPath est spécifié, SharedLogId doit l'être aussi. |
| SharedLogSizeInMB |Mo |8 192 |Spécifie le nombre de hello Mo d’espace disque toostatically allouer pour les journaux partagés hello. valeur de Hello doit être supérieure ou 2048. |

### <a name="sample-cluster-manifest-section"></a>Exemple de section du manifeste de cluster
```xml
   <Section Name="KtlLogger">
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
     <Parameter Name="SharedLogSizeInMB" Value="16383"/>
   </Section>
```

### <a name="remarks"></a>Remarques
enregistreur d’événements Hello dispose d’un pool global de mémoire allouée à partir de la mémoire non paginée du noyau tooall disponibles des services fiables sur un nœud de mise en cache des données d’état avant d’être écrites toohello dédié journal est associé avec le réplica de service fiable hello. taille du pool Hello est contrôlé par hello WriteBufferMemoryPoolMinimumInKB et WriteBufferMemoryPoolMaximumInKB paramètres. WriteBufferMemoryPoolMinimumInKB spécifie à la fois hello taille initiale de ce pool de mémoire et le pool de mémoire hello plus petit taille toowhich hello peut réduire. WriteBufferMemoryPoolMaximumInKB est le pool de mémoire du hello toowhich de la taille la plus élevée hello peut croître. Chaque réplica de service fiable qui est ouvert peut augmenter la taille hello hello du pool de mémoire d’une quantité de système de déterminer des tooWriteBufferMemoryPoolMaximumInKB. S’il existe à la demande plus de mémoire à partir du pool de mémoire hello qu’il n’est disponible, les demandes de mémoire seront retardées jusqu'à ce que la mémoire est disponible. Par conséquent, si le pool de mémoires tampon hello écriture est trop petit pour une configuration particulière puis performances risquent d’en pâtir.

Hello SharedLogId et SharedLogPath sont toujours utilisés toodefine ensemble hello GUID et l’emplacement par défaut de hello partagé journal pour tous les nœuds de cluster de hello. journal partagé de Hello par défaut est utilisé pour tous les services fiables qui ne spécifient pas de paramètres de hello dans settings.xml hello pour un service spécifique de hello. Pour de meilleures performances, les fichiers de journal partagé doivent être placés sur des disques qui sont utilisés exclusivement pour la contention de tooreduce du fichier journal hello partagé.

SharedLogSizeInMB spécifie hello toopreallocate d’espace disque pour des journaux hello partagé par défaut sur tous les nœuds.  SharedLogId et SharedLogPath n’avez pas besoin de toobe spécifiée pour toobe SharedLogSizeInMB spécifié.

## <a name="replicator-security-configuration"></a>Configuration de la sécurité du réplicateur
Configurations de sécurité réplicateur sont un canal de communication utilisé toosecure hello est utilisé lors de la réplication. Cela signifie que les services ne peut pas voir le trafic de réplication à l’autre, s’assurer que les données de salutation hautement disponible sont également sécurisées.
Par défaut, une section de configuration de sécurité vide empêche de sécuriser la réplication.

### <a name="section-name"></a>Nom de la section
&lt;ActorName&gt;ServiceReplicatorSecurityConfig

## <a name="replicator-configuration"></a>Configuration du réplicateur
Les configurations de réplicateur sont réplicateur hello tooconfigure utilisé qui est responsable de l’état de fournisseur d’état d’acteur hello hautement fiable par la réplication et la persistance d’état hello localement.
configuration par défaut de Hello est générée par le modèle de Visual Studio hello et suffisante. Cette section décrit les configurations supplémentaires qui sont le réplicateur de hello tootune disponibles.

### <a name="section-name"></a>Nom de la section
&lt;ActorName&gt;ServiceReplicatorConfig

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Secondes |0.015 |Période de temps pour le réplicateur hello au temps d’attente secondaire hello après la réception d’une opération avant le renvoi d’un toohello d’accusé de réception principal. Toutes les autres toobe d’accusés de réception envoyé pour les opérations de traitement dans cet intervalle sont envoyés sous la forme d’une réponse. |
| ReplicatorEndpoint |N/A |Aucune valeur par défaut (paramètre obligatoire) |Adresse IP et port qui hello principal/secondaire réplicateur utilisera toocommunicate avec autres duplicateurs hello jeu de réplicas. Cela doit faire référence à un point de terminaison TCP ressource de manifeste de service hello. Consultez trop[les ressources de manifeste de Service](service-fabric-service-manifest-resources.md) tooread plus d’informations sur la définition des ressources d’un point de terminaison dans le manifeste de service. |
| MaxReplicationMessageSize |Octets |50 Mo |Taille maximale des données de réplication pouvant être transmises dans un même message. |
| MaxPrimaryReplicationQueueSize |Nombre d'opérations |8 192 |Nombre maximal d’opérations dans la file d’attente principale de hello. Une opération est libérée après que Réplicateur principal de hello reçoit un accusé de réception auprès de tous les fabricants de hello secondaire. Cette valeur doit être supérieure à 64 et être une puissance de 2. |
| MaxSecondaryReplicationQueueSize |Nombre d'opérations |16 384 |Nombre maximal d’opérations dans la file d’attente secondaire de hello. Une opération est libérée une fois son état devenu hautement disponible grâce à la persistance. Cette valeur doit être supérieure à 64 et être une puissance de 2. |
| CheckpointThresholdInMB |Mo |200 |Quantité d’espace de fichier journal après laquelle l’état hello est point de contrôle. |
| MaxRecordSizeInKB |Ko |1 024 |Plus grande taille d’enregistrement qui hello réplicateur peut-être écrire dans le journal de hello. Cette valeur doit être un multiple de 4 et supérieure à 16. |
| OptimizeLogForLowerDiskUsage |Boolean |true |Lorsque la valeur est true, les journaux hello sont configuré afin que les fichiers journaux dédié du réplica hello sont créé à l’aide d’un fichier partiellement alloué NTFS. Cela réduit l’espace fichier de hello hello disque réel. Si la valeur est false, les fichier hello sont créé avec des allocations fixes, qui offrent de meilleures performances en écriture hello. |
| SharedLogId |GUID |"" |Spécifie un toouse guid unique pour identifier le fichier journal partagé hello utilisé avec ce réplica. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogId est spécifié, SharedLogPath doit l'être aussi. |
| SharedLogPath |Nom de chemin complet |"" |Spécifie le chemin d’accès qualifié complet hello où hello partagé fichier journal pour ce réplica sera créé. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogPath est spécifié, SharedLogId doit l'être aussi. |

## <a name="sample-configuration-file"></a>Exemple de fichier de configuration
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="MyActorServiceReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="MyActorServiceReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="180" />
   </Section>
   <Section Name="MyActorServiceReplicatorSecurityConfig">
      <Parameter Name="CredentialType" Value="X509" />
      <Parameter Name="FindType" Value="FindByThumbprint" />
      <Parameter Name="FindValue" Value="9d c9 06 b1 69 dc 4f af fd 16 97 ac 78 1e 80 67 90 74 9d 2f" />
      <Parameter Name="StoreLocation" Value="LocalMachine" />
      <Parameter Name="StoreName" Value="My" />
      <Parameter Name="ProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="AllowedCommonNames" Value="My-Test-SAN1-Alice,My-Test-SAN1-Bob" />
   </Section>
</Settings>
```

## <a name="remarks"></a>Remarques
paramètre de BatchAcknowledgementInterval Hello contrôle la latence de réplication. La valeur '0' entraîne hello latence minimale, au coût de hello de débit (comme les autres messages d’accusé de réception doivent être envoyées et traitées, contenant chacune des accusés de réception moins).
Hello plus grande valeur hello pour BatchAcknowledgementInterval, hello hello plu globale débit de la réplication, au coût de hello de latence d’opération plus élevée. Cela traduit directement toohello une latence de transaction est validée.

Hello CheckpointThresholdInMB paramètre contrôles hello quantité d’espace disque hello replicator peut utiliser toostore les informations d’état dans fichier de journal dédié du réplica hello. Augmentation de cette valeur plus élevée tooa que par défaut de hello peut entraîner des temps de reconfiguration plus rapides lorsqu’un nouveau réplica est ajouté toohello ensemble. Il s’agit en raison d’un transfert toohello partielle de l’état a lieu en raison de la disponibilité de toohello des détails de l’historique des opérations dans le journal de hello. Cela peut potentiellement accroître le temps de récupération hello d’un réplica après un incident.

Si vous définissez OptimizeForLowerDiskUsage tootrue, espace de fichier journal sera surconfiguré afin que les réplicas actifs peuvent stocker plus d’informations sur l’état de leurs fichiers journaux, tandis que les réplicas inactifs utilise moins d’espace disque. Cela rend possible toohost plusieurs réplicas sur un nœud. Si vous définissez OptimizeForLowerDiskUsage toofalse, informations d’état hello sont écrit des fichiers journaux toohello plus rapidement.

paramètre de MaxRecordSizeInKB Hello définit la taille maximale de hello d’un enregistrement qui peut être écrite par le réplicateur de hello dans le fichier journal de hello. Dans la plupart des cas, la taille d’enregistrement de 1024 Ko hello par défaut est optimal. Toutefois, si le service de hello pose plus grande partie toobe des éléments de données des informations d’état hello, cette valeur peut-être toobe augmenté. Il est peu d’intérêt dans la création de MaxRecordSizeInKB inférieure à 1024, comme enregistrements plus petits uniquement utilisent l’hello espace nécessaire pour l’enregistrement de plus petit hello. Nous espérons que cette valeur doit toobe modifiée uniquement dans de rares cas.

les paramètres SharedLogId et SharedLogPath Hello sont toujours toomake ensemble utilisé un service, utilisez un journal partagé distinct à partir des journaux hello partagé par défaut pour le nœud de hello. Pour plus d’efficacité, les services autant que possible doivent spécifier hello partagée journal. Les fichiers de journal partagé doivent être placés sur des disques qui sont utilisés uniquement pour le fichier journal partagé hello, contention de mouvement de la tête tooreduce. Nous espérons que toobe modifiée uniquement dans de rares cas aurait besoin de ces valeurs.

