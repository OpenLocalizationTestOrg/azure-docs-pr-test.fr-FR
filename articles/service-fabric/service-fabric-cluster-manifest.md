---
title: "aaaConfigure votre cluster d’autonome d’Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment tooconfigure votre autonome ou un cluster Service Fabric privé."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Paramètres de configuration pour un cluster Windows autonome
Cet article décrit la manière dont un cluster Service Fabric autonomes à l’aide de tooconfigure hello ***ClusterConfig.JSON*** fichier. Vous pouvez utiliser ces informations toospecify de fichier tels que des nœuds de Service Fabric hello et leurs adresses IP, les différents types de nœuds de cluster de hello, configurations de sécurité hello, ainsi que la topologie de réseau hello en termes de domaines de pannes/mise à niveau, pour votre autonome cluster.

Lorsque vous [télécharger le package de Service Fabric autonomes hello](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), quelques exemples de fichier ClusterConfig.JSON de hello sont téléchargés tooyour poste. les exemples Hello ayant *DevCluster* dans leurs noms vous aide à créer un cluster avec tous les trois nœuds hello même ordinateur, comme la logique de nœuds. Parmi ces nœuds, au moins un doit être marqué comme nœud principal. Ce cluster est utile pour un environnement de test ou de développement et n’est pas pris en charge comme cluster de production. les exemples Hello ayant *MultiMachine* dans leurs noms, vous aide à créer un cluster de qualité production, chaque nœud sur un ordinateur distinct.

1. *ClusterConfig.Unsecure.DevCluster.JSON* et *ClusterConfig.Unsecure.MultiMachine.JSON* montrent comment cluster respectivement toocreate un test non sécurisé ou production. 
2. *ClusterConfig.Windows.DevCluster.JSON* et *ClusterConfig.Windows.MultiMachine.JSON* indiquent comment toocreate cluster de test ou de production, sécurisées à l’aide de [sécurité Windows](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* et *ClusterConfig.X509.MultiMachine.JSON* indiquent comment toocreate cluster de test ou de production, sécurisés à l’aide [X509 sécurité basée sur certificat](service-fabric-windows-cluster-x509-security.md). 

Maintenant, nous allons examiner hello différentes sections d’un ***ClusterConfig.JSON*** de fichiers comme indiqué ci-dessous.

## <a name="general-cluster-configurations"></a>Configurations de cluster générales
Cette rubrique décrit hello cluster large des configurations spécifiques, comme indiqué dans l’extrait de JSON hello ci-dessous.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Vous pouvez attribuer à n’importe quel cluster Service Fabric de tooyour nom convivial en lui assignant toohello **nom** variable. Hello **clusterConfigurationVersion** est le numéro de version de hello de votre cluster, vous devez l’augmenter chaque fois que vous mettez à niveau votre cluster Service Fabric. Vous devez laisser toutefois hello **apiVersion** toohello par défaut.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Nœuds de cluster de hello
Vous pouvez configurer des nœuds de hello sur votre cluster Service Fabric à l’aide de hello **nœuds** section, comme hello ci-dessous illustre d’extrait de code.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Un cluster Service Fabric doit contenir au moins 3 nœuds. Vous pouvez ajouter la section de toothis plusieurs nœuds conformément à votre installation. Hello tableau suivant décrit les paramètres de configuration de hello pour chaque nœud.

| **Configuration de nœuds** | **Description** |
| --- | --- |
| nodeName |Vous pouvez donner n’importe quel nœud de toohello nom convivial. |
| iPAddress |Rechercher adresse IP de hello du nœud en ouvrant une fenêtre de commande et en tapant `ipconfig`. Notez l’adresse de hello IPV4 et affectez-le toohello **iPAddress** variable. |
| nodeTypeRef |Chaque nœud peut être associé à un type de nœud différent. Hello [types de nœuds](#nodetypes) sont définis dans la section hello ci-dessous. |
| faultDomain |Erreur domaines activer administrateurs toodefine hello physiques nœuds de cluster risque d’échouer au hello même moment en raison des dépendances de physique tooshared. |
| upgradeDomain |Domaines de mise à niveau décrivent les jeux de nœuds qui ne sont pas arrêtés pour Service Fabric met à niveau à hello sur la même heure. Vous pouvez choisir le toowhich tooassign de nœuds domaines de mise à niveau, car ils ne sont pas limités par des exigences physiques. |

## <a name="cluster-properties"></a>Propriétés du cluster
Hello **propriétés** section Bonjour ClusterConfig.JSON est le cluster de hello tooconfigure utilisés comme suit.

<a id="reliability"></a>

### <a name="reliability"></a>Fiabilité
concept Hello de **reliabilityLevel** définit le nombre hello de réplicas ou les instances de services de système de Service Fabric hello pouvant s’exécuter sur les nœuds principaux hello du cluster de hello. Il détermine la fiabilité hello de ces services et donc hello cluster. valeur de Hello est calculée par le système de hello au moment de la création et la mise à niveau de cluster.

### <a name="diagnostics"></a>Diagnostics
Hello **diagnosticsStore** section vous permet de diagnostics de tooenable tooconfigure paramètres et nœud de résolution des problèmes ou défaillances de cluster, comme indiqué dans hello suivant extrait de code. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Hello **métadonnées** est une description de diagnostics de votre cluster et peut être définie en fonction de votre installation. Ces variables vous aident à collecter les journaux de suivi ETW, les vidages sur incident ainsi que les compteurs de performance. Consultez les sections [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) (Journal de suivi) et [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) pour plus d’informations sur les journaux de suivi ETW. Tous les journaux, y compris [vidages sur incident](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) et [les compteurs de performance](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) peut être dirigé toohello **connectionString** dossier sur votre ordinateur. Vous pouvez également utiliser *AzureStorage* pour le stockage des diagnostics. Voici un exemple d’extrait de code.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Sécurité
Hello **sécurité** section n’est nécessaire pour un cluster de Service Fabric autonomes sécurisé. Hello suivant extrait de code montre une partie de cette section.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Hello **métadonnées** est une description de votre cluster sécurisé et peut être définie en fonction de votre installation. Hello **ClusterCredentialType** et **ServerCredentialType** déterminer le type hello de sécurité qui implémentent les cluster hello et les nœuds de hello. Ils peuvent être définies tooeither *X509* pour une sécurité basée sur certificat, ou *Windows* pour une sécurité basée sur Active Directory de Azure. Hello reste Hello **sécurité** section reposera sur le type hello de sécurité de hello. Lecture [sécurité basée sur les certificats dans un cluster autonome](service-fabric-windows-cluster-x509-security.md) ou [sécurité Windows dans un cluster autonome](service-fabric-windows-cluster-windows-security.md) pour plus d’informations sur comment toofill out hello reste de hello **sécurité**section.

<a id="nodetypes"></a>

### <a name="node-types"></a>Types de nœuds
Hello **nodeTypes** section décrit le type hello de nœuds de hello votre cluster. Type de nœud au moins doit être spécifié pour un cluster, comme indiqué dans l’extrait de code hello ci-dessous. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Hello **nom** est hello le nom convivial pour ce type de nœud particulier. toocreate un nœud de ce type de nœud, attribuer son nom convivial de toohello **le nodeTypeRef** variable pour ce nœud, comme indiqué [ci-dessus](#clusternodes). Pour chaque type de nœud, définissez hello connexion points de terminaison qui seront utilisés. Vous pouvez choisir n’importe quel numéro de port pour ces points de terminaison de connexion, à condition qu’ils n’entrent pas en conflit avec d’autres points de terminaison de ce cluster. Dans un cluster à plusieurs nœud, il y aura un ou plusieurs nœuds principales (autrement dit, **isPrimary** défini trop*true*), en fonction de hello [ **reliabilityLevel** ](#reliability). Lecture [les considérations de planification de la capacité de cluster Service Fabric](service-fabric-cluster-capacity.md) pour plus d’informations sur **nodeTypes** et **reliabilityLevel**et tooknow les principaux et hello types de nœud principal. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Points de terminaison utilisés des types de nœuds hello tooconfigure
* *clientConnectionEndpointPort* est hello le port utilisé par hello client tooconnect toohello le cluster, lors de l’utilisation des API clientes hello. 
* *clusterConnectionEndpointPort* est le port hello à laquelle les nœuds hello communiquent entre eux.
* *leaseDriverEndpointPort* est hello le port utilisé par le pilote du bail hello cluster toofind out si les nœuds de hello sont toujours actifs. 
* *serviceConnectionEndpointPort* est le port hello utilisé par les applications hello et les services déployés sur un nœud, toocommunicate avec le client de Service Fabric hello sur ce nœud particulier.
* *httpGatewayEndpointPort* est hello le port utilisé par hello Service Fabric Explorer tooconnect toohello cluster.
* *ephemeralPorts* remplacer hello [ports dynamiques utilisés par hello du système d’exploitation](https://support.microsoft.com/kb/929851). L’infrastructure de service utilisera une partie de ces ports d’application et hello restant sera disponible pour hello du système d’exploitation. Il sera également mapper cette plage toohello plage existante dans hello du système d’exploitation, pour tous les besoins, vous pouvez utiliser des plages hello données dans les fichiers JSON exemple hello. Vous devez toomake que différence hello entre le début de hello et les ports finaux hello est au moins de 255. Vous pouvez rencontrer des conflits si cette différence est trop faible, étant donné que cette plage est partagée avec le système d’exploitation de hello. Afficher la plage de ports dynamiques hello configuré en exécutant `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* sont des ports hello qui seront utilisées par les applications de Service Fabric hello. plage de ports d’application Hello doit être suffisamment grand toocover exigence de point de terminaison hello de vos applications. Cette plage doit être exclusif à partir de la plage de ports dynamiques hello sur ordinateur hello, c'est-à-dire hello *ephemeralPorts* plage défini dans la configuration de hello.  L’infrastructure de service utilisera ces chaque fois que les nouveaux ports sont nécessaires, ainsi que la prenez soin d’ouvrir le pare-feu hello pour ces ports. 
* *reverseProxyEndpointPort* est un point de terminaison de proxy inverse facultatif. Consultez [Proxy inverse de Service Fabric](service-fabric-reverseproxy.md) pour en savoir plus. 

### <a name="log-settings"></a>Paramètres du journal
Hello **fabricSettings** section vous permet de répertoires de racines tooset hello pour les données de Service Fabric hello et les journaux. Vous pouvez personnaliser ces uniquement lors de la création initiale du cluster de hello. Voici un exemple d’extrait de cette section.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

Il est recommandé à l’aide d’un disque du système d’exploitation non hello FabricDataRoot et FabricLogRoot car il fournit une fiabilité accrue contre les pannes du système d’exploitation. Notez que si vous personnalisez uniquement la racine de données hello, puis racine de journal hello sera placé un niveau sous la racine de données hello.

### <a name="stateful-reliable-service-settings"></a>Paramètres Reliable Service avec état
Hello **KtlLogger** section vous permet de paramètres de configuration globale tooset hello pour les Services fiables. Pour plus d’informations sur ces paramètres, consultez [Configuration de services fiables (Reliable Services) avec état](service-fabric-reliable-services-configuration.md).
exemple Hello ci-dessous montre le journal des transactions partagées toochange hello hello qui obtient la création de tooback toutes les collections fiables pour les services avec état.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Fonctionnalités supplémentaires
fonctionnalités du module complémentaire tooconfigure, hello apiVersion doit être configuré en tant que « 04-2017' ou une version ultérieure, et addonFeatures doit toobe configuré :

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Support pour les conteneurs
tooenable conteneur prise en charge à la fois de conteneur windows server et de conteneur hyper-v pour les clusters d’autonome, fonctionnalité des modules complémentaires 'DnsService' hello doit toobe activé.


## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez un fichier ClusterConfig.JSON complet configuré conformément à votre installation de cluster autonome, vous pouvez déployer votre cluster par article hello suivant [créer un cluster de Service Fabric autonomes](service-fabric-cluster-creation-for-windows-server.md) , puis effectuez trop[visualiser votre cluster avec Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).

