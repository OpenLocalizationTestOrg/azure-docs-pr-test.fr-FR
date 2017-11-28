---
title: "les comptes de stockage Azure supplémentaires d’aaaAdd tooHDInsight | Documents Microsoft"
description: "Découvrez comment le stockage Azure supplémentaires tooadd comptes tooan les cluster HDInsight existant."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="a0aab-103">Ajouter tooHDInsight des comptes de stockage supplémentaire</span><span class="sxs-lookup"><span data-stu-id="a0aab-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="a0aab-104">Découvrez comment toouse script actions tooadd supplémentaires le stockage Azure comptes tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0aab-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="a0aab-105">Hello étapes de ce document ajoutent un cluster HDInsight de basés sur Linux stockage compte tooan existant.</span><span class="sxs-lookup"><span data-stu-id="a0aab-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0aab-106">informations Hello dans ce document sont sur l’ajout de cluster de stockage supplémentaire tooa après que qu’elle a été créée.</span><span class="sxs-lookup"><span data-stu-id="a0aab-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="a0aab-107">Pour plus d’informations sur l’ajout de comptes de stockage lors de la création du cluster, voir [Configurer des clusters dans HDInsight avec Hadoop, Spark, Kafka, etc](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a0aab-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a0aab-108">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="a0aab-108">How it works</span></span>

<span data-ttu-id="a0aab-109">Ce script accepte hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="a0aab-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="a0aab-110">__Nom de compte de stockage Azure__: nom hello du cluster HDInsight de hello stockage compte tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="a0aab-111">Après avoir exécuté le script de hello, HDInsight peut lire et écrire les données stockées dans ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="a0aab-112">__Clé de compte de stockage Azure__: une clé qui accorde l’accès toohello de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="a0aab-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="a0aab-113">__p -__ (facultatif) : si spécifié, la clé de hello n’est pas chiffré et est stocké dans le fichier core-site.XML de hello en tant que texte brut.</span><span class="sxs-lookup"><span data-stu-id="a0aab-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="a0aab-114">Au cours du traitement, hello de script effectue hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="a0aab-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="a0aab-115">Si hello compte de stockage existe déjà dans la configuration de base-site.XML hello pour le cluster de hello, hello script s’arrête et aucune action supplémentaire n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="a0aab-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="a0aab-116">Vérifie que le compte de stockage hello existe et est accessible à l’aide de la clé de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="a0aab-117">Chiffre clé hello à l’aide des informations d’identification du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="a0aab-118">Ajoute le fichier core-site.XML toohello hello stockage compte.</span><span class="sxs-lookup"><span data-stu-id="a0aab-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="a0aab-119">Arrête et redémarre les services Oozie, fils, MapReduce2 et HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="a0aab-120">Arrêter et démarrer ces services leur permet de toouse hello nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="a0aab-121">À l’aide d’un compte de stockage dans un emplacement autre que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a0aab-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="a0aab-122">script de Hello</span><span class="sxs-lookup"><span data-stu-id="a0aab-122">hello script</span></span>

<span data-ttu-id="a0aab-123">__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="a0aab-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="a0aab-124">__Conditions requises__ :</span><span class="sxs-lookup"><span data-stu-id="a0aab-124">__Requirements__:</span></span>

* <span data-ttu-id="a0aab-125">script de Hello doit être appliquée sur hello __Head nœuds__.</span><span class="sxs-lookup"><span data-stu-id="a0aab-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="a0aab-126">script de hello toouse</span><span class="sxs-lookup"><span data-stu-id="a0aab-126">toouse hello script</span></span>

<span data-ttu-id="a0aab-127">Ce script peut être utilisé à partir de hello portail Azure, Azure PowerShell, ou hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="a0aab-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="a0aab-128">Pour plus d’informations, consultez hello [HDInsight de basés sur Linux de personnaliser des clusters à l’aide d’action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="a0aab-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0aab-129">Lorsque vous utilisez les étapes de hello fournies dans le document de personnalisation hello, utilisez hello suivant informations tooapply ce script :</span><span class="sxs-lookup"><span data-stu-id="a0aab-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="a0aab-130">Remplacez les URI d’action de script exemple hello URI pour ce script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="a0aab-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="a0aab-131">Remplacez les exemples de paramètres avec le nom de compte de stockage Windows Azure hello et la clé de cluster de hello stockage compte toobe toohello ajouté.</span><span class="sxs-lookup"><span data-stu-id="a0aab-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="a0aab-132">Si à l’aide de hello le portail Azure, ces paramètres doivent être séparés par un espace.</span><span class="sxs-lookup"><span data-stu-id="a0aab-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="a0aab-133">Vous n’avez pas besoin toomark ce script en tant que __Persisted__, tel qu’il met à jour hello Ambari de configuration pour hello cluster directement.</span><span class="sxs-lookup"><span data-stu-id="a0aab-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a0aab-134">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="a0aab-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="a0aab-135">Comptes de stockage non affichés dans le portail ou les outils Azure</span><span class="sxs-lookup"><span data-stu-id="a0aab-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="a0aab-136">Lors de l’affichage hello HDInsight cluster Bonjour portail Azure, en sélectionnant hello __comptes de stockage__ entrée sous __propriétés__ n’affiche pas les comptes de stockage ajoutés à cette action de script.</span><span class="sxs-lookup"><span data-stu-id="a0aab-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="a0aab-137">Azure PowerShell et CLI d’Azure n’affichent pas compte de stockage supplémentaire hello soit.</span><span class="sxs-lookup"><span data-stu-id="a0aab-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="a0aab-138">informations de stockage Hello n’est pas affichées, car le script de hello modifie uniquement hello core-site.XML de configuration pour hello cluster.</span><span class="sxs-lookup"><span data-stu-id="a0aab-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="a0aab-139">Ces informations ne sont pas utilisées lors de la récupération des informations de cluster hello à l’aide des API de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="a0aab-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="a0aab-140">les informations de compte de stockage tooview ajouté cluster toohello à l’aide de ce script, utilisez hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="a0aab-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="a0aab-141">Utilisez hello suivant de commandes tooretrieve ces informations pour votre cluster :</span><span class="sxs-lookup"><span data-stu-id="a0aab-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="a0aab-142">Définissez `$clusterName` nom toohello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="a0aab-143">Définissez `$storageAccountName` nom toohello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="a0aab-144">Lorsque vous y êtes invité, entrez la connexion de cluster hello (admin) et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a0aab-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="a0aab-145">Définissez `$PASSWORD` mot de passe de compte à la connexion (admin) toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="a0aab-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="a0aab-146">Définissez `$CLUSTERNAME` nom toohello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="a0aab-147">Définissez `$STORAGEACCOUNTNAME` nom toohello hello du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="a0aab-148">Cet exemple utilise [curl (http://curl.haxx.se/)](http://curl.haxx.se/) et [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve et l’analyse des données JSON.</span><span class="sxs-lookup"><span data-stu-id="a0aab-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="a0aab-149">Lorsque vous utilisez cette commande, remplacez __CLUSTERNAME__ avec nom hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="a0aab-150">Remplacez __mot de passe__ avec un mot de passe de connexion pour le cluster de hello hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0aab-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="a0aab-151">Remplacez __STORAGEACCOUNT__ avec nom hello hello du compte de stockage ajouté à l’aide d’action de script.</span><span class="sxs-lookup"><span data-stu-id="a0aab-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="a0aab-152">Informations retournées par cette commande apparaissent toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="a0aab-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="a0aab-153">Ce texte est un exemple d’une clé chiffrée, ce qui est utilisé tooaccess hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="a0aab-154">Stockage tooaccess impossible après avoir modifié la clé</span><span class="sxs-lookup"><span data-stu-id="a0aab-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="a0aab-155">Si vous modifiez la clé de hello pour un compte de stockage, HDInsight peut ne plus accéder aux comptes de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="a0aab-156">HDInsight utilise une copie mise en cache de clé dans hello core-site.XML pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="a0aab-157">Cette copie mise en cache doit être la nouvelle clé de hello toomatch mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a0aab-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="a0aab-158">Action de script hello à nouveau en cours d’exécution est __pas__ mettre à jour de la clé de hello, que le contrôle de script de hello toosee si une entrée pour le compte de stockage hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="a0aab-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="a0aab-159">Si une entrée existe déjà, aucune modification n’est apportée.</span><span class="sxs-lookup"><span data-stu-id="a0aab-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="a0aab-160">toowork résoudre ce problème, vous devez supprimer l’entrée existante de hello hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0aab-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="a0aab-161">Utilisez hello étapes tooremove hello existant entrée suivante :</span><span class="sxs-lookup"><span data-stu-id="a0aab-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="a0aab-162">Dans un navigateur web, ouvrez hello l’interface utilisateur de Ambari Web pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0aab-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="a0aab-163">Hello URI est https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a0aab-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="a0aab-164">Remplacez __CLUSTERNAME__ avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a0aab-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="a0aab-165">Lorsque vous y êtes invité, entrez hello HTTP nom d’utilisateur et mot de passe pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="a0aab-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="a0aab-166">À partir de la liste de hello des services sur la gauche hello de page de hello, sélectionnez __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="a0aab-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="a0aab-167">Puis sélectionnez hello __configurations__ onglet dans le centre de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="a0aab-168">Bonjour __filtre...__  , entrez une valeur de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="a0aab-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="a0aab-169">Cela retourne les entrées pour tous les comptes de stockage supplémentaires ont été ajoutées toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="a0aab-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="a0aab-170">Il existe deux types d’entrées : __keyprovider__ et __key__.</span><span class="sxs-lookup"><span data-stu-id="a0aab-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="a0aab-171">Tous les deux contenir le nom hello hello du compte de stockage en tant que partie du nom de la clé hello.</span><span class="sxs-lookup"><span data-stu-id="a0aab-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="a0aab-172">Hello Voici des exemples d’entrées pour un compte de stockage nommé __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="a0aab-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="a0aab-173">Après avoir identifié les clés hello pour le compte de stockage hello vous devez tooremove, utilisez hello rouge '-' toohello icône à droite de hello entrée toodelete il.</span><span class="sxs-lookup"><span data-stu-id="a0aab-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="a0aab-174">Utilisez ensuite hello __enregistrer__ bouton toosave vos modifications.</span><span class="sxs-lookup"><span data-stu-id="a0aab-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="a0aab-175">Une fois que les modifications ont été enregistrées, utilisez le compte de stockage hello script action tooadd hello et le nouveau cluster toohello de valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="a0aab-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="a0aab-176">Problèmes de performances</span><span class="sxs-lookup"><span data-stu-id="a0aab-176">Poor performance</span></span>

<span data-ttu-id="a0aab-177">Si le compte de stockage hello est dans une autre région que le cluster HDInsight de hello, vous pouvez rencontrer des performances médiocres.</span><span class="sxs-lookup"><span data-stu-id="a0aab-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="a0aab-178">L’accès aux données dans un autre région envoie réseau du trafic à l’extérieur du centre de données Azure régional hello et à travers hello internet public, qui peut introduire une latence.</span><span class="sxs-lookup"><span data-stu-id="a0aab-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="a0aab-179">À l’aide d’un compte de stockage dans une autre région que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a0aab-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="a0aab-180">Frais supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a0aab-180">Additional charges</span></span>

<span data-ttu-id="a0aab-181">Si le compte de stockage hello est dans une autre région de hello cluster HDInsight, vous remarquerez peut-être des frais de sortie supplémentaires sur votre facturation Azure.</span><span class="sxs-lookup"><span data-stu-id="a0aab-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="a0aab-182">Des frais de sortie sont appliqués lorsque des données quittent un centre de données régional.</span><span class="sxs-lookup"><span data-stu-id="a0aab-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="a0aab-183">Ces frais sont appliqués même si le trafic de hello est destiné à un autre centre de données Azure dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="a0aab-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="a0aab-184">À l’aide d’un compte de stockage dans une autre région que le cluster HDInsight de hello n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a0aab-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0aab-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a0aab-185">Next steps</span></span>

<span data-ttu-id="a0aab-186">Vous avez appris comment les comptes de stockage de plus de tooadd tooan les cluster HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="a0aab-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="a0aab-187">Pour plus d’informations sur les actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a0aab-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
