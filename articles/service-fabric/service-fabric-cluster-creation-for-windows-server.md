---
title: "un cluster d’Azure Service Fabric autonomes d’aaaCreate | Documents Microsoft"
description: "Créez un cluster Azure Service Fabric sur n’importe quel ordinateur (physique ou virtuel) exécutant Windows Server, qu’il soit local ou dans un cloud."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a>Créer un cluster autonome s’exécutant sur Windows Server
Vous pouvez utiliser Azure Service Fabric toocreate Service Fabric clusters sur des ordinateurs virtuels ou des ordinateurs exécutant Windows Server. Cela signifie que vous pouvez déployer et exécuter des applications Service Fabric dans n’importe quel environnement contenant un ensemble d’ordinateurs Windows Server interconnectés, que ce soit en local ou avec un fournisseur cloud. L’infrastructure de service fournit un toocreate du package d’installation de clusters Service Fabric appelé package de Windows Server autonome hello.

Cet article vous guide tout au long des étapes hello pour créer un cluster autonome de Service Fabric.

> [!NOTE]
> Ce package de Windows Server autonome est commercialisé et peut être utilisé pour les déploiements de production. Ce package peut contenir de nouvelles fonctionnalités Service Fabric en version « préliminaire ». Faites défiler la liste trop »[incluses dans ce package de fonctionnalités en version préliminaire](#previewfeatures_anchor). » section de la liste de hello de fonctionnalités en version préliminaire hello. Vous pouvez [télécharger une copie du CLUF de hello](http://go.microsoft.com/fwlink/?LinkID=733084) maintenant.
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a>Obtenir un support technique pour le package de Service Fabric pour Windows Server hello
* Demandez les Communautés hello package autonome de Service Fabric hello pour Windows Server Bonjour [forum d’Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).
* Ouvrez un ticket pour obtenir le [support professionnel Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).  En savoir plus sur le support professionnel Microsoft [ici](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).
* Vous pouvez également bénéficier du support pour ce package dans le cadre du [Support Premier Microsoft](https://support.microsoft.com/en-us/premier).
* Pour plus d’informations, consultez [Options de support d’Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).
* journaux toocollect pour des raisons de prise en charge, exécutez hello [Service Fabric autonomes Log collector](service-fabric-cluster-standalone-package-contents.md).

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a>Téléchargez hello Service Fabric pour Windows Server
cluster de hello toocreate, utiliser le package Service Fabric pour Windows Server hello (Windows Server 2012 R2 et version ultérieure) est disponible ici : <br>
[Lien de téléchargement - Package autonome Service Fabric - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)

Plus d’informations sur le contenu du package de hello [ici](service-fabric-cluster-standalone-package-contents.md).

package de runtime Service Fabric Hello est automatiquement téléchargé lors de la création du cluster. Si le déploiement à partir d’un ordinateur non connecté toohello internet, téléchargez le package de runtime hello hors bande à partir d’ici : <br>
[Lien de téléchargement - Runtime Service Fabric - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)

Recherchez des exemples de configuration de cluster autonome sous : <br>
[Exemples de configuration de cluster autonome](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a>Créer le cluster de hello
Service Fabric peut être un cluster de développement d’une machine tooa déployé à l’aide de hello *ClusterConfig.Unsecure.DevCluster.json* fichier inclus dans [exemples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

Décompressez le package tooyour ordinateur hello autonome, copie hello exemple config fichier toohello ordinateur local, puis exécution hello *CreateServiceFabricCluster.ps1* script via une session PowerShell d’administrateur, de hello autonome dossier du package :
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a>Étape 1A : Créer un cluster de développement local non sécurisé
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

Consultez hello de section de configuration de l’environnement à [planifier et préparer le déploiement de clusters](service-fabric-cluster-standalone-deployment-preparation.md) pour les détails de résolution.

Si vous avez terminé les scénarios de développement en cours d’exécution, vous pouvez supprimer cluster Service Fabric de hello à partir de l’ordinateur de hello en vous reportant toosteps dans la section «[supprimer un cluster](#removecluster_anchor)». 

### <a name="step-1b-create-a-multi-machine-cluster"></a>Étape 1B : Créer un cluster de plusieurs ordinateurs
Une fois que vous avez parcouru hello planification et des étapes de préparation détaillés au hello sous le lien, vous êtes prêt à toocreate votre cluster de production à l’aide de votre fichier de configuration de cluster. <br>
[Planifier et préparer le déploiement de cluster](service-fabric-cluster-standalone-deployment-preparation.md)

1. Valider le fichier de configuration hello que vous avez écrit en exécutant hello *TestConfiguration.ps1* script à partir du dossier du package autonome hello :  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    Un résultat similaire à ce qui suit s’affiche normalement. Si le champ du bas hello « Réussite » est retourné comme « True », les vérifications des tests ont réussi et cluster de hello recherche toobe déployable en fonction de la configuration d’entrée de hello.

    ```
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

2. Créer le cluster de hello : exécutez hello *CreateServiceFabricCluster.ps1* cluster de script toodeploy hello Service Fabric sur chaque ordinateur dans la configuration de hello. 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> Les traces de déploiement sont écrites toohello VM/ordinateur sur lequel vous avez exécuté hello CreateServiceFabricCluster.ps1 de script PowerShell. Vous la trouverez dans le sous-dossier de hello DeploymentTraces, dans le répertoire hello à partir de quels hello script a été exécuté. toosee si l’infrastructure de Service a été déployé correctement tooa machine, hello installé se trouvent dans le répertoire de FabricDataRoot hello, comme indiqué dans le fichier de configuration de cluster hello FabricSettings section (valeur par défaut c:\ProgramData\SF). De même, vous pouvez consulter l’exécution des processus FabricHost.exe et Fabric.exe dans le Gestionnaire des tâches.
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a>Étape 1C : Créer un cluster hors connexion (déconnecté d’Internet)
package de runtime Service Fabric Hello est automatiquement téléchargé lors de la création du cluster. Lorsque la déployer un cluster de toomachines ne pas connecté toohello internet, vous devez le hello toodownload Service Fabric runtime package séparément et fournir tooit de chemin d’accès hello lors de la création du cluster.
Hello package runtime peut être téléchargé séparément, à partir d’un autre ordinateur connecté toohello internet, à [lien Télécharger - Runtime du Service de l’ensemble fibre optique - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354). Copiez hello runtime package toowhere vous déployez cluster hors connexion de hello à partir d’et créez un cluster de hello en exécutant `CreateServiceFabricCluster.ps1` avec hello `-FabricRuntimePackagePath` paramètre inclus, comme indiqué ci-dessous : 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
où `.\ClusterConfig.json` et `.\MicrosoftAzureServiceFabric.cab` sont respectivement de configuration du cluster toohello hello chemins d’accès et un fichier .cab d’exécution hello.


### <a name="step-2-connect-toohello-cluster"></a>Étape 2 : Se connecter toohello cluster
cluster sécurisée de tooa tooconnect, consultez [Service fabric connecter toosecure cluster](service-fabric-connect-to-secure-cluster.md).

cluster non sécurisée de la tooan du tooconnect, exécutez hello suivant de commande PowerShell :

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
Exemple :
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a>Étape 3 : Afficher Service Fabric Explorer
Maintenant vous pouvez vous connecter toohello cluster avec Service Fabric Explorer directement à partir d’un des ordinateurs hello http://localhost:19080/Explorer/index.html ou à distance avec http://&lt*IPAddressofaMachine*> : 19080 / Explorer/index.HTML.

## <a name="add-and-remove-nodes"></a>Ajouter et supprimer des nœuds
Vous pouvez ajouter ou supprimer le cluster Service Fabric de nœuds tooyour autonome comme l’évolution des besoins de votre entreprise. Consultez [ajouter ou supprimer le cluster de nœuds tooa Service Fabric autonomes](service-fabric-cluster-windows-server-add-remove-nodes.md) pour obtenir des instructions détaillées.

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a>Supprimer un cluster
tooremove un cluster, exécutez hello *RemoveServiceFabricCluster.ps1* script PowerShell à partir de dossier du package hello et passe hello chemin d’accès toohello fichier de configuration JSON. Vous pouvez éventuellement spécifier un emplacement pour le journal de hello de suppression de hello.

Ce script peut être exécuté sur n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds dans le fichier de configuration de cluster hello. ordinateur Hello ce script s’exécute n’a pas de partie toobe du cluster de hello.

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a>Données de télémétrie recueillies et la manière dont tooopt sortie
Par défaut, les produits hello collecte une télémétrie sur le produit hello tooimprove hello Service Fabric d’utilisation. Hello Best Practice Analyzer qui s’exécute comme une partie du programme d’installation hello vérifie pour la connectivité trop[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1). Si elle n’est pas accessible, le programme d’installation hello échoue, sauf si vous refuser de télémétrie.

1. pipeline de télémétrie Hello tente hello tooupload suivant des données trop[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) une fois par jour. Il est un téléchargement de meilleur effort et n’a aucun impact sur les fonctionnalités de cluster hello. les données de télémétrie Hello sont envoyée uniquement à partir du nœud de hello que s’exécute hello principal de gestionnaire de basculement. Aucun autre nœud n’envoie des données de télémétrie.
2. les données de télémétrie Hello se compose de suivant de hello :

* Nombre de services
* Nombre de ServiceTypes
* Nombre de Applications
* Nombre de ApplicationUpgrades
* Nombre de FailoverUnits
* Nombre de InBuildFailoverUnits
* Nombre de UnhealthyFailoverUnits
* Nombre de Replicas
* Nombre de InBuildReplicas
* Nombre de StandByReplicas
* Nombre de OfflineReplicas
* CommonQueueLength
* QueryQueueLength
* FailoverUnitQueueLength
* CommitQueueLength
* Nombre de nœuds
* IsContextComplete : True/False
* ClusterId : GUID généré de manière aléatoire pour chaque cluster
* ServiceFabricVersion
* Adresse IP de la machine virtuelle de hello ou téléchargée à partir de quels hello télémétrie

données de télémétrie toodisable, ajouter hello suivant trop*propriétés* dans votre configuration de cluster : *enableTelemetry : false*.

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a>Fonctionnalités préliminaires incluses dans ce package
Aucune.


> [!NOTE]
> En commençant par hello nouvelle [version générale d’un cluster d’autonome hello pour Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), vous pouvez mettre à niveau votre cluster toofuture les versions, manuellement ou automatiquement. Consultez trop[mise à niveau d’une version autonome du cluster Service Fabric](service-fabric-cluster-upgrade-windows-server.md) document pour plus d’informations.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Déployer et supprimer des applications avec PowerShell](service-fabric-deploy-remove-applications.md)
* [Paramètres de configuration pour un cluster Windows autonome](service-fabric-cluster-manifest.md)
* [Ajouter ou supprimer le cluster Service Fabric de nœuds tooa autonome](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Mettre à niveau une version autonome du cluster Service Fabric](service-fabric-cluster-upgrade-windows-server.md)
* [Créer un cluster Service Fabric autonome avec des machines virtuelles Azure Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [Sécuriser un cluster autonome sur Windows à l’aide de la sécurité Windows](service-fabric-windows-cluster-windows-security.md)
* [Sécuriser un cluster autonome sur Windows à l’aide de certificats X509](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
