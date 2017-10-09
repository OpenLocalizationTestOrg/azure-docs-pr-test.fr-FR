---
title: "Création - Azure d’un cluster aaaAdd les bibliothèques Hive pendant HDInsight | Documents Microsoft"
description: "Découvrez comment les bibliothèques Hive tooadd (fichiers jar), tooan HDInsight de cluster lors de la création du cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="0c891-103">Ajouter des bibliothèques Hive personnalisées lors de la création de votre cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="0c891-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="0c891-104">Si vous avez des bibliothèques que vous utilisez fréquemment avec Hive dans HDInsight, ce document contient des informations sur l’utilisation de bibliothèques de hello toopre-charge un Action de Script lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="0c891-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="0c891-105">Bibliothèques ajoutés à l’aide des étapes de hello dans ce document sont disponibles dans la ruche - il n’existe aucun besoin toouse [ajouter JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload les.</span><span class="sxs-lookup"><span data-stu-id="0c891-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="0c891-106">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="0c891-106">How it works</span></span>

<span data-ttu-id="0c891-107">Lorsque vous créez un cluster, vous pouvez éventuellement spécifier une Action de Script qui exécute un script sur les nœuds de cluster hello lors de leur création.</span><span class="sxs-lookup"><span data-stu-id="0c891-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="0c891-108">script Hello dans ce document accepte un seul paramètre, qui est un emplacement WASB contenant toobe de bibliothèques (stockés en tant que fichiers jar) hello préchargé.</span><span class="sxs-lookup"><span data-stu-id="0c891-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="0c891-109">Lors de la création du cluster, script de hello énumère les fichiers de hello, copie les toohello `/usr/lib/customhivelibs/` active sur les nœuds de tête et de travail, puis les ajoute toohello `hive.aux.jars.path` propriété Bonjour `core-site.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="0c891-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="0c891-110">Sur les clusters basés sur Linux, il met également à jour hello `hive-env.sh` fichier à l’emplacement des fichiers de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="0c891-111">À l’aide des actions de script hello dans cet article fournit les bibliothèques hello Bonjour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="0c891-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="0c891-112">**HDInsight de basés sur Linux** : quand à l’aide de hello un client Hive, **WebHCat**, et **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="0c891-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="0c891-113">**Basé sur Windows de HDInsight** - lors de l’utilisation du client de ruche hello et **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="0c891-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="0c891-114">script de Hello</span><span class="sxs-lookup"><span data-stu-id="0c891-114">hello script</span></span>

<span data-ttu-id="0c891-115">**Emplacement du script**</span><span class="sxs-lookup"><span data-stu-id="0c891-115">**Script location**</span></span>

<span data-ttu-id="0c891-116">Pour les **clusters basés sur Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="0c891-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="0c891-117">Pour les **clusters basés sur Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="0c891-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c891-118">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0c891-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0c891-119">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0c891-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="0c891-120">**Configuration requise**</span><span class="sxs-lookup"><span data-stu-id="0c891-120">**Requirements**</span></span>

* <span data-ttu-id="0c891-121">les scripts Hello doivent être appliqué tooboth hello **Head nœuds** et **nœuds Worker**.</span><span class="sxs-lookup"><span data-stu-id="0c891-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="0c891-122">Hello JAR que vous souhaitez tooinstall doivent être stockées dans le stockage d’objets Blob Azure dans un **seul conteneur**.</span><span class="sxs-lookup"><span data-stu-id="0c891-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="0c891-123">compte de stockage Hello contenant la bibliothèque hello des fichiers jar **doit** être toohello lié HDInsight cluster lors de la création.</span><span class="sxs-lookup"><span data-stu-id="0c891-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="0c891-124">Il doit être compte de stockage par défaut hello ou un compte ajouté via __configuration facultative__.</span><span class="sxs-lookup"><span data-stu-id="0c891-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="0c891-125">conteneur de toohello Hello WASB chemin d’accès doit être spécifiée comme un toohello du paramètre Action de Script.</span><span class="sxs-lookup"><span data-stu-id="0c891-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="0c891-126">Par exemple, si hello JAR est stockés dans un conteneur nommé **libs** sur un compte de stockage nommé **mystorage**, paramètre hello serait  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="0c891-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0c891-127">Ce document suppose que vous avez déjà créer un compte de stockage, conteneur d’objets blob et tooit des fichiers téléchargés hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="0c891-128">Si vous n’avez pas créé un compte de stockage, vous pouvez le faire via hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c891-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0c891-129">Vous pouvez ensuite utiliser un utilitaire tel que [Azure Storage Explorer](http://storageexplorer.com/) toocreate un conteneur dans le compte de hello et le téléchargement des fichiers tooit.</span><span class="sxs-lookup"><span data-stu-id="0c891-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="0c891-130">Créer un cluster à l’aide du script de hello</span><span class="sxs-lookup"><span data-stu-id="0c891-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="0c891-131">Hello suit créer un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="0c891-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0c891-132">toocreate un cluster basé sur Windows, sélectionnez **Windows** comme hello de cluster du système d’exploitation lors de la création du cluster de hello et utiliser le script de Windows (PowerShell) hello au lieu de script d’interpréteur de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="0c891-133">Vous pouvez également utiliser Azure PowerShell ou toocreate du Kit de développement logiciel HDInsight .NET hello un cluster à l’aide de ce script.</span><span class="sxs-lookup"><span data-stu-id="0c891-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="0c891-134">Pour plus d’informations sur ces méthodes, consultez [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0c891-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="0c891-135">Démarrer l’approvisionnement d’un cluster à l’aide des étapes hello dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md), mais n’effectuez pas la mise en service.</span><span class="sxs-lookup"><span data-stu-id="0c891-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="0c891-136">Sur hello **Configuration facultative** panneau, sélectionnez **Actions de Script**et fournir hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c891-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="0c891-137">**NOM**: entrez un nom convivial pour l’action de script hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="0c891-138">**URI du script** : https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="0c891-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="0c891-139">**HEAD**: cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="0c891-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="0c891-140">**WORKER** : cochez cette option.</span><span class="sxs-lookup"><span data-stu-id="0c891-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="0c891-141">**ZOOKEEPER** : laissez ce champ vide.</span><span class="sxs-lookup"><span data-stu-id="0c891-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="0c891-142">**PARAMÈTRES**: entrez hello WASB toohello conteneur et le stockage compte d’adresse qui contient les fichiers JAR hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="0c891-143">Par exemple : **wasb://libs@mystorage.blob.core.windows.net/**.</span><span class="sxs-lookup"><span data-stu-id="0c891-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="0c891-144">En bas de hello Hello **Actions de Script**, utilisez hello **sélectionnez** configuration hello toosave du bouton.</span><span class="sxs-lookup"><span data-stu-id="0c891-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="0c891-145">Sur hello **Configuration facultative** panneau, sélectionnez **des comptes de stockage liés** et sélectionnez hello **ajouter une clé de stockage** lien.</span><span class="sxs-lookup"><span data-stu-id="0c891-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="0c891-146">Sélectionnez le compte de stockage hello qui contient les fichiers JAR hello et utilisez hello **sélectionnez** paramètres toosave de boutons et retour hello **Configuration facultative** panneau.</span><span class="sxs-lookup"><span data-stu-id="0c891-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="0c891-147">Hello d’utilisation **sélectionnez** bouton bas hello hello **Configuration facultative** informations de configuration facultatives panneau toosave hello.</span><span class="sxs-lookup"><span data-stu-id="0c891-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="0c891-148">Continuer la mise en service de cluster de hello comme décrit dans [HDInsight de configurer des clusters sur Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0c891-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="0c891-149">Une fois la création du cluster terminée, vous êtes en mesure de toouse fichiers JAR hello ajoutées via ce script à partir de la ruche sans avoir toouse hello `ADD JAR` instruction.</span><span class="sxs-lookup"><span data-stu-id="0c891-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c891-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c891-150">Next steps</span></span>

<span data-ttu-id="0c891-151">Pour plus d'informations sur l’utilisation de Hive, consultez la rubrique [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="0c891-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
