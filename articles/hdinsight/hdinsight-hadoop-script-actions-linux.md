---
title: "développement de l’action aaaScript hdinsight basés sur Linux - Azure | Documents Microsoft"
description: "Découvrez comment toouse Bash scripts toocustomize basés sur Linux de HDInsight clusters. fonctionnalité d’action de script Hello de HDInsight vous permet de toorun scripts pendant ou après la création du cluster. Les scripts peuvent être toochange utilisé les paramètres de configuration de cluster ou installer des logiciels supplémentaires."
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
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="055db-105">Développement d’actions de script avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-105">Script action development with HDInsight</span></span>

<span data-ttu-id="055db-106">Découvrez comment votre cluster HDInsight à l’aide Bash toocustomize des scripts.</span><span class="sxs-lookup"><span data-stu-id="055db-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="055db-107">Actions de script sont un moyen de toocustomize HDInsight pendant ou après la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="055db-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="055db-108">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="055db-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="055db-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="055db-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="055db-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="055db-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="055db-111">Définition des actions de script</span><span class="sxs-lookup"><span data-stu-id="055db-111">What are script actions</span></span>

<span data-ttu-id="055db-112">Actions de script sont des scripts Bash Azure s’exécute sur les modifications de configuration hello cluster nœuds toomake ou installer des logiciels.</span><span class="sxs-lookup"><span data-stu-id="055db-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="055db-113">Une action de script est exécutée en tant que racine et fournit un accès complet de nœuds de cluster toohello droits.</span><span class="sxs-lookup"><span data-stu-id="055db-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="055db-114">Actions de script peuvent être appliquées via hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="055db-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="055db-115">Utilisez cette méthode de tooapply un script...</span><span class="sxs-lookup"><span data-stu-id="055db-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="055db-116">Pendant la création du cluster...</span><span class="sxs-lookup"><span data-stu-id="055db-116">During cluster creation...</span></span> | <span data-ttu-id="055db-117">Sur un cluster en cours d'exécution...</span><span class="sxs-lookup"><span data-stu-id="055db-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="055db-118">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="055db-118">Azure portal</span></span> |<span data-ttu-id="055db-119">✓ </span><span class="sxs-lookup"><span data-stu-id="055db-119">✓</span></span> |<span data-ttu-id="055db-120">✓</span><span class="sxs-lookup"><span data-stu-id="055db-120">✓</span></span> |
| <span data-ttu-id="055db-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="055db-121">Azure PowerShell</span></span> |<span data-ttu-id="055db-122">✓</span><span class="sxs-lookup"><span data-stu-id="055db-122">✓</span></span> |<span data-ttu-id="055db-123">✓</span><span class="sxs-lookup"><span data-stu-id="055db-123">✓</span></span> |
| <span data-ttu-id="055db-124">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="055db-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="055db-125">✓</span><span class="sxs-lookup"><span data-stu-id="055db-125">✓</span></span> |
| <span data-ttu-id="055db-126">Kit de développement logiciel (SDK) .NET de HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="055db-127">✓</span><span class="sxs-lookup"><span data-stu-id="055db-127">✓</span></span> |<span data-ttu-id="055db-128">✓</span><span class="sxs-lookup"><span data-stu-id="055db-128">✓</span></span> |
| <span data-ttu-id="055db-129">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="055db-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="055db-130">✓</span><span class="sxs-lookup"><span data-stu-id="055db-130">✓</span></span> |&nbsp; |

<span data-ttu-id="055db-131">Pour plus d’informations sur l’utilisation de ces actions de script tooapply méthodes, consultez [HDInsight de personnaliser des clusters à l’aide des actions de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="055db-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="055db-132"><a name="bestPracticeScripting"></a>Meilleures pratiques relatives au développement de scripts</span><span class="sxs-lookup"><span data-stu-id="055db-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="055db-133">Lorsque vous développez un script personnalisé pour un cluster HDInsight, il existe plusieurs meilleures tookeep de pratiques à l’esprit :</span><span class="sxs-lookup"><span data-stu-id="055db-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="055db-134">Version de Hadoop hello cible</span><span class="sxs-lookup"><span data-stu-id="055db-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="055db-135">Cibler hello Version du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="055db-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="055db-136">Fournir stable lie les ressources tooscript</span><span class="sxs-lookup"><span data-stu-id="055db-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="055db-137">Utiliser des ressources précompilées</span><span class="sxs-lookup"><span data-stu-id="055db-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="055db-138">Assurez-vous que le script de personnalisation de cluster hello est idempotente</span><span class="sxs-lookup"><span data-stu-id="055db-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="055db-139">Garantir une haute disponibilité de l’architecture de cluster hello</span><span class="sxs-lookup"><span data-stu-id="055db-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="055db-140">Configurer le stockage d’objets Blob Azure hello des composants personnalisés toouse</span><span class="sxs-lookup"><span data-stu-id="055db-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="055db-141">Écrire des informations tooSTDOUT et STDERR</span><span class="sxs-lookup"><span data-stu-id="055db-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="055db-142">Enregistrer des fichiers au format ASCII avec les fins de ligne LF</span><span class="sxs-lookup"><span data-stu-id="055db-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="055db-143">Utilisez toorecover logique de nouvelle tentative d’erreurs transitoires</span><span class="sxs-lookup"><span data-stu-id="055db-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="055db-144">Actions de script doivent se terminer dans les 60 minutes ou hello processus échoue.</span><span class="sxs-lookup"><span data-stu-id="055db-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="055db-145">Lors de la configuration de nœud, script de hello s’exécute en même temps que d’autres processus d’installation et la configuration.</span><span class="sxs-lookup"><span data-stu-id="055db-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="055db-146">Concurrence pour les ressources, telles que la bande passante du réseau ou de temps processeur peut entraîner hello script tootake plu toofinish qu’il ne le fait dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="055db-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="055db-147"><a name="bPS1"></a>Version de Hadoop hello cible</span><span class="sxs-lookup"><span data-stu-id="055db-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="055db-148">Différentes versions de HDInsight sont équipées de différentes versions de services Hadoop et des composants installés.</span><span class="sxs-lookup"><span data-stu-id="055db-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="055db-149">Si votre script attend une version spécifique d’un service ou un composant, vous devez uniquement utiliser le script de hello avec version hello de HDInsight qui inclut les composants requis de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="055db-150">Vous trouverez plus d’informations sur les versions des composants inclus dans HDInsight à l’aide de hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="055db-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="055db-151"><a name="bps10"></a>Version de hello du système d’exploitation cible</span><span class="sxs-lookup"><span data-stu-id="055db-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="055db-152">HDInsight de basés sur Linux est basée sur hello distribution Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="055db-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="055db-153">Les différentes versions de HDInsight s’appuient sur des versions différentes d’Ubuntu, ce qui peut avoir une incidence sur le comportement de votre script.</span><span class="sxs-lookup"><span data-stu-id="055db-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="055db-154">Par exemple, HDInsight 3.4 et les versions antérieures sont basées sur des versions Ubuntu qui utilisent Upstart.</span><span class="sxs-lookup"><span data-stu-id="055db-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="055db-155">La version 3.5 est basée sur 16.04 Ubuntu, qui utilise Systemd.</span><span class="sxs-lookup"><span data-stu-id="055db-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="055db-156">Systemd et Upstart s’appuient sur les différentes commandes pour votre script doit être écrits toowork avec les deux.</span><span class="sxs-lookup"><span data-stu-id="055db-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="055db-157">Autre différence importante entre HDInsight 3.4 et 3.5 `JAVA_HOME` pointe tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="055db-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="055db-158">Vous pouvez vérifier la version de hello du système d’exploitation à l’aide de `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="055db-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="055db-159">Hello de code suivant montre comment toodetermine si hello script s’exécute sur Ubuntu 14 ou 16 :</span><span class="sxs-lookup"><span data-stu-id="055db-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="055db-160">Vous trouverez le script complet hello qui contient ces extraits de code à https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="055db-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="055db-161">Pour la version hello Ubuntu est utilisé par HDInsight, consultez hello [HDInsight la version du composant](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="055db-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="055db-162">différences de hello toounderstand entre Systemd et Upstart, consultez [Systemd pour les utilisateurs de Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="055db-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="055db-163"><a name="bPS2"></a>Fournir stable lie les ressources tooscript</span><span class="sxs-lookup"><span data-stu-id="055db-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="055db-164">Hello script et des ressources associées doivent rester disponibles pour l’ensemble de la durée de vie hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="055db-165">Ces ressources sont requises si de nouveaux nœuds sont ajoutés toohello cluster pendant les opérations de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="055db-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="055db-166">meilleure pratique de Hello est toodownload et archivez tous les éléments dans un compte de stockage Azure de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="055db-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="055db-167">compte de stockage Hello utilisé doit être le compte de stockage par défaut hello pour le cluster de hello ou un conteneur public en lecture seule sur un autre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="055db-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="055db-168">Par exemple, les exemples hello fournis par Microsoft sont stockés dans hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="055db-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="055db-169">Il s’agit d’un conteneur public en lecture seule géré par l’équipe de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="055db-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="055db-170"><a name="bPS4"></a>Utiliser des ressources précompilées</span><span class="sxs-lookup"><span data-stu-id="055db-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="055db-171">tooreduce hello fois qu’il prend toorun hello script, évitez les opérations qui compile les ressources à partir de code source.</span><span class="sxs-lookup"><span data-stu-id="055db-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="055db-172">Par exemple, de précompiler des ressources et de les stocker dans un objet blob du compte Azure Storage Bonjour même centre de données en tant que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="055db-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="055db-173"><a name="bPS3"></a>Assurez-vous que le script de personnalisation de cluster hello est idempotente</span><span class="sxs-lookup"><span data-stu-id="055db-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="055db-174">Les scripts doivent être idempotents.</span><span class="sxs-lookup"><span data-stu-id="055db-174">Scripts must be idempotent.</span></span> <span data-ttu-id="055db-175">Si le script de hello exécute plusieurs fois, elle doit retourner hello toohello cluster même chaque fois que l’état.</span><span class="sxs-lookup"><span data-stu-id="055db-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="055db-176">Par exemple, un script qui modifie les fichiers de configuration ne doit pas ajouter d’entrées en double s’il est exécuté plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="055db-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="055db-177"><a name="bPS5"></a>Garantir une haute disponibilité de l’architecture de cluster hello</span><span class="sxs-lookup"><span data-stu-id="055db-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="055db-178">Les clusters HDInsight basés sur Linux fournissent deux nœuds principaux qui sont actives au sein du cluster de hello et exécutent des actions de script sur les deux nœuds.</span><span class="sxs-lookup"><span data-stu-id="055db-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="055db-179">Si vous installez des composants hello n'attendent qu’un seul nœud principal, n’installez pas de composants de hello sur les deux nœuds principal.</span><span class="sxs-lookup"><span data-stu-id="055db-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="055db-180">Services fournis dans le cadre de HDInsight sont conçu toofail entre deux nœuds de tête hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="055db-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="055db-181">Cette fonctionnalité n’est pas étendue toocustom les composants installés par le biais des actions de script.</span><span class="sxs-lookup"><span data-stu-id="055db-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="055db-182">Si vous avez besoin que les composants personnalisés soient très disponibles, vous devez implémenter votre propre mécanisme de basculement.</span><span class="sxs-lookup"><span data-stu-id="055db-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="055db-183"><a name="bPS6"></a>Configurer le stockage d’objets Blob Azure hello des composants personnalisés toouse</span><span class="sxs-lookup"><span data-stu-id="055db-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="055db-184">Les composants que vous installez sur un cluster de hello peuvent avoir une configuration par défaut qui utilise le stockage de système de fichiers distribués Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="055db-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="055db-185">HDInsight utilise le stockage Azure ou Data Lake Store comme stockage par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="055db-186">Fournissent un système de fichier compatible HDFS qui conserve les données même si le cluster de hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="055db-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="055db-187">Vous devrez peut-être les composants tooconfigure vous installez toouse WASB ou ADL au lieu de HDFS.</span><span class="sxs-lookup"><span data-stu-id="055db-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="055db-188">Pour la plupart des opérations, vous n’avez pas besoin de système de fichiers toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="055db-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="055db-189">Par exemple, suivant de hello copie fichier giraph-Examples.jar de hello stockage toocluster de système de fichiers local hello :</span><span class="sxs-lookup"><span data-stu-id="055db-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="055db-190">Dans cet exemple, hello `hdfs` commande utilise en toute transparence de stockage de cluster par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="055db-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="055db-191">Pour certaines opérations, vous devrez peut-être toospecify hello URI.</span><span class="sxs-lookup"><span data-stu-id="055db-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="055db-192">Par exemple, `adl:///example/jars` pour Data Lake Store ou `wasb:///example/jars` pour Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="055db-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="055db-193"><a name="bPS7"></a>Écrire des informations tooSTDOUT et STDERR</span><span class="sxs-lookup"><span data-stu-id="055db-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="055db-194">HDInsight enregistre la sortie du script qui est écrit tooSTDOUT et STDERR.</span><span class="sxs-lookup"><span data-stu-id="055db-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="055db-195">Vous pouvez afficher ces informations à l’aide de l’interface utilisateur web de Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="055db-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="055db-196">Ambari est disponible uniquement si hello cluster a été créé.</span><span class="sxs-lookup"><span data-stu-id="055db-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="055db-197">Si vous utilisez une action de script lors de la création du cluster et Échec de la création, consultez hello section Dépannage [HDInsight de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) pour d’autres façons d’accéder aux informations consignées.</span><span class="sxs-lookup"><span data-stu-id="055db-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="055db-198">La plupart des utilitaires et des packages d’installation écrivent déjà les informations tooSTDOUT et STDERR, toutefois, vous souhaiterez peut-être tooadd la journalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="055db-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="055db-199">toosend tooSTDOUT de texte, utilisez `echo`.</span><span class="sxs-lookup"><span data-stu-id="055db-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="055db-200">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="055db-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="055db-201">Par défaut, `echo` envoie hello tooSTDOUT de chaîne.</span><span class="sxs-lookup"><span data-stu-id="055db-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="055db-202">toodirect il tooSTDERR, ajoutez `>&2` avant `echo`.</span><span class="sxs-lookup"><span data-stu-id="055db-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="055db-203">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="055db-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="055db-204">Redirige les informations écrites tooSTDOUT tooSTDERR (2) à la place.</span><span class="sxs-lookup"><span data-stu-id="055db-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="055db-205">Pour plus d’informations sur la redirection des E/S, consultez [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="055db-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="055db-206">Pour plus d’informations sur l’affichage des informations consignées par les actions de script, voir [Personnalisation de clusters HDInsight à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="055db-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="055db-207"><a name="bps8"></a> Enregistrer des fichiers au format ASCII avec les fins de ligne LF</span><span class="sxs-lookup"><span data-stu-id="055db-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="055db-208">Les scripts d’interpréteur de commandes doivent être stockés au format ASCII, avec des lignes terminées se terminant par LF.</span><span class="sxs-lookup"><span data-stu-id="055db-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="055db-209">Les fichiers sont stockés au format UTF-8 ou utilisent CRLF comme fin de ligne hello peuvent échouer avec hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="055db-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="055db-210"><a name="bps9"></a>Utilisez toorecover logique de nouvelle tentative d’erreurs transitoires</span><span class="sxs-lookup"><span data-stu-id="055db-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="055db-211">Lors du téléchargement de fichiers, l’installation de packages à l’aide d’apt-get, ou autres actions que la transmettent de données hello internet, action de hello peut échouer en raison d’erreurs de mise en réseau tootransient.</span><span class="sxs-lookup"><span data-stu-id="055db-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="055db-212">Par exemple, les ressources distantes hello avec que vous communiquez soit en cours de hello du basculement sur le nœud de sauvegarde tooa.</span><span class="sxs-lookup"><span data-stu-id="055db-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="055db-213">toomake vos erreurs résilient tootransient script, vous pouvez implémenter la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="055db-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="055db-214">Hello suivant fonction montre comment tooimplement logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="055db-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="055db-215">Il effectue une nouvelle tentative opération hello trois fois avant d’échouer.</span><span class="sxs-lookup"><span data-stu-id="055db-215">It retries hello operation three times before failing.</span></span>

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

<span data-ttu-id="055db-216">Hello exemples suivants montrent comment toouse cette fonction.</span><span class="sxs-lookup"><span data-stu-id="055db-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="055db-217"><a name="helpermethods"></a>Méthodes d'assistance pour les scripts personnalisés</span><span class="sxs-lookup"><span data-stu-id="055db-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="055db-218">Les méthodes d’assistance aux actions de script sont des utilitaires que vous pouvez utiliser lors de l’écriture de scripts personnalisés.</span><span class="sxs-lookup"><span data-stu-id="055db-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="055db-219">Ces méthodes sont contenues dans le script[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="055db-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="055db-220">Utilisez hello suivant toodownload et les utiliser dans le cadre de votre script :</span><span class="sxs-lookup"><span data-stu-id="055db-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="055db-221">Hello suivant disponibles pour une utilisation dans votre script :</span><span class="sxs-lookup"><span data-stu-id="055db-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="055db-222">Utilisation de l’aide</span><span class="sxs-lookup"><span data-stu-id="055db-222">Helper usage</span></span> | <span data-ttu-id="055db-223">Description</span><span class="sxs-lookup"><span data-stu-id="055db-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="055db-224">Télécharge un fichier hello source URI toohello chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="055db-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="055db-225">Par défaut, il ne remplace pas un fichier existant.</span><span class="sxs-lookup"><span data-stu-id="055db-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="055db-226">Extrait un fichier tar (à l’aide de `-xf`) répertoire de destination toohello.</span><span class="sxs-lookup"><span data-stu-id="055db-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="055db-227">Lorsqu’il est exécuté sur un nœud principal de cluster, la valeur 1 est renvoyée ; dans le cas contraire, c’est la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="055db-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="055db-228">Si le nœud actuel de hello est un nœud de données (traitement), retourner la valeur 1 ; Sinon, 0.</span><span class="sxs-lookup"><span data-stu-id="055db-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="055db-229">Si hello le nœud actuel est hello commencez par les données (traitement) nœud (nommée workernode0) retourner la valeur 1 ; Sinon, 0.</span><span class="sxs-lookup"><span data-stu-id="055db-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="055db-230">Retourne le nom de domaine complet de hello de hello headnodes dans un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="055db-231">Les noms sont séparés par des virgules.</span><span class="sxs-lookup"><span data-stu-id="055db-231">Names are comma delimited.</span></span> <span data-ttu-id="055db-232">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="055db-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="055db-233">Obtient le nom de domaine complet de hello de nœud principal de principal hello.</span><span class="sxs-lookup"><span data-stu-id="055db-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="055db-234">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="055db-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="055db-235">Obtient le nom de domaine complet de hello du nœud principal secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="055db-236">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="055db-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="055db-237">Obtient le suffixe numérique hello nœud principal principal de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="055db-238">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="055db-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="055db-239">Obtient le suffixe numérique hello nœud principal secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="055db-240">Une chaîne vide est renvoyée en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="055db-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="055db-241"><a name="commonusage"></a>Modes d'utilisation courants</span><span class="sxs-lookup"><span data-stu-id="055db-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="055db-242">Cette section fournit des conseils sur l’implémentation des modèles d’utilisation courants hello que vous pouvez rencontrer lors de l’écriture de votre propre script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="055db-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="055db-243">Passage de paramètres tooa script</span><span class="sxs-lookup"><span data-stu-id="055db-243">Passing parameters tooa script</span></span>

<span data-ttu-id="055db-244">Dans certains cas, votre script peut nécessiter des paramètres.</span><span class="sxs-lookup"><span data-stu-id="055db-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="055db-245">Par exemple, vous devrez peut-être mot de passe administrateur hello pour le cluster de hello lors de l’utilisation de hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="055db-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="055db-246">Paramètres passés toohello script sont appelés *paramètres positionnels*et sont affectées trop`$1` pour le premier paramètre de hello, `$2` pour hello deuxième et donc sur.</span><span class="sxs-lookup"><span data-stu-id="055db-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="055db-247">`$0`contient le nom hello de script hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="055db-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="055db-248">Les valeurs passées toohello script en tant que paramètres doivent être placées par des guillemets simples (').</span><span class="sxs-lookup"><span data-stu-id="055db-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="055db-249">Cela garantit que hello valeur passée est traité comme un littéral.</span><span class="sxs-lookup"><span data-stu-id="055db-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="055db-250">Définition des variables d'environnement</span><span class="sxs-lookup"><span data-stu-id="055db-250">Setting environment variables</span></span>

<span data-ttu-id="055db-251">Définition d’une variable d’environnement est effectuée par hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="055db-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="055db-252">Où NOM_VARIABLE est nom hello de variable de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="055db-253">utilisation de la variable, de tooaccess hello `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="055db-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="055db-254">Par exemple, tooassign une valeur fournie par un paramètre positionnel comme variable d’environnement nommée mot de passe, vous utiliseriez hello après l’instruction :</span><span class="sxs-lookup"><span data-stu-id="055db-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="055db-255">Informations de toohello accès ultérieur peut ensuite l’utiliser `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="055db-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="055db-256">Variables d’environnement définies dans le script de hello n’existent que dans la portée de hello du script de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="055db-257">Dans certains cas, vous devrez peut-être les variables d’environnement système tooadd qui persistent une fois le script de hello est terminé.</span><span class="sxs-lookup"><span data-stu-id="055db-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="055db-258">les variables d’environnement système tooadd, ajouter une variable de hello trop`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="055db-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="055db-259">Par exemple, après l’instruction de hello ajoute `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="055db-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="055db-260">Toolocations d’accès où sont stockés les scripts personnalisés hello</span><span class="sxs-lookup"><span data-stu-id="055db-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="055db-261">Scripts utilisés toocustomize un cluster doit toobe stockée dans un des emplacements suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="055db-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="055db-262">Un __compte de stockage Azure__ associé au cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="055db-263">Un __compte de stockage supplémentaire__ associé hello cluster.</span><span class="sxs-lookup"><span data-stu-id="055db-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="055db-264">Une __URI lisible publiquement__.</span><span class="sxs-lookup"><span data-stu-id="055db-264">A __publicly readable URI__.</span></span> <span data-ttu-id="055db-265">Par exemple, une URL toodata stocké sur OneDrive, Dropbox ou un autre fichier de service d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="055db-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="055db-266">Un __compte Azure Data Lake Store__ associé au cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="055db-267">Pour plus d’informations sur l’utilisation d'Azure Data Lake Store avec HDInsight, voir [Créer un cluster HDInsight avec Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="055db-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="055db-268">Hello service principal HDInsight utilise tooaccess Data Lake Store doit avoir accès en lecture toohello script.</span><span class="sxs-lookup"><span data-stu-id="055db-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="055db-269">Ressources utilisées par le script de hello doivent également être publiquement disponibles.</span><span class="sxs-lookup"><span data-stu-id="055db-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="055db-270">Le stockage des fichiers de hello dans un compte de stockage Azure ou dans Azure Data Lake Store fournit un accès rapide, comme les deux dans hello réseau Azure.</span><span class="sxs-lookup"><span data-stu-id="055db-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="055db-271">Hello URI format utilisé tooreference hello script diffère selon service hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="055db-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="055db-272">Pour les comptes de stockage associés au cluster HDInsight de hello, utilisez `wasb://` ou `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="055db-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="055db-273">Pour des URI lisibles publiquement, utilisez `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="055db-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="055db-274">Pour Data Lake Store, utilisez `adl://`.</span><span class="sxs-lookup"><span data-stu-id="055db-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="055db-275">Vérification de la version du système d’exploitation hello</span><span class="sxs-lookup"><span data-stu-id="055db-275">Checking hello operating system version</span></span>

<span data-ttu-id="055db-276">Différentes versions de HDInsight s’appuient sur des versions spécifiques d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="055db-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="055db-277">Il peut exister des différences entre les versions de système d’exploitation que vous devez vérifier dans votre script.</span><span class="sxs-lookup"><span data-stu-id="055db-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="055db-278">Par exemple, vous devrez peut-être tooinstall un binaire qui est la version liée toohello d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="055db-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="055db-279">version de hello du système d’exploitation toocheck, utilisez `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="055db-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="055db-280">Par exemple, hello script suivant montre comment tooreference un tar spécifique de fichiers en fonction de la version du système d’exploitation de hello :</span><span class="sxs-lookup"><span data-stu-id="055db-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

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

## <span data-ttu-id="055db-281"><a name="deployScript"></a>Liste de vérification pour le déploiement d'une action de script</span><span class="sxs-lookup"><span data-stu-id="055db-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="055db-282">Voici les étapes hello que étaient lors de la préparation toodeploy ces scripts :</span><span class="sxs-lookup"><span data-stu-id="055db-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="055db-283">Placez les fichiers hello qui contiennent des scripts personnalisés hello dans un emplacement accessible par les nœuds de cluster hello lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="055db-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="055db-284">Par exemple, hello du stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="055db-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="055db-285">Les fichiers peuvent également être stockés dans les services d’hébergement lisibles publiquement.</span><span class="sxs-lookup"><span data-stu-id="055db-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="055db-286">Vérifiez que le script de hello est impotent.</span><span class="sxs-lookup"><span data-stu-id="055db-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="055db-287">Ainsi, hello script toobe exécutée plusieurs fois sur hello même nœud.</span><span class="sxs-lookup"><span data-stu-id="055db-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="055db-288">Utilisez un Bonjour tookeep de fichier temporaire répertoire /tmp téléchargé les fichiers utilisés par les scripts hello et puis les nettoyer après aient l’exécution de scripts.</span><span class="sxs-lookup"><span data-stu-id="055db-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="055db-289">Si les paramètres au niveau du système d’exploitation ou les fichiers de configuration de service Hadoop sont modifiées, vous souhaiterez toorestart HDInsight services.</span><span class="sxs-lookup"><span data-stu-id="055db-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="055db-290"><a name="runScriptAction"></a>Comment toorun une action de script</span><span class="sxs-lookup"><span data-stu-id="055db-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="055db-291">Vous pouvez utiliser des clusters HDInsight script actions toocustomize sont à l’aide de hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="055db-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="055db-292">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="055db-292">Azure portal</span></span>
* <span data-ttu-id="055db-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="055db-293">Azure PowerShell</span></span>
* <span data-ttu-id="055db-294">Modèles Microsoft Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="055db-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="055db-295">Hello HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="055db-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="055db-296">Pour plus d’informations sur l’utilisation de chaque méthode, consultez [comment toouse de script action](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="055db-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="055db-297"><a name="sampleScripts"></a>Exemples de scripts personnalisés</span><span class="sxs-lookup"><span data-stu-id="055db-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="055db-298">Microsoft fournit des exemples de scripts tooinstall composants sur un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="055db-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="055db-299">Consultez hello suivant les liens pour plus d’actions de script d’exemple.</span><span class="sxs-lookup"><span data-stu-id="055db-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="055db-300">Installer et utiliser Hue sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="055db-301">Installer et utiliser Solr sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="055db-302">Installer et utiliser Giraph sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="055db-303">Installer ou mettre à niveau Mono sur les clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="055db-304">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="055db-304">Troubleshooting</span></span>

<span data-ttu-id="055db-305">Hello Voici les erreurs que vous pouvez rencontrer lors de l’utilisation de scripts que vous avez développé :</span><span class="sxs-lookup"><span data-stu-id="055db-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="055db-306">**Erreur** : `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="055db-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="055db-307">Parfois suivi par `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="055db-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="055db-308">*Cause*: cette erreur se produit lorsque des lignes de hello dans un script se terminant par CRLF.</span><span class="sxs-lookup"><span data-stu-id="055db-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="055db-309">Les systèmes UNIX attendent LF uniquement en tant que la fin de ligne hello.</span><span class="sxs-lookup"><span data-stu-id="055db-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="055db-310">Ce problème se produit souvent lorsque le script de hello est créé dans un environnement Windows, comme CRLF est une ligne commune se terminant par de nombreux éditeurs de texte sous Windows.</span><span class="sxs-lookup"><span data-stu-id="055db-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="055db-311">*Résolution*: si elle est une option dans votre éditeur de texte, sélectionnez un format Unix ou saut de ligne de fin de ligne hello.</span><span class="sxs-lookup"><span data-stu-id="055db-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="055db-312">Vous pouvez également utiliser hello suivant de commandes sur un système Unix toochange les tooan CRLF d’hello LF :</span><span class="sxs-lookup"><span data-stu-id="055db-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="055db-313">Hello commandes suivantes sont à peu près équivalentes dans la mesure où ils doivent modifier hello CRLF ligne fins tooLF.</span><span class="sxs-lookup"><span data-stu-id="055db-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="055db-314">Sélectionnez une basée sur les utilitaires hello disponibles sur votre système.</span><span class="sxs-lookup"><span data-stu-id="055db-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="055db-315">Commande</span><span class="sxs-lookup"><span data-stu-id="055db-315">Command</span></span> | <span data-ttu-id="055db-316">Remarques</span><span class="sxs-lookup"><span data-stu-id="055db-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="055db-317">fichier d’origine de Hello est sauvegardée avec un. Extension BAK</span><span class="sxs-lookup"><span data-stu-id="055db-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="055db-318">OUTFILE contient une version avec des terminaisons LF uniquement</span><span class="sxs-lookup"><span data-stu-id="055db-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="055db-319">Modifie le fichier de hello directement</span><span class="sxs-lookup"><span data-stu-id="055db-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="055db-320">OUTFILE contient une version avec des terminaisons LF uniquement.</span><span class="sxs-lookup"><span data-stu-id="055db-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="055db-321">**Erreur** : `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="055db-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="055db-322">*Cause*: cette erreur se produit lorsque hello script a été enregistré au format UTF-8 avec marque d’ordre d’octet (BOM).</span><span class="sxs-lookup"><span data-stu-id="055db-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="055db-323">*Résolution*: hello enregistrer le fichier au format ASCII ou UTF-8 sans une nomenclature.</span><span class="sxs-lookup"><span data-stu-id="055db-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="055db-324">Vous pouvez également utiliser hello suivant de commande sur un système Unix ou Linux toocreate un fichier sans hello nomenclature :</span><span class="sxs-lookup"><span data-stu-id="055db-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="055db-325">Remplacez `INFILE` avec le fichier de hello contenant hello nomenclature.</span><span class="sxs-lookup"><span data-stu-id="055db-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="055db-326">`OUTFILE`doit être un nouveau nom de fichier, qui contient le script hello sans hello nomenclature.</span><span class="sxs-lookup"><span data-stu-id="055db-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="055db-327"><a name="seeAlso"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="055db-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="055db-328">Découvrez comment trop[HDInsight de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="055db-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="055db-329">Hello d’utilisation [référence du Kit de développement logiciel HDInsight .NET](https://msdn.microsoft.com/library/mt271028.aspx) toolearn plus d’informations sur la création d’applications .NET qui gérer HDInsight</span><span class="sxs-lookup"><span data-stu-id="055db-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="055db-330">Hello d’utilisation [API REST de HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn comment des actions de gestion tooperform toouse reste sur HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="055db-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
