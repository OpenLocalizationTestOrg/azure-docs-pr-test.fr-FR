---
title: "Ajouter des comptes de stockage Azure supplémentaires à HDInsight | Microsoft Docs"
description: "Découvrez comment ajouter des comptes de stockage Azure supplémentaires à un cluster HDInsight existant."
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
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="14b43-103">Ajouter des comptes de stockage supplémentaires à HDInsight</span><span class="sxs-lookup"><span data-stu-id="14b43-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="14b43-104">Découvrez comment utiliser des actions de script pour ajouter des comptes de stockage Azure à HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="14b43-105">Les étapes décrites dans ce document permettent d’ajouter un compte de stockage à un cluster HDInsight existant basé sur Linux.</span><span class="sxs-lookup"><span data-stu-id="14b43-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14b43-106">Ce document porte sur l’ajout de stockage supplémentaire à un cluster après que celui-ci a été créé.</span><span class="sxs-lookup"><span data-stu-id="14b43-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="14b43-107">Pour plus d’informations sur l’ajout de comptes de stockage lors de la création du cluster, voir [Configurer des clusters dans HDInsight avec Hadoop, Spark, Kafka, etc](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="14b43-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="14b43-108">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="14b43-108">How it works</span></span>

<span data-ttu-id="14b43-109">Le script utilise les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="14b43-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="14b43-110">__Nom du compte de stockage Azure__ : nom du compte de stockage à ajouter au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="14b43-111">Une fois le script exécuté, HDInsight est en mesure de lire et d’écrire des données stockées dans ce compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="14b43-112">__Clé du compte de stockage Azure__ : clé qui donne accès au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="14b43-113">__p -__ (facultatif) : si ce paramètre est spécifié, la clé n’est pas chiffrée et est stockée en texte brut dans le fichier core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="14b43-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="14b43-114">Pendant le traitement, le script effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="14b43-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="14b43-115">Si le compte de stockage existe déjà dans la configuration core-site.xml du cluster, le script s’arrête et aucune action supplémentaire n’est effectuée.</span><span class="sxs-lookup"><span data-stu-id="14b43-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="14b43-116">Il vérifie que le compte de stockage existe et est accessible à l’aide de la clé.</span><span class="sxs-lookup"><span data-stu-id="14b43-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="14b43-117">Il chiffre la clé à l’aide des informations d’identification du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="14b43-118">Il ajoute le compte de stockage dans le fichier core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="14b43-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="14b43-119">Il arrête et redémarre les services Oozie, YARN, MapReduce2 et HDFS.</span><span class="sxs-lookup"><span data-stu-id="14b43-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="14b43-120">L’arrêt et le redémarrage de ces services leur permettent d’utiliser le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="14b43-121">L’utilisation d’un compte de stockage dans un autre emplacement que le cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="14b43-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="14b43-122">Le script</span><span class="sxs-lookup"><span data-stu-id="14b43-122">The script</span></span>

<span data-ttu-id="14b43-123">__Emplacement du script__ : [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="14b43-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="14b43-124">__Conditions requises__ :</span><span class="sxs-lookup"><span data-stu-id="14b43-124">__Requirements__:</span></span>

* <span data-ttu-id="14b43-125">Le script doit être appliqué sur les __nœuds principaux__.</span><span class="sxs-lookup"><span data-stu-id="14b43-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="14b43-126">Pour utiliser le script</span><span class="sxs-lookup"><span data-stu-id="14b43-126">To use the script</span></span>

<span data-ttu-id="14b43-127">Le script peut être utilisé avec le portail Azure, Azure PowerShell ou Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="14b43-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="14b43-128">Pour plus d’informations, consultez le document [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une action de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="14b43-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14b43-129">Lorsque vous suivez les étapes décrites dans le document de personnalisation, utilisez les informations suivantes pour appliquer ce script :</span><span class="sxs-lookup"><span data-stu-id="14b43-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="14b43-130">Remplacez l’URI des exemples d’actions de script par l’URI de ce script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="14b43-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="14b43-131">Remplacez les paramètres des exemples par le nom du compte de stockage Azure et la clé du compte de stockage à ajouter au cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="14b43-132">Si vous utilisez le portail Azure, ces paramètres doivent être séparés par une espace.</span><span class="sxs-lookup"><span data-stu-id="14b43-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="14b43-133">Vous n’avez pas besoin de marquer ce script comme __Persistant__, car il met directement à jour la configuration Ambari.</span><span class="sxs-lookup"><span data-stu-id="14b43-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="14b43-134">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="14b43-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="14b43-135">Comptes de stockage non affichés dans le portail ou les outils Azure</span><span class="sxs-lookup"><span data-stu-id="14b43-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="14b43-136">Lorsque vous affichez le cluster HDInsight dans le portail Azure, les comptes de stockage ajoutés à l’aide de cette action de script ne s’affichent pas lorsque vous sélectionnez l’entrée __Comptes de stockage__ sous __Propriétés__.</span><span class="sxs-lookup"><span data-stu-id="14b43-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="14b43-137">Azure PowerShell et l’interface de ligne de commande Azure n’affichent pas non plus les comptes de stockage supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="14b43-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="14b43-138">Les informations de stockage n’apparaissent pas car le script modifie uniquement la configuration core-site.xml du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="14b43-139">Ces informations ne sont pas utilisées lors de la récupération des informations du cluster à l’aide des API de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="14b43-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="14b43-140">Pour afficher les informations des comptes de stockage ajoutés au cluster à l’aide de ce script, utilisez l’API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="14b43-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="14b43-141">Pour récupérer ces informations pour votre cluster, utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="14b43-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="14b43-142">Définissez `$clusterName` sur le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="14b43-143">Définissez `$storageAccountName` sur le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="14b43-144">Lorsque vous y êtes invité, entrez l’ID de connexion (admin) et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="14b43-145">Définissez `$PASSWORD` sur l’ID de connexion (admin) et le mot de passe du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="14b43-146">Définissez `$CLUSTERNAME` sur le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="14b43-147">Définissez `$STORAGEACCOUNTNAME` sur le nom du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="14b43-148">Cet exemple utilise [curl (http://curl.haxx.se/)](http://curl.haxx.se/) et [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) pour récupérer et analyser les données JSON.</span><span class="sxs-lookup"><span data-stu-id="14b43-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="14b43-149">Lorsque vous utilisez cette commande, remplacez __CLUSTERNAME__ par le nom du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="14b43-150">Remplacez __PASSWORD__ par le mot de passe de connexion HTTP du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="14b43-151">Remplacez __STORAGEACCOUNT__ par le nom du compte de stockage ajouté à l’aide de l’action de script.</span><span class="sxs-lookup"><span data-stu-id="14b43-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="14b43-152">Les informations renvoyées par cette commande sont semblables au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="14b43-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="14b43-153">Ce texte est un exemple de clé chiffrée, utilisée pour accéder au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="14b43-154">Impossible d’accéder au stockage après avoir modifié la clé</span><span class="sxs-lookup"><span data-stu-id="14b43-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="14b43-155">Si vous modifiez la clé d’un compte de stockage, HDInsight ne peut plus accéder au compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="14b43-156">HDInsight utilise une copie de la clé mise en cache dans le fichier core-site.xml pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="14b43-157">Cette copie mise en cache doit être mise à jour pour correspondre à la nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="14b43-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="14b43-158">Si vous exécutez de nouveau l’action de script, la clé n’est __pas__ mise à jour, car le script vérifie s’il existe déjà une entrée pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="14b43-159">Si une entrée existe déjà, aucune modification n’est apportée.</span><span class="sxs-lookup"><span data-stu-id="14b43-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="14b43-160">Pour contourner ce problème, vous devez supprimer l’entrée existante pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="14b43-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="14b43-161">Procédez comme suit pour supprimer l’entrée existante :</span><span class="sxs-lookup"><span data-stu-id="14b43-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="14b43-162">Dans un navigateur web, ouvrez l’interface utilisateur web Ambari pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="14b43-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="14b43-163">L’URI est https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="14b43-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="14b43-164">Remplacez __CLUSTERNAME__ par le nom de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="14b43-165">Lorsque vous y êtes invité, saisissez le nom d’utilisateur et le mot de passe de connexion HTTP de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="14b43-166">Dans la liste des services située à gauche de la page, sélectionnez __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="14b43-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="14b43-167">Ensuite, sélectionnez l’onglet __Configurations__ au centre de la page.</span><span class="sxs-lookup"><span data-stu-id="14b43-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="14b43-168">Dans la __Filtrer...__, entrez une valeur de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="14b43-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="14b43-169">Des entrées sont renvoyées pour tous les comptes de stockage supplémentaires qui ont été ajoutés au cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="14b43-170">Il existe deux types d’entrées : __keyprovider__ et __key__.</span><span class="sxs-lookup"><span data-stu-id="14b43-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="14b43-171">Les deux contiennent le nom du compte de stockage dans le nom de la clé.</span><span class="sxs-lookup"><span data-stu-id="14b43-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="14b43-172">Voici des exemples d’entrées pour un compte de stockage nommé __mystorage__ :</span><span class="sxs-lookup"><span data-stu-id="14b43-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="14b43-173">Après avoir identifié les clés du compte de stockage à supprimer, utilisez l’icône « - » rouge à droite de l’entrée pour procéder à la suppression.</span><span class="sxs-lookup"><span data-stu-id="14b43-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="14b43-174">Ensuite, cliquez sur le bouton __Enregistrer__ pour enregistrer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="14b43-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="14b43-175">Une fois les modifications enregistrées, utilisez l’action de script pour ajouter le compte de stockage et la nouvelle valeur de clé du cluster.</span><span class="sxs-lookup"><span data-stu-id="14b43-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="14b43-176">Problèmes de performances</span><span class="sxs-lookup"><span data-stu-id="14b43-176">Poor performance</span></span>

<span data-ttu-id="14b43-177">Si le compte de stockage se trouve dans une région différente de celle du cluster HDInsight, il se peut que vous rencontriez des problèmes de performances.</span><span class="sxs-lookup"><span data-stu-id="14b43-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="14b43-178">Lorsque vous accédez à des données stockées dans une autre région, le trafic réseau sort du centre de données Azure régional, puis est acheminé via l’Internet public, ce qui peut entraîner de la latence.</span><span class="sxs-lookup"><span data-stu-id="14b43-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="14b43-179">L’utilisation d’un compte de stockage dans une région différente de celle du cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="14b43-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="14b43-180">Frais supplémentaires</span><span class="sxs-lookup"><span data-stu-id="14b43-180">Additional charges</span></span>

<span data-ttu-id="14b43-181">Si le compte de stockage se trouve dans une région différente de celle du cluster HDInsight, vous remarquerez peut-être des frais de sortie supplémentaires sur votre facture Azure.</span><span class="sxs-lookup"><span data-stu-id="14b43-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="14b43-182">Des frais de sortie sont appliqués lorsque des données quittent un centre de données régional.</span><span class="sxs-lookup"><span data-stu-id="14b43-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="14b43-183">Ces frais sont appliqués même si le trafic est destiné à un autre centre de données Azure situé dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="14b43-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="14b43-184">L’utilisation d’un compte de stockage dans une région différente de celle du cluster HDInsight n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="14b43-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14b43-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14b43-185">Next steps</span></span>

<span data-ttu-id="14b43-186">Vous avez découvert comment ajouter des comptes de stockage Azure supplémentaires à un cluster HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="14b43-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="14b43-187">Pour plus d’informations sur les actions de script, consultez [Personnalisation de clusters HDInsight basés sur Linux à l’aide d’une d’action de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="14b43-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
