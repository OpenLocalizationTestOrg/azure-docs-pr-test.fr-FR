---
title: aaaUpgrade autonome Azure Service Fabric cluster sur Windows Server | Documents Microsoft
description: "Mettre à niveau le code d’Azure Service Fabric hello et/ou de configuration qui s’exécute à un cluster Service Fabric autonomes, notamment en définissant le mode de mise à jour de cluster hello."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 66296cc6-9524-4c6a-b0a6-57c253bdf67e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 5132795e544b6f0185accedbf5092dcaafd66df0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a>Mettre à niveau un cluster Azure Service Fabric autonome sur Windows Server
> [!div class="op_single_selector"]
> * [Cluster Azure](service-fabric-cluster-upgrade.md)
> * [Cluster autonome](service-fabric-cluster-upgrade-windows-server.md)
>
>

Pour n’importe quel système moderne, hello capacité tooupgrade est un succès à long terme toohello clé de votre produit. Un cluster Azure Service Fabric est une ressource que vous possédez. Cet article décrit comment vous pouvez vous assurer que le cluster hello s’exécute toujours les versions prises en charge de code de l’infrastructure de Service et les configurations.

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a>Version du Service Fabric hello contrôle qui s’exécute sur votre cluster
tooset toodownload de votre cluster met à jour de Service Fabric lorsque Microsoft publie une nouvelle version, jeu hello **fabricClusterAutoupgradeEnabled** tootrue de configuration de cluster. une version prise en charge de l’infrastructure de Service que vous souhaitez votre toobe de cluster sur hello du jeu de tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuration de cluster.

> [!NOTE]
> Veillez à ce que votre cluster exécute toujours une version de Service Fabric prise en charge. Lorsque Microsoft annonce version hello d’une nouvelle version de l’infrastructure de Service, version précédente de hello est marquée pour la fin de la prise en charge un minimum de 60 jours à partir de la date de hello d’annonce de type hello. Nouvelles versions sont annoncées [sur le blog de l’équipe Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/). mise en production Hello est toochoose disponible à ce stade.
>
>

Vous pouvez mettre à niveau votre version du nouveau cluster toohello uniquement si vous utilisez une configuration de nœud de style de production, où chaque nœud de Service Fabric est alloué sur un ordinateur virtuel ou physique distinct. Si vous disposez d’un cluster de développement, où plusieurs nœuds de Service Fabric est sur un seul ordinateur physique ou virtuel, vous devez recréer le cluster hello avec la nouvelle version de hello.

Deux flux de travail distinctes permettre mettre à niveau votre version la plus récente toohello cluster ou une version prise en charge de l’infrastructure de Service. Un flux de travail est pour les clusters dont la version plus récente de connectivité toodownload hello automatiquement. Hello autres flux de travail est pour les clusters qui n’ont pas la version la plus récente Service Fabric connectivité toodownload hello.

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a>Mise à niveau de clusters qui ont la configuration et le dernier code de connectivité toodownload hello
Utilisez ces tooupgrade étapes votre version du cluster tooa pris en charge si vos nœuds de cluster possède trop de connectivité Internet[http://download.microsoft.com](http://download.microsoft.com).

Pour les clusters qui ont trop de connectivité[http://download.microsoft.com](http://download.microsoft.com), Microsoft vérifie régulièrement la disponibilité de hello de nouvelles versions de Service Fabric.

Lorsqu’une nouvelle version de l’infrastructure de Service est disponible, package de hello est téléchargée localement toohello cluster et configuré pour la mise à niveau. En outre, client hello tooinform cette nouvelle version du système de hello montre un avertissement de contrôle d’intégrité de cluster explicite est similaire toohello suivant :

« hello actuelle version (version #) prise en charge termine [Date]. »

Une fois le cluster de hello s’exécute la version la plus récente hello, avertissement de hello disparaît.

#### <a name="cluster-upgrade-workflow"></a>Flux de travail de mise à niveau de cluster
Une fois que vous voyez avertissement d’intégrité du cluster hello, procédez comme hello suivant :

1. Se connecter toohello cluster à partir de n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds de cluster de hello. ordinateur Hello ce script s’exécute n’a pas de partie toobe du cluster de hello.

    ```powershell

    ###### connect toohello secure cluster using certs
    $ClusterName= "mysecurecluster.something.com:19000"
    $CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7FG2D630F8F3"
    Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
        -X509Credential `
        -ServerCertThumbprint $CertThumbprint  `
        -FindType FindByThumbprint `
        -FindValue $CertThumbprint `
        -StoreLocation CurrentUser `
        -StoreName My
    ```

2. Obtenir la liste de hello des versions de l’infrastructure de Service que vous pouvez mettre en œuvre.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    Vous devez obtenir un toothis similaire de sortie :

    ![Obtenir des versions de Service Fabric][getfabversions]
3. Démarrer une version disponible tooan mise à niveau de cluster à l’aide de la [ServiceFabricClusterUpgrade de début](https://msdn.microsoft.com/library/mt125872.aspx) cmd de PowerShell.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   progression de hello toomonitor de mise à niveau hello, vous pouvez utiliser Service Fabric Explorer ou exécution hello suivant de commande Windows PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. toospecify des stratégies de contrôle d’intégrité personnalisé pour hello **Start-ServiceFabricClusterUpgrade** command, consultez la documentation de [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Après avoir résolu les problèmes de hello qui a provoqué la restauration hello, lancer mise à niveau hello à nouveau en suivant hello mêmes étapes comme décrit précédemment.

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a>Mise à niveau de clusters qui ont <U>aucune connectivité</u> code de dernière toodownload hello et la configuration
Utilisez ces tooupgrade étapes votre version du cluster tooa pris en charge si vos nœuds de cluster n’ont pas de connectivité Internet trop[http://download.microsoft.com](http://download.microsoft.com).

> [!NOTE]
> Si vous utilisez un cluster qui n’est pas connecté toohello Internet, vous devez toomonitor hello Service Fabric team blog toolearn sur une nouvelle version. système de Hello n’affiche pas une tooalert d’avertissement de contrôle d’intégrité cluster d’une nouvelle version.  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a>Approvisionnement automatique vs. approvisionnement manuel
téléchargement automatique tooenable et inscription pour la dernière version du code hello, configurer le Service de mise à jour de l’infrastructure de Service. Consultez toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt à l’intérieur de hello [Package autonome](service-fabric-cluster-standalone-package-contents.md) pour obtenir des instructions.
Pour un processus manuel, suivez les instructions de hello ci-dessous.

Modifiez votre hello de tooset de configuration de cluster suivant toofalse de propriété avant de commencer une mise à niveau de la configuration.

        "fabricClusterAutoupgradeEnabled": false,

Consultez trop[ServiceFabricClusterConfigurationUpgrade de début PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) pour plus de détails. Assurez-vous que tooupdate 'clusterConfigurationVersion' dans votre JSON avant de commencer la mise à niveau de la configuration hello.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a>Flux de travail de mise à niveau de cluster

1. Exécutez Get-ServiceFabricClusterUpgrade à partir d’un des nœuds des clusters de hello hello et notez hello TargetCodeVersion.
2. Suit hello exécution à partir d’un toolist d’ordinateur connecté internet tous les mettre à niveau des versions compatibles avec la version actuelle de hello et télécharger les hello correspondant du package à partir des liens de téléchargement associé hello.

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. Se connecter toohello cluster à partir de n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds de cluster de hello. ordinateur Hello que ce script est exécuté sur n’a pas de partie toobe du cluster de hello

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. Copiez hello téléchargé package dans le magasin d’images hello cluster.

5. Inscrire les package hello copié.

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. Démarrez une version disponible tooan mise à niveau de cluster.

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer, ou vous pouvez exécuter hello suivant de commande PowerShell.

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée. toospecify des stratégies de contrôle d’intégrité personnalisé pour hello **Start-ServiceFabricClusterUpgrade** command, consultez la documentation de hello pour [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).

Après avoir résolu les problèmes de hello qui a provoqué la restauration hello, lancer mise à niveau hello à nouveau en suivant hello mêmes étapes comme décrit précédemment.


## <a name="upgrade-hello-cluster-configuration"></a>Mise à niveau de la configuration de cluster hello
Avant de vous lancez la mise à niveau de la configuration hello, vous pouvez tester votre nouveau json de configuration de cluster en exécutant un script powershell de hello dans le package autonome de hello.

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
ou

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

Certaines configurations ne peuvent pas être mises à niveau, notamment les points de terminaison, le nom du cluster, l’IP du nœud, etc. Cela json de configuration de cluster nouvelle hello contre hello ancien de test et générer des erreurs dans la fenêtre de Powershell hello s’il existe un problème.

mise à niveau de cluster configuration tooupgrade hello, exécutez **Start-ServiceFabricClusterConfigurationUpgrade**. mise à niveau de la configuration Hello est le domaine de mise à niveau traité par le domaine de mise à niveau.

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a>Mise à niveau de la configuration du certificat de cluster  
Certificat de cluster est utilisé pour l’authentification entre les nœuds de cluster, afin de substituer des certificats de hello doit être effectuée avec prudence, car échec bloquera communication hello entre les nœuds de cluster.  
Techniquement, trois options sont prises en charge :  

1. Mise à niveau de certificat unique : chemin d’accès de la mise à niveau hello est « certificat (principal) -> B de certificat (principal) -> C de certificat (principal) ->...'.   
2. Double mise à niveau de certificat : chemin d’accès de la mise à niveau hello est « certificat (principal) -> certificats (principal) et B (secondaire) -> B de certificat (principal) -> B de certificat (principal) et C (secondaire) -> C de certificat (principal) ->...'.
3. Mise à niveau du type de certificat : configuration de certificats basée sur Thumbprint <> configuration de certificats basée sur CommonName. Par exemple, certificat Thumbprint A (Principal) et Thumbprint B (Secondaire) -> certificat CommonName C.


## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment toocustomize certains [les paramètres de cluster Service Fabric](service-fabric-cluster-fabric-settings.md).
* Découvrez comment trop[mettre à l’échelle et l’extraction de votre cluster](service-fabric-cluster-scale-up-down.md).
* Découvrez les [mises à niveau d’applications](service-fabric-application-upgrade.md).

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
