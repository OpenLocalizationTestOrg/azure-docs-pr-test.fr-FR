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
# <a name="upgrade-your-standalone-azure-service-fabric-on-windows-server-cluster"></a><span data-ttu-id="1ff1d-103">Mettre à niveau un cluster Azure Service Fabric autonome sur Windows Server</span><span class="sxs-lookup"><span data-stu-id="1ff1d-103">Upgrade your standalone Azure Service Fabric on Windows Server cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ff1d-104">Cluster Azure</span><span class="sxs-lookup"><span data-stu-id="1ff1d-104">Azure Cluster</span></span>](service-fabric-cluster-upgrade.md)
> * [<span data-ttu-id="1ff1d-105">Cluster autonome</span><span class="sxs-lookup"><span data-stu-id="1ff1d-105">Standalone Cluster</span></span>](service-fabric-cluster-upgrade-windows-server.md)
>
>

<span data-ttu-id="1ff1d-106">Pour n’importe quel système moderne, hello capacité tooupgrade est un succès à long terme toohello clé de votre produit.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-106">For any modern system, hello ability tooupgrade is a key toohello long-term success of your product.</span></span> <span data-ttu-id="1ff1d-107">Un cluster Azure Service Fabric est une ressource que vous possédez.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-107">An Azure Service Fabric cluster is a resource that you own.</span></span> <span data-ttu-id="1ff1d-108">Cet article décrit comment vous pouvez vous assurer que le cluster hello s’exécute toujours les versions prises en charge de code de l’infrastructure de Service et les configurations.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-108">This article describes how you can make sure that hello cluster always runs supported versions of Service Fabric code and configurations.</span></span>

## <a name="control-hello-service-fabric-version-that-runs-on-your-cluster"></a><span data-ttu-id="1ff1d-109">Version du Service Fabric hello contrôle qui s’exécute sur votre cluster</span><span class="sxs-lookup"><span data-stu-id="1ff1d-109">Control hello Service Fabric version that runs on your cluster</span></span>
<span data-ttu-id="1ff1d-110">tooset toodownload de votre cluster met à jour de Service Fabric lorsque Microsoft publie une nouvelle version, jeu hello **fabricClusterAutoupgradeEnabled** tootrue de configuration de cluster.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-110">tooset your cluster toodownload updates of Service Fabric when Microsoft releases a new version, set hello **fabricClusterAutoupgradeEnabled** cluster configuration tootrue.</span></span> <span data-ttu-id="1ff1d-111">une version prise en charge de l’infrastructure de Service que vous souhaitez votre toobe de cluster sur hello du jeu de tooselect **fabricClusterAutoupgradeEnabled** toofalse de configuration de cluster.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-111">tooselect a supported version of Service Fabric that you want your cluster toobe on, set hello **fabricClusterAutoupgradeEnabled** cluster configuration toofalse.</span></span>

> [!NOTE]
> <span data-ttu-id="1ff1d-112">Veillez à ce que votre cluster exécute toujours une version de Service Fabric prise en charge.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-112">Make sure that your cluster always runs a supported Service Fabric version.</span></span> <span data-ttu-id="1ff1d-113">Lorsque Microsoft annonce version hello d’une nouvelle version de l’infrastructure de Service, version précédente de hello est marquée pour la fin de la prise en charge un minimum de 60 jours à partir de la date de hello d’annonce de type hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-113">When Microsoft announces hello release of a new version of Service Fabric, hello previous version is marked for end of support after a minimum of 60 days from hello date of hello announcement.</span></span> <span data-ttu-id="1ff1d-114">Nouvelles versions sont annoncées [sur le blog de l’équipe Service Fabric hello](https://blogs.msdn.microsoft.com/azureservicefabric/).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-114">New releases are announced [on hello Service Fabric team blog](https://blogs.msdn.microsoft.com/azureservicefabric/).</span></span> <span data-ttu-id="1ff1d-115">mise en production Hello est toochoose disponible à ce stade.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-115">hello new release is available toochoose at that point.</span></span>
>
>

<span data-ttu-id="1ff1d-116">Vous pouvez mettre à niveau votre version du nouveau cluster toohello uniquement si vous utilisez une configuration de nœud de style de production, où chaque nœud de Service Fabric est alloué sur un ordinateur virtuel ou physique distinct.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-116">You can upgrade your cluster toohello new version only if you are using a production-style node configuration, where each Service Fabric node is allocated on a separate physical or virtual machine.</span></span> <span data-ttu-id="1ff1d-117">Si vous disposez d’un cluster de développement, où plusieurs nœuds de Service Fabric est sur un seul ordinateur physique ou virtuel, vous devez recréer le cluster hello avec la nouvelle version de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-117">If you have a development cluster, where more than one Service Fabric node is on a single physical or virtual machine, you must re-create hello cluster with hello new version.</span></span>

<span data-ttu-id="1ff1d-118">Deux flux de travail distinctes permettre mettre à niveau votre version la plus récente toohello cluster ou une version prise en charge de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-118">Two distinct workflows can upgrade your cluster toohello latest version or a supported Service Fabric version.</span></span> <span data-ttu-id="1ff1d-119">Un flux de travail est pour les clusters dont la version plus récente de connectivité toodownload hello automatiquement.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-119">One workflow is for clusters that have connectivity toodownload hello latest version automatically.</span></span> <span data-ttu-id="1ff1d-120">Hello autres flux de travail est pour les clusters qui n’ont pas la version la plus récente Service Fabric connectivité toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-120">hello other workflow is for clusters that do not have connectivity toodownload hello latest Service Fabric version.</span></span>

### <a name="upgrade-clusters-that-have-connectivity-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="1ff1d-121">Mise à niveau de clusters qui ont la configuration et le dernier code de connectivité toodownload hello</span><span class="sxs-lookup"><span data-stu-id="1ff1d-121">Upgrade clusters that have connectivity toodownload hello latest code and configuration</span></span>
<span data-ttu-id="1ff1d-122">Utilisez ces tooupgrade étapes votre version du cluster tooa pris en charge si vos nœuds de cluster possède trop de connectivité Internet[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-122">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

<span data-ttu-id="1ff1d-123">Pour les clusters qui ont trop de connectivité[http://download.microsoft.com](http://download.microsoft.com), Microsoft vérifie régulièrement la disponibilité de hello de nouvelles versions de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-123">For clusters that have connectivity too[http://download.microsoft.com](http://download.microsoft.com), Microsoft periodically checks for hello availability of new Service Fabric versions.</span></span>

<span data-ttu-id="1ff1d-124">Lorsqu’une nouvelle version de l’infrastructure de Service est disponible, package de hello est téléchargée localement toohello cluster et configuré pour la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-124">When a new Service Fabric version is available, hello package is downloaded locally toohello cluster and provisioned for upgrade.</span></span> <span data-ttu-id="1ff1d-125">En outre, client hello tooinform cette nouvelle version du système de hello montre un avertissement de contrôle d’intégrité de cluster explicite est similaire toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="1ff1d-125">Additionally, tooinform hello customer of this new version, hello system shows an explicit cluster health warning that's similar toohello following:</span></span>

<span data-ttu-id="1ff1d-126">« hello actuelle version (version #) prise en charge termine [Date]. »</span><span class="sxs-lookup"><span data-stu-id="1ff1d-126">“hello current cluster version [version#] support ends [Date]."</span></span>

<span data-ttu-id="1ff1d-127">Une fois le cluster de hello s’exécute la version la plus récente hello, avertissement de hello disparaît.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-127">After hello cluster is running hello latest version, hello warning goes away.</span></span>

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="1ff1d-128">Flux de travail de mise à niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="1ff1d-128">Cluster upgrade workflow</span></span>
<span data-ttu-id="1ff1d-129">Une fois que vous voyez avertissement d’intégrité du cluster hello, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="1ff1d-129">After you see hello cluster health warning, do hello following:</span></span>

1. <span data-ttu-id="1ff1d-130">Se connecter toohello cluster à partir de n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-130">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="1ff1d-131">ordinateur Hello ce script s’exécute n’a pas de partie toobe du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-131">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

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

2. <span data-ttu-id="1ff1d-132">Obtenir la liste de hello des versions de l’infrastructure de Service que vous pouvez mettre en œuvre.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-132">Get hello list of Service Fabric versions that you can upgrade to.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Get-ServiceFabricRegisteredClusterCodeVersion
    ```

    <span data-ttu-id="1ff1d-133">Vous devez obtenir un toothis similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="1ff1d-133">You should get an output similar toothis:</span></span>

    ![Obtenir des versions de Service Fabric][getfabversions]
3. <span data-ttu-id="1ff1d-135">Démarrer une version disponible tooan mise à niveau de cluster à l’aide de la [ServiceFabricClusterUpgrade de début](https://msdn.microsoft.com/library/mt125872.aspx) cmd de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-135">Start a cluster upgrade tooan available version by using the [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx) PowerShell cmd.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="1ff1d-136">progression de hello toomonitor de mise à niveau hello, vous pouvez utiliser Service Fabric Explorer ou exécution hello suivant de commande Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-136">toomonitor hello progress of hello upgrade, you can use Service Fabric Explorer or run hello following Windows PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="1ff1d-137">Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-137">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="1ff1d-138">toospecify des stratégies de contrôle d’intégrité personnalisé pour hello **Start-ServiceFabricClusterUpgrade** command, consultez la documentation de [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-138">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="1ff1d-139">Après avoir résolu les problèmes de hello qui a provoqué la restauration hello, lancer mise à niveau hello à nouveau en suivant hello mêmes étapes comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-139">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>

### <a name="upgrade-clusters-that-have-uno-connectivityu-toodownload-hello-latest-code-and-configuration"></a><span data-ttu-id="1ff1d-140">Mise à niveau de clusters qui ont <U>aucune connectivité</u> code de dernière toodownload hello et la configuration</span><span class="sxs-lookup"><span data-stu-id="1ff1d-140">Upgrade clusters that have <U>no connectivity</u> toodownload hello latest code and configuration</span></span>
<span data-ttu-id="1ff1d-141">Utilisez ces tooupgrade étapes votre version du cluster tooa pris en charge si vos nœuds de cluster n’ont pas de connectivité Internet trop[http://download.microsoft.com](http://download.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-141">Use these steps tooupgrade your cluster tooa supported version if your cluster nodes do not have Internet connectivity too[http://download.microsoft.com](http://download.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="1ff1d-142">Si vous utilisez un cluster qui n’est pas connecté toohello Internet, vous devez toomonitor hello Service Fabric team blog toolearn sur une nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-142">If you are running a cluster that is not connected toohello Internet, you will have toomonitor hello Service Fabric team blog toolearn about a new release.</span></span> <span data-ttu-id="1ff1d-143">système de Hello n’affiche pas une tooalert d’avertissement de contrôle d’intégrité cluster d’une nouvelle version.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-143">hello system does not show a cluster health warning tooalert you of a new release.</span></span>  
>
>

#### <a name="auto-provisioning-vs-manual-provisioning"></a><span data-ttu-id="1ff1d-144">Approvisionnement automatique vs. approvisionnement manuel</span><span class="sxs-lookup"><span data-stu-id="1ff1d-144">Auto Provisioning vs Manual Provisioning</span></span>
<span data-ttu-id="1ff1d-145">téléchargement automatique tooenable et inscription pour la dernière version du code hello, configurer le Service de mise à jour de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-145">tooenable automatic downloading and registration for hello latest code version, set up Service Fabric Update Service.</span></span> <span data-ttu-id="1ff1d-146">Consultez toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt à l’intérieur de hello [Package autonome](service-fabric-cluster-standalone-package-contents.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-146">Refer toohello Tools\ServiceFabricUpdateService.zip\Readme_InstructionsAndHowTos.txt inside hello [Standalone Package](service-fabric-cluster-standalone-package-contents.md) for instructions.</span></span>
<span data-ttu-id="1ff1d-147">Pour un processus manuel, suivez les instructions de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-147">For manual process, follow hello instructions below.</span></span>

<span data-ttu-id="1ff1d-148">Modifiez votre hello de tooset de configuration de cluster suivant toofalse de propriété avant de commencer une mise à niveau de la configuration.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-148">Modify your cluster configuration tooset hello following property toofalse before you start a configuration upgrade.</span></span>

        "fabricClusterAutoupgradeEnabled": false,

<span data-ttu-id="1ff1d-149">Consultez trop[ServiceFabricClusterConfigurationUpgrade de début PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-149">Refer too[Start-ServiceFabricClusterConfigurationUpgrade PS cmd ](https://msdn.microsoft.com/en-us/library/mt788302.aspx) for usage details.</span></span> <span data-ttu-id="1ff1d-150">Assurez-vous que tooupdate 'clusterConfigurationVersion' dans votre JSON avant de commencer la mise à niveau de la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-150">Make sure tooupdate 'clusterConfigurationVersion' in your JSON before you start hello configuration upgrade.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

#### <a name="cluster-upgrade-workflow"></a><span data-ttu-id="1ff1d-151">Flux de travail de mise à niveau de cluster</span><span class="sxs-lookup"><span data-stu-id="1ff1d-151">Cluster upgrade workflow</span></span>

1. <span data-ttu-id="1ff1d-152">Exécutez Get-ServiceFabricClusterUpgrade à partir d’un des nœuds des clusters de hello hello et notez hello TargetCodeVersion.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-152">Run Get-ServiceFabricClusterUpgrade from one of hello nodes in hello cluster and note hello TargetCodeVersion.</span></span>
2. <span data-ttu-id="1ff1d-153">Suit hello exécution à partir d’un toolist d’ordinateur connecté internet tous les mettre à niveau des versions compatibles avec la version actuelle de hello et télécharger les hello correspondant du package à partir des liens de téléchargement associé hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-153">Run hello following from an internet connected machine toolist all upgrade compatible versions with hello current version and download hello corresponding package from hello associated download links.</span></span>

    ```powershell

    ###### Get list of all upgrade compatible packages  
    Get-ServiceFabricRuntimeUpgradeVersion -BaseVersion <TargetCodeVersion as noted in Step 1> 
    ```

3. <span data-ttu-id="1ff1d-154">Se connecter toohello cluster à partir de n’importe quel ordinateur qui a accès tooall hello machines d’administrateur sont répertoriés en tant que nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-154">Connect toohello cluster from any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster.</span></span> <span data-ttu-id="1ff1d-155">ordinateur Hello que ce script est exécuté sur n’a pas de partie toobe du cluster de hello</span><span class="sxs-lookup"><span data-stu-id="1ff1d-155">hello machine that this script is run on does not have toobe part of hello cluster</span></span>

    ```powershell

   ###### Get hello list of available Service Fabric versions
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file including hello path tooit> -ImageStoreConnectionString "fabric:ImageStore"

   ###### Here is a filled-out example
    Copy-ServiceFabricClusterPackage -Code -CodePackagePath .\MicrosoftAzureServiceFabric.5.3.301.9590.cab -ImageStoreConnectionString "fabric:ImageStore"

    ```
4. <span data-ttu-id="1ff1d-156">Copiez hello téléchargé package dans le magasin d’images hello cluster.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-156">Copy hello downloaded package into hello cluster image store.</span></span>

5. <span data-ttu-id="1ff1d-157">Inscrire les package hello copié.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-157">Register hello copied package.</span></span>

    ```powershell

    ###### Get hello list of available Service Fabric versions
    Register-ServiceFabricClusterPackage -Code -CodePackagePath <name of hello .cab file>

    ###### Here is a filled-out example
    Register-ServiceFabricClusterPackage -Code -CodePackagePath MicrosoftAzureServiceFabric.5.3.301.9590.cab

     ```
6. <span data-ttu-id="1ff1d-158">Démarrez une version disponible tooan mise à niveau de cluster.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-158">Start a cluster upgrade tooan available version.</span></span>

    ```Powershell

    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion <codeversion#> -Monitored -FailureAction Rollback

    ###### Here is a filled-out example
    Start-ServiceFabricClusterUpgrade -Code -CodePackageVersion 5.3.301.9590 -Monitored -FailureAction Rollback

    ```
   <span data-ttu-id="1ff1d-159">Vous pouvez surveiller la progression de hello de mise à niveau de hello sur Service Fabric Explorer, ou vous pouvez exécuter hello suivant de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-159">You can monitor hello progress of hello upgrade on Service Fabric Explorer, or you can run hello following PowerShell command.</span></span>

    ```powershell

    Get-ServiceFabricClusterUpgrade
    ```

    <span data-ttu-id="1ff1d-160">Si les stratégies d’intégrité de cluster hello ne sont pas remplies, mise à niveau hello est restaurée.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-160">If hello cluster health policies are not met, hello upgrade is rolled back.</span></span> <span data-ttu-id="1ff1d-161">toospecify des stratégies de contrôle d’intégrité personnalisé pour hello **Start-ServiceFabricClusterUpgrade** command, consultez la documentation de hello pour [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-161">toospecify custom health policies for hello **Start-ServiceFabricClusterUpgrade** command, see hello documentation for [Start-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/library/mt125872.aspx).</span></span>

<span data-ttu-id="1ff1d-162">Après avoir résolu les problèmes de hello qui a provoqué la restauration hello, lancer mise à niveau hello à nouveau en suivant hello mêmes étapes comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-162">After you fix hello issues that resulted in hello rollback, initiate hello upgrade again by following hello same steps as previously described.</span></span>


## <a name="upgrade-hello-cluster-configuration"></a><span data-ttu-id="1ff1d-163">Mise à niveau de la configuration de cluster hello</span><span class="sxs-lookup"><span data-stu-id="1ff1d-163">Upgrade hello cluster configuration</span></span>
<span data-ttu-id="1ff1d-164">Avant de vous lancez la mise à niveau de la configuration hello, vous pouvez tester votre nouveau json de configuration de cluster en exécutant un script powershell de hello dans le package autonome de hello.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-164">Before you initiate hello configuration upgrade, you can test your new cluster configuration json by running hello powershell script in hello standalone package.</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File>

```
<span data-ttu-id="1ff1d-165">ou</span><span class="sxs-lookup"><span data-stu-id="1ff1d-165">or</span></span>

```powershell

    TestConfiguration.ps1 -ClusterConfigFilePath <Path toohello new Configuration File> -OldClusterConfigFilePath <Path toohello old Configuration File> -FabricRuntimePackagePath <Path toohello .cab file which you want tootest hello configuration against>

```

<span data-ttu-id="1ff1d-166">Certaines configurations ne peuvent pas être mises à niveau, notamment les points de terminaison, le nom du cluster, l’IP du nœud, etc. Cela json de configuration de cluster nouvelle hello contre hello ancien de test et générer des erreurs dans la fenêtre de Powershell hello s’il existe un problème.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-166">Some configurations can't be upgraded, such as endpoints, cluster name, node IP, etc. This will test hello new cluster configuration json against hello old one and throw errors in hello Powershell window if there is any issue.</span></span>

<span data-ttu-id="1ff1d-167">mise à niveau de cluster configuration tooupgrade hello, exécutez **Start-ServiceFabricClusterConfigurationUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-167">tooupgrade hello cluster configuration upgrade, run **Start-ServiceFabricClusterConfigurationUpgrade**.</span></span> <span data-ttu-id="1ff1d-168">mise à niveau de la configuration Hello est le domaine de mise à niveau traité par le domaine de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-168">hello configuration upgrade is processed upgrade domain by upgrade domain.</span></span>

```powershell

    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

```

### <a name="cluster-certificate-config-upgrade"></a><span data-ttu-id="1ff1d-169">Mise à niveau de la configuration du certificat de cluster</span><span class="sxs-lookup"><span data-stu-id="1ff1d-169">Cluster certificate config upgrade</span></span>  
<span data-ttu-id="1ff1d-170">Certificat de cluster est utilisé pour l’authentification entre les nœuds de cluster, afin de substituer des certificats de hello doit être effectuée avec prudence, car échec bloquera communication hello entre les nœuds de cluster.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-170">Cluster certificate is used for authentication between cluster nodes, so hello certificate roll over should be performed with extra caution because failure will block hello communication among cluster nodes.</span></span>  
<span data-ttu-id="1ff1d-171">Techniquement, trois options sont prises en charge :</span><span class="sxs-lookup"><span data-stu-id="1ff1d-171">Technically, three options are supported:</span></span>  

1. <span data-ttu-id="1ff1d-172">Mise à niveau de certificat unique : chemin d’accès de la mise à niveau hello est « certificat (principal) -> B de certificat (principal) -> C de certificat (principal) ->...'.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-172">Single certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate B (Primary) -> Certificate C (Primary) -> ...'.</span></span>   
2. <span data-ttu-id="1ff1d-173">Double mise à niveau de certificat : chemin d’accès de la mise à niveau hello est « certificat (principal) -> certificats (principal) et B (secondaire) -> B de certificat (principal) -> B de certificat (principal) et C (secondaire) -> C de certificat (principal) ->...'.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-173">Double certificate upgrade: hello upgrade path is 'Certificate A (Primary) -> Certificate A (Primary) and B (Secondary) -> Certificate B (Primary) -> Certificate B (Primary) and C (Secondary) -> Certificate C (Primary) -> ...'.</span></span>
3. <span data-ttu-id="1ff1d-174">Mise à niveau du type de certificat : configuration de certificats basée sur Thumbprint <> configuration de certificats basée sur CommonName.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-174">Certificate type upgrade: Thumbprint-based certificate configuration <-> CommonName-based certificate configuration.</span></span> <span data-ttu-id="1ff1d-175">Par exemple, certificat Thumbprint A (Principal) et Thumbprint B (Secondaire) -> certificat CommonName C.</span><span class="sxs-lookup"><span data-stu-id="1ff1d-175">For example, Certificate Thumbprint A (Primary) and Thumbprint B (Secondary) -> Certificate CommonName C.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1ff1d-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ff1d-176">Next steps</span></span>
* <span data-ttu-id="1ff1d-177">Découvrez comment toocustomize certains [les paramètres de cluster Service Fabric](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-177">Learn how toocustomize some [Service Fabric cluster settings](service-fabric-cluster-fabric-settings.md).</span></span>
* <span data-ttu-id="1ff1d-178">Découvrez comment trop[mettre à l’échelle et l’extraction de votre cluster](service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-178">Learn how too[scale your cluster in and out](service-fabric-cluster-scale-up-down.md).</span></span>
* <span data-ttu-id="1ff1d-179">Découvrez les [mises à niveau d’applications](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1ff1d-179">Learn about [application upgrades](service-fabric-application-upgrade.md).</span></span>

<!--Image references-->
[getfabversions]: ./media/service-fabric-cluster-upgrade-windows-server/getfabversions.PNG
