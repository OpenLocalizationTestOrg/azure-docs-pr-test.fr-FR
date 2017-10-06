---
title: microservices de Azure fiables aaaConfigure | Documents Microsoft
description: "En savoir plus sur la configuration de Reliable Services avec état dans Azure Service Fabric."
services: Service-Fabric
documentationcenter: .net
author: sumukhs
manager: timlt
editor: vturecek
ms.assetid: 9f72373d-31dd-41e3-8504-6e0320a11f0e
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: sumukhs
ms.openlocfilehash: 1e9c2890b62890a777561f25c04dc0fd11db9f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-stateful-reliable-services"></a>Configuration des services fiables (Reliable Services) avec état
Il existe deux ensembles de paramètres de configuration pour les services fiables (Reliable Services). Un ensemble est global pour tous les services fiables dans le cluster de hello tandis que tooa spécifique de service fiable particulier est hello autre ensemble.

## <a name="global-configuration"></a>Configuration globale
configuration de service fiable global Hello est spécifiée dans le manifeste du cluster pour le cluster hello sous hello KtlLogger section hello. Il permet de configurer hello partagé limites du journal d’emplacement et taille plus hello mémoire globale utilisée par l’enregistreur d’événements hello. manifeste du cluster Hello est un fichier XML qui contient les paramètres et les configurations qui s’appliquent tooall nœuds et les services de cluster de hello. fichier de Hello est généralement appelée ClusterManifest.xml. Vous pouvez voir le manifeste de cluster hello pour votre cluster à l’aide de la commande powershell de hello Get-ServiceFabricClusterManifest.

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| WriteBufferMemoryPoolMinimumInKB |Ko |8388608 |Nombre minimal de tooallocate Ko en mode noyau pour l’enregistreur d’événements hello pool de mémoire tampon d’écriture. Ce pool de mémoire est utilisé pour la mise en cache des informations d’état avant d’écrire toodisk. |
| WriteBufferMemoryPoolMaximumInKB |Ko |Aucune limite |Pool de mémoire tampon de taille maximale toowhich hello enregistreur d’événements écriture peut atteindre. |
| SharedLogId |GUID |"" |Spécifie un toouse GUID unique pour identifier le fichier journal partagé par défaut hello utilisé par tous les services fiables sur tous les nœuds de cluster de hello qui ne spécifient pas hello SharedLogId dans leur configuration de service spécifique. Si SharedLogId est spécifié, SharedLogPath doit l’être aussi. |
| SharedLogPath |Nom de chemin complet |"" |Spécifie le chemin d’accès qualifié complet hello où hello partagé de fichier journal utilisé par tous les services fiables sur tous les nœuds de cluster de hello qui ne spécifient pas hello SharedLogPath dans leur configuration de service spécifique. Toutefois, si SharedLogPath est spécifié, SharedLogId doit l'être aussi. |
| SharedLogSizeInMB |Mo |8 192 |Spécifie le nombre de hello Mo d’espace disque toostatically allouer pour les journaux partagés hello. valeur de Hello doit être supérieure ou 2048. |

Dans Azure ARM ou un modèle JSON localement, hello ci-dessous montre toochange hello hello partagé journal des transactions qui obtient la création de tooback toutes les collections fiables pour les services avec état.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="sample-local-developer-cluster-manifest-section"></a>Exemple de section du manifeste de cluster pour développeur local
Si vous voulez toochange sur votre environnement de développement local, vous devez fichier de tooedit hello clustermanifest.xml local.

```xml
   <Section Name="KtlLogger">
     <Parameter Name="SharedLogSizeInMB" Value="4096"/>
     <Parameter Name="WriteBufferMemoryPoolMinimumInKB" Value="8192" />
     <Parameter Name="WriteBufferMemoryPoolMaximumInKB" Value="8192" />
     <Parameter Name="SharedLogId" Value="{7668BB54-FE9C-48ed-81AC-FF89E60ED2EF}"/>
     <Parameter Name="SharedLogPath" Value="f:\SharedLog.Log"/>
   </Section>
```

### <a name="remarks"></a>Remarques
enregistreur d’événements Hello dispose d’un pool global de mémoire allouée à partir de la mémoire non paginée du noyau tooall disponibles des services fiables sur un nœud de mise en cache des données d’état avant d’être écrites toohello dédié journal est associé avec le réplica de service fiable hello. taille du pool Hello est contrôlé par hello WriteBufferMemoryPoolMinimumInKB et WriteBufferMemoryPoolMaximumInKB paramètres. WriteBufferMemoryPoolMinimumInKB spécifie à la fois hello taille initiale de ce pool de mémoire et le pool de mémoire hello plus petit taille toowhich hello peut réduire. WriteBufferMemoryPoolMaximumInKB est le pool de mémoire du hello toowhich de la taille la plus élevée hello peut croître. Chaque réplica de service fiable qui est ouvert peut augmenter la taille hello hello du pool de mémoire d’une quantité de système de déterminer des tooWriteBufferMemoryPoolMaximumInKB. S’il existe à la demande plus de mémoire à partir du pool de mémoire hello qu’il n’est disponible, les demandes de mémoire seront retardées jusqu'à ce que la mémoire est disponible. Par conséquent, si le pool de mémoires tampon hello écriture est trop petit pour une configuration particulière puis performances risquent d’en pâtir.

Hello SharedLogId et SharedLogPath sont toujours utilisés toodefine ensemble hello GUID et l’emplacement par défaut de hello partagé journal pour tous les nœuds de cluster de hello. journal partagé de Hello par défaut est utilisé pour tous les services fiables qui ne spécifient pas de paramètres de hello dans settings.xml hello pour un service spécifique de hello. Pour de meilleures performances, les fichiers de journal partagé doivent être placés sur des disques qui sont utilisés exclusivement pour la contention de tooreduce du fichier journal hello partagé.

SharedLogSizeInMB spécifie hello toopreallocate d’espace disque pour des journaux hello partagé par défaut sur tous les nœuds.  SharedLogId et SharedLogPath n’avez pas besoin de toobe spécifiée pour toobe SharedLogSizeInMB spécifié.

## <a name="service-specific-configuration"></a>Configuration spécifiques à un service
Vous pouvez modifier les configurations de Services fiables avec état par défaut à l’aide de package de configuration hello (configuration) ou hello d’implémentation de service (code).

* **Config** -Configuration via le package de configuration hello s’effectue en modifiant le fichier Settings.xml hello qui est généré dans la racine du package Microsoft Visual Studio hello dans le dossier de configuration hello pour chaque service de l’application hello.
* **Code** -Configuration via le code est obtenue en créant un ReliableStateManager à l’aide d’un objet ReliableStateManagerConfiguration avec l’ensemble d’options appropriées hello.

Par défaut, le runtime de Azure Service Fabric hello recherche des noms de section prédéfinie dans le fichier Settings.xml de hello et consomme des valeurs de configuration hello lors de la création de hello sous-jacent des composants d’exécution.

> [!NOTE]
> Faire **pas** supprimer des noms de section hello Hello suivant des configurations dans le fichier Settings.xml hello qui est généré dans la solution Visual Studio de hello, sauf si vous prévoyez tooconfigure votre service via le code.
> Renommer un nom de package ou de la section de configuration hello nécessitera une modification du code lors de la configuration hello ReliableStateManager.
> 
> 

### <a name="replicator-security-configuration"></a>Configuration de la sécurité du réplicateur
Configurations de sécurité réplicateur sont un canal de communication utilisé toosecure hello est utilisé lors de la réplication. Cela signifie que les services ne seront pas toosee en mesure de l’autre le trafic de réplication, garantissant que les données de salutation hautement disponible sont également sécurisé. Par défaut, une section de configuration de sécurité vide empêche de sécuriser la réplication.

### <a name="default-section-name"></a>Nom de la section par défaut
ReplicatorSecurityConfig

> [!NOTE]
> toochange ce nom de la section remplacement hello replicatorSecuritySectionName paramètre toohello ReliableStateManagerConfiguration constructeur lors de la création de hello ReliableStateManager pour ce service.
> 
> 

### <a name="replicator-configuration"></a>Configuration du réplicateur
Configurations de réplicateur configurer réplicateur hello qui est chargé d’effectuer hello avec état de le fiable état du Service hautement fiable par la réplication et la persistance d’état hello localement.
configuration par défaut de Hello est générée par le modèle de Visual Studio hello et suffisante. Cette section décrit les configurations supplémentaires qui sont le réplicateur de hello tootune disponibles.

### <a name="default-section-name"></a>Nom de la section par défaut
ReplicatorConfig

> [!NOTE]
> toochange ce nom de la section remplacement hello replicatorSettingsSectionName paramètre toohello ReliableStateManagerConfiguration constructeur lors de la création de hello ReliableStateManager pour ce service.
> 
> 

### <a name="configuration-names"></a>Noms des configurations
| Nom | Unité | Valeur par défaut | Remarques |
| --- | --- | --- | --- |
| BatchAcknowledgementInterval |Secondes |0.015 |Période de temps pour le réplicateur hello au temps d’attente secondaire hello après la réception d’une opération avant le renvoi d’un toohello d’accusé de réception principal. Toutes les autres toobe d’accusés de réception envoyé pour les opérations de traitement dans cet intervalle sont envoyés sous la forme d’une réponse. |
| ReplicatorEndpoint |N/A |Aucune valeur par défaut (paramètre obligatoire) |Adresse IP et port qui hello principal/secondaire réplicateur utilisera toocommunicate avec autres duplicateurs hello jeu de réplicas. Cela doit faire référence à un point de terminaison TCP ressource de manifeste de service hello. Consultez trop[les ressources de manifeste de Service](service-fabric-service-manifest-resources.md) tooread plus d’informations sur la définition des ressources d’un point de terminaison dans un manifeste de service. |
| MaxPrimaryReplicationQueueSize |Nombre d'opérations |8 192 |Nombre maximal d’opérations dans la file d’attente principale de hello. Une opération est libérée après que Réplicateur principal de hello reçoit un accusé de réception auprès de tous les fabricants de hello secondaire. Cette valeur doit être supérieure à 64 et être une puissance de 2. |
| MaxSecondaryReplicationQueueSize |Nombre d'opérations |16 384 |Nombre maximal d’opérations dans la file d’attente secondaire de hello. Une opération est libérée une fois son état devenu hautement disponible grâce à la persistance. Cette valeur doit être supérieure à 64 et être une puissance de 2. |
| CheckpointThresholdInMB |Mo |50 |Quantité d’espace de fichier journal après laquelle l’état hello est point de contrôle. |
| MaxRecordSizeInKB |Ko |1 024 |Plus grande taille d’enregistrement qui hello réplicateur peut-être écrire dans le journal de hello. Cette valeur doit être un multiple de 4 et supérieure à 16. |
| MinLogSizeInMB |Mo |0 (système déterminé) |Taille minimale du journal des transactions hello. journal de Hello ne pourra pas tootruncate tooa taille est inférieure à ce paramètre. 0 indique que Réplicateur hello déterminera la taille du journal minimale hello. L’augmentation de cette valeur augmente hello possibilité copies partielles et les sauvegardes incrémentielles depuis les chances de troncation est abaissée des enregistrements de journal pertinents. |
| TruncationThresholdFactor |Facteur |2 |Détermine à la taille du journal de hello, troncation sera déclenchée. Le seuil de troncation est déterminé par MinLogSizeInMB multiplié par TruncationThresholdFactor. TruncationThresholdFactor doit être supérieur à 1. MinLogSizeInMB * TruncationThresholdFactor doit être inférieur à MaxStreamSizeInMB. |
| ThrottlingThresholdFactor |Facteur |4 |Détermine la taille du journal de hello, le réplica de hello démarre à limitée. Le seuil de limitation (en Mo) est déterminé par Max ((MinLogSizeInMB * ThrottlingThresholdFactor),(CheckpointThresholdInMB * ThrottlingThresholdFactor)). Le seuil de limitation (en Mo) doit être supérieur au seuil de troncation (en Mo). Le seuil de troncation (en Mo) doit être inférieur à MaxStreamSizeInMB. |
| MaxAccumulatedBackupLogSizeInMB |Mo |800 |Taille cumulée maximale (en Mo) des journaux de sauvegarde dans une séquence de journaux de sauvegarde donnée. Un demandes de sauvegarde incrémentielle échoue si la sauvegarde incrémentielle hello génèrent une instruction backup log susceptibles de provoquer des journaux de sauvegarde hello accumulé depuis hello applique une sauvegarde complète toobe plus grande taille. Dans ce cas, utilisateur est requis tootake une sauvegarde complète. |
| SharedLogId |GUID |"" |Spécifie un toouse GUID unique pour identifier le fichier journal partagé hello utilisé avec ce réplica. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogId est spécifié, SharedLogPath doit l'être aussi. |
| SharedLogPath |Nom de chemin complet |"" |Spécifie le chemin d’accès qualifié complet hello où hello partagé fichier journal pour ce réplica sera créé. En règle générale, les services ne doivent pas utiliser ce paramètre. Toutefois, si SharedLogPath est spécifié, SharedLogId doit l'être aussi. |
| SlowApiMonitoringDuration |Secondes |300 |Définit hello intervalle pour les appels d’API managées d’analyse. Exemple : fonction de rappel de sauvegarde fournie par l’utilisateur. Une fois que l’intervalle de salutation est passée, un rapport de contrôle d’intégrité d’avertissement recevront toohello Gestionnaire de contrôle d’intégrité. |

### <a name="sample-configuration-via-code"></a>Exemple de configuration au moyen du code
```csharp
class Program
{
    /// <summary>
    /// This is hello entry point of hello service host process.
    /// </summary>
    static void Main()
    {
        ServiceRuntime.RegisterServiceAsync("HelloWorldStatefulType",
            context => new HelloWorldStateful(context, 
                new ReliableStateManager(context, 
        new ReliableStateManagerConfiguration(
                        new ReliableStateManagerReplicatorSettings()
            {
                RetryInterval = TimeSpan.FromSeconds(3)
                        }
            )))).GetAwaiter().GetResult();
    }
}    
```
```csharp
class MyStatefulService : StatefulService
{
    public MyStatefulService(StatefulServiceContext context, IReliableStateManagerReplica stateManager)
        : base(context, stateManager)
    { }
    ...
}
```


### <a name="sample-configuration-file"></a>Exemple de fichier de configuration
```xml
<?xml version="1.0" encoding="utf-8"?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Section Name="ReplicatorConfig">
      <Parameter Name="ReplicatorEndpoint" Value="ReplicatorEndpoint" />
      <Parameter Name="BatchAcknowledgementInterval" Value="0.05"/>
      <Parameter Name="CheckpointThresholdInMB" Value="512" />
   </Section>
   <Section Name="ReplicatorSecurityConfig">
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


### <a name="remarks"></a>Remarques
BatchAcknowledgementInterval contrôle la latence de réplication. La valeur '0' entraîne hello latence minimale, au coût de hello de débit (comme les autres messages d’accusé de réception doivent être envoyées et traitées, contenant chacune des accusés de réception moins).
Hello plus grande valeur hello pour BatchAcknowledgementInterval, hello hello plu globale débit de la réplication, au coût de hello de latence d’opération plus élevée. Cela traduit directement toohello une latence de transaction est validée.

valeur de Hello pour CheckpointThresholdInMB contrôles hello quantité d’espace que hello réplicateur peut utiliser des informations d’état toostore dans fichier de journal dédié du réplica hello. Augmentation de cette valeur plus élevée tooa que par défaut de hello peut entraîner des temps de reconfiguration plus rapides lorsqu’un nouveau réplica est ajouté toohello ensemble. Il s’agit en raison d’un transfert toohello partielle de l’état a lieu en raison de la disponibilité de toohello des détails de l’historique des opérations dans le journal de hello. Cela peut potentiellement accroître le temps de récupération hello d’un réplica après un incident.

paramètre de MaxRecordSizeInKB Hello définit la taille maximale de hello d’un enregistrement qui peut être écrite par le réplicateur de hello dans le fichier journal de hello. Dans la plupart des cas, la taille d’enregistrement de 1024 Ko hello par défaut est optimal. Toutefois, si le service de hello pose plus grande partie toobe des éléments de données des informations d’état hello, cette valeur peut-être toobe augmenté. Il est peu d’intérêt dans la création de MaxRecordSizeInKB inférieure à 1024, comme enregistrements plus petits uniquement utilisent l’hello espace nécessaire pour l’enregistrement de plus petit hello. Nous espérons que cette valeur doit toobe modifié dans de rares cas uniquement.

les paramètres SharedLogId et SharedLogPath Hello sont toujours toomake ensemble utilisé un service, utilisez un journal partagé distinct à partir des journaux hello partagé par défaut pour le nœud de hello. Pour plus d’efficacité, les services autant que possible doivent spécifier hello partagée journal. Les fichiers de journal partagé doivent être placés sur des disques qui sont utilisés uniquement pour les contentions de mouvement de la tête hello partagé journal fichier tooreduce. Nous espérons que cette valeur doit toobe modifié dans de rares cas uniquement.

## <a name="next-steps"></a>Étapes suivantes
* [Déboguer votre application Service Fabric dans Visual Studio](service-fabric-debugging-your-application.md)
* [Référence du développeur pour les services fiables](https://msdn.microsoft.com/library/azure/dn706529.aspx)

