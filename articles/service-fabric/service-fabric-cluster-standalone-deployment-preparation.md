---
title: "Préparation du déploiement de Cluster Service Fabric autonomes d’aaaAzure | Documents Microsoft"
description: "Documentation liée environnement de hello toopreparing et créez la configuration de cluster hello, toobe considérée comme toodeploying préalable un cluster conçu pour gérer une charge de travail de production."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 1/17/2017
ms.author: maburlik;chackdan
ms.openlocfilehash: e503c61a64b408af3f22bd75ab02f1c34ac9f380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
<a id="preparemachines"></a>

## <a name="plan-and-prepare-your-service-fabric-standalone-cluster-deployment"></a>Planifier et préparer votre déploiement de cluster Service Fabric autonome
Effectuer hello comme suit avant de créer votre cluster.

### <a name="step-1-plan-your-cluster-infrastructure"></a>Étape 1 : planifier votre infrastructure de cluster
Vous êtes sur le toocreate un cluster Service Fabric sur les ordinateurs que vous possédez, afin de décider quels types d’échecs, vous souhaitez hello toosurvive du cluster. Par exemple, avez-vous besoin de lignes distinctes, ou les connexions Internet fourni des machines de toothese ? En outre, envisagez de sécurité physique de hello de ces ordinateurs. Où sont trouvent les machines hello et qui a besoin d’accès toothem ? Après avoir apporté ces décisions, vous pouvez logiquement mapper hello machines toohello différents domaines d’erreur (voir l’étape 4). planification pour les clusters de production de l’infrastructure Hello est plus complexe que pour les clusters de test.

### <a name="step-2-prepare-hello-machines-toomeet-hello-prerequisites"></a>Étape 2 : Préparer hello machines toomeet conditions préalables de hello
Configuration requise pour chaque ordinateur que vous souhaitez tooadd toohello cluster :

* Un minimum de 16 Go de RAM est recommandé.
* Un minimum de 40 Go d’espace disque disponible est recommandé.
* Un processeur 4 cœurs ou plus est recommandé.
* Connectivité tooa sécurisé ou les réseaux pour tous les ordinateurs.
* Windows Server 2012 R2 ou Windows Server 2016. 
* [.NET Framework 4.5.1 ou une version ultérieure](https://www.microsoft.com/download/details.aspx?id=40773), installation complète.
* [Windows PowerShell 3.0](https://msdn.microsoft.com/powershell/scripting/setup/installing-windows-powershell).
* Hello [RemoteRegistry service](https://technet.microsoft.com/library/cc754820) doit s’exécuter sur tous les ordinateurs hello.

Hello déploiement et la configuration de cluster de hello l’administrateur de cluster doit avoir [des privilèges d’administrateur](https://social.technet.microsoft.com/wiki/contents/articles/13436.windows-server-2012-how-to-add-an-account-to-a-local-administrator-group.aspx) sur chacun des ordinateurs de hello. Vous ne pouvez pas installer Service Fabric sur un contrôleur de domaine.

### <a name="step-3-determine-hello-initial-cluster-size"></a>Étape 3 : Déterminer la taille initiale du cluster de hello
Chaque nœud dans un cluster de Service Fabric autonomes a hello Service Fabric runtime déployé et qu’il est membre du cluster de hello. Un déploiement de production type comprend un nœud par instance du système d’exploitation (physique ou virtuel). taille de cluster Hello est déterminée par les besoins de votre entreprise. Toutefois, vous devez disposer d’une taille minimale de cluster de trois nœuds (ordinateurs ou machines virtuelles).
À des fins de développement, vous pouvez avoir plusieurs nœuds sur un ordinateur donné. Dans un environnement de production, Service Fabric ne prend en charge qu’un seul nœud par ordinateur physique ou virtuel.

### <a name="step-4-determine-hello-number-of-fault-domains-and-upgrade-domains"></a>Étape 4 : Déterminer le nombre de hello de domaines d’erreur et domaines de mise à niveau
A *domaine d’erreur* (DP) est une unité physique de l’échec et est directement lié, toohello l’infrastructure physique hello centres de données. Un domaine d’erreur est constitué de composants matériels (ordinateurs, commutateurs, réseaux, etc.) qui partagent un point de défaillance unique. Bien qu’il n’existe aucun mappage 1:1 entre les domaines d’erreur et les racks, chaque rack peut être considéré au sens large comme un domaine d’erreur. Lorsque vous envisagez de nœuds hello dans votre cluster, nous recommandons vivement que les nœuds hello distribuée entre au moins trois domaines d’erreur.

Lorsque vous spécifiez des groupes dans le fichier ClusterConfig.json, vous pouvez choisir le nom hello pour chaque lecteur de disquette. Service Fabric prend en charge les domaines d’erreur hiérarchiques pour vous permettre d’y refléter votre topologie d’infrastructure.  Par exemple, hello suivant groupes est valide :

* "faultDomain": "fd:/Room1/Rack1/Machine1"
* "faultDomain": "fd:/FD1"
* "faultDomain": "fd:/Room1/Rack1/PDU1/M1"

Un *domaine de mise à niveau (UD)* est une unité logique de nœuds. Pendant les mises à niveau de Service Fabric orchestrés (une mise à niveau de l’application ou une mise à niveau de cluster), tous les nœuds dans un UD sont mis hors service de la mise à niveau de tooperform hello tandis que les nœuds dans d’autres domaines d’erreur restent disponibles tooserve demandes. Hello vous effectuez sur vos ordinateurs les mises à niveau du microprogramme n’honorent pas ces domaines d’erreur, vous devez les faire un ordinateur à la fois.

Hello toothink de façon la plus simple à ces concepts est tooconsider mise en tant qu’unité hello d’échec non planifié et de domaines d’erreur en tant qu’unité hello de maintenance planifiée.

Lorsque vous spécifiez des domaines d’erreur dans le fichier ClusterConfig.json, vous pouvez choisir le nom hello pour chaque UD. Par exemple, hello suivant de noms est valide :

* "upgradeDomain": "UD0"
* "upgradeDomain": "UD1A"
* "upgradeDomain": "DomainRed"
* "upgradeDomain": "Blue"

Pour plus d’informations sur les domaines de mise à niveau et les domaines d’erreur, consultez [Description d’un cluster Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md) .

### <a name="step-5-download-hello-service-fabric-standalone-package-for-windows-server"></a>Étape 5 : Téléchargez le package autonome de Service Fabric hello pour Windows Server
[Télécharger le lien - Package de Service Fabric autonomes - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) et décompressez le package de hello, soit déploiement tooa ordinateur ne fait pas partie du cluster de hello ou tooone d’ordinateurs hello qui feront partie de votre cluster.

### <a name="step-6-modify-cluster-configuration"></a>Étape 6 : Modifier la configuration du cluster
toocreate un cluster autonome que vous avez toocreate un fichier autonome cluster configuration ClusterConfig.json qui décrit la spécification de hello du cluster de hello. Vous pouvez baser le fichier de configuration hello sur des modèles hello à hello lien ci-après. <br>
[Configurations de cluster autonome](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

Pour plus d’informations sur les sections hello dans ce fichier, consultez [paramètres de Configuration de cluster de Windows autonome](service-fabric-cluster-manifest.md).

Un des fichiers de ClusterConfig.json hello ouvrir à partir du package hello que vous avez téléchargé et modifier hello suivant les paramètres :
| **Paramètres de configuration** | **Description** |
| --- | --- |
| **NodeTypes** |Autorisent les types de nœuds vous tooseparate vos nœuds de cluster dans différents groupes. Un cluster doit comprendre au moins un NodeType. Tous les nœuds dans un groupe ont hello suivant des caractéristiques communes : <br> **Nom** -Ceci est le nom de type de nœud de hello. <br>**Endpoints Ports** : il s’agit de différents points de terminaison (ports) nommés qui sont associés à ce type de nœud. Vous pouvez utiliser n’importe quel numéro de port que vous le souhaitez, tant qu’ils ne sont pas en conflit avec rien d’autre dans ce manifeste et ne sont pas déjà en cours d’utilisation par une autre application en cours d’exécution sur la machine de hello/machine virtuelle. <br> **Propriétés de positionnement** -elles décrivent les propriétés pour ce type de nœud que vous utilisez en tant que contraintes de sélection élective pour les services système hello ou vos services. Ces propriétés sont des paires clé/valeur définies par l’utilisateur qui fournissent des métadonnées supplémentaires pour un nœud donné. Exemples de propriétés de nœud serait indique si le nœud de hello a un disque dur ou la carte graphique, le nombre de hello de piles dans son disque dur, les cœurs et autres propriétés physiques. <br> **Capacités** -définissent les capacités de nœud nom de hello et la quantité d’une ressource spécifique qu’un nœud particulier est disponible pour la consommation. Par exemple, un nœud peut définir qu’il possède la capacité pour une mesure appelée « MemoryInMb » et qu’il dispose de 2 048 Mo de mémoire disponible par défaut. Ces capacités sont utilisées au tooensure runtime que les services qui nécessitent une quantité spécifique de ressources placés sur les nœuds de hello qu’aient les ressources disponibles dans hello requis quantités.<br>**IsPrimary** : Si vous avez plusieurs NodeType défini Assurez-vous que seul est tooprimary avec la valeur de hello *true*, emplacements où les services de système de hello exécuter. Valeur de toohello doivent être définis à tous les autres types de nœud *false* |
| **Nœuds** |Voici les détails de hello pour chacun des nœuds hello qui font partie du cluster hello (type de nœud, nom de nœud, IP adresse, domaine d’erreur et domaine de mise à niveau du nœud de hello). les machines Hello souhaité hello toobe de cluster créé sur toobe besoin répertorié ici avec leurs adresses IP. <br> Si vous utilisez hello même adresse IP pour tous les nœuds de hello, puis d’un cluster d’une zone est créée, vous pouvez utiliser à des fins de test. N’utilisez pas les clusters à boîtier unique pour le déploiement de charges de travail de production. |

Une fois la configuration du cluster hello a un environnement de toohello tous les paramètres configurés, il peut être testé par rapport à l’environnement de cluster hello (étape 7).

<a id="environmentsetup"></a>

### <a name="step-7-environment-setup"></a>Étape 7. Configuration de l’environnement

Lorsqu’un administrateur de cluster configure un cluster autonome de Service Fabric, hello environnement est besoins toobe configuré avec hello suivant des critères : <br>
1. utilisateur Hello création hello cluster doit avoir la sécurité au niveau de l’administrateur des privilèges tooall machines qui sont répertoriés en tant que nœuds dans le fichier de configuration de cluster hello.
2. Ordinateur à partir de quels hello cluster est créé, ainsi que chaque ordinateur nœud de cluster doit :
* le Kit de développement logiciel (SDK) Service Fabric doit être désinstallé ;
* le runtime Service Fabric doit être désinstallé ; 
* Avez hello service de pare-feu Windows (mpssvc) activé
* Hello Service Registre distant (remoteregistry) avez activé
* le partage de fichiers (SMB) doit être activé ;
* les ports requis doivent être ouverts, selon les ports de configuration du cluster ;
* les ports requis doivent êtres ouverts pour le service Registre distant et SMB Windows : 135, 137, 138, 139 et 445 ;
* Ont tooone de connectivité réseau une autre
3. Aucun des ordinateurs hello du nœud de cluster doit être un contrôleur de domaine.
4. Si toobe de cluster hello déployé est un cluster sécurisé, valider sécurité hello conditions préalables sont en place et sont correctement configurés sur la configuration de hello.
5. Si les ordinateurs du cluster hello ne sont pas accessibles sur internet, qui suit hello ensemble dans hello configuration du cluster :
* Désactiver la télémétrie : sous *Propriétés*, définissez *« enableTelemetry » : false*
* Désactiver automatique de téléchargement de version de l’ensemble fibre optique & de cette version du cluster actuel hello est proche de sa fin de prise en charge des notifications : sous *propriétés* définir *« fabricClusterAutoupgradeEnabled » : false*
* Vous pouvez également si l’accès à internet de réseau est toowhite dans la liste des domaines limités, les domaines hello ci-dessous sont requis pour la mise à niveau automatique : go.microsoft.com download.microsoft.com

6. Définissez les exclusions antivirus Service Fabric appropriées :

| **Répertoires exclus de l’antivirus** |
| --- |
| Program Files\Microsoft Service Fabric |
| FabricDataRoot (dans la configuration du cluster) |
| FabricLogRoot (dans la configuration du cluster) |

| **Processus exclus de l’antivirus** |
| --- |
| Fabric.exe |
| FabricHost.exe |
| FabricInstallerService.exe |
| FabricSetup.exe |
| FabricDeployer.exe |
| ImageBuilder.exe |
| FabricGateway.exe |
| FabricDCA.exe |
| FabricFAS.exe |
| FabricUOS.exe |
| FabricRM.exe |
| FileStoreService.exe |

### <a name="step-8-validate-environment-using-testconfiguration-script"></a>Étape 8 : Valider l’environnement à l’aide du script TestConfiguration
Vous trouverez Hello TestConfiguration.ps1 script dans le package autonome de hello. Il est utilisé comme un toovalidate Best Practices Analyzer, certains des critères hello ci-dessus et doit être utilisé comme un toovalidate de vérification de validité si un cluster peut être déployé sur un environnement donné. S’il existe une défaillance, consultez la liste toohello sous [configuration de l’environnement](service-fabric-cluster-standalone-deployment-preparation.md) pour le dépannage. 

Ce script peut être exécuté sur n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds dans le fichier de configuration de cluster hello. ordinateur Hello ce script s’exécute n’a pas de partie toobe du cluster de hello.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
Running Best Practices Analyzer...
Best Practices Analyzer completed successfully.


LocalAdminPrivilege        : True
IsJsonValid                : True
IsCabValid                 : True
RequiredPortsOpen          : True
RemoteRegistryAvailable    : True
FirewallAvailable          : True
RpcCheckPassed             : True
NoConflictingInstallations : True
FabricInstallable          : True
Passed                     : True
```

Actuellement ce module de test de configuration ne valide pas la configuration de sécurité hello par conséquent, il a toobe fait indépendamment.  

> [!NOTE]
> Nous en permanence apportons des améliorations toomake ce module plus robuste, par conséquent, s’il existe un défectueux ou manquant casse, ce qui vous pensez n’est pas actuellement interceptée par TestConfiguration, faites-le nous savoir via notre [prennent en charge des canaux](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).   
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Créer un cluster autonome s’exécutant sur Windows Server](service-fabric-cluster-creation-for-windows-server.md)
