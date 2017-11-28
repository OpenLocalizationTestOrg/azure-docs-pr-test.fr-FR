---
title: "Commandes de l’interface de ligne de commande Azure en mode Resource Manager | Microsoft Docs"
description: "Les commandes de l’interface de ligne de commande Azure permettent de gérer les ressources dans le modèle de déploiement Resource Manager."
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: be957651af78519f678321aec511b71cb18a85f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="1d6f5-103">Commandes de l’interface de ligne de commande Azure en mode Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d6f5-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="1d6f5-104">Cet article fournit la syntaxe et les options des commandes de l’interface de ligne de commande Azure régulièrement utilisées pour créer et gérer les ressources Azure dans le modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use to create and manage Azure resources in the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="1d6f5-105">Pour accéder à ces commandes, exécutez l’interface de ligne de commande en mode Resource Manager (arm).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-105">You access these commands by running the CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="1d6f5-106">Il ne s’agit pas d’une référence complète, et votre version de l’interface de ligne de commande peut présenter des commandes ou paramètres légèrement différents.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="1d6f5-107">Pour obtenir une vue d'ensemble des ressources et groupes de ressources Azure, consultez [Vue d'ensemble d'Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="1d6f5-108">Cet article illustre les commandes du mode Resource Manager dans l’interface de ligne de commande Azure, parfois appelée Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-108">This article shows Resource Manager mode commands in the Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="1d6f5-109">Pour travailler dans le modèle Resource Manager, vous pouvez également essayer [Azure CLI 2.0](/cli/azure/install-az-cli2), notre nouvelle génération d’interface CLI multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-109">To work in the Resource Manager model, you can also try the [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="1d6f5-110">En savoir plus sur [les ancienne et nouvelle interfaces de ligne de commande Azure](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-110">Find out more about the [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="1d6f5-111">Pour commencer, [installez l’interface de ligne de commande (CLI) Azure](../cli-install-nodejs.md) et [connectez-vous à votre abonnement Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-111">To get started, first [install the Azure CLI](../cli-install-nodejs.md) and [connect to your Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="1d6f5-112">Pour la syntaxe et les options de commande courantes dans la ligne de commande en mode Resource Manager, tapez `azure help` ou, pour afficher de l’aide concernant une commande particulière, `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-112">For current command syntax and options at the command line in Resource Manager mode, type `azure help` or, to display help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="1d6f5-113">Dans la documentation, vous trouverez également des exemples d’interface CLI permettant de créer et de gérer certains services Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-113">Also find CLI examples in the documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="1d6f5-114">Les paramètres facultatifs sont indiqués entre crochets (par exemple, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="1d6f5-115">Tous les autres paramètres sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-115">All other parameters are required.</span></span>

<span data-ttu-id="1d6f5-116">Outre les paramètres facultatifs propres aux commandes qui vous sont présentés dans ce document, vous pouvez utiliser trois paramètres facultatifs pour afficher une sortie détaillée, telle que les options de demande et les codes d'état.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-116">In addition to command-specific optional parameters documented here, there are three optional parameters that can be used to display detailed output such as request options and status codes.</span></span> <span data-ttu-id="1d6f5-117">Si le paramètre `-v` fournit une sortie détaillée, le paramètre `-vv` propose des informations encore plus complètes.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-117">The `-v` parameter provides verbose output, and the `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="1d6f5-118">L’option `--json` génère le résultat au format JSON brut.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-118">The `--json` option outputs the result in raw json format.</span></span>

## <a name="setting-the-resource-manager-mode"></a><span data-ttu-id="1d6f5-119">Définition du mode Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d6f5-119">Setting the Resource Manager mode</span></span>
<span data-ttu-id="1d6f5-120">Utilisez la commande suivante pour activer les commandes du mode Resource Manager de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-120">Use the following command to enable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="1d6f5-121">Le mode Azure Resource Manager et le mode Azure Service Management de l’interface CLI s’excluent mutuellement.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-121">The CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="1d6f5-122">En d'autres termes, les ressources créées dans un mode ne peuvent pas être gérées dans l'autre mode.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-122">That is, resources created in one mode cannot be managed from the other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="1d6f5-123">compte azure : gérer vos informations de compte</span><span class="sxs-lookup"><span data-stu-id="1d6f5-123">azure account: Manage your account information</span></span>
<span data-ttu-id="1d6f5-124">L'outil se sert des informations sur votre abonnement Azure pour se connecter à votre compte.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-124">Your Azure subscription information is used by the tool to connect to your account.</span></span>

<span data-ttu-id="1d6f5-125">**Répertorier les abonnements importés**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-125">**List the imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="1d6f5-126">**Afficher les détails d'un abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="1d6f5-127">**Définir l'abonnement actif**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-127">**Set the current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="1d6f5-128">**Supprimer un abonnement ou environnement, ou supprimer toutes les informations de compte et d'environnement stockées**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-128">**Remove a subscription or environment, or clear all of the stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="1d6f5-129">**Commandes pour gérer votre environnement de compte**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-129">**Commands to manage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-to-display-active-directory-objects"></a><span data-ttu-id="1d6f5-130">azure ad : commandes pour afficher les objets Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d6f5-130">azure ad: Commands to display Active Directory objects</span></span>
<span data-ttu-id="1d6f5-131">**Commandes pour afficher les applications Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-131">**Commands to display active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="1d6f5-132">**Commandes pour afficher les groupes Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-132">**Commands to display active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="1d6f5-133">**Commandes pour fournir des informations sur un sous-groupe ou membre Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-133">**Commands to provide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="1d6f5-134">**Commandes pour afficher les principaux du service Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-134">**Commands to display active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="1d6f5-135">**Commandes pour afficher les utilisateurs Active Directory**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-135">**Commands to display active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-to-manage-your-availability-sets"></a><span data-ttu-id="1d6f5-136">azure availset : commandes pour gérer vos groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1d6f5-136">azure availset: commands to manage your availability sets</span></span>
<span data-ttu-id="1d6f5-137">**Créer un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="1d6f5-138">**Répertorier les groupes à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-138">**Lists the availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="1d6f5-139">**Obtenir un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="1d6f5-140">**Supprimer un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-to-manage-your-local-settings"></a><span data-ttu-id="1d6f5-141">azure config : commandes pour gérer vos paramètres locaux</span><span class="sxs-lookup"><span data-stu-id="1d6f5-141">azure config: commands to manage your local settings</span></span>
<span data-ttu-id="1d6f5-142">**Répertorier les paramètres de configuration de l'interface CLI Azure**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="1d6f5-143">**Supprimer un paramètre de configuration**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="1d6f5-144">**Mettre à jour un paramètre de configuration**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="1d6f5-145">**Définir le mode de fonctionnement de l’interface CLI Azure avec la valeur `arm` ou `asm`**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-145">**Sets the Azure CLI working mode to either `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-to-manage-account-features"></a><span data-ttu-id="1d6f5-146">azure feature : commandes pour gérer les fonctionnalités de compte</span><span class="sxs-lookup"><span data-stu-id="1d6f5-146">azure feature: commands to manage account features</span></span>
<span data-ttu-id="1d6f5-147">**Répertorier toutes les fonctionnalités disponibles pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="1d6f5-148">**Présenter une fonctionnalité**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="1d6f5-149">**Enregistrer une fonctionnalité préliminaire d'un fournisseur de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-to-manage-your-resource-groups"></a><span data-ttu-id="1d6f5-150">azure group : commandes pour gérer vos groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="1d6f5-150">azure group: Commands to manage your resource groups</span></span>
<span data-ttu-id="1d6f5-151">**Créer un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="1d6f5-152">**Définir des balises dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-152">**Set tags to a resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="1d6f5-153">**Supprimer un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="1d6f5-154">**Répertorier les groupes de ressources pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-154">**Lists the resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="1d6f5-155">**Afficher un groupe de ressources pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="1d6f5-156">**Commandes pour gérer les journaux de groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-156">**Commands to manage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="1d6f5-157">**Commandes pour gérer votre déploiement dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-157">**Commands to manage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="1d6f5-158">**Commandes pour gérer le modèle de votre groupe de ressources local ou de la galerie**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-158">**Commands to manage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-to-manage-your-hdinsight-clusters"></a><span data-ttu-id="1d6f5-159">azure hdinsight : Commandes pour gérer vos clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="1d6f5-159">azure hdinsight: Commands to manage your HDInsight clusters</span></span>
<span data-ttu-id="1d6f5-160">**Commandes pour créer ou ajouter un fichier de configuration de cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-160">**Commands to create or add to a cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="1d6f5-161">Exemple : créer un fichier de configuration qui contient une action de script à exécuter lors de la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-161">Example: Create a configuration file that contains a script action to run when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="1d6f5-162">**Commande pour créer un cluster dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-162">**Command to create a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="1d6f5-163">Exemple : créer un Storm sur Linux cluster</span><span class="sxs-lookup"><span data-stu-id="1d6f5-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="1d6f5-164">Exemple : créer un cluster avec une action de script</span><span class="sxs-lookup"><span data-stu-id="1d6f5-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting the request to create cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="1d6f5-165">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       The name of the resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for the cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url to use for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key to the storage account to use for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in the storage account to use for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for the cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes to use for the cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for the cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for the cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for the cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for the cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In the format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for the external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for the external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for the external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for the external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for the external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for the external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for the external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for the external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    The subscription id
    --tags <tags>                                              Tags to set to the cluster.
    Can be multiple.
    In the format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="1d6f5-166">**Commande pour supprimer un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-166">**Command to delete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="1d6f5-167">**Commande pour afficher les détails du cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-167">**Command to show cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="1d6f5-168">**Commande pour répertorier tous les clusters (dans un groupe de ressources spécifique, si fourni)**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-168">**Command to list all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="1d6f5-169">**Commande pour redimensionner un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-169">**Command to resize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="1d6f5-170">**Commande pour activer l’accès HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-170">**Command to enable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="1d6f5-171">**Commande pour désactiver l’accès HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-171">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="1d6f5-172">**Commande pour activer l’accès RDP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-172">**Command to enable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="1d6f5-173">**Commande pour désactiver l’accès HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-173">**Command to disable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-to-monitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="1d6f5-174">azure insights : commandes liées à la surveillance d'informations détaillées (événements, règles d'alerte, paramètres de mise à l'échelle automatique, mesures)</span><span class="sxs-lookup"><span data-stu-id="1d6f5-174">azure insights: Commands related to monitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="1d6f5-175">**Récupérer les journaux des opérations pour un abonnement, un ID de corrélation, un groupe de ressources, une ressource ou un fournisseur de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-to-get-the-available-locations-for-all-resource-types"></a><span data-ttu-id="1d6f5-176">azure location : commandes pour obtenir les emplacements disponibles pour tous les types de ressource</span><span class="sxs-lookup"><span data-stu-id="1d6f5-176">azure location: Commands to get the available locations for all resource types</span></span>
<span data-ttu-id="1d6f5-177">**Répertorier les emplacements disponibles**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-177">**List the available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-to-manage-network-resources"></a><span data-ttu-id="1d6f5-178">azure network : commandes pour gérer les ressources réseau</span><span class="sxs-lookup"><span data-stu-id="1d6f5-178">azure network: Commands to manage network resources</span></span>
<span data-ttu-id="1d6f5-179">**Commandes pour gérer les réseaux virtuels**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-179">**Commands to manage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="1d6f5-180">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-180">Creates a virtual network.</span></span> <span data-ttu-id="1d6f5-181">Dans l'exemple suivant, nous créons un réseau virtuel nommé newvnet pour le groupe de ressources myresourcegroup dans la région Ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-181">In the following example we create a virtual network named newvnet for resource group myresourcegroup in the West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="1d6f5-182">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      the name of the resource group
     -n, --name <name>                          the name of the virtual network
     -l, --location <location>                  the location
     -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            the comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          the tags set on this virtual network.
      Can be multiple. In the format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="1d6f5-183">Met à jour une configuration de réseau virtuel dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="1d6f5-184">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      the name of the resource group
       -n, --name <name>                          the name of the virtual network
       -a, --address-prefixes <address-prefixes>  the comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended to the current list of address prefixes.
        The address prefixes in this list should not overlap between them.
        The address prefixes in this list should not overlap with existing address prefixes in the vnet.

       -d, --dns-servers [dns-servers]            the comma separated list of DNS servers IP addresses.
        This list will be appended to the current list of DNS server IP addresses.

       -t, --tags <tags>                          the tags set on this virtual network.
        Can be multiple. In the format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended to the current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          the subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="1d6f5-185">La commande répertorie tous les réseaux virtuels dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-185">The command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="1d6f5-186">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  the name of the resource group
      -s, --subscription <subscription>      the subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="1d6f5-187">La commande affiche les propriétés du réseau virtuel dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-187">The command shows the virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="1d6f5-188">La commande supprime un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-188">The command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="1d6f5-189">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="1d6f5-190">**Commandes pour gérer les sous-réseaux de réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-190">**Commands to manage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="1d6f5-191">Ajoute un autre sous-réseau à un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-191">Adds another subnet to an existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up the subnet "subnet"
    + Creating subnet "subnet"
    + Looking up the subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="1d6f5-192">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            the name of the resource group
     -e, --vnet-name <vnet-name>                                      the name of the virtual network
     -n, --name <name>                                                the name of the subnet
     -a, --address-prefix <address-prefix>                            the address prefix
     -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  the network security group name
     -s, --subscription <subscription>                                the subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="1d6f5-193">Définit un sous-réseau de réseau virtuel spécifique au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="1d6f5-194">Répertorie tous les sous-réseaux d'un réseau virtuel spécifique au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-194">Lists all the virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up the subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="1d6f5-195">Affiche les propriétés des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1d6f5-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up the subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="1d6f5-196">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -e, --vnet-name <vnet-name>            the name of the virtual network
    -n, --name <name>                      the name of the subnet
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="1d6f5-197">Supprime un sous-réseau d'un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up the subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="1d6f5-198">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -e, --vnet-name <vnet-name>            the name of the virtual network
     -n, --name <name>                      the subnet name
     -s, --subscription <subscription>      the subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="1d6f5-199">**Commandes pour gérer les équilibrages de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-199">**Commands to manage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="1d6f5-200">Crée un jeu d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up the load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="1d6f5-201">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -l, --location <location>              the location
    -t, --tags <tags>                      the list of tags.
     Can be multiple. In the format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="1d6f5-202">Répertorie les ressources d'équilibrage de charge au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting the load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="1d6f5-203">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="1d6f5-204">Affiche les informations d'un équilibrage de charge spécifique au sein d'un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="1d6f5-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="1d6f5-205">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="1d6f5-206">Supprime les ressources d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up the load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="1d6f5-207">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -n, --name <name>                      the name of the load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="1d6f5-208">**Commandes pour gérer les sondes d'équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-208">**Commands to manage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-209">Crée la configuration de sonde pour l'état d'intégrité dans l'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-209">Create the probe configuration for health status in the load balancer.</span></span> <span data-ttu-id="1d6f5-210">N'oubliez pas que pour exécuter cette commande, votre équilibrage de charge requiert une ressource IP frontale (consultez la commande « azure network frontend-ip » pour attribuer une adresse IP à l'équilibrage de charge).</span><span class="sxs-lookup"><span data-stu-id="1d6f5-210">Keep in mind to run this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" to assign an ip address to load balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="1d6f5-211">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -p, --protocol <protocol>              the probe protocol
    -o, --port <port>                      the probe port
    -f, --path <path>                      the probe path
    -i, --interval <interval>              the probe interval in seconds
    -c, --count <count>                    the number of probes
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-212">Met à jour la sonde d’un équilibrage de charge existant avec de nouvelles valeurs.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="1d6f5-213">Options de paramètre</span><span class="sxs-lookup"><span data-stu-id="1d6f5-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the probe
    -e, --new-probe-name <new-probe-name>  the new name of the probe
    -p, --protocol <protocol>              the new value for probe protocol
    -o, --port <port>                      the new value for probe port
    -f, --path <path>                      the new value for probe path
    -i, --interval <interval>              the new value for probe interval in seconds
    -c, --count <count>                    the new value for number of probes
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="1d6f5-214">Répertorie les propriétés de sonde pour un jeu d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-214">List the probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up the load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="1d6f5-215">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-216">Supprime la sonde créée pour l'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-216">Removes the probe created for the load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up the load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="1d6f5-217">**Commandes pour gérer les configurations IP frontales d'un équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-217">**Commands to manage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-218">Crée une configuration IP frontale dans un jeu d'équilibrage de charge existant.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-218">Creates a frontend IP configuration to an existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up the load balancer "mylb"
    + Looking up the subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-219">Met à jour une configuration existante d’adresse IP frontale. La commande suivante ajoute une adresse IP publique appelée mypubip5 à une adresse IP frontale d’équilibrage de charge nommée myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-219">Updates an existing configuration of a frontend IP.The command below adds a public IP called mypubip5 to an existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up the load balancer "mylb"
    + Looking up the public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="1d6f5-220">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              the name of the resource group
    -l, --lb-name <lb-name>                                            the name of the load balancer
    -n, --name <name>                                                  the name of the frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      the private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  the private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  the public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              the public ip name.
    This public ip must exist in the same resource group as the lb.
    Please use public-ip-id if that is not the case.
    -b, --subnet-id <subnet-id>                                        the subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    the subnet name
    -m, --vnet-name <vnet-name>                                        the virtual network name.
    This virtual network must exist in the same resource group as the lb.
    Please use subnet-id if that is not the case.
    -s, --subscription <subscription>                                  the subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="1d6f5-221">Répertorie toutes les ressources IP frontales configurées pour l'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-221">Lists all the frontend IP resources configured for the load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="1d6f5-222">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-223">Supprime l'objet IP frontal associé à l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="1d6f5-223">Deletes the frontend IP object associated to load balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up the load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="1d6f5-224">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="1d6f5-225">**Commandes pour gérer les pools d'adresses principales d'un équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-225">**Commands to manage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-226">Crée un pool d'adresses principales pour un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="1d6f5-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="1d6f5-227">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -s, --subscription <subscription>      the subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="1d6f5-228">Indique la plage du pool d'adresses IP principales pour un groupe de ressources spécifique</span><span class="sxs-lookup"><span data-stu-id="1d6f5-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up the load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="1d6f5-229">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  the name of the resource group
     -l, --lb-name <lb-name>                the name of the load balancer
     -s, --subscription <subscription>      the subscription identifier

<BR>
    <span data-ttu-id="1d6f5-230">supprimer des livres-pool d’adresses réseau [options] < groupe de ressources >< lb-name ><name></span><span class="sxs-lookup"><span data-stu-id="1d6f5-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="1d6f5-231">Supprime la ressource de la plage du pool d'adresses IP principales dans l'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-231">Removes the backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up the load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="1d6f5-232">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="1d6f5-233">**Commandes pour gérer les règles d'équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-233">**Commands to manage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-234">Crée des règles d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-234">Create load balancer rules.</span></span>

<span data-ttu-id="1d6f5-235">Vous pouvez créer une règle d’équilibrage de charge qui configure le point de terminaison frontal pour l’équilibrage de charge et la plage du pool d’adresses principales qui reçoit le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-235">You can create a load balancer rule configuring the frontend endpoint for the load balancer and the backend address pool range to receive the incoming network traffic.</span></span> <span data-ttu-id="1d6f5-236">Les paramètres incluent également les ports du point de terminaison de l'adresse IP frontale et les ports de la plage du pool d'adresses IP principales.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-236">Settings also include the ports for frontend IP endpoint and ports for the backend address pool range.</span></span>

<span data-ttu-id="1d6f5-237">L’exemple suivant montre comment créer une règle d’équilibrage de charge, le point de terminaison frontal écoutant le port TCP 80 et le trafic réseau de l’équilibrage de charge étant envoyé sur le port 8080 pour la plage du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-237">The following example shows how to create a load balancer rule,  the frontend endpoint listening to port 80 TCP and load balancing network traffic sending to port 8080 for the backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-238">Met à jour une règle d'équilibrage de charge existante définie dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="1d6f5-239">Dans l’exemple suivant, nous avons remplacé le nom de la règle mylbrule par mynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-239">In the following example, we changed the rule name from mylbrule to mynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="1d6f5-240">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              the name of the resource group
    -l, --lb-name <lb-name>                            the name of the load balancer
    -n, --name <name>                                  the name of the rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          the rule protocol
    -f, --frontend-port <frontend-port>                the frontend port
    -b, --backend-port <backend-port>                  the backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  the idle timeout in minutes
    -a, --probe-name [probe-name]                      the name of the probe defined in the same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          the name of the frontend ip configuration in the same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of the backend address pool defined in the same load balancer
    -s, --subscription <subscription>                  the subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="1d6f5-241">Répertorie toutes les règles d'équilibrage de charge configurées pour un équilibrage de charge dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up the load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="1d6f5-242">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-243">Supprime une règle d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up the load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="1d6f5-244">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="1d6f5-245">**Commandes pour gérer les règles NAT entrantes d'équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-245">**Commands to manage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-246">Crée une règle NAT entrante pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="1d6f5-247">Dans l’exemple suivant, nous avons créé une règle NAT à partir d’une adresse IP frontale (préalablement définie à l’aide de la commande « azure network frontend-ip ») avec un port d’écoute entrant et un port de sortie que l’équilibreur de charge utilise pour envoyer le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-247">In the following example  we created a NAT rule from frontend IP (which was previously defined using the "azure network frontend-ip" command) with an inbound listening port and outbound port that the load balancer uses to send the network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="1d6f5-248">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id <vm-id>                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.This VM must exist in the same resource group as the lb.
    Please use vm-id if that is not the case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="1d6f5-249">Met à jour une règle NAT entrante existante.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="1d6f5-250">Dans l’exemple suivant, nous avons remplacé le port d’écoute entrant 80 par 81.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-250">In the following example, we changed the inbound listening port from 80 to 81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up the load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up the load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="1d6f5-251">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          the name of the resource group
    -l, --lb-name <lb-name>                        the name of the load balancer
    -n, --name <name>                              the name of the inbound NAT rule
    -p, --protocol <protocol>                      the rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            the frontend port [0-65535]
    -b, --backend-port <backend-port>              the backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                the name of the frontend ip configuration
    -m, --vm-id [vm-id]                            the VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        the VM name.
    This virtual machine must exist in the same resource group as the lb.
    Please use vm-id if that is not the case
    -s, --subscription <subscription>              the subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="1d6f5-252">Répertorie toutes les règles NAT entrantes pour un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up the load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="1d6f5-253">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -s, --subscription <subscription>      the subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="1d6f5-254">Supprime la règle NAT pour l'équilibrage de charge dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-254">Deletes NAT rule for the load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up the load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="1d6f5-255">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -l, --lb-name <lb-name>                the name of the load balancer
    -n, --name <name>                      the name of the inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier

<span data-ttu-id="1d6f5-256">**Commandes pour gérer les adresses IP publiques**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-256">**Commands to manage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="1d6f5-257">Crée une ressource IP publique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-257">Creates a public ip resource.</span></span> <span data-ttu-id="1d6f5-258">Vous créez la ressource IP publique et l'associez à un nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-258">You will create the public ip resource and associate to a domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up the public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="1d6f5-259">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -l, --location <location>                    the location
    -d, --domain-name-label <domain-name-label>  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            the subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="1d6f5-260">Met à jour les propriétés d'une ressource IP publique existante.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-260">Updates the properties of an existing public ip resource.</span></span> <span data-ttu-id="1d6f5-261">Dans l'exemple suivant, nous avons remplacé l'adresse IP publique dynamique en adresse IP statique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-261">In the following example we changed the public IP address from Dynamic to Static.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up the public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="1d6f5-262">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        the name of the resource group
    -n, --name <name>                            the name of the public ip
    -d, --domain-name-label [domain-name-label]  the domain name label.
    This set DNS to <domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  the allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              the idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            the reverse fqdn
    -t, --tags <tags>                            the list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            the subscription identifier

<br>
    <span data-ttu-id="1d6f5-263">network public-ip list [options] &lt;groupe-ressources&gt; Répertorie toutes les ressources IP publiques au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting the public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="1d6f5-264">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -s, --subscription <subscription>      the subscription identifier
<BR>
    <span data-ttu-id="1d6f5-265">réseau public-ip afficher [options] < groupe de ressources ><name></span><span class="sxs-lookup"><span data-stu-id="1d6f5-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="1d6f5-266">Affiche les propriétés d’adresse IP publique pour une ressource IP publique au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up the public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="1d6f5-267">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -s, --subscription <subscription>      the subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="1d6f5-268">Supprime une ressource IP publique.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up the public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="1d6f5-269">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  the name of the resource group
    -n, --name <name>                      the name of the public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      the subscription identifier


<span data-ttu-id="1d6f5-270">**Commandes pour gérer les interfaces réseau**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-270">**Commands to manage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="1d6f5-271">Crée une ressource appelée interface réseau (NIC) qui peut être utilisée pour les équilibrages de charge ou associée à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate to a Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up the network interface "testnic1"
    + Looking up the subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up the network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="1d6f5-272">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="1d6f5-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            the name of the resource group
    -n, --name <name>                                                the name of the network interface
    -l, --location <location>                                        the location
    -w, --network-security-group-id <network-security-group-id>      the network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  the network security group name.
    This network security group must exist in the same resource group as the nic.
    Please use network-security-group-id if that is not the case.
    -i, --public-ip-id <public-ip-id>                                the public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            the public IP name.
    This public ip must exist in the same resource group as the nic.
    Please use public-ip-id if that is not the case.
    -a, --private-ip-address <private-ip-address>                    the private IP address
    -u, --subnet-id <subnet-id>                                      the subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  the subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        the vnet name under which subnet-name exists
    -t, --tags <tags>                                                the comma seperated list of tags.
    Can be multiple. In the format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                the subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="1d6f5-273">**Commandes pour gérer les groupes de sécurité réseau**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-273">**Commands to manage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="1d6f5-274">**Commandes pour gérer les règles de groupe de sécurité réseau**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-274">**Commands to manage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="1d6f5-275">**Commandes pour gérer le profil Traffic Manager**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-275">**Commands to manage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="1d6f5-276">**Commandes pour gérer les points de terminaison Traffic Manager**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-276">**Commands to manage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="1d6f5-277">**Commandes pour gérer les passerelles de réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-277">**Commands to manage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-to-manage-resource-provider-registrations"></a><span data-ttu-id="1d6f5-278">azure provider : commandes pour gérer les enregistrements de fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="1d6f5-278">azure provider: Commands to manage resource provider registrations</span></span>
<span data-ttu-id="1d6f5-279">**Répertorier les fournisseurs actuellement enregistrés dans Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="1d6f5-280">**Afficher les détails de l'espace de noms du fournisseur demandé**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-280">**Show details about the requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="1d6f5-281">**Enregistrer le fournisseur avec l'abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-281">**Register provider with the subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="1d6f5-282">**Annuler l'enregistrement du fournisseur dans l'abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-282">**Unregister provider with the subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-to-manage-your-resources"></a><span data-ttu-id="1d6f5-283">azure resource : commandes pour gérer vos ressources</span><span class="sxs-lookup"><span data-stu-id="1d6f5-283">azure resource: Commands to manage your resources</span></span>
<span data-ttu-id="1d6f5-284">**Créer une ressource dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="1d6f5-285">**Mettre à jour une ressource dans un groupe de ressources sans aucun modèle ou paramètre**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="1d6f5-286">**Répertorier les ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-286">**Lists the resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="1d6f5-287">**Obtenir une ressource au sein d'un groupe de ressources ou d'un abonnement**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="1d6f5-288">**Supprimer une ressource dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-to-manage-your-azure-roles"></a><span data-ttu-id="1d6f5-289">azure role : commandes pour gérer vos rôles Azure</span><span class="sxs-lookup"><span data-stu-id="1d6f5-289">azure role: Commands to manage your Azure roles</span></span>
<span data-ttu-id="1d6f5-290">**Obtenir toutes les définitions de rôles disponibles**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="1d6f5-291">**Obtenir une définition de rôles disponible**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="1d6f5-292">**Commandes pour gérer votre attribution de rôle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-292">**Commands to manage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-to-manage-your-storage-objects"></a><span data-ttu-id="1d6f5-293">azure storage : commandes pour gérer vos objets de stockage</span><span class="sxs-lookup"><span data-stu-id="1d6f5-293">azure storage: Commands to manage your Storage objects</span></span>
<span data-ttu-id="1d6f5-294">**Commandes pour gérer vos comptes de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-294">**Commands to manage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="1d6f5-295">**Commandes pour gérer vos clés de compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-295">**Commands to manage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="1d6f5-296">**Commandes pour afficher votre chaîne de connexion de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-296">**Commands to show your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="1d6f5-297">**Commandes pour gérer vos conteneurs de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-297">**Commands to manage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="1d6f5-298">**Commandes pour gérer les signatures d'accès partagé de votre conteneur de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-298">**Commands to manage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="1d6f5-299">**Commandes pour gérer les stratégies d'accès stockées de votre conteneur de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-299">**Commands to manage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="1d6f5-300">**Commandes pour gérer vos objets blob de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-300">**Commands to manage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="1d6f5-301">**Commandes pour gérer vos opérations de copie d'objet blob**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-301">**Commands to manage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="1d6f5-302">**Commandes pour gérer la signature d'accès partagé de votre objet blob de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-302">**Commands to manage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="1d6f5-303">**Commandes pour gérer vos partages de fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-303">**Commands to manage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="1d6f5-304">**Commandes pour gérer vos fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-304">**Commands to manage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="1d6f5-305">**Commandes pour gérer votre répertoire de fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-305">**Commands to manage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="1d6f5-306">**Commandes pour gérer vos files d'attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-306">**Commands to manage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="1d6f5-307">**Commandes pour gérer les signatures d'accès partagé de votre file d'attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-307">**Commands to manage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="1d6f5-308">**Commandes pour gérer les stratégies d'accès stockées de votre file d'attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-308">**Commands to manage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="1d6f5-309">**Commandes pour gérer vos propriétés de journalisation de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-309">**Commands to manage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="1d6f5-310">**Commandes pour gérer vos propriétés de mesure de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-310">**Commands to manage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="1d6f5-311">**Commandes pour gérer vos tables de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-311">**Commands to manage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="1d6f5-312">**Commandes pour gérer les signatures d'accès partagé de votre table de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-312">**Commands to manage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="1d6f5-313">**Commandes pour gérer les stratégies d'accès stockées de votre table de stockage**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-313">**Commands to manage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-to-manage-your-resource-manager-tag"></a><span data-ttu-id="1d6f5-314">azure tag : commandes pour gérer les balises de votre gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="1d6f5-314">azure tag: Commands to manage your resource manager tag</span></span>
<span data-ttu-id="1d6f5-315">**Ajouter une balise**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="1d6f5-316">**Supprimer une balise entière ou une valeur de balise**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="1d6f5-317">**Répertorier les informations de balise**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-317">**Lists the tag information**</span></span>

    tag list [options]

<span data-ttu-id="1d6f5-318">**Obtenir une balise**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-to-manage-your-azure-virtual-machines"></a><span data-ttu-id="1d6f5-319">azure vm : commandes pour gérer vos machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="1d6f5-319">azure vm: Commands to manage your Azure Virtual Machines</span></span>
<span data-ttu-id="1d6f5-320">**Créer une machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="1d6f5-321">**Créer une machine virtuelle avec les ressources par défaut**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="1d6f5-322">À partir de l’interface de ligne de commande version 0.10, vous pouvez fournir un court alias tel que « UbuntuLTS » ou « Win2012R2Datacenter » comme `image-urn` pour certaines images Marketplace populaires.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as the `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="1d6f5-323">Exécutez `azure help vm quick-create` pour voir les options.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="1d6f5-324">En outre, à partir de la version 0.10, `azure vm quick-create` utilise le stockage Premium par défaut s’il est disponible dans la région sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="1d6f5-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in the selected region.</span></span>
> 
> 

<span data-ttu-id="1d6f5-325">**Répertorier les machines virtuelles dans un compte**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-325">**List the virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="1d6f5-326">**Obtenir une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="1d6f5-327">**Supprimer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="1d6f5-328">**Arrêter une machine virtuelle au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="1d6f5-329">**Redémarrer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="1d6f5-330">**Démarrer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="1d6f5-331">**Arrêter une machine virtuelle au sein d'un groupe de ressources et libérer les ressources de calcul**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-331">**Shutdown one virtual machine within a resource group and releases the compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="1d6f5-332">**Répertorier les tailles disponibles des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="1d6f5-333">**Capturer la machine virtuelle en tant qu'image de système d'exploitation ou image de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-333">**Capture the VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="1d6f5-334">**Régler l'état de la machine virtuelle sur Généralisé**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-334">**Set the state of the VM to Generalized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="1d6f5-335">**Obtenir la vue d'instance de la machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-335">**Get instance view of the VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="1d6f5-336">**Vous permet de réinitialiser les paramètres d'accès au Bureau à distance ou SSH sur une machine virtuelle et de réinitialiser le mot de passe pour le compte disposant d’un administrateur ou d’une autorité sudo**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-336">**Enable you to reset Remote Desktop Access or SSH settings on a Virtual Machine and to reset the password for the account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="1d6f5-337">**Mettre à jour une machine virtuelle avec de nouvelles données**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="1d6f5-338">**Commandes pour gérer vos disques de données de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-338">**Commands to manage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="1d6f5-339">**Commandes pour gérer les extensions de ressource de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-339">**Commands to manage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="1d6f5-340">**Commandes pour gérer votre machine virtuelle Docker**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-340">**Commands to manage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="1d6f5-341">**Commandes pour gérer les images de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="1d6f5-341">**Commands to manage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
