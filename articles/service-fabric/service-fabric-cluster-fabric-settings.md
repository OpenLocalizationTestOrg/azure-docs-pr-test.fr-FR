---
title: "les paramètres de cluster Azure Service Fabric aaaChange | Documents Microsoft"
description: "Cet article décrit les paramètres de la structure hello et hello fabric mise à niveau des stratégies que vous pouvez personnaliser."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Personnaliser les paramètres de cluster Service Fabric et la stratégie de mise à niveau de la structure
Ce document vous indique comment toocustomize hello différents paramètres de la structure et une stratégie de mise à niveau de fabric hello pour votre cluster Service Fabric. Vous pouvez les personnaliser dans le portail de hello ou un modèle Azure Resource Manager.

> [!NOTE]
> Certains paramètres peuvent être disponibles via le portail de hello. Au cas où un paramètre répertorié ci-dessous n’est pas disponible via le portail de hello personnaliser à l’aide d’un modèle Azure Resource Manager.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Personnalisation des paramètres de cluster Service Fabric à l’aide de modèles Azure Resource Manager
étapes Hello ci-dessous montrent comment tooadd un nouveau paramètre *MaxDiskQuotaInMB* toohello *Diagnostics* section.

1. Accédez toohttps://resources.azure.com
2. Accédez tooyour abonnement en développant les abonnements -> -> des groupes de ressources Microsoft.ServiceFabric -> votre nom de Cluster
3. Dans hello coin supérieur droit, sélectionnez « En lecture/écriture »
4. Sélectionnez Modifier et mettre à jour hello `fabricSettings` élément JSON et ajouter un nouvel élément

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Paramètres de structure que vous pouvez personnaliser
Les paramètres de l’ensemble fibre optique hello que vous pouvez personnaliser sont :

### <a name="section-name-diagnostics"></a>Nom de la section : Diagnostics
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ConsumerInstances |String |liste de Hello des instances de consommateur DCA. |
| ProducerInstances |String |liste de Hello des instances de producteur DCA. |
| AppEtwTraceDeletionAgeInDays |Entier (valeur par défaut : 3) |Délai en jours à l’issue duquel nous supprimons les anciens fichiers ETL contenant les traces ETW d’application. |
| AppDiagnosticStoreAccessRequiresImpersonation |Valeur booléenne (valeur par défaut : true) |Indique si l’emprunt d’identité est requis lors de l’accès aux diagnostics stocke au nom de l’application hello. |
| MaxDiskQuotaInMB |Entier (valeur par défaut : 65536) |Quota de disque (en Mo) pour les fichiers journaux de Windows Fabric. |
| DiskFullSafetySpaceInMB |Entier (valeur par défaut : 1024) |Espace disque restant dans tooprotect Mo d’une utilisation par DCA. |
| ApplicationLogsFormatVersion |Entier (valeur par défaut : 0) |Version du format des journaux de l’application. Valeurs prises en charge : 0 et 1. Version 1 inclut plus de champs à partir de l’enregistrement d’événement ETW de hello que version 0. |
| ClusterId |String |id unique de Hello du cluster de hello. Il est généré lors de la création du cluster hello. |
| EnableTelemetry |Valeur booléenne (valeur par défaut : true) |Il est en train de tooenable ou désactiver la télémétrie. |
| EnableCircularTraceSession |Valeur booléenne (valeur par défaut : false) |Indicateur spécifiant si les sessions de trace circulaire doivent être utilisées. |

### <a name="section-name-traceetw"></a>Nom de la section : Trace/Etw
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| Level |Entier (valeur par défaut : 4) |Le niveau etw de la trace accepte les valeurs 1, 2, 3, 4. prise en charge de toobe vous devez conserver le niveau de trace hello à 4 |

### <a name="section-name-performancecounterlocalstore"></a>Nom de la section : PerformanceCounterLocalStore
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| IsEnabled |Valeur booléenne (valeur par défaut : true) |Indicateur spécifiant si la collection de compteurs de performance sur le nœud local est activée. |
| SamplingIntervalInSeconds |Entier (valeur par défaut : 60) |Intervalle d’échantillonnage des compteurs de performances collectés. |
| Counters |String |Liste de séparées par des virgules des toocollect des compteurs de performances. |
| MaxCounterBinaryFileSizeInMB |Entier (valeur par défaut : 1) |Taille maximale (en Mo) de chaque fichier binaire de compteur de performances. |
| NewCounterBinaryFileCreationIntervalInMinutes |Entier (valeur par défaut : 10) |Durée maximale (en secondes) après lequel un fichier binaire de compteur de performances est créé. |

### <a name="section-name-setup"></a>Nom de la section : Setup
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| FabricDataRoot |String |Répertoire racine des données Service Fabric. La valeur par défaut pour Azure est d:\svcfab |
| FabricDataRoot |String |Répertoire racine du journal Service Fabric. Il s’agit de l’emplacement des journaux et des traces de SF. |
| ServiceRunAsAccountName |String |nom du compte Hello sous le service hôte de l’ensemble fibre optique toorun. |
| ServiceStartupType |String |type de démarrage de Hello du service hôte de l’ensemble fibre optique hello. |
| SkipFirewallConfiguration |Valeur booléenne (valeur par défaut : false) |Spécifie si les paramètres de pare-feu doivent toobe définie par le système de hello ou non. Cela s’applique uniquement si vous utilisez le pare-feu Windows. Si vous utilisez des pare-feu tiers, vous devez ouvrir les ports hello pour toouse système et des applications de hello |

### <a name="section-name-transactionalreplicator"></a>Nom de la section : TransactionalReplicator
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| MaxCopyQueueSize |Valeur Uint (valeur par défaut : 16384) |Valeur maximale de hello définit la taille initiale de hello pour une file d’attente hello qui gère les opérations de réplication. Ce nombre doit être une puissance de 2. Si pendant l’exécution atteint la file d’attente de hello operations de taille toothis seront limitées entre les duplicateurs principaux et secondaires hello. |
| BatchAcknowledgementInterval | Durée en secondes (valeur par défaut : 0.015) | Spécifiez la durée en secondes. Détermine la durée hello que hello attentes réplicateur après la réception d’une opération avant le renvoi d’un accusé de réception. Autres opérations reçues au cours de cette période auront leurs accusés de réception renvoyés dans un seul message -> réduction du trafic réseau, mais potentiellement réduire le débit hello du réplicateur de hello. |
| MaxReplicationMessageSize |Valeur Uint (valeur par défaut : 52428800) | Taille maximale des messages des opérations de réplication. Valeur par défaut : 50 Mo. |
| ReplicatorAddress |Chaîne (valeur par défaut : "localhost:0") | point de terminaison Hello sous forme d’une chaîne, « IP : port » qui est utilisé par les connexions de tooestablish Windows Fabric réplicateur hello avec d’autres réplicas dans les opérations de toosend et de la réception de commande. |
| InitialPrimaryReplicationQueueSize |Valeur Uint (valeur par défaut : 64) | Cette valeur définit la taille initiale de hello pour une file d’attente hello qui gère les opérations de réplication hello sur hello principal. Ce nombre doit être une puissance de 2.|
| MaxPrimaryReplicationQueueSize |Valeur Uint (valeur par défaut : 8192) |Ceci est hello le nombre maximal d’opérations qui peuvent exister dans la file d’attente de réplication principale hello. Ce nombre doit être une puissance de 2. |
| MaxPrimaryReplicationQueueMemorySize |Valeur Uint (valeur par défaut : 0) |Il s’agit de valeur maximale de hello de file d’attente de réplication principale hello en octets. |
| InitialSecondaryReplicationQueueSize |Valeur Uint (valeur par défaut : 64) |Cette valeur définit la taille initiale de hello pour une file d’attente hello qui gère les opérations de réplication hello sur hello secondaire. Ce nombre doit être une puissance de 2. |
| MaxSecondaryReplicationQueueSize |Valeur Uint (valeur par défaut : 16384) |Ceci est hello le nombre maximal d’opérations qui peuvent exister dans la file d’attente de réplication secondaire hello. Ce nombre doit être une puissance de 2. |
| MaxSecondaryReplicationQueueMemorySize |Valeur Uint (valeur par défaut : 0) |Il s’agit de valeur maximale de hello de file d’attente de réplication secondaire hello en octets. |
| SecondaryClearAcknowledgedOperations |Valeur booléenne (valeur par défaut : false) |Valeur booléenne qui contrôle si les opérations de hello sur réplicateur secondaire de hello sont effacées une fois qu’ils sont reconnus toohello principal (disque toohello vidé). Cette tooTRUE peut entraîner des lectures supplémentaires sur les paramètres hello nouveau réplica principal, lors de l’interception des réplicas après un basculement. |
| MaxMetadataSizeInKB |Entier (valeur par défaut : 4) |Taille maximale de métadonnées de flux de données de journal hello. |
| MaxRecordSizeInKB |Valeur Uint (valeur par défaut : 1024) | Taille maximale de l’enregistrement du flux de journal. |
| CheckpointThresholdInMB |Entier (valeur par défaut : 50) |Un point de contrôle sera initialisé lorsque l’utilisation du journal hello dépasse cette valeur. |
| MaxAccumulatedBackupLogSizeInMB |Entier (valeur par défaut : 800) |Taille cumulée maximale (en Mo) des journaux de sauvegarde dans une séquence de journaux de sauvegarde donnée. Un demandes de sauvegarde incrémentielle échoue si la sauvegarde incrémentielle hello génèrent une instruction backup log susceptibles de provoquer des journaux de sauvegarde hello accumulé depuis hello applique une sauvegarde complète toobe plus grande taille. Dans ce cas, utilisateur est requis tootake une sauvegarde complète. |
| MaxWriteQueueDepthInKB |Entier (valeur par défaut : 0) | Int maximale écrire profondeur de file d’attente de ce journal de base hello peut servir spécifiée en kilo-octets de journal hello qui est associé à ce réplica. Cette valeur est le nombre maximal de hello d’octets qui peuvent être en attente au cours des mises à jour du journal de base. Il peut être 0 pour hello toocompute d’enregistreur d’événements de base une valeur appropriée ou un multiple de 4. |
| SharedLogId |String |Identificateur du journal partagé. Cette valeur est un GUID et doit être propre à chaque journal partagé. |
| SharedLogPath |String |Journal partagé toohello de chemin d’accès. Si cette valeur est vide de journal partagé hello par défaut est utilisé. |
| SlowApiMonitoringDuration |Durée en secondes, la valeur par défaut est 300 | Spécifiez la durée de l’API avant l’émission d’un événement d’avertissement.|
| MinLogSizeInMB |Entier (valeur par défaut : 0) |Taille minimale du journal des transactions hello. journal de Hello ne pourra pas tootruncate tooa taille est inférieure à ce paramètre. 0 indique que Réplicateur hello déterminera la taille minimale du journal de hello selon les paramètres tooother. L’augmentation de cette valeur augmente hello possibilité copies partielles et les sauvegardes incrémentielles depuis les chances de troncation est abaissée des enregistrements de journal pertinents. |

### <a name="section-name-fabricclient"></a>Nom de la section : FabricClient
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| NodeAddresses |Chaîne (valeur par défaut : "") |Une collection d’adresses (chaînes de connexion) sur des nœuds différents qui peuvent être utilisé toocommunicate avec Bonjour Bonjour Naming Service. Initialement hello que client connecte en sélectionnant une adresses de hello de façon aléatoire. Si plus d’une chaîne de connexion est spécifiée et une connexion échoue en raison d’une communication ou d’une erreur de délai d’attente ; Hello Client bascule l’adresse suivant toouse hello séquentiellement. Consultez la section de nouvelle tentative d’adresse du Service d’affectation de noms de hello pour plus d’informations sur la sémantique de nouvelles tentatives. |
| ConnectionInitializationTimeout |Durée en secondes (valeur par défaut : 2) |Spécifiez la durée en secondes. Intervalle de délai de connexion pour chaque client de temps tente tooopen une passerelle toohello de connexion. |
| PartitionLocationCacheLimit |Entier (valeur par défaut : 100000) |Nombre de partitions mis en cache pour la résolution de service (la valeur too0 pour aucune limite). |
| ServiceChangePollInterval |Durée en secondes (valeur par défaut : 120) |Spécifiez la durée en secondes. intervalle de salutation entre deux interrogations consécutives pour service remplace hello client toohello passerelle pour les rappels de notifications de modification service inscrit. |
| KeepAliveIntervalInSeconds |Entier (valeur par défaut : 20) |intervalle de salutation à quels hello fabricclient ne transport envoie passerelle toohello de messages persistants. À 0, le paramètre keepAlive est désactivé. Cette valeur doit être un entier positif. |
| HealthOperationTimeout |Durée en secondes (valeur par défaut : 120) |Spécifiez la durée en secondes. délai d’attente de Hello pour un message de rapport envoyé tooHealth Manager. |
| HealthReportSendInterval |Durée en secondes, la valeur par défaut est 30 |Spécifiez la durée en secondes. intervalle de salutation à quel composant de création de rapports envoie accumulé d’intégrité signale tooHealth Manager. |
| HealthReportRetrySendInterval |Durée en secondes, la valeur par défaut est 30 |Spécifiez la durée en secondes. intervalle de salutation à quel composant de création de rapports envoie à nouveau accumulé d’intégrité signale tooHealth Manager. |
| RetryBackoffInterval |Durée en secondes (valeur par défaut : 3) |Spécifiez la durée en secondes. Hello intervalle de temporisation avant de recommencer l’opération de hello. |
| MaxFileSenderThreads |Valeur Uint (valeur par défaut : 10) |nombre maximal de Hello des fichiers qui sont transférés en parallèle. |

### <a name="section-name-common"></a>Nom de la section : Common
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| PerfMonitorInterval |Durée en secondes (valeur par défaut : 1) |Spécifiez la durée en secondes. Interface de surveillance des performances. Désactive la surveillance too0 de paramètre ou une valeur négative. |

### <a name="section-name-healthmanager"></a>Nom de la section : HealthManager
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Valeur booléenne (valeur par défaut : false) |Stratégie d’évaluation de l’intégrité du cluster : activer pour chaque évaluation de l’intégrité du type d’application. |

### <a name="section-name-fabricnode"></a>Nom de la section : FabricNode
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| StateTraceInterval |Durée en secondes, la valeur par défaut est 300 |Spécifiez la durée en secondes. Intervalle Hello pour le suivi d’état du nœud sur chaque nœud et les nœuds sur FM/FMM. |

### <a name="section-name-nodedomainids"></a>Nom de la section : NodeDomainIds
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| UpgradeDomainId |Chaîne (valeur par défaut : "") |Décrit le domaine de mise à niveau hello qu'un nœud appartient. |
| PropertyGroup |NodeFaultDomainIdCollection |Décrit les domaines d’erreur hello qu'un nœud appartient. domaine d’erreur Hello est défini via un URI qui décrit l’emplacement du nœud hello dans le centre de données hello hello.  Erreur URI sont Hello format fd : / fd suivie d’un segment de chemin d’accès d’URI.|

### <a name="section-name-nodeproperties"></a>Nom de la section : NodeProperties
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Collection de paires clé-valeur de chaîne pour les propriétés du nœud. |

### <a name="section-name-nodecapacities"></a>Nom de la section : NodeCapacities
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Collection des capacités du nœud pour les différentes mesures. |

### <a name="section-name-fabricnode"></a>Nom de la section : FabricNode
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| StartApplicationPortRange |Entier (valeur par défaut : 0) |Début de ports d’application hello gérés par le sous-système d’hébergement. Requis si EndpointFilteringEnabled a la valeur true dans Hosting. |
| EndApplicationPortRange |Entier (valeur par défaut : 0) |Fin (non incluse) de ports d’application hello gérés par le sous-système d’hébergement. Requis si EndpointFilteringEnabled a la valeur true dans Hosting. |
| ClusterX509StoreName |Chaîne (valeur par défaut : "My") |Nom du magasin de certificats X.509 qui contient le certificat de cluster utilisé pour sécuriser les communications internes au cluster. |
| ClusterX509FindType |Chaîne (valeur par défaut : "FindByThumbprint") |Indique comment toosearch certificat de cluster dans le magasin de hello spécifié par valeurs ClusterX509StoreName prises en charge : « FindByThumbprint » ; « FindBySubjectName » avec « FindBySubjectName » ; Lorsqu’il existe plusieurs correspondances ; Hello une date d’expiration de la plus lointaine hello est utilisée. |
| ClusterX509FindValue |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé un certificat de cluster toolocate. |
| ClusterX509FindValueSecondary |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé un certificat de cluster toolocate. |
| ServerAuthX509StoreName |Chaîne (valeur par défaut : "My") |Nom du magasin de certificats X.509 qui contient le certificat de serveur pour le service d’entrée. |
| ServerAuthX509FindType |Chaîne (valeur par défaut : "FindByThumbprint") |Indique comment toosearch pour le certificat de serveur dans le magasin de hello spécifié par ServerAuthX509StoreName pris en charge la valeur : FindByThumbprint ; FindBySubjectName. |
| ServerAuthX509FindValue |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé un certificat de serveur toolocate. |
| ServerAuthX509FindValueSecondary |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé un certificat de serveur toolocate. |
| ClientAuthX509StoreName |Chaîne (valeur par défaut : "My") |Nom du magasin de certificats X.509 hello qui contient le certificat pour le rôle d’administrateur par défaut fabricclient ne. |
| ClientAuthX509FindType |Chaîne (valeur par défaut : "FindByThumbprint") |Indique comment toosearch pour le certificat dans le magasin de hello spécifié par ClientAuthX509StoreName pris en charge la valeur : FindByThumbprint ; FindBySubjectName. |
| ClientAuthX509FindValue |Chaîne (valeur par défaut : "") | Valeur de filtre de recherche utilisé toolocate certificat pour le rôle d’administrateur par défaut fabricclient ne. |
| ClientAuthX509FindValueSecondary |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé toolocate certificat pour le rôle d’administrateur par défaut fabricclient ne. |
| UserRoleClientX509StoreName |Chaîne (valeur par défaut : "My") |Nom du magasin de certificats X.509 hello qui contient le certificat pour le rôle d’utilisateur par défaut fabricclient ne. |
| UserRoleClientX509FindType |Chaîne (valeur par défaut : "FindByThumbprint") |Indique comment toosearch pour le certificat dans le magasin de hello spécifié par UserRoleClientX509StoreName pris en charge la valeur : FindByThumbprint ; FindBySubjectName. |
| UserRoleClientX509FindValue |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé toolocate certificat pour le rôle d’utilisateur par défaut fabricclient ne. |
| UserRoleClientX509FindValueSecondary |Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé toolocate certificat pour le rôle d’utilisateur par défaut fabricclient ne. |

### <a name="section-name-paas"></a>Nom de la section : Paas
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ClusterId |Chaîne (valeur par défaut : "") |Magasin de certificats X509 utilisé par l’infrastructure pour protéger la configuration. |

### <a name="section-name-fabrichost"></a>Nom de la section : FabricHost
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| StopTimeout |Durée en secondes, la valeur par défaut est 300 |Spécifiez la durée en secondes. délai d’attente de Hello pour l’activation du service hébergé ; désactivation et la mise à niveau. |
| StartTimeout |Durée en secondes, la valeur par défaut est 300 |Spécifiez la durée en secondes. Délai d’expiration pour le démarrage de fabricactivationmanager. |
| ActivationRetryBackoffInterval |Durée en secondes (valeur par défaut : 5) |Spécifiez la durée en secondes. Intervalle de refus sur tous les échecs d’activation ; À chaque activation continue système hello de défaillance effectuera une nouvelle tentative d’activation de hello pour les toohello MaxActivationFailureCount. intervalle avant nouvelle tentative de Hello à chaque tentative est un produit de l’activation continue échec et hello activation intervalle de temporisation. |
| ActivationMaxRetryInterval |Durée en secondes, la valeur par défaut est 300 |Spécifiez la durée en secondes. Intervalle maximum avant une nouvelle tentative d’activation. Lors de chaque tentative de hello échec continue intervalle est calculé en tant que Min (ActivationMaxRetryInterval ; Nombre d’échecs continue * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Entier (valeur par défaut : 10) |Il s’agit de nombre maximal de hello pour lequel système réessaie d’échec de l’activation avant d’abandonner. |
| EnableServiceFabricAutomaticUpdates |Valeur booléenne (valeur par défaut : false) |Il s’agit de mise à jour automatique tooenable fabric via Windows Update. |
| EnableServiceFabricBaseUpgrade |Valeur booléenne (valeur par défaut : false) |Il s’agit de mise à jour pour le serveur de base tooenable. |
| EnableRestartManagement |Valeur booléenne (valeur par défaut : false) |Il s’agit de redémarrage du serveur tooenable. |


### <a name="section-name-failovermanager"></a>Nom de la section : FailoverManager
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Durée en secondes (valeur par défaut : 60.0 * 30) |Spécifiez la durée en secondes. Lorsqu’un réplica persistant s’arrête ; Windows Fabric attend que cette durée pour hello réplica toocome sauvegarder avant de créer de nouveaux réplicas de remplacement (ce qui nécessitent une copie de l’état de hello). |
| QuorumLossWaitDuration |Durée en secondes (valeur par défaut : MaxValue) |Spécifiez la durée en secondes. Il s’agit de durée maximale de hello pour lequel nous autoriser un toobe de partition dans un état de la perte de quorum. Si la partition de hello est toujours une perte de quorum après cette durée ; partition de Hello est récupérée à partir de la perte de quorum en considérant hello vers le bas des réplicas sont perdues. Notez que cela peut potentiellement provoquer une perte de données. |
| UserStandByReplicaKeepDuration |Durée en secondes (valeur par défaut : 3600.0 * 24 * 7) |Spécifiez la durée en secondes. Lorsqu’un réplica persistant n’est plus défaillant, il peut avoir déjà été remplacé. Cette minuterie détermine la durée pendant laquelle hello FM conservera le réplica en attente de hello avant de les supprimer. |
| UserMaxStandByReplicaCount |Entier (valeur par défaut : 1) |nombre maximal de Hello par défaut de réplicas StandBy hello système conserve pour les services de l’utilisateur. |

### <a name="section-name-namingservice"></a>Nom de la section : NamingService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| TargetReplicaSetSize |Entier (valeur par défaut : 7) |nombre de Hello du réplica de jeux pour chaque partition du magasin du Service de dénomination hello. Augmenter le nombre hello du réplica jeux augmente hello niveau de fiabilité pour plus d’informations hello Bonjour magasin du Service d’affectation de noms ; diminution de modification hello hello informations seront perdue à la suite de défaillances de nœud ; à un coût de l’augmentation de la charge sur Windows Fabric et hello temps dure tooperform les mises à jour les données d’affectation de noms toohello.|
|MinReplicaSetSize | Entier (valeur par défaut : 3) | nombre minimal de Hello de réplicas d’affectation de noms de Service requis toowrite dans toocomplete une mise à jour. S’il y a moins de réplicas que cette active Bonjour du système hello fiabilité système refuse la banque du Service d’affectation de noms toohello mises à jour jusqu'à ce que les réplicas sont restaurés. Cette valeur ne doit jamais être supérieure à hello TargetReplicaSetSize. |
|ReplicaRestartWaitDuration | Durée en secondes (valeur par défaut : 60.0 * 30)| Spécifiez la durée en secondes. Ce minuteur démarre lorsqu’un réplica du service d’attribution de noms tombe en panne.  Lorsqu’il expire hello FM commencera réplicas hello tooreplace vers le bas (il ne pas encore prendre en compte les perdu). |
|QuorumLossWaitDuration | Durée en secondes (valeur par défaut : MaxValue) | Spécifiez la durée en secondes. Ce minuteur démarre lorsqu’un service d’attribution de noms passe en perte de quorum.  Lorsqu’il expire hello FM considérera hello vers le bas des réplicas sont perdues ; et essayez de toorecover quorum. Notez que cela peut entraîner une perte de données. |
|StandByReplicaKeepDuration | Durée en secondes (valeur par défaut : 3600.0*2) | Spécifiez la durée en secondes. Lorsqu’un réplica du Service d’attribution de noms n’est plus défaillant, il peut avoir déjà été remplacé.  Cette minuterie détermine la durée pendant laquelle hello FM conservera le réplica en attente de hello avant de les supprimer. |
|PlacementConstraints | Chaîne (valeur par défaut : "") | Contrainte de placement pour hello Naming Service. |
|ServiceDescriptionCacheLimit | Entier (valeur par défaut : 0) | nombre maximal de Hello d’entrées maintenues dans le cache de description de service LRU hello à hello d’affectation de noms de Service de banque (la valeur too0 pour aucune limite). |
|RepairInterval | Durée en secondes (valeur par défaut : 5) | Spécifiez la durée en secondes. Intervalle dans quel hello démarrera d’affectation de noms réparation d’une incohérence entre hello autorité propriétaire et nom. |
|MaxNamingServiceHealthReports | Entier (valeur par défaut : 10) | nombre maximal de Hello d’opérations lentes qui stockent les d’affectation de noms de service non intègre des rapports à la fois. Si vous spécifiez 0, toutes les opérations lentes sont envoyées. |
| MaxMessageSize |Entier, valeur par défaut : 4*1024*1024 |Hello taille maximale du message pour la communication du nœud client lors de l’utilisation d’affectation de noms. Atténuation d’attaque par déni de service. Valeur par défaut : 4 Mo. |
| MaxFileOperationTimeout |Durée en secondes, la valeur par défaut est 30 |Spécifiez la durée en secondes. délai d’attente maximal Hello autorisée pour l’opération de service de fichier store. Les requêtes spécifiant un délai d’expiration supérieur seront rejetées. |
| MaxOperationTimeout |Durée en secondes (valeur par défaut : 600) |Spécifiez la durée en secondes. délai d’attente maximal Hello autorisée pour les opérations du client. Les requêtes spécifiant un délai d’expiration supérieur seront rejetées. |
| MaxClientConnections |Entier, valeur par défaut : 1000 |Hello nombre maximal autorisé de connexions de client par la passerelle. |
| ServiceNotificationTimeout |Durée en secondes, la valeur par défaut est 30 |Spécifiez la durée en secondes. délai d’expiration de Hello utilisé lors de la remise client toohello notifications du service. |
| MaxOutstandingNotificationsPerClient |Entier, valeur par défaut : 1000 |nombre maximal de Hello de notifications en attente avant l’inscription du client est dû être fermée par la passerelle de hello. |
| MaxIndexedEmptyPartitions |Entier, valeur par défaut : 1000 |nombre maximal de Hello de partitions vides qui restera indexées dans le cache de notification hello pour la synchronisation des clients se reconnectant. Toutes les partitions vides au-dessus de ce nombre en seront retirées index hello recherche version ordre croissant. La reconnexion de clients peut toujours synchroniser et recevoir des mises à jour de la partition vide manquantes ; mais le protocole de synchronisation hello devient plus coûteux. |
| GatewayServiceDescriptionCacheLimit |Entier (valeur par défaut : 0) |nombre maximal de Hello d’entrées maintenues dans le cache de description de service LRU hello à hello d’affectation de noms de passerelle (la valeur too0 pour aucune limite). |
| PartitionCount |Entier (valeur par défaut : 3) |nombre de Hello de partitions de hello Naming Service magasin toobe est créé. Chaque partition possède une clé de partition unique correspondant tooits index ; C’est le cas [0 ; les clés de partition PartitionCount) existe. Nombre croissant de hello de Naming Service partitions augmente échelle hello hello Naming Service peut effectuer en réduisant la durée moyenne hello données détenues par n’importe quel réplica de sauvegarde est défini ; pour un coût de l’utilisation accrue de ressources (depuis PartitionCount * ReplicaSetSize les réplicas de service doivent être conservées).|

### <a name="section-name-runas"></a>Nom de la section : RunAss
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| RunAsAccountName |Chaîne (valeur par défaut : "") |Indique le nom de compte d’identification hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser ou ManagedServiceAccount. Les valeurs autorisées sont "domain\user" ou "user@domain". |
|RunAsAccountType|Chaîne (valeur par défaut : "") |Indique le type de compte d’identification hello. Ce paramètre est nécessaire pour toutes les sections RunAs. Les valeurs autorisées DomainUser/NetworkService/ManagedServiceAccount/LocalSystem.|
|RunAsPassword|Chaîne (valeur par défaut : "") |Indique le mot de passe RunAs hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser. |

### <a name="section-name-runasfabric"></a>Nom de la section : RunAs_Fabric
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| RunAsAccountName |Chaîne (valeur par défaut : "") |Indique le nom de compte d’identification hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser ou ManagedServiceAccount. Les valeurs autorisées sont "domain\user" ou "user@domain". |
|RunAsAccountType|Chaîne (valeur par défaut : "") |Indique le type de compte d’identification hello. Ce paramètre est nécessaire pour toutes les sections RunAs. Les valeurs autorisées sont LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem. |
|RunAsPassword|Chaîne (valeur par défaut : "") |Indique le mot de passe RunAs hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser. |

### <a name="section-name-runashttpgateway"></a>Nom de la section : RunAs_HttpGateway
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| RunAsAccountName |Chaîne (valeur par défaut : "") |Indique le nom de compte d’identification hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser ou ManagedServiceAccount. Les valeurs autorisées sont "domain\user" ou "user@domain". |
|RunAsAccountType|Chaîne (valeur par défaut : "") |Indique le type de compte d’identification hello. Ce paramètre est nécessaire pour toutes les sections RunAs. Les valeurs autorisées sont LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem. |
|RunAsPassword|Chaîne (valeur par défaut : "") |Indique le mot de passe RunAs hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser. |

### <a name="section-name-runasdca"></a>Nom de la section : RunAs_DCA
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| RunAsAccountName |Chaîne (valeur par défaut : "") |Indique le nom de compte d’identification hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser ou ManagedServiceAccount. Les valeurs autorisées sont "domain\user" ou "user@domain". |
|RunAsAccountType|Chaîne (valeur par défaut : "") |Indique le type de compte d’identification hello. Ce paramètre est nécessaire pour toutes les sections RunAs. Les valeurs autorisées sont LocalUser/DomainUser/NetworkService/ManagedServiceAccount/LocalSystem. |
|RunAsPassword|Chaîne (valeur par défaut : "") |Indique le mot de passe RunAs hello. Ce paramètre n’est nécessaire que pour le type de compte DomainUser. |

### <a name="section-name-httpgateway"></a>Nom de la section : HttpGateway
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
|IsEnabled|Valeur booléenne (valeur par défaut : false) | Active/désactive hello httpgateway. Httpgateway est désactivé par défaut et cette configuration doit toobe ensemble tooenable il. |
|ActiveListeners |Valeur Uint (valeur par défaut : 50) | Nombre de file d’attente de lectures toopost toohello http server. Ce paramètre contrôle nombre hello de demandes simultanées qui peuvent être satisfaites par hello HttpGateway. |
|MaxEntityBodySize |Valeur Uint (valeur par défaut : 4194304) |  Donne la taille maximale de hello hello du corps de qui peuvent se produire à partir d’une requête http. Valeur par défaut : 4 Mo. Le paramètre httpgateway ne peut pas traiter une requête si son corps a une taille supérieure à cette valeur. La taille minimum du bloc de lectures est de 4096 octets. Par conséquent, il a toobe > = 4096. |
|HttpGatewayHealthReportSendInterval |Durée en secondes, la valeur par défaut est 30 | Spécifiez la durée en secondes. intervalle de salutation à quels hello passerelle Http envoie accumulées tooHealth de rapports d’intégrité Manager. |

### <a name="section-name-ktllogger"></a>Nom de la section : KtlLogger
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Entier (valeur par défaut : 1) | Indicateur qui indique si les paramètres de mémoire hello doivent être automatiquement et dynamiquement configurés. Si les paramètres de configuration zéro puis hello mémoire sont utilisés directement et ne changent pas en fonction des conditions de système. Si une mémoire hello paramètres sont configurées automatiquement et peuvent changer selon les conditions système. |
|WriteBufferMemoryPoolMinimumInKB |Entier (valeur par défaut : 8388608) |nombre de Hello de Ko tooinitially allouer pour le pool de mémoires tampon hello écriture. Utilisez 0 tooindicate aucune limite par défaut ne doit être cohérente avec SharedLogSizeInMB ci-dessous. |
|WriteBufferMemoryPoolMaximumInKB | Entier (valeur par défaut : 0) |nombre de Hello Ko tooallow Hello écriture toogrow de pool de mémoire tampon jusqu'à. N’Utilisez 0 tooindicate aucune limite. |
|MaximumDestagingWriteOutstandingInKB | Entier (valeur par défaut : 0) | nombre de Hello Ko tooallow Hello partagé tooadvance journal avance journal dédié de hello. N’Utilisez 0 tooindicate aucune limite.
|SharedLogPath |Chaîne (valeur par défaut : "") | Chemin d’accès et nom toolocation tooplace partagé conteneur de journal. Utilisez "" pour utiliser le chemin par défaut sous la racine des données de structure. |
|SharedLogId |Chaîne (valeur par défaut : "") |GUID unique du conteneur du journal partagé. Utilisez "" si vous choisissez le chemin par défaut sous la racine des données de structure. |
|SharedLogSizeInMB |Entier (valeur par défaut : 8192) | nombre de Hello de tooallocate Mo dans le conteneur de journal partagé hello. |

### <a name="section-name-applicationgatewayhttp"></a>Nom de la section : ApplicationGateway/Http
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
|IsEnabled |Valeur booléenne (valeur par défaut : false) | Active/désactive hello HttpApplicationGateway. HttpApplicationGateway est désactivé par défaut et cette configuration doit toobe ensemble tooenable il. |
|NumberOfParallelOperations | Valeur Uint (par défaut : 5000) | Nombre de file d’attente de lectures toopost toohello http server. Ce paramètre contrôle nombre hello de demandes simultanées qui peuvent être satisfaites par hello HttpGateway. |
|DefaultHttpRequestTimeout |Durée en secondes. La valeur par défaut est 120 |Spécifiez la durée en secondes.  Donne le délai de demande par défaut hello pour les demandes http hello en cours de traitement dans la passerelle d’application http hello. |
|ResolveServiceBackoffInterval |Durée en secondes (valeur par défaut : 5) |Spécifiez la durée en secondes.  Donne l’intervalle de temporisation par défaut hello avant de retenter une opération de service de résolution a échoué. |
|BodyChunkSize |Valeur Uint (valeur par défaut : 16384) |  Donne la taille hello de pour segment hello en octets utilisée du corps de tooread hello. |
|GatewayAuthCredentialType |Chaîne (valeur par défaut : "None") | Indique le type hello de toouse d’informations d’identification de sécurité au niveau de valeurs valide point de terminaison de passerelle application hello http sont « None / X 509. |
|GatewayX509CertificateStoreName |Chaîne (valeur par défaut : "My") | Nom du magasin de certificats X.509 qui contient le certificat de la passerelle d’application HTTP. |
|GatewayX509CertificateFindType |Chaîne (valeur par défaut : "FindByThumbprint") | Indique comment toosearch pour le certificat dans le magasin de hello spécifié par GatewayX509CertificateStoreName pris en charge la valeur : FindByThumbprint ; FindBySubjectName. |
|GatewayX509CertificateFindValue | Chaîne (valeur par défaut : "") | Valeur de filtre de recherche utilisé le certificat de passerelle toolocate hello http application. Ce certificat est configuré sur le point de terminaison https hello et peut également être identité de hello tooverify utilisés de l’application hello si nécessaire par les services de hello. Le paramètre FindValue est consulté en premier. S’il n’existe pas, FindValueSecondary est consulté. |
|GatewayX509CertificateFindValueSecondary | Chaîne (valeur par défaut : "") |Valeur de filtre de recherche utilisé le certificat de passerelle toolocate hello http application. Ce certificat est configuré sur le point de terminaison https hello et peut également être identité de hello tooverify utilisés de l’application hello si nécessaire par les services de hello. Le paramètre FindValue est consulté en premier. S’il n’existe pas, FindValueSecondary est consulté.|

### <a name="section-name-management"></a>Nom de la section : Management
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Toohello de chaîne de connexion racine pour les images. |
| ImageStoreMinimumTransferBPS | Entier (valeur par défaut : 1024) |taux de transfert minimale Hello entre le cluster de hello et images. Cette valeur est le délai d’attente de toodetermine utilisé hello lors de l’accès à hello des images externes. Modifiez cette valeur uniquement si la latence entre le cluster de hello et images hello est haute tooallow plus de temps pour toodownload de cluster hello de hello images externes. |
|AzureStorageMaxWorkerThreads | Entier (valeur par défaut : 25) | nombre maximal de Hello de threads de travail en parallèle. |
|AzureStorageMaxConnections | Entier (valeur par défaut : 5000) | nombre maximal de Hello de stockage tooazure de connexions simultanées. |
|AzureStorageOperationTimeout | Durée en secondes (valeur par défaut : 6000) | Spécifiez la durée en secondes. Délai d’attente pour xstore opération toocomplete. |
|ImageCachingEnabled | Valeur booléenne (valeur par défaut : true) | Cette configuration permet de tooenable ou désactiver la mise en cache. |
|DisableChecksumValidation | Valeur booléenne (valeur par défaut : false) | Cette configuration permet de tooenable ou désactiver la validation de somme de contrôle lors de la configuration de l’application. |
|DisableServerSideCopy | Valeur booléenne (valeur par défaut : false) | Cette configuration Active ou désactive les copie sur le côté serveur du package d’application hello images lors de la configuration de l’application. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Nom de la section : HealthManager/ClusterHealthPolicy
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ConsiderWarningAsError |Valeur booléenne (valeur par défaut : false) |Stratégie d’évaluation d’intégrité de cluster : avertissements traités comme des erreurs. |
| MaxPercentUnhealthyNodes | Entier (valeur par défaut : 0) |Stratégie d’évaluation d’intégrité de cluster : pourcentage maximal de nœuds non intègres autorisés pour hello cluster toobe sain. |
| MaxPercentUnhealthyApplications | Entier (valeur par défaut : 0) |Stratégie d’évaluation d’intégrité de cluster : pourcentage maximal d’applications non intègres autorisés pour hello cluster toobe sain. |
|MaxPercentDeltaUnhealthyNodes | Entier (valeur par défaut : 10) |Stratégie d’évaluation de mise à niveau d’intégrité de cluster : pourcentage maximal de nœuds non intègres du delta autorisées pour hello cluster toobe sain. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Entier (valeur par défaut : 15) |Stratégie d’évaluation de mise à niveau d’intégrité de cluster : pourcentage maximal de delta de nœuds défectueux dans un domaine de mise à niveau autorisée pour hello cluster toobe sain.|

### <a name="section-name-faultanalysisservice"></a>Nom de la section : FaultAnalysisService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| TargetReplicaSetSize |Entier (valeur par défaut : 0) |Hello NOT_PLATFORM_UNIX_START TargetReplicaSetSize pour FaultAnalysisService. |
| MinReplicaSetSize |Entier (valeur par défaut : 0) |Hello MinReplicaSetSize pour FaultAnalysisService. |
| ReplicaRestartWaitDuration |Durée en secondes (valeur par défaut : 60 minutes)|Spécifiez la durée en secondes. Hello ReplicaRestartWaitDuration pour FaultAnalysisService. |
| QuorumLossWaitDuration | Durée en secondes (valeur par défaut : MaxValue) |Spécifiez la durée en secondes. Hello QuorumLossWaitDuration pour FaultAnalysisService. |
| StandByReplicaKeepDuration| Durée en secondes (valeur par défaut : 60*24*7 minutes) |Spécifiez la durée en secondes. Hello StandByReplicaKeepDuration pour FaultAnalysisService. |
| PlacementConstraints | Chaîne (valeur par défaut : "")| Hello PlacementConstraints pour FaultAnalysisService. |
| StoredActionCleanupIntervalInSeconds | Entier (valeur par défaut : 3600) |Il s’agit de la fréquence à laquelle hello magasin est nettoyé.  Seules les actions dans un état terminal et celles qui exécutées il y a au moins CompletedActionKeepDurationInSeconds secondes seront supprimées. |
| CompletedActionKeepDurationInSeconds | Entier (valeur par défaut : 604800) | Il s’agit d’environ combien tookeep que les actions dans un état terminal.  Cela dépend également de StoredActionCleanupIntervalInSeconds ; hello travail toocleanup est effectuée uniquement sur cet intervalle. 604800 correspond à 7 jours. |
| StoredChaosEventCleanupIntervalInSeconds | Entier (valeur par défaut : 3600) |Il s’agit de la fréquence à laquelle hello magasin est audité pour le nettoyage ; Si le nombre de hello d’événements est plus de 30000 ; démarre le nettoyage Hello. |

### <a name="section-name-filestoreservice"></a>Nom de la section : FileStoreService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| NamingOperationTimeout |Durée en secondes, la valeur par défaut est 60 |Spécifiez la durée en secondes. délai d’expiration de Hello pour effectuer une opération d’affectation de noms. |
| QueryOperationTimeout | Durée en secondes, la valeur par défaut est 60 |Spécifiez la durée en secondes. délai d’expiration de Hello pour effectuer l’opération de requête. |
| MaxCopyOperationThreads | Valeur Uint (valeur par défaut : 0) | nombre maximal de Hello de fichiers parallèles cette base de données secondaire peut copier du serveur principal. 0 = nombre de cœurs. |
| MaxFileOperationThreads | Valeur Uint (valeur par défaut : 100) | nombre maximal de Hello de threads parallèles autorisées tooperform FileOperations (copie/déplacement) Bonjour principal. 0 = nombre de cœurs. |
| MaxStoreOperations | Valeur Uint (valeur par défaut : 4096) |nombre maximal de Hello parallèle transcation des opérations de stockage autorisé sur le réplica principal. 0 = nombre de cœurs. |
| MaxRequestProcessingThreads | Valeur Uint (valeur par défaut : 200) |nombre maximal de Hello de threads parallèles tooprocess de demandes autorisées dans hello principal. 0 = nombre de cœurs. |
| MaxSecondaryFileCopyFailureThreshold | Valeur Uint (valeur par défaut : 25)| nombre maximal de Hello de nouvelles tentatives de copie de fichier sur hello secondaire avant d’abandonner. |
| AnonymousAccessEnabled | Valeur booléenne (valeur par défaut : true) |Activer ou désactiver toohello l’accès anonyme que filestoreservice partage. |
| PrimaryAccountType | Chaîne (valeur par défaut : "") |partage de AccountType de Bonjour tooACL principal Bonjour FileStoreService Hello principal. |
| PrimaryAccountUserName | Chaîne (valeur par défaut : "") |nom d’utilisateur de partages de FileStoreService hello hello tooACL principal de compte principal Hello. |
| PrimaryAccountUserPassword | Valeur SecureString (valeur par défaut : vide) |le mot de passe du compte de principal de Hello Hello du principal tooACL hello FileStoreService partage. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | Valeur SecureString (valeur par défaut : vide) | secret de mot de passe Hello qui utilisé en tant que valeur de départ toogenerated même mot de passe lors de l’utilisation de l’authentification NTLM. |
| PrimaryAccountNTLMX509StoreLocation | Chaîne (valeur par défaut : "LocalMachine")| emplacement du magasin de certificats de hello X509 Hello utilisé toogenerate HMAC sur hello PrimaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |
| PrimaryAccountNTLMX509StoreName | Chaîne (valeur par défaut : "MY")| nom du magasin de certificats de hello X509 Hello utilisé toogenerate HMAC sur hello PrimaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |
| PrimaryAccountNTLMX509Thumbprint | Chaîne (valeur par défaut : "")|Hello empreinte numérique du hello X509 certificat utilisé toogenerate HMAC sur hello PrimaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |
| SecondaryAccountType | Chaîne (valeur par défaut : "")| partage de AccountType de Bonjour tooACL principal Bonjour FileStoreService Hello secondaire. |
| SecondaryAccountUserName | Chaîne (valeur par défaut : "")| nom d’utilisateur de partages de FileStoreService hello hello tooACL principal de compte secondaire Hello. |
| SecondaryAccountUserPassword | Valeur SecureString (valeur par défaut : vide) |un mot de passe de compte secondaire de Bonjour tooACL principal Bonjour Hello FileStoreService partage.  |
| SecondaryAccountNTLMPasswordSecret | Valeur SecureString (valeur par défaut : vide) | secret de mot de passe Hello qui utilisé en tant que valeur de départ toogenerated même mot de passe lors de l’utilisation de l’authentification NTLM. |
| SecondaryAccountNTLMX509StoreLocation | Chaîne (valeur par défaut : "LocalMachine") |emplacement du magasin de certificats de hello X509 Hello utilisé toogenerate HMAC sur hello SecondaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |
| SecondaryAccountNTLMX509StoreName | Chaîne (valeur par défaut : "MY") |nom du magasin de certificats de hello X509 Hello utilisé toogenerate HMAC sur hello SecondaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |
| SecondaryAccountNTLMX509Thumbprint | Chaîne (valeur par défaut : "")| Hello empreinte numérique du hello X509 certificat utilisé toogenerate HMAC sur hello SecondaryAccountNTLMPasswordSecret lors de l’utilisation de l’authentification NTLM. |

### <a name="section-name-imagestoreservice"></a>Nom de la section : ImageStoreService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| Activé |Valeur booléenne (valeur par défaut : false) |Hello pour ImageStoreService l’indicateur activé. |
| TargetReplicaSetSize | Entier (valeur par défaut : 7) |Hello TargetReplicaSetSize pour ImageStoreService. |
| MinReplicaSetSize | Entier (valeur par défaut : 3) |Hello MinReplicaSetSize pour ImageStoreService. |
| ReplicaRestartWaitDuration | Durée en secondes (valeur par défaut : 60.0 * 30) | Spécifiez la durée en secondes. Hello ReplicaRestartWaitDuration pour ImageStoreService. |
| QuorumLossWaitDuration | Durée en secondes (valeur par défaut : MaxValue) | Spécifiez la durée en secondes. Hello QuorumLossWaitDuration pour ImageStoreService. |
| StandByReplicaKeepDuration | Durée en secondes (valeur par défaut : 3600.0*2) | Spécifiez la durée en secondes. Hello StandByReplicaKeepDuration pour ImageStoreService. |
| PlacementConstraints | Chaîne (valeur par défaut : "") | Hello PlacementConstraints pour ImageStoreService. |
| ClientUploadTimeout | Durée en secondes (valeur par défaut : 1800) |Spécifiez la durée en secondes. Valeur de délai d’attente pour le téléchargement de niveau supérieur demander un Service de banque d’informations tooImage. |
| ClientCopyTimeout | Durée en secondes (valeur par défaut : 1800) | Spécifiez la durée en secondes. Valeur de délai d’attente pour la copie de niveau supérieur demander un Service de banque d’informations tooImage. |
| ClientDownloadTimeout | Durée en secondes (valeur par défaut : 1800) | Spécifiez la durée en secondes. Valeur de délai d’attente pour le téléchargement de niveau supérieur des demandes de Service de banque d’informations tooImage |
| ClientListTimeout | Durée en secondes (valeur par défaut : 600) | Spécifiez la durée en secondes. Valeur de délai d’attente de niveau supérieur demander un Service de banque d’informations tooImage. |
| ClientDefaultTimeout | Durée en secondes (valeur par défaut : 180) | Spécifiez la durée en secondes. Valeur de délai d’attente pour toutes les demandes non-non-télécharger (par exemple, il existe ; supprimer) tooImage Service de banque. |

### <a name="section-name-imagestoreclient"></a>Nom de la section : ImageStoreClient
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ClientUploadTimeout |Durée en secondes (valeur par défaut : 1800) | Spécifiez la durée en secondes. Valeur de délai d’attente pour le téléchargement de niveau supérieur demander un Service de banque d’informations tooImage. |
| ClientCopyTimeout | Durée en secondes (valeur par défaut : 1800) | Spécifiez la durée en secondes. Valeur de délai d’attente pour la copie de niveau supérieur demander un Service de banque d’informations tooImage. |
|ClientDownloadTimeout | Durée en secondes (valeur par défaut : 1800) | Spécifiez la durée en secondes. Valeur de délai d’attente pour le téléchargement de niveau supérieur demander un Service de banque d’informations tooImage. |
|ClientListTimeout | Durée en secondes (valeur par défaut : 600) |Spécifiez la durée en secondes. Valeur de délai d’attente de niveau supérieur demander un Service de banque d’informations tooImage. |
|ClientDefaultTimeout | Durée en secondes (valeur par défaut : 180) | Spécifiez la durée en secondes. Valeur de délai d’attente pour toutes les demandes non-non-télécharger (par exemple, il existe ; supprimer) tooImage Service de banque. |

### <a name="section-name-tokenvalidationservice"></a>Nom de la section : TokenValidationService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| Fournisseurs |Chaîne (valeur par défault : "DSTS") |Liste séparée par des virgules de tooenable de fournisseurs de validation du jeton (fournisseurs valides sont : DSTS ; AAD). Pour l’instant, un seul fournisseur peut être activé à la fois. |

### <a name="section-name-upgradeorchestrationservice"></a>Nom de la section : UpgradeOrchestrationService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| TargetReplicaSetSize |Entier (valeur par défaut : 0) |Hello TargetReplicaSetSize pour UpgradeOrchestrationService. |
| MinReplicaSetSize |Entier (valeur par défaut : 0) | Hello MinReplicaSetSize pour UpgradeOrchestrationService.
| ReplicaRestartWaitDuration | Durée en secondes (valeur par défaut : 60 minutes)| Spécifiez la durée en secondes. Hello ReplicaRestartWaitDuration pour UpgradeOrchestrationService. |
| QuorumLossWaitDuration | Durée en secondes (valeur par défaut : MaxValue) | Spécifiez la durée en secondes. Hello QuorumLossWaitDuration pour UpgradeOrchestrationService. |
| StandByReplicaKeepDuration | Durée en secondes (valeur par défaut : 60*24*7 minutes) | Spécifiez la durée en secondes. Hello StandByReplicaKeepDuration pour UpgradeOrchestrationService. |
| PlacementConstraints | Chaîne (valeur par défaut : "") | Hello PlacementConstraints pour UpgradeOrchestrationService. |
| AutoupgradeEnabled | Valeur booléenne (valeur par défaut : true) | Interrogation automatique et action de mise à niveau basée sur un fichier d’état d’objectif. |
| UpgradeApprovalRequired | Valeur booléenne (valeur par défaut : false) | Mise à niveau du code paramètre toomake exiger l’approbation de l’administrateur avant de continuer. |

### <a name="section-name-upgradeservice"></a>Nom de la section : UpgradeService
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| PlacementConstraints |Chaîne (valeur par défaut : "") |Hello PlacementConstraints pour le service de mise à niveau. |
| TargetReplicaSetSize | Entier (valeur par défaut : 3) | Hello TargetReplicaSetSize pour UpgradeService. |
| MinReplicaSetSize | Entier (valeur par défaut : 2) | Hello MinReplicaSetSize pour UpgradeService. |
| CoordinatorType | Chaîne (valeur par défault : "WUTest")| Hello CoordinatorType pour UpgradeService. |
| BaseUrl | Chaîne (valeur par défaut : "") |Paramètre BaseUrl pour UpgradeService. |
| ClusterId | Chaîne (valeur par défaut : "") | Paramètre ClusterId pour UpgradeService. |
| X509StoreName | Chaîne (valeur par défaut : "My")| Paramètre X509StoreName pour UpgradeService. |
| X509StoreLocation | Chaîne (valeur par défaut : "") | Paramètre X509StoreLocation pour UpgradeService. |
| X509FindType | Chaîne (valeur par défaut : "")| Paramètre X509FindType pour UpgradeService. |
| X509FindValue | Chaîne (valeur par défaut : "") | Paramètre X509FindValue pour UpgradeService. |
| X509SecondaryFindValue | Chaîne (valeur par défaut : "") | Paramètre X509SecondaryFindValue pour UpgradeService. |
| OnlyBaseUpgrade | Valeur booléenne (valeur par défaut : false) | Paramètre OnlyBaseUpgrade pour UpgradeService. |
| TestCabFolder | Chaîne (valeur par défaut : "") | Paramètre TestCabFolder pour UpgradeService. |

### <a name="section-name-securityclientaccess"></a>Nom de la section : Security/ClientAccess
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| CreateName |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour la création d’URI d’attribution de noms. |
| DeleteName |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour la suppression d’URI d’attribution de noms. |
| PropertyWriteBatch |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour les opérations d’écriture de la propriété d’attribution de noms. |
| CreateService |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour la création de services. |
| CreateServiceFromTemplate |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour la création de services à partir d’un modèle. |
| UpdateService |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour les mises à niveau de services. |
| DeleteService  |Chaîne (valeur par défault : "Admin") |Configuration de la sécurité pour la suppression de services. |
| ProvisionApplicationType |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour l’approvisionnement du type d’application. |
| CreateApplication |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour la création d’applications. |
| DeleteApplication |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour la suppression d’applications. |
| UpgradeApplication |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour démarrer ou arrêter des mises à niveau d’application. |
| RollbackApplicationUpgrade |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour annuler des mises à niveau d’application. |
| UnprovisionApplicationType |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour annuler l’approvisionnement du type d’application. |
| MoveNextUpgradeDomain |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour reprendre des mises à niveau d’application avec un domaine de mise à niveau explicite. |
| ReportUpgradeHealth |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour la reprise des mises à niveau de l’application avec la progression de mise à niveau en cours hello. |
| ReportHealth |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour créer un rapport d’intégrité. |
| ProvisionFabric |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour l’approvisionnement de MSI et/ou du manifeste de cluster. |
| UpgradeFabric |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour démarrer des mises à niveau de cluster. |
| RollbackFabricUpgrade |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour annuler des mises à niveau de cluster. |
| UnprovisionFabric |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour annuler l’approvisionnement de MSI et/ou du manifeste de cluster. |
| MoveNextFabricUpgradeDomain |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour reprendre des mises à niveau de cluster avec un domaine de mise à niveau explicite. |
| ReportFabricUpgradeHealth |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour la reprise des mises à niveau de cluster avec hello actuelle mise à niveau de progression. |
| StartInfrastructureTask |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour démarrer des tâches d’infrastructure. |
| FinishInfrastructureTask |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour terminer des tâches d’infrastructure. |
| ActivateNode |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour activer un nœud. |
| DeactivateNode |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour désactiver un nœud. |
| DeactivateNodesBatch |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour désactiver plusieurs nœuds. |
| RemoveNodeDeactivations |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour annuler la désactivation sur plusieurs nœuds. |
| GetNodeDeactivationStatus |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour vérifier l’état de désactivation. |
| NodeStateRemoved |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour signaler l’état de nœud supprimé. |
| RecoverPartition |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour restaurer une partition. |
| RecoverPartitions |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour restaurer des partitions. |
| RecoverServicePartitions |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour restaurer des partitions de service. |
| RecoverSystemPartitions |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour restaurer des partitions du service système. |
| ReportFault |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour signaler une défaillance. |
| InvokeInfrastructureCommand |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour les commandes de gestion des tâches d’infrastructure. |
| FileContent |Chaîne (valeur par défault : "Admin") | Configuration de sécurité pour l’image de stocker le transfert de fichiers client (toocluster externe). |
| FileDownload |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité image store client fichier téléchargement pour l’émission de (toocluster externe). |
| InternalList |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour l’opération de liste de fichiers clients deumagasin d’images (interne). |
| Supprimer |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour l’opération de suppression de clients du magasin d’images (interne). |
| Télécharger |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour l’opération de chargement de clients du magasin d’images. |
| GetStagingLocation |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour récupérer l’emplacement intermédiaire du client du magasin d’images. |
| GetStoreLocation |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour récupérer l’emplacement du client du magasin d’images. |
| NodeControl |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour démarrer, arrêter et redémarrer des nœuds. |
| CodePackageControl |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour redémarrer des packages de code. |
| UnreliableTransportControl |Chaîne (valeur par défault : "Admin") | Transport non fiable pour ajouter et supprimer des comportements. |
| MoveReplicaControl |Chaîne (valeur par défault : "Admin") | Déplacez un réplica. |
| PredeployPackageToNode |Chaîne (valeur par défault : "Admin") | API de pré-déploiement. |
| StartPartitionDataLoss |Chaîne (valeur par défault : "Admin") | Provoque la perte de données sur une partition. |
| StartPartitionQuorumLoss |Chaîne (valeur par défault : "Admin") | Provoque la perte de quorum sur une partition. |
| StartPartitionRestart |Chaîne (valeur par défault : "Admin") | Redémarre simultanément des réplicas de hello tout ou partie d’une partition. |
| CancelTestCommand |Chaîne (valeur par défault : "Admin") | Annule une commande de test si elle est en cours. |
| StartChaos |Chaîne (valeur par défault : "Admin") | Démarre Chaos si ce n’est déjà fait. |
| StopChaos |Chaîne (valeur par défault : "Admin") | Arrête Chaos s’il a été démarré. |
| StartNodeTransition |Chaîne (valeur par défault : "Admin") | Configuration de la sécurité pour démarrer une transition de nœud. |
| StartClusterConfigurationUpgrade |Chaîne (valeur par défault : "Admin") | Déclenche StartClusterConfigurationUpgrade sur une partition. |
| GetUpgradesPendingApproval |Chaîne (valeur par défault : "Admin") | Déclenche GetUpgradesPendingApproval sur une partition. |
| StartApprovedUpgrades |Chaîne (valeur par défault : "Admin") | Déclenche StartApprovedUpgrades sur une partition. |
| Ping |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour les tests ping de clients |
| Interroger |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour les requêtes. |
| NameExists |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour la vérification de l’existence des URI d’attribution de noms. |
| EnumerateSubnames |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour l’énumération d’URI d’attribution de noms. |
| EnumerateProperties |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour l’énumération de propriétés d’attribution de noms. |
| PropertyReadBatch |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour les opérations de lecture de propriétés d’attribution de noms. |
| GetServiceDescription |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour la lecture des descriptions de service et les notifications de sondage de longue durée. |
| ResolveService |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour la résolution de services en fonction de la réclamation. |
| ResolveNameOwner |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour résoudre le propriétaire de l’URI d’attribution de noms. |
| ResolvePartition |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour résoudre les services du système. |
| ServiceNotifications |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour les notifications de service basées sur l’événement. |
| PrefixResolveService |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour la résolution de préfixe de service en fonction de la réclamation. |
| GetUpgradeStatus |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour interroger l’état de mise à niveau de l’application. |
| GetFabricUpgradeStatus |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour interroger l’état de mise à niveau du cluster. |
| InvokeInfrastructureQuery |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour interroger les tâches d’infrastructure. |
| Énumérer |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour l’opération de liste de fichiers clients du magasin d’images. |
| ResetPartitionLoad |Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour la charge de réinitialisation d’une unité failoverUnit. |
| ToggleVerboseServicePlacementHealthReporting | Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour l’activation ou la désactivation du rapport d’intégrité détaillé sur le placement du service. |
| GetPartitionDataLossProgress | Chaîne (valeur par défault : "Admin\)|\|User") | Extrait la progression hello pour un appel d’api invoke données perte. |
| GetPartitionQuorumLossProgress | Chaîne (valeur par défault : "Admin\)|\|User") | Extrait la progression hello pour un appel d’api invoke quorum perte. |
| GetPartitionRestartProgress | Chaîne (valeur par défault : "Admin\)|\|User") | Extrait la progression hello pour un appel d’api de redémarrage de partition. |
| GetChaosReport | Chaîne (valeur par défault : "Admin\)|\|User") | Extrait l’état hello de Chaos durant une période donnée. |
| GetNodeTransitionProgress | Chaîne (valeur par défault : "Admin\)|\|User") | Configuration de la sécurité pour obtenir l’état d’avancement d’une commande de transition de nœud. |
| GetClusterConfigurationUpgradeStatus | Chaîne (valeur par défault : "Admin\)|\|User") | Déclenche GetClusterConfigurationUpgradeStatus sur une partition. |
| GetClusterConfiguration | Chaîne (valeur par défault : "Admin\)|\|User") | Déclenche GetClusterConfiguration sur une partition. |

### <a name="section-name-reconfigurationagent"></a>Nom de la section : ReconfigurationAgent
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Durée en secondes (valeur par défaut : 900) |Spécifiez la durée en secondes. Durée Hello pour le hello système attend avant de mettre fin à des hôtes de service qui contiennent des réplicas qui sont bloqués dans le fermer. |
| ServiceApiHealthDuration | Durée en secondes (valeur par défaut : 30 minutes) | Spécifiez la durée en secondes. ServiceApiHealthDuration définit la durée pendant laquelle nous attendre un toorun d’API de service avant que nous le signaler défectueux. |
| ServiceReconfigurationApiHealthDuration | Durée en secondes, la valeur par défaut est 30 | Spécifiez la durée en secondes. ServiceReconfigurationApiHealthDuration définit la durée pendant laquelle hello avant qu’un service dans la reconfiguration est signalé comme défectueux. |
| PeriodicApiSlowTraceInterval | Durée en secondes (valeur par défaut : 5 minutes) | Spécifiez la durée en secondes. PeriodicApiSlowTraceInterval définit l’intervalle de salutation sur lequel les ralentissez les appels API seront actualisation par le moniteur de l’API hello. |
| NodeDeactivationMaxReplicaCloseDuration | Durée en secondes (valeur par défaut : 900) | Spécifiez la durée en secondes. Bonjour toowait de durée maximale avant de mettre fin à un hôte de service qui bloque la désactivation du nœud. |
| FabricUpgradeMaxReplicaCloseDuration | Durée en secondes (valeur par défaut : 900) | Spécifiez la durée en secondes. Hello durée maximale pendant laquelle RA attend avant d’arrêter l’hôte de service du réplica qui ne se ferme pas. |
| IsDeactivationInfoEnabled | Valeur booléenne (valeur par défaut : true) | Détermine si RA utilise les informations de désactivation pour effectuer des renouvelable principal pour les nouveaux clusters tootrue pour les clusters existants sont mis à niveau doit être définie à cette configuration, consultez les notes de version de hello sur la façon de tooenable cela. |

### <a name="section-name-placementandloadbalancing"></a>Nom de la section : PlacementAndLoadBalancing
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| TraceCRMReasons |Valeur booléenne (valeur par défaut : true) |Spécifie si les raisons tootrace CRM émis canal de mouvements toohello les événements opérationnels. |
| ValidatePlacementConstraint | Valeur booléenne (valeur par défaut : true) | Spécifie si hello expression PlacementConstraint pour un service est validée lors de la mise à jour ServiceDescription d’un service. |
| PlacementConstraintValidationCacheSize | Entier (valeur par défaut : 10000) | Limites hello la taille de la table hello utilisé pour la validation rapide et mise en cache des Expressions de contrainte de Placement. |
|VerboseHealthReportLimit | Entier (valeur par défaut : 20) | Définit le nombre de hello de fois où qu'un réplica a toogo non placé avant un avertissement d’intégrité est signalé pour lui (si le rapport d’état détaillé est activé). |
|ConstraintViolationHealthReportLimit | Entier (valeur par défaut : 50) | Définit le nombre de hello de contrainte de violation de réplica a toobe non rectifiée de manière permanente avant de diagnostics sont effectuées et les rapports d’intégrité sont émis. |
|DetailedConstraintViolationHealthReportLimit | Entier (valeur par défaut : 200) | Définit le nombre de hello de contrainte de violation de réplica a toobe non rectifiée de manière permanente avant de diagnostics sont effectuées et les rapports d’intégrité détaillées sont émis. |
|DetailedVerboseHealthReportLimit | Entier (valeur par défaut : 200) | Définit le nombre de hello de fois où qu'un réplica non placé a toobe de façon persistante non placé avant d’intégrité détaillées rapports sont émis. |
|ConsecutiveDroppedMovementsHealthReportLimit | Entier (valeur par défaut : 20) | Définit le nombre hello de fois consécutives que ResourceBalancer émis les mouvements sont supprimés avant le diagnostic est effectuée et les avertissements de contrôle d’intégrité sont émis. Negative : aucun avertissement émis sous cette condition. |
|DetailedNodeListLimit | Entier (valeur par défaut : 15) | Définit le nombre hello de nœuds par tooinclude contrainte avant la troncature Bonjour que réplica Unplaced signale. |
|DetailedPartitionListLimit | Entier (valeur par défaut : 15) | Définit le nombre de hello de partitions par entrée de diagnostic pour un tooinclude contrainte avant la troncature dans les Diagnostics. |
|DetailedDiagnosticsInfoListLimit | Entier (valeur par défaut : 15) | Définit le nombre hello d’entrées de diagnostic (avec des informations détaillées) par tooinclude contrainte avant de troncation dans les Diagnostics.|
|PLBRefreshGap | Durée en secondes (valeur par défaut : 1) | Spécifiez la durée en secondes. Définit hello délai minimal qui doit s’écouler avant PLB actualise état nouveau. |
|MinPlacementInterval | Durée en secondes (valeur par défaut : 1) | Spécifiez la durée en secondes. Définit hello délai minimal qui doit s’écouler avant que deux des tentatives consécutives de la sélection élective. |
|MinConstraintCheckInterval | Durée en secondes (valeur par défaut : 1) | Spécifiez la durée en secondes. Définit hello délai minimal qui doit s’écouler avant que deux contraintes consécutifs archivent essais. |
|MinLoadBalancingInterval | Durée en secondes (valeur par défaut : 5) | Spécifiez la durée en secondes. Définit hello délai minimal qui doit s’écouler avant que deux des essais équilibrage consécutifs. |
|BalancingDelayAfterNodeDown | Durée en secondes (valeur par défaut : 120) |Spécifiez la durée en secondes. Ne démarrez pas l’équilibrage des activités pendant cette période après un événement d’arrêt de nœud. |
|BalancingDelayAfterNewNode | Durée en secondes (valeur par défaut : 120) |Spécifiez la durée en secondes. Ne démarrez pas l’équilibrage des activités pendant cette période après l’ajout d’un nouveau nœud. |
|ConstraintFixPartialDelayAfterNodeDown | Durée en secondes (valeur par défaut : 120) | Spécifiez la durée en secondes. Ne corrigez pas les violations de contrainte FaultDomain et UpgradeDomain pendant cette période après un événement d’arrêt de nœud. |
|ConstraintFixPartialDelayAfterNewNode | Durée en secondes (valeur par défaut : 120) | Spécifiez la durée en secondes. Ne corrigez pas les violations de contrainte FaultDomain et UpgradeDomain pendant cette période après l’ajout d’un nouveau nœud. |
|GlobalMovementThrottleThreshold | Valeur Uint (valeur par défaut : 1000) | Nombre maximal autorisé dans des mouvements hello l’équilibrage de la Phase dans hello passée intervalle indiqué par GlobalMovementThrottleCountingInterval. |
|GlobalMovementThrottleThresholdForPlacement | Valeur Uint (valeur par défaut : 0) | Nombre maximal de mouvements autorisé dans la Phase de la sélection élective hello passée intervalle indiqué par GlobalMovementThrottleCountingInterval.0 n’indique aucune limite.|
|GlobalMovementThrottleThresholdForBalancing | Valeur Uint (valeur par défaut : 0) | Nombre maximal de mouvements autorisé dans l’équilibrage de la Phase hello passée intervalle indiqué par GlobalMovementThrottleCountingInterval. 0 indique aucune limite. |
|GlobalMovementThrottleCountingInterval | Durée en secondes (valeur par défaut : 600) | Spécifiez la durée en secondes. Indiquer la longueur de hello hello au-delà de l’intervalle pour le tootrack par les mouvements de réplica de domaine (utilisé avec GlobalMovementThrottleThreshold). Peut être défini too0 tooignore global limitation complètement. |
|MovementPerPartitionThrottleThreshold | Valeur Uint (valeur par défaut : 50) | Aucun équilibrage ne liées déplacement se produit pour une partition si nombre hello d’équilibrage de mouvements connexes pour les réplicas de cette partition a atteint ou dépassé le MovementPerFailoverUnitThrottleThreshold Bonjour passées intervalle indiqué par MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Durée en secondes (valeur par défaut : 600) | Spécifiez la durée en secondes. Indiquer la longueur de hello hello au-delà de l’intervalle pour les mouvements de réplica tootrack pour chaque partition (utilisée avec MovementPerPartitionThrottleThreshold). |
|PlacementSearchTimeout | Durée en secondes (valeur par défaut est 0.5) | Spécifiez la durée en secondes. Lors du placement de services, effectuez une recherche au moins aussi longue avant de renvoyer un résultat. |
|UseMoveCostReports | Valeur booléenne (valeur par défaut : false) | Indique l’élément de coût hello LB tooignore hello Hello score fonction ; ce qui entraîne un nombre potentiellement important de se déplace pour mieux la sélection élective à charge équilibrée. |
|PreventTransientOvercommit | Valeur booléenne (valeur par défaut : false) | Détermine doit-elle PLB compter immédiatement sur les ressources seront libérées par les déplacements de hello initiée. Par défaut ; PLB peut initier le retirer et passer hello sollicitation excessive du même nœud qui peut créer temporaire. Paramètre tootrue de ce paramètre empêche celles overcommits type d’et à la demande défragmentation (également appelé placementWithMove) est désactivée. |
|InBuildThrottlingEnabled | Valeur booléenne (valeur par défaut : false) | Déterminer si la limitation dans la génération de hello est activée. |
|InBuildThrottlingAssociatedMetric | Chaîne (valeur par défaut : "") | Hello associés nom de métrique pour cette limitation. |
|InBuildThrottlingGlobalMaxValue | Entier (valeur par défaut : 0) |nombre maximal de Hello des réplicas dans la génération autorisé globalement. |
|SwapPrimaryThrottlingEnabled | Valeur booléenne (valeur par défaut : false)| Déterminer si la limitation de principal de l’échange hello est activée. |
|SwapPrimaryThrottlingAssociatedMetric | Chaîne (valeur par défaut : "")| Hello associés nom de métrique pour cette limitation. |
|SwapPrimaryThrottlingGlobalMaxValue | Entier (valeur par défaut : 0) | nombre maximal de Hello de réplicas échange principal autorisé globalement. |
|PlacementConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte de placement : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|PreferredLocationConstraintPriority | Entier (valeur par défaut : 2)| Détermine la priorité hello de contrainte d’emplacement par défaut : 0 : dur ; 1 : logicielle ; 2 : optimisation ; négatif : ignorer |
|CapacityConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte de capacité : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|AffinityConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte d’affinité : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|FaultDomainConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte de domaine d’erreur : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|UpgradeDomainConstraintPriority | Entier (valeur par défaut : 1)| Détermine la priorité hello de contrainte de mise à niveau de domaine : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|ScaleoutCountConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte de nombre de montée en puissance parallèle : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|ApplicationCapacityConstraintPriority | Entier (valeur par défaut : 0) | Détermine la priorité hello de contrainte de capacité : 0 : dur ; 1 : logicielle ; négatif : ignorer. |
|MoveParentToFixAffinityViolation | Valeur booléenne (valeur par défaut : false) | Paramètre qui détermine si les réplicas parent peuvent être déplacé toofix des contraintes d’affinité.|
|MoveExistingReplicaForPlacement | Valeur booléenne (valeur par défaut : true) |Paramètre qui détermine si des réplicas existants toomove pendant la sélection élective. |
|UseSeparateSecondaryLoad | Valeur booléenne (valeur par défaut : true) | Paramètre déterminant s’il convient d’utiliser une charge secondaire différente. |
|PlaceChildWithoutParent | Valeur booléenne (valeur par défaut : true) | Paramètre déterminant si le réplica de service enfant peut être placé si aucun réplica parent n’est actif. |
|PartiallyPlaceServices | Valeur booléenne (valeur par défaut : true) | Détermine si tous les réplicas de service dans le cluster seront placés selon le principe du « tout ou rien », en fonction du nombre limité de nœuds appropriés pour eux.|
|InterruptBalancingForAllFailoverUnitUpdates | Valeur booléenne (valeur par défaut : false) | Détermine si n’importe quel type de mise à jour des unités de basculement doit interrompre l’exécution lente ou rapide de l’équilibrage. Avec la valeur « false », l’exécution de l’équilibrage est interrompue si FailoverUnit est créé/supprimé, a des réplicas manquants, a modifié l’emplacement du réplica principal ou a modifié le nombre de réplicas. L’exécution de l’équilibrage n’est pas interrompue si FailoverUnit a des réplicas supplémentaires, a modifié un indicateur de réplica, n’a modifié que la version de la partition ou dans tout autre cas. |

### <a name="section-name-security"></a>Nom de la section : Sécurité
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ClusterProtectionLevel |None ou EncryptAndSign |None (par défaut) pour les clusters non sécurisés, EncryptAndSign pour les clusters sécurisés. |

### <a name="section-name-hosting"></a>Nom de la section : Hébergement
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Durée en secondes, la valeur par défaut est 300 |Durée maximale autorisée pour hello ServiceType toobe est enregistré avec l’ensemble fibre optique |
| ServiceTypeDisableFailureThreshold |Nombre entier, la valeur par défaut est 1 |Il s’agit de seuil de hello de type de service toodisable hello sur ce nœud, puis réessayez un nœud différent pour la sélection élective informé hello après laquelle le Gestionnaire de basculement (FM) est le nombre d’échecs. |
| ActivationRetryBackoffInterval |Durée en secondes, la valeur par défaut est 5 |Intervalle de refus sur tous les échecs d’activation ; Chaque cas d’échec d’activation continue, tentatives de système hello hello d’activation pour les toohello MaxActivationFailureCount. intervalle avant nouvelle tentative de Hello à chaque tentative est un produit de l’activation continue échec et hello activation intervalle de temporisation. |
| ActivationMaxRetryInterval |Durée en secondes, la valeur par défaut est 300 |Chaque cas d’échec d’activation continue, tentatives de système hello hello d’activation pour les tooActivationMaxFailureCount. ActivationMaxRetryInterval spécifie l’intervalle de temps d’attente avant une nouvelle tentative après chaque échec d’activation |
| ActivationMaxFailureCount |Nombre entier, la valeur par défaut est 10 |Nombre de fois où les nouvelles tentatives système ont échoué à l’activation avant d’abandonner |

### <a name="section-name-failovermanager"></a>Nom de la section : FailoverManager
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Durée en secondes, la valeur par défaut est 10 |Ce paramètre détermine la fréquence à laquelle hello de vérification de l’équipe de support technique pour de nouveaux rapports de charge |

### <a name="section-name-federation"></a>Nom de la section : Fédération
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| LeaseDuration |Durée en secondes, la valeur par défaut est 30 |Durée de bail entre un nœud et ses voisins. |
| LeaseDurationAcrossFaultDomain |Durée en secondes, la valeur par défaut est 30 |Durée de bail entre un nœud et ses voisins dans des domaines d’erreur. |

### <a name="section-name-clustermanager"></a>Nom de la section : ClusterManager
| **Paramètre** | **Valeurs autorisées** | **Conseils ou brève description** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Durée en secondes, la valeur par défaut est 60 |fréquence de Hello d’interrogation de l’état de mise à niveau l’application. Cette valeur détermine le taux de hello de mise à jour pour n’importe quel appel GetApplicationUpgradeProgress |
| UpgradeHealthCheckInterval |Durée en secondes, la valeur par défaut est 60 |fréquence de Hello du statut d’intégrité vérifie pendant une mise à niveau de l’application analysée |
| FabricUpgradeStatusPollInterval |Durée en secondes, la valeur par défaut est 60 |fréquence de Hello d’interrogation pour l’état de mise à niveau de l’ensemble fibre optique. Cette valeur détermine le taux de hello de mise à jour pour n’importe quel appel GetFabricUpgradeProgress |
| FabricUpgradeHealthCheckInterval |Durée en secondes, la valeur par défaut est 60 |fréquence de Hello de vérification de l’état d’intégrité pendant une mise à niveau de Fabric analysé |
|InfrastructureTaskProcessingInterval | Durée en secondes, la valeur par défaut est 10 |Spécifiez la durée en secondes. intervalle de traitement Hello utilisé par l’ordinateur d’état du traitement de tâches infrastructure hello. |
|TargetReplicaSetSize |Entier (valeur par défaut : 7) |Hello TargetReplicaSetSize pour ClusterManager. |
|MinReplicaSetSize |Entier (valeur par défaut : 3) |Hello MinReplicaSetSize pour ClusterManager. |
|ReplicaRestartWaitDuration |Durée en secondes (valeur par défaut : 60.0 * 30)|Spécifiez la durée en secondes. Hello ReplicaRestartWaitDuration pour ClusterManager. |
|QuorumLossWaitDuration |Durée en secondes (valeur par défaut : MaxValue) | Spécifiez la durée en secondes. Hello QuorumLossWaitDuration pour ClusterManager. |
|StandByReplicaKeepDuration | Durée en secondes (valeur par défaut : 3600.0 * 2)|Spécifiez la durée en secondes. Hello StandByReplicaKeepDuration pour ClusterManager. |
|PlacementConstraints | Chaîne (valeur par défaut : "") |Hello PlacementConstraints pour ClusterManager. |
|SkipRollbackUpdateDefaultService | Valeur booléenne (valeur par défaut : false) |Hello CM ignorera la restauration des services de mise à jour par défaut lors de la restauration de mise à niveau application. |
|EnableDefaultServicesUpgrade | Valeur booléenne (valeur par défaut : false) |Active la mise à niveau des services par défaut lors de la mise à niveau de l’application. Les descriptions de service par défaut sont remplacées après la mise à niveau. |
|InfrastructureTaskHealthCheckWaitDuration |Durée en secondes (valeur par défaut : 0)| Spécifiez la durée en secondes. Durée Hello toowait de temps avant de commencer les vérifications d’intégrité après une tâche d’infrastructure de post-traitement. |
|InfrastructureTaskHealthCheckStableDuration | Durée en secondes (valeur par défaut : 0)| Spécifiez la durée en secondes. quantité de Hello de temps tooobserve consécutifs passé contrôle d’intégrité vérifie avant la fin de traitement d’une tâche de l’infrastructure avec succès. L’observation d’un contrôle d’intégrité ayant échoué réinitialise ce minuteur. |
|InfrastructureTaskHealthCheckRetryTimeout | Durée en secondes, la valeur par défaut est 60 |Spécifiez la durée en secondes. Durée Hello toospend temps une nouvelle tentative de vérifications d’intégrité a échoué lors d’une tâche de l’infrastructure de post-traitement. L’examen d’un contrôle d’intégrité réussi réinitialise ce minuteur. |
|ImageBuilderTimeoutBuffer |Durée en secondes (valeur par défaut : 3) |Spécifiez la durée en secondes. Durée Hello tooallow de temps pour le client toohello tooreturn Image Builder du délai d’attente des erreurs. Si cette mémoire tampon est trop petit ; client de hello expire avant le serveur de hello, puis obtient une erreur de délai d’attente générique. |
|MinOperationTimeout | Durée en secondes, la valeur par défaut est 60 |Spécifiez la durée en secondes. Hello minimale délai d’expiration global pour le traitement des opérations sur ClusterManager en interne. |
|MaxOperationTimeout |Durée en secondes (valeur par défaut : MaxValue) | Spécifiez la durée en secondes. Hello globale délai d’attente maximal pour le traitement des opérations sur ClusterManager en interne. |
|MaxTimeoutRetryBuffer | Durée en secondes (valeur par défaut : 600) |Spécifiez la durée en secondes. Hello de délai d’attente de l’opération maximale en interne une nouvelle tentative échéance tootimeouts est <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Un délai d’expiration supplémentaire est ajouté en incréments de MinOperationTimeout. |
|MaxCommunicationTimeout |Durée en secondes (valeur par défaut : 600) |Spécifiez la durée en secondes. Hello délai d’attente maximal pour les communications internes entre ClusterManager et d’autres services du système (c'est-à-dire) ; Service d’affectation de noms ; Gestionnaire de basculement, etc.). Ce délai d’expiration doit être inférieur au MaxOperationTimeout global (car il peut y avoir plusieurs communications entre les composants du système pour chaque opération de client). |
|MaxDataMigrationTimeout |Durée en secondes (valeur par défaut : 600) |Spécifiez la durée en secondes. Bonjour le délai d’attente maximal pour les opérations de récupération de la migration de données après qu’une mise à niveau de Fabric a eu lieu. |
|MaxOperationRetryDelay |Durée en secondes (valeur par défaut : 5)| Spécifiez la durée en secondes. délai maximal de Hello pour les nouvelles tentatives internes lors de la défaillance. |
|ReplicaSetCheckTimeoutRollbackOverride |Durée en secondes (valeur par défaut : 1200) | Spécifiez la durée en secondes. Si ReplicaSetCheckTimeout a la valeur toohello valeur maximale DWORD ; Ensuite, il est remplacé par la valeur hello de cette configuration à des fins hello de restauration. valeur de Hello utilisée pour la restauration par progression n’est jamais substituée. |
|ImageBuilderJobQueueThrottle |Entier (valeur par défaut : 10) |Limitation du nombre de threads pour la file d’attente de travaux proxy Image Builder sur les demandes d’application. |

## <a name="next-steps"></a>Étapes suivantes
Lisez les articles suivants pour plus d’informations sur la gestion des clusters :

[Ajouter, restaurer, supprimer des certificats de votre cluster Azure ](service-fabric-cluster-security-update-certs-azure.md) 

