---
title: "Développement d’une action de script avec HDInsight basé sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment utiliser des scripts Bash pour personnaliser des clusters HDInsight basés sur Linux. La fonctionnalité d’action de script de HDInsights vous permet d’exécuter des scripts pendant ou après la création de cluster. Vous pouvez utiliser des scripts pour modifier les paramètres de configuration d’un cluster ou installer un logiciel supplémentaire."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="58e34-105">Développement d’actions de script avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-105">Script action development with HDInsight</span></span>

<span data-ttu-id="58e34-106">Découvrez comment personnaliser votre cluster HDInsight à l’aide de scripts bash.</span><span class="sxs-lookup"><span data-stu-id="58e34-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="58e34-107">Les actions de script sont un moyen de personnaliser HDInsight pendant ou après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58e34-108">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Linux.</span><span class="sxs-lookup"><span data-stu-id="58e34-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="58e34-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="58e34-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="58e34-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="58e34-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="58e34-111">Définition des actions de script</span><span class="sxs-lookup"><span data-stu-id="58e34-111">What are script actions</span></span>

<span data-ttu-id="58e34-112">Les actions de script sont des scripts d'interpréteur de commandes qu’Azure exécute sur les nœuds de cluster pour apporter des modifications de configuration ou installer des logiciels.</span><span class="sxs-lookup"><span data-stu-id="58e34-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="58e34-113">Une action de script est exécutée en tant qu’administrateur et offre des droits d’accès complets aux nœuds du cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="58e34-114">Les actions de script peuvent être appliquées selon les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e34-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="58e34-115">Utilisez cette méthode pour appliquer un script...</span><span class="sxs-lookup"><span data-stu-id="58e34-115">Use this method to apply a script...</span></span> | <span data-ttu-id="58e34-116">Pendant la création du cluster...</span><span class="sxs-lookup"><span data-stu-id="58e34-116">During cluster creation...</span></span> | <span data-ttu-id="58e34-117">Sur un cluster en cours d'exécution...</span><span class="sxs-lookup"><span data-stu-id="58e34-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="58e34-118">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="58e34-118">Azure portal</span></span> |<span data-ttu-id="58e34-119">✓ </span><span class="sxs-lookup"><span data-stu-id="58e34-119">✓</span></span> |<span data-ttu-id="58e34-120">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-120">✓</span></span> |
| <span data-ttu-id="58e34-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58e34-121">Azure PowerShell</span></span> |<span data-ttu-id="58e34-122">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-122">✓</span></span> |<span data-ttu-id="58e34-123">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-123">✓</span></span> |
| <span data-ttu-id="58e34-124">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="58e34-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="58e34-125">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-125">✓</span></span> |
| <span data-ttu-id="58e34-126">Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="58e34-127">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-127">✓</span></span> |<span data-ttu-id="58e34-128">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-128">✓</span></span> |
| <span data-ttu-id="58e34-129">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="58e34-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="58e34-130">✓</span><span class="sxs-lookup"><span data-stu-id="58e34-130">✓</span></span> |&nbsp; |

<span data-ttu-id="58e34-131">Pour plus d’informations sur l’utilisation de ces méthodes pour appliquer des actions de script, consultez [Personnalisation de clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="58e34-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="58e34-132"><a name="bestPracticeScripting"></a>Meilleures pratiques relatives au développement de scripts</span><span class="sxs-lookup"><span data-stu-id="58e34-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="58e34-133">Quand vous développez un script personnalisé pour un cluster HDInsight, tenez compte des meilleures pratiques suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e34-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="58e34-134">Rechercher la version Hadoop</span><span class="sxs-lookup"><span data-stu-id="58e34-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="58e34-135">Cibler la version du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="58e34-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="58e34-136">Fournir des liens stables vers les ressources de script</span><span class="sxs-lookup"><span data-stu-id="58e34-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="58e34-137">Utiliser des ressources précompilées</span><span class="sxs-lookup"><span data-stu-id="58e34-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="58e34-138">S’assurer que le script de personnalisation du cluster est idempotent</span><span class="sxs-lookup"><span data-stu-id="58e34-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="58e34-139">Garantir la haute disponibilité de l’architecture du cluster</span><span class="sxs-lookup"><span data-stu-id="58e34-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="58e34-140">Configurer les composants personnalisés pour utiliser le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="58e34-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="58e34-141">Écrire des informations sur STDOUT et STDERR</span><span class="sxs-lookup"><span data-stu-id="58e34-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="58e34-142">Enregistrer des fichiers au format ASCII avec les fins de ligne LF</span><span class="sxs-lookup"><span data-stu-id="58e34-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="58e34-143">Utilisation de la logique de nouvelle tentative pour récupérer après une erreur temporaire</span><span class="sxs-lookup"><span data-stu-id="58e34-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="58e34-144">Les actions de script doivent se terminer dans les 60 minutes, ou le processus échoue.</span><span class="sxs-lookup"><span data-stu-id="58e34-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="58e34-145">Lors de l’approvisionnement du nœud, le script s’exécute en même temps que les autres processus d'installation et de configuration.</span><span class="sxs-lookup"><span data-stu-id="58e34-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="58e34-146">En raison de cette concurrence pour les ressources, par exemple au niveau du temps processeur ou de la bande passante, l’exécution du script risque de prendre plus de temps que dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="58e34-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="58e34-147"><a name="bPS1"></a>Rechercher la version Hadoop</span><span class="sxs-lookup"><span data-stu-id="58e34-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="58e34-148">Différentes versions de HDInsight sont équipées de différentes versions de services Hadoop et des composants installés.</span><span class="sxs-lookup"><span data-stu-id="58e34-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="58e34-149">Si votre script attend une version de service ou de composant spécifique, vous devez utiliser uniquement le script avec la version de HDInsight qui inclut les composants requis.</span><span class="sxs-lookup"><span data-stu-id="58e34-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="58e34-150">Vous trouverez des informations sur les versions de composant incluses dans HDInsight à l’aide du document [Contrôle des versions du composant HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="58e34-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="58e34-151"><a name="bps10"></a> Cibler la version du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="58e34-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="58e34-152">HDInsight sous Linux est basé sur la distribution Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="58e34-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="58e34-153">Les différentes versions de HDInsight s’appuient sur des versions différentes d’Ubuntu, ce qui peut avoir une incidence sur le comportement de votre script.</span><span class="sxs-lookup"><span data-stu-id="58e34-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="58e34-154">Par exemple, HDInsight 3.4 et les versions antérieures sont basées sur des versions Ubuntu qui utilisent Upstart.</span><span class="sxs-lookup"><span data-stu-id="58e34-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="58e34-155">La version 3.5 est basée sur 16.04 Ubuntu, qui utilise Systemd.</span><span class="sxs-lookup"><span data-stu-id="58e34-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="58e34-156">Systemd et Upstart reposent sur différentes commandes, donc votre script doit être écrit pour travailler avec les deux.</span><span class="sxs-lookup"><span data-stu-id="58e34-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="58e34-157">L’autre différence majeure entre HDInsight 3.4 et 3.5 résident dans le fait que `JAVA_HOME` pointe désormais vers Java 8.</span><span class="sxs-lookup"><span data-stu-id="58e34-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="58e34-158">Vous pouvez vérifier la version du système d’exploitation à l’aide de `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="58e34-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="58e34-159">Le code suivant montre comment déterminer si le script est exécuté sur Ubuntu 14 ou 16 :</span><span class="sxs-lookup"><span data-stu-id="58e34-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="58e34-160">Le script complet contenant ces extraits de code est consultable à l’adresse https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="58e34-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="58e34-161">Pour la version d’Ubuntu utilisée par HDInsight, consultez le document [Version du composant HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="58e34-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="58e34-162">Pour comprendre les différences entre Systemd et Upstart, consultez [Systemd pour les utilisateurs Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="58e34-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="58e34-163"><a name="bPS2"></a>Fournir des liens stables vers les ressources de script</span><span class="sxs-lookup"><span data-stu-id="58e34-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="58e34-164">Le script et les ressources associées doivent rester disponibles pendant toute la durée de vie du cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="58e34-165">Ces ressources sont requises si de nouveaux nœuds sont ajoutés au cluster pendant les opérations de mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="58e34-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="58e34-166">La meilleure pratique consiste à tout télécharger et à tout archiver dans un compte de stockage Azure de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="58e34-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58e34-167">Le compte de stockage utilisé doit être le compte de stockage par défaut du cluster ou un conteneur public en lecture seule d’un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="58e34-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="58e34-168">Par exemple, les exemples fournis par Microsoft sont stockés dans le compte de stockage [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="58e34-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="58e34-169">Il s’agit d’un conteneur public en lecture seule géré par l’équipe de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e34-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="58e34-170"><a name="bPS4"></a>Utiliser des ressources précompilées</span><span class="sxs-lookup"><span data-stu-id="58e34-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="58e34-171">Pour réduire le temps nécessaire à l’exécution du script, évitez les opérations qui compilent des ressources depuis le code source.</span><span class="sxs-lookup"><span data-stu-id="58e34-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="58e34-172">Par exemple, précompilez les ressources et stockez-les dans un compte de stockage de blobs Azure dans le même centre de données que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e34-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="58e34-173"><a name="bPS3"></a>S’assurer que le script de personnalisation du cluster est idempotent</span><span class="sxs-lookup"><span data-stu-id="58e34-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="58e34-174">Les scripts doivent être idempotents.</span><span class="sxs-lookup"><span data-stu-id="58e34-174">Scripts must be idempotent.</span></span> <span data-ttu-id="58e34-175">Si le script est exécuté plusieurs fois, il doit retourner le cluster au même état à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="58e34-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="58e34-176">Par exemple, un script qui modifie les fichiers de configuration ne doit pas ajouter d’entrées en double s’il est exécuté plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="58e34-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="58e34-177"><a name="bPS5"></a>Garantir la haute disponibilité de l’architecture du cluster</span><span class="sxs-lookup"><span data-stu-id="58e34-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="58e34-178">Les clusters HDInsight basés sur Linux proposent deux nœuds principaux actifs au sein du cluster, et les actions de script sont exécutées sur les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="58e34-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="58e34-179">Si les composants que vous installez n'attendent qu’un seul nœud principal, n’installez pas les composants sur les deux nœuds principaux.</span><span class="sxs-lookup"><span data-stu-id="58e34-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58e34-180">Les services fournis dans le cadre de HDInsight sont conçus pour basculer entre les deux nœuds principaux si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="58e34-181">Cette fonctionnalité n’est pas étendue aux composants personnalisés installés à l’aide d’actions de script.</span><span class="sxs-lookup"><span data-stu-id="58e34-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="58e34-182">Si vous avez besoin que les composants personnalisés soient très disponibles, vous devez implémenter votre propre mécanisme de basculement.</span><span class="sxs-lookup"><span data-stu-id="58e34-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="58e34-183"><a name="bPS6"></a>Configurer les composants personnalisés pour utiliser le stockage d’objets blob Azure</span><span class="sxs-lookup"><span data-stu-id="58e34-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="58e34-184">Les composants que vous installez sur le cluster peuvent être configurés par défaut pour utiliser le stockage HDFS (Hadoop Distributed File System).</span><span class="sxs-lookup"><span data-stu-id="58e34-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="58e34-185">HDInsight utilise Stockage Azure ou Data Lake Store comme magasin par défaut.</span><span class="sxs-lookup"><span data-stu-id="58e34-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="58e34-186">Chacun d’eux fournit un système de fichiers compatible HDFS qui rend persistantes les données même en cas de suppression du cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="58e34-187">Vous devrez peut-être configurer les composants que vous installez pour utiliser WASB ou ADL au lieu de HDFS.</span><span class="sxs-lookup"><span data-stu-id="58e34-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="58e34-188">Pour la plupart des opérations, il est inutile de spécifier le système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="58e34-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="58e34-189">Par exemple, le texte suivant copie le fichier giraph-examples.jar du système de fichiers local vers l’emplacement de stockage du cluster :</span><span class="sxs-lookup"><span data-stu-id="58e34-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="58e34-190">Dans cet exemple, la commande `hdfs` utilise en toute transparence l’emplacement de stockage de cluster par défaut.</span><span class="sxs-lookup"><span data-stu-id="58e34-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="58e34-191">Pour certaines opérations, vous devrez peut-être spécifier l’URI.</span><span class="sxs-lookup"><span data-stu-id="58e34-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="58e34-192">Par exemple, `adl:///example/jars` pour Data Lake Store ou `wasb:///example/jars` pour Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="58e34-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="58e34-193"><a name="bPS7"></a>Écrire des informations sur STDOUT et STDERR</span><span class="sxs-lookup"><span data-stu-id="58e34-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="58e34-194">HDInsight journalise la sortie de script qui est écrite dans STDOUT et STDERR.</span><span class="sxs-lookup"><span data-stu-id="58e34-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="58e34-195">Vous pouvez afficher ces informations à l’aide de l’interface utilisateur web d’Ambari.</span><span class="sxs-lookup"><span data-stu-id="58e34-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="58e34-196">Ambari n’est disponible que si le cluster a été créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="58e34-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="58e34-197">Si vous utilisez une action de script lors de la création du cluster et que la création échoue, consultez la section de dépannage de [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) pour découvrir d’autres façons d’accéder aux informations de journalisation.</span><span class="sxs-lookup"><span data-stu-id="58e34-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="58e34-198">La plupart des utilitaires et des packages d’installation ont déjà écrit des informations dans STDOUT et STDERR. Toutefois, vous pouvez ajouter un enregistrement supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="58e34-199">Pour envoyer du texte à STDOUT, utilisez `echo`.</span><span class="sxs-lookup"><span data-stu-id="58e34-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="58e34-200">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e34-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="58e34-201">Par défaut, `echo` envoie la chaîne vers STDOUT.</span><span class="sxs-lookup"><span data-stu-id="58e34-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="58e34-202">Pour la diriger vers STDERR, ajoutez `>&2` avant `echo`.</span><span class="sxs-lookup"><span data-stu-id="58e34-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="58e34-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="58e34-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="58e34-204">Cela redirige les informations écrites dans STDOUT vers STDERR (2) à la place.</span><span class="sxs-lookup"><span data-stu-id="58e34-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="58e34-205">Pour plus d’informations sur la redirection des E/S, consultez [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="58e34-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="58e34-206">Pour plus d’informations sur l’affichage des informations consignées par les actions de script, voir [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="58e34-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="58e34-207"><a name="bps8"></a> Enregistrer des fichiers au format ASCII avec les fins de ligne LF</span><span class="sxs-lookup"><span data-stu-id="58e34-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="58e34-208">Les scripts d’interpréteur de commandes doivent être stockés au format ASCII, avec des lignes terminées se terminant par LF.</span><span class="sxs-lookup"><span data-stu-id="58e34-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="58e34-209">Les fichiers qui sont stockés au format UTF-8 ou utilisent CRLF comme fin de ligne peuvent échouer avec l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="58e34-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="58e34-210"><a name="bps9"></a> Utilisation de la logique de nouvelle tentative pour récupérer après une erreur temporaire</span><span class="sxs-lookup"><span data-stu-id="58e34-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="58e34-211">Lors du téléchargement de fichiers, de l’installation de packages à l’aide d’apt-get ou d’autres actions qui transmettent des données sur Internet, l’action peut échouer en raison d’erreurs réseau temporaires.</span><span class="sxs-lookup"><span data-stu-id="58e34-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="58e34-212">Par exemple, la ressource distante avec laquelle vous communiquez peut être en train de basculer vers un nœud de secours.</span><span class="sxs-lookup"><span data-stu-id="58e34-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="58e34-213">Pour rendre votre script résistant aux erreurs temporaires, vous pouvez implémenter la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="58e34-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="58e34-214">La fonction suivante montre comment implémenter la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="58e34-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="58e34-215">Elle réessaie l’opération trois fois avant d’échouer.</span><span class="sxs-lookup"><span data-stu-id="58e34-215">It retries the operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="58e34-216">Les exemples suivants montrent comment utiliser cette fonction.</span><span class="sxs-lookup"><span data-stu-id="58e34-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="58e34-217"><a name="helpermethods"></a>Méthodes d'assistance pour les scripts personnalisés</span><span class="sxs-lookup"><span data-stu-id="58e34-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="58e34-218">Les méthodes d’assistance aux actions de script sont des utilitaires que vous pouvez utiliser lors de l’écriture de scripts personnalisés.</span><span class="sxs-lookup"><span data-stu-id="58e34-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="58e34-219">Ces méthodes sont contenues dans le script[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="58e34-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="58e34-220">Pour les télécharger et les utiliser dans le cadre de votre script, utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="58e34-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="58e34-221">Les programmes d’assistance suivants disponibles pour une utilisation dans votre script :</span><span class="sxs-lookup"><span data-stu-id="58e34-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="58e34-222">Utilisation de l’aide</span><span class="sxs-lookup"><span data-stu-id="58e34-222">Helper usage</span></span> | <span data-ttu-id="58e34-223">Description</span><span class="sxs-lookup"><span data-stu-id="58e34-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="58e34-224">Télécharge un fichier de l’URI source vers le chemin d’accès de fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="58e34-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="58e34-225">Par défaut, il ne remplace pas un fichier existant.</span><span class="sxs-lookup"><span data-stu-id="58e34-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="58e34-226">Extrait un fichier tar (à l’aide de `-xf`,) dans le répertoire de destination.</span><span class="sxs-lookup"><span data-stu-id="58e34-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="58e34-227">Lorsqu’il est exécuté sur un nœud principal de cluster, la valeur 1 est renvoyée ; dans le cas contraire, c’est la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="58e34-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="58e34-228">Si le nœud actuel est un nœud de données (worker), la valeur 1 est renvoyée ; dans le cas contraire, c’est la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="58e34-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="58e34-229">Si le nœud actuel est le premier nœud de données (worker) (nommé workernode0,) la valeur 1 est renvoyée ; dans le cas contraire, c’est la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="58e34-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="58e34-230">Renvoie le nom de domaine complet des nœuds principaux dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="58e34-231">Les noms sont séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="58e34-231">Names are comma delimited.</span></span> <span data-ttu-id="58e34-232">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="58e34-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="58e34-233">Obtient le nom de domaine complet du nœud principal primaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="58e34-234">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="58e34-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="58e34-235">Obtient le nom de domaine complet du nœud principal secondaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="58e34-236">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="58e34-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="58e34-237">Obtient le suffixe numérique du nœud principal primaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="58e34-238">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="58e34-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="58e34-239">Obtient le suffixe numérique du nœud principal secondaire.</span><span class="sxs-lookup"><span data-stu-id="58e34-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="58e34-240">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="58e34-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="58e34-241"><a name="commonusage"></a>Modes d'utilisation courants</span><span class="sxs-lookup"><span data-stu-id="58e34-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="58e34-242">Cette section fournit des conseils sur l'implémentation de certains des modèles d'utilisation courants que vous pouvez rencontrer lors de l'écriture de votre propre script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="58e34-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="58e34-243">Transmission de paramètres vers un script</span><span class="sxs-lookup"><span data-stu-id="58e34-243">Passing parameters to a script</span></span>

<span data-ttu-id="58e34-244">Dans certains cas, votre script peut nécessiter des paramètres.</span><span class="sxs-lookup"><span data-stu-id="58e34-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="58e34-245">Par exemple, vous aurez peut-être besoin du mot de passe d’administrateur pour le cluster lors de l’utilisation de l’API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="58e34-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="58e34-246">Les paramètres transmis au script sont appelés *paramètres positionnels* et sont affectés à `$1` pour ce qui concerne le premier paramètre, `$2` pour le deuxième et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="58e34-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="58e34-247">`$0` contient le nom du script lui-même.</span><span class="sxs-lookup"><span data-stu-id="58e34-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="58e34-248">Les valeurs transmises au script comme paramètres doivent être entourées de guillemets simples (').</span><span class="sxs-lookup"><span data-stu-id="58e34-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="58e34-249">Cela permet de s’assurer que la valeur transmise est traitée comme un littéral.</span><span class="sxs-lookup"><span data-stu-id="58e34-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="58e34-250">Définition des variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="58e34-250">Setting environment variables</span></span>

<span data-ttu-id="58e34-251">La définition d’une variable d’environnement est effectuée de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="58e34-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="58e34-252">Où VARIABLENAME est le nom de la variable.</span><span class="sxs-lookup"><span data-stu-id="58e34-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="58e34-253">Pour accéder à la variable, utilisez `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="58e34-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="58e34-254">Par exemple, pour affecter une valeur fournie par un paramètre de positionnement tel qu’une variable d’environnement nommée PASSWORD, utilisez l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="58e34-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="58e34-255">Lors des accès ultérieurs aux informations, il est possible d’utiliser `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="58e34-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="58e34-256">Les variables d’environnement définies dans le script existent uniquement dans le cadre du script.</span><span class="sxs-lookup"><span data-stu-id="58e34-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="58e34-257">Dans certains cas, vous devrez peut-être ajouter des variables d’environnement de niveau système qui persisteront une fois le script terminé.</span><span class="sxs-lookup"><span data-stu-id="58e34-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="58e34-258">Pour ajouter des variables d’environnement de niveau système, ajoutez la variable à `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="58e34-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="58e34-259">Par exemple, l’instruction suivante ajoute `HADOOP_CONF_DIR` :</span><span class="sxs-lookup"><span data-stu-id="58e34-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="58e34-260">Accès aux emplacements où sont stockés les scripts personnalisés</span><span class="sxs-lookup"><span data-stu-id="58e34-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="58e34-261">Les scripts utilisés pour personnaliser un cluster doivent être stockés dans un des emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="58e34-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="58e34-262">Un __compte de stockage Azure__ qui est associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="58e34-263">Un __compte de stockage supplémentaire__ associé au cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="58e34-264">Une __URI lisible publiquement__.</span><span class="sxs-lookup"><span data-stu-id="58e34-264">A __publicly readable URI__.</span></span> <span data-ttu-id="58e34-265">Par exemple, une URL menant aux données stockées sur OneDrive, Dropbox ou un autre service d’hébergement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="58e34-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="58e34-266">Un compte __Azure Data Lake Store__ est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="58e34-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="58e34-267">Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="58e34-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="58e34-268">Le principal de service que HDInsight utilise pour accéder au Data Lake Store doit avoir accès en lecture au script.</span><span class="sxs-lookup"><span data-stu-id="58e34-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="58e34-269">Les ressources utilisées par le script doivent également être disponibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="58e34-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="58e34-270">Le stockage des fichiers dans un compte de stockage Azure ou Azure Data Lake Store fournit un accès rapide, car tous deux se trouvent dans le réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="58e34-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="58e34-271">Le format d’URI utilisé pour référencer le script diffère selon le service utilisé.</span><span class="sxs-lookup"><span data-stu-id="58e34-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="58e34-272">Pour les comptes de stockage associés au cluster HDInsight, utilisez `wasb://` ou `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="58e34-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="58e34-273">Pour des URI lisibles publiquement, utilisez `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="58e34-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="58e34-274">Pour Data Lake Store, utilisez `adl://`.</span><span class="sxs-lookup"><span data-stu-id="58e34-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="58e34-275">Vérification de la version du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="58e34-275">Checking the operating system version</span></span>

<span data-ttu-id="58e34-276">Différentes versions de HDInsight s’appuient sur des versions spécifiques d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="58e34-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="58e34-277">Il peut exister des différences entre les versions de système d’exploitation que vous devez vérifier dans votre script.</span><span class="sxs-lookup"><span data-stu-id="58e34-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="58e34-278">Par exemple, vous devrez peut-être installer un fichier binaire qui est lié à la version d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="58e34-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="58e34-279">Pour vérifier la version du système d’exploitation, utilisez `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="58e34-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="58e34-280">Par exemple, le script suivant montre comment référencer un fichier tar spécifique selon la version du système d’exploitation :</span><span class="sxs-lookup"><span data-stu-id="58e34-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="58e34-281"><a name="deployScript"></a>Liste de vérification pour le déploiement d'une action de script</span><span class="sxs-lookup"><span data-stu-id="58e34-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="58e34-282">Voici les étapes à suivre avant de déployer des scripts :</span><span class="sxs-lookup"><span data-stu-id="58e34-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="58e34-283">Placez les fichiers qui contiennent les scripts personnalisés dans un emplacement accessible aux nœuds du cluster lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="58e34-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="58e34-284">Par exemple, l’emplacement de stockage par défaut du cluster.</span><span class="sxs-lookup"><span data-stu-id="58e34-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="58e34-285">Les fichiers peuvent également être stockés dans les services d’hébergement lisibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="58e34-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="58e34-286">Vérifiez que le script est impotent.</span><span class="sxs-lookup"><span data-stu-id="58e34-286">Verify that the script is impotent.</span></span> <span data-ttu-id="58e34-287">Ainsi, le script peut être exécuté plusieurs fois sur le même nœud.</span><span class="sxs-lookup"><span data-stu-id="58e34-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="58e34-288">Utilisez un dossier de fichiers temporaires /tmp pour conserver le fichier téléchargé utilisé par les scripts, puis nettoyez-les une fois que les scripts ont été exécutés.</span><span class="sxs-lookup"><span data-stu-id="58e34-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="58e34-289">Si les paramètres au niveau du système d’exploitation ou les fichiers de configuration du service Hadoop sont modifiés, vous pouvez redémarrer les services HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e34-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="58e34-290"><a name="runScriptAction"></a>Comment exécuter une action de script</span><span class="sxs-lookup"><span data-stu-id="58e34-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="58e34-291">Vous pouvez utiliser des actions de script pour personnaliser des clusters HDInsight à l’aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="58e34-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="58e34-292">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="58e34-292">Azure portal</span></span>
* <span data-ttu-id="58e34-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58e34-293">Azure PowerShell</span></span>
* <span data-ttu-id="58e34-294">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="58e34-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="58e34-295">Le kit de développement logiciel (SDK) HDInsight .NET.</span><span class="sxs-lookup"><span data-stu-id="58e34-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="58e34-296">Pour plus d’informations sur l’utilisation de chaque méthode, consultez [Comment utiliser une action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="58e34-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="58e34-297"><a name="sampleScripts"></a>Exemples de scripts personnalisés</span><span class="sxs-lookup"><span data-stu-id="58e34-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="58e34-298">Microsoft fournit des exemples de scripts pour installer des composants sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e34-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="58e34-299">Consultez les liens suivants pour voir d’autres exemples d’action de script.</span><span class="sxs-lookup"><span data-stu-id="58e34-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="58e34-300">Installer et utiliser Hue sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="58e34-301">Installer et utiliser Solr sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="58e34-302">Installer et utiliser Giraph sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="58e34-303">Installer ou mettre à niveau Mono sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="58e34-304">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="58e34-304">Troubleshooting</span></span>

<span data-ttu-id="58e34-305">Voici les erreurs que vous pouvez rencontrer lorsque vous utilisez les scripts que vous avez développé :</span><span class="sxs-lookup"><span data-stu-id="58e34-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="58e34-306">**Erreur** : `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="58e34-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="58e34-307">Parfois suivi par `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="58e34-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="58e34-308">*Cause*: cette erreur se produit lorsque les lignes d’un script se terminent par CRLF.</span><span class="sxs-lookup"><span data-stu-id="58e34-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="58e34-309">Les systèmes UNIX attendent seulement LF comme fin de ligne.</span><span class="sxs-lookup"><span data-stu-id="58e34-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="58e34-310">Ce problème se produit souvent lorsque le script est créé dans un environnement Windows, car CRLF est une fin de ligne commune à de nombreux éditeurs de texte sous Windows.</span><span class="sxs-lookup"><span data-stu-id="58e34-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="58e34-311">*Résolution*: si c’est une option dans votre éditeur de texte, sélectionnez le format Unix ou LF comme fin de ligne.</span><span class="sxs-lookup"><span data-stu-id="58e34-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="58e34-312">Vous pouvez également utiliser les commandes suivantes sur un système Unix pour changer la séquence CRLF en LF :</span><span class="sxs-lookup"><span data-stu-id="58e34-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="58e34-313">Les commandes suivantes sont à peu près équivalentes dans la mesure où elles doivent changer les fins de ligne CRLF en LF.</span><span class="sxs-lookup"><span data-stu-id="58e34-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="58e34-314">Sélectionnez-en une basée sur les utilitaires disponibles sur votre système.</span><span class="sxs-lookup"><span data-stu-id="58e34-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="58e34-315">Commande</span><span class="sxs-lookup"><span data-stu-id="58e34-315">Command</span></span> | <span data-ttu-id="58e34-316">Remarques</span><span class="sxs-lookup"><span data-stu-id="58e34-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="58e34-317">Le fichier d’origine est sauvegardé avec une extension .BAK</span><span class="sxs-lookup"><span data-stu-id="58e34-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="58e34-318">OUTFILE contient une version avec des terminaisons LF uniquement</span><span class="sxs-lookup"><span data-stu-id="58e34-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="58e34-319">Modifie directement le fichier</span><span class="sxs-lookup"><span data-stu-id="58e34-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="58e34-320">OUTFILE contient une version avec des terminaisons LF uniquement.</span><span class="sxs-lookup"><span data-stu-id="58e34-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="58e34-321">**Erreur** : `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="58e34-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="58e34-322">*Cause*: cette erreur se produit lorsque le script a été enregistré en tant qu’UTF-8 avec une marque d’ordre d’octet (BOM).</span><span class="sxs-lookup"><span data-stu-id="58e34-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="58e34-323">*Résolution*: enregistrer le fichier au format ASCII ou UTF-8 sans marque d’ordre d’octet.</span><span class="sxs-lookup"><span data-stu-id="58e34-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="58e34-324">Vous pouvez également utiliser la commande suivante sur un système Linux ou Unix pour créer un fichier sans marque d’ordre d’octet :</span><span class="sxs-lookup"><span data-stu-id="58e34-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="58e34-325">Remplacez `INFILE` par le fichier contenant la marque d’ordre d’octet.</span><span class="sxs-lookup"><span data-stu-id="58e34-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="58e34-326">`OUTFILE` doit être un nouveau nom de fichier contenant le script sans la marque d’ordre d’octet.</span><span class="sxs-lookup"><span data-stu-id="58e34-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="58e34-327"><a name="seeAlso"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="58e34-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="58e34-328">Découvrez comment [Personnaliser des clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="58e34-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="58e34-329">Utilisez la [Référence du Kit de développement logiciel (SDK) .NET HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) pour en savoir plus sur la création d’applications .NET qui gèrent HDInsight</span><span class="sxs-lookup"><span data-stu-id="58e34-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="58e34-330">Utilisez l’ [API REST HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) pour savoir comment utiliser REST pour effectuer des actions de gestion sur des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="58e34-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
