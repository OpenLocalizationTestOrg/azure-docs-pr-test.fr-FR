---
title: aaaAzure CLI des commandes en mode de gestionnaire de ressources | Documents Microsoft
description: "Interface de ligne de commande (CLI) Azure commandes toomanage des ressources dans le modèle de déploiement du Gestionnaire de ressources hello"
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
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="e182f-103">Commandes de l’interface de ligne de commande Azure en mode Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e182f-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="e182f-104">Cet article fournit la syntaxe et options pour Azure interface de ligne de commande (CLI) commandes que vous devez généralement utilisent toocreate et gérer des ressources Azure dans le modèle de déploiement du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e182f-105">Pour accéder à ces commandes en exécutant hello CLI en mode de gestionnaire de ressources (arm).</span><span class="sxs-lookup"><span data-stu-id="e182f-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="e182f-106">Il ne s’agit pas d’une référence complète, et votre version de l’interface de ligne de commande peut présenter des commandes ou paramètres légèrement différents.</span><span class="sxs-lookup"><span data-stu-id="e182f-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="e182f-107">Pour obtenir une vue d'ensemble des ressources et groupes de ressources Azure, consultez [Vue d'ensemble d'Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e182f-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="e182f-108">Ce article affiche les commandes de mode du Gestionnaire de ressources Bonjour CLI d’Azure, parfois appelé Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="e182f-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="e182f-109">toowork dans le modèle de gestionnaire de ressources hello, vous pouvez aussi essayer hello [Azure CLI 2.0](/cli/azure/install-az-cli2), notre nouvelle génération de plusieurs plates-formes CLI.</span><span class="sxs-lookup"><span data-stu-id="e182f-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="e182f-110">En savoir plus sur hello [CLI d’Azure anciennes et nouvelles](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="e182f-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="e182f-111">tooget démarré en premier [installer hello CLI d’Azure](../cli-install-nodejs.md) et [connecter tooyour abonnement Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e182f-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="e182f-112">Syntaxe de la commande et les options de ligne de commande hello en mode de gestionnaire de ressources, tapez `azure help` ou, à l’aide toodisplay pour une commande spécifique, `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="e182f-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="e182f-113">Exemples montrent également CLI dans la documentation de hello pour la création et la gestion des services Azure spécifiques.</span><span class="sxs-lookup"><span data-stu-id="e182f-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="e182f-114">Les paramètres facultatifs sont indiqués entre crochets (par exemple, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="e182f-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="e182f-115">Tous les autres paramètres sont obligatoires.</span><span class="sxs-lookup"><span data-stu-id="e182f-115">All other parameters are required.</span></span>

<span data-ttu-id="e182f-116">Dans les paramètres facultatifs spécifiques toocommand plus documentés ici, il existe trois paramètres facultatifs qui peuvent être utilisé toodisplay détaillées sortie tels que les options de demande et les codes d’état.</span><span class="sxs-lookup"><span data-stu-id="e182f-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="e182f-117">Hello `-v` paramètre fournit la sortie des commentaires et hello `-vv` paramètre fournit encore plus la sortie des commentaires.</span><span class="sxs-lookup"><span data-stu-id="e182f-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="e182f-118">Hello `--json` option génère le résultat de hello au format json brut.</span><span class="sxs-lookup"><span data-stu-id="e182f-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="e182f-119">Paramètre de mode de gestionnaire de ressources hello</span><span class="sxs-lookup"><span data-stu-id="e182f-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="e182f-120">Utilisez hello suivant les commandes du mode commande tooenable Azure CLI Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e182f-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="e182f-121">mode Azure Resource Manager et le mode de gestion des services Azure de Hello CLI sont mutuellement exclusifs.</span><span class="sxs-lookup"><span data-stu-id="e182f-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="e182f-122">Autrement dit, les ressources créées dans un mode ne peut pas être gérés à partir de hello autre mode.</span><span class="sxs-lookup"><span data-stu-id="e182f-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="e182f-123">compte azure : gérer vos informations de compte</span><span class="sxs-lookup"><span data-stu-id="e182f-123">azure account: Manage your account information</span></span>
<span data-ttu-id="e182f-124">Vos informations d’abonnement Azure sont utilisées par le compte de tooyour tooconnect hello outil.</span><span class="sxs-lookup"><span data-stu-id="e182f-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="e182f-125">**Dresser la liste des abonnements de hello importé**</span><span class="sxs-lookup"><span data-stu-id="e182f-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="e182f-126">**Afficher les détails d'un abonnement**</span><span class="sxs-lookup"><span data-stu-id="e182f-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="e182f-127">**Définir l’abonnement actuel de hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="e182f-128">**Supprimer un abonnement ou un environnement, ou effacer toutes les informations de compte et environnement stockée hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="e182f-129">**Commandes toomanage votre environnement de compte**</span><span class="sxs-lookup"><span data-stu-id="e182f-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="e182f-130">Azure ad : commandes toodisplay les objets Active Directory</span><span class="sxs-lookup"><span data-stu-id="e182f-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="e182f-131">**Applications de commandes toodisplay active directory**</span><span class="sxs-lookup"><span data-stu-id="e182f-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="e182f-132">**Commandes toodisplay les groupes Active Directory**</span><span class="sxs-lookup"><span data-stu-id="e182f-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="e182f-133">**Commandes tooprovide l’informations de groupe ou un membre de sub active directory**</span><span class="sxs-lookup"><span data-stu-id="e182f-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="e182f-134">**Principaux du service active directory commandes toodisplay**</span><span class="sxs-lookup"><span data-stu-id="e182f-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="e182f-135">**Commandes toodisplay les utilisateurs Active Directory**</span><span class="sxs-lookup"><span data-stu-id="e182f-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="e182f-136">Azure availset : ensembles de votre disponibilité toomanage de commandes</span><span class="sxs-lookup"><span data-stu-id="e182f-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="e182f-137">**Créer un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="e182f-138">**Listes hello haute disponibilité au sein d’un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="e182f-139">**Obtenir un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="e182f-140">**Supprimer un groupe à haute disponibilité au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="e182f-141">configuration d’Azure : commandes toomanage vos paramètres régionaux</span><span class="sxs-lookup"><span data-stu-id="e182f-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="e182f-142">**Répertorier les paramètres de configuration de l'interface CLI Azure**</span><span class="sxs-lookup"><span data-stu-id="e182f-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="e182f-143">**Supprimer un paramètre de configuration**</span><span class="sxs-lookup"><span data-stu-id="e182f-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="e182f-144">**Mettre à jour un paramètre de configuration**</span><span class="sxs-lookup"><span data-stu-id="e182f-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="e182f-145">**Jeux de hello CLI d’Azure fonctionne en mode tooeither `arm` ou`asm`**</span><span class="sxs-lookup"><span data-stu-id="e182f-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="e182f-146">la fonctionnalité Azure : fonctionnalités de compte toomanage des commandes</span><span class="sxs-lookup"><span data-stu-id="e182f-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="e182f-147">**Répertorier toutes les fonctionnalités disponibles pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="e182f-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="e182f-148">**Présenter une fonctionnalité**</span><span class="sxs-lookup"><span data-stu-id="e182f-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="e182f-149">**Enregistrer une fonctionnalité préliminaire d'un fournisseur de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="e182f-150">groupe Azure : commandes toomanage vos groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="e182f-151">**Créer un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="e182f-152">**Groupe de ressources de jeu de balises tooa**</span><span class="sxs-lookup"><span data-stu-id="e182f-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="e182f-153">**Supprimer un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="e182f-154">**Répertorie les groupes de ressources hello pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="e182f-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="e182f-155">**Afficher un groupe de ressources pour votre abonnement**</span><span class="sxs-lookup"><span data-stu-id="e182f-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="e182f-156">**Journaux du groupe de commandes toomanage ressource**</span><span class="sxs-lookup"><span data-stu-id="e182f-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="e182f-157">**Commandes toomanage votre déploiement dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="e182f-158">**Commandes toomanage votre modèle de groupe de ressources local ou de la galerie**</span><span class="sxs-lookup"><span data-stu-id="e182f-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="e182f-159">Azure hdinsight : commandes toomanage vos clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e182f-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="e182f-160">**Commandes toocreate ou ajouter le fichier de configuration de cluster tooa**</span><span class="sxs-lookup"><span data-stu-id="e182f-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="e182f-161">Exemple : Création d’un fichier de configuration qui contient un toorun d’action de script lors de la création d’un cluster.</span><span class="sxs-lookup"><span data-stu-id="e182f-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="e182f-162">**Commande toocreate un cluster dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="e182f-163">Exemple : créer un Storm sur Linux cluster</span><span class="sxs-lookup"><span data-stu-id="e182f-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="e182f-164">Exemple : créer un cluster avec une action de script</span><span class="sxs-lookup"><span data-stu-id="e182f-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="e182f-165">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="e182f-166">**Commande toodelete un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="e182f-167">**Détails du cluster commande tooshow**</span><span class="sxs-lookup"><span data-stu-id="e182f-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="e182f-168">**Toolist commande tous les clusters (dans un groupe de ressources spécifique, si fournie)**</span><span class="sxs-lookup"><span data-stu-id="e182f-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="e182f-169">**Commande tooresize un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="e182f-170">**Commande d’accès tooenable HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="e182f-171">**Commande d’accès toodisable HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="e182f-172">**Commande tooenable RDP accès pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="e182f-173">**Commande d’accès toodisable HTTP pour un cluster**</span><span class="sxs-lookup"><span data-stu-id="e182f-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="e182f-174">Azure insights : commandes liées Insights toomonitoring (événements, règles d’alerte, les paramètres de mise à l’échelle, mesures)</span><span class="sxs-lookup"><span data-stu-id="e182f-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="e182f-175">**Récupérer les journaux des opérations pour un abonnement, un ID de corrélation, un groupe de ressources, une ressource ou un fournisseur de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="e182f-176">emplacement Azure : commandes emplacements de hello tooget disponibles pour tous les types de ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="e182f-177">**Liste des emplacements disponibles hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="e182f-178">réseau Azure : ressources du réseau toomanage des commandes</span><span class="sxs-lookup"><span data-stu-id="e182f-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="e182f-179">**Réseaux virtuels toomanage de commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="e182f-180">Créer un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e182f-180">Creates a virtual network.</span></span> <span data-ttu-id="e182f-181">Bonjour exemple suivant, nous créons un réseau virtuel nommé newvnet pour myresourcegroup de groupe de ressources dans la région ouest des États-Unis hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

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


<span data-ttu-id="e182f-182">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="e182f-183">Met à jour une configuration de réseau virtuel dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-183">Updates a virtual network configuration within a resource group.</span></span>

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

<span data-ttu-id="e182f-184">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="e182f-185">commande Hello répertorie tous les réseaux virtuels dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-185">hello command lists all virtual networks in a resource group.</span></span>

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

<span data-ttu-id="e182f-186">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="e182f-187">commande Hello affiche les propriétés de réseau virtuel hello dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-187">hello command shows hello virtual network properties in a resource group.</span></span>

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
<span data-ttu-id="e182f-188">commande Hello supprime un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e182f-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="e182f-189">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="e182f-190">**Sous-réseaux du réseau virtuel commandes toomanage**</span><span class="sxs-lookup"><span data-stu-id="e182f-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="e182f-191">Ajoute un autre sous-réseau tooan réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e182f-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="e182f-192">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="e182f-193">Définit un sous-réseau de réseau virtuel spécifique au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="e182f-194">Répertorie tous les sous-réseaux du réseau virtuel hello pour un réseau virtuel spécifique au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="e182f-195">Affiche les propriétés des sous-réseaux de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="e182f-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="e182f-196">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="e182f-197">Supprime un sous-réseau d'un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="e182f-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="e182f-198">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="e182f-199">**Équilibreurs de charge toomanage de commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="e182f-200">Crée un jeu d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="e182f-201">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="e182f-202">Répertorie les ressources d'équilibrage de charge au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="e182f-203">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="e182f-204">Affiche les informations d'un équilibrage de charge spécifique au sein d'un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="e182f-205">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="e182f-206">Supprime les ressources d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="e182f-207">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e182f-208">**Commandes toomanage les sondes d’équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="e182f-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e182f-209">Créer la configuration de sonde de hello pour l’état d’intégrité de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="e182f-210">Conserver dans l’esprit toorun cette commande, votre équilibreur de charge requiert une ressource d’adresse ip frontale (extraction de la commande « azure frontal-adresse ip de réseau » tooassign un équilibrage de tooload d’adresse ip).</span><span class="sxs-lookup"><span data-stu-id="e182f-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="e182f-211">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e182f-212">Met à jour la sonde d’un équilibrage de charge existant avec de nouvelles valeurs.</span><span class="sxs-lookup"><span data-stu-id="e182f-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="e182f-213">Options de paramètre</span><span class="sxs-lookup"><span data-stu-id="e182f-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="e182f-214">Propriétés de sonde hello pour un jeu d’équilibrage de charge de la liste.</span><span class="sxs-lookup"><span data-stu-id="e182f-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="e182f-215">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-216">Supprime la sonde hello créé pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="e182f-217">**Commandes toomanage frontal des configurations ip d’un équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="e182f-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-218">Crée un tooan de configuration IP serveur frontal existant du jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-219">Les mises à jour une configuration existante d’un serveur frontal commande IP.hello ci-dessous ajoute une adresse IP publique appelée mypubip5 tooan existant charge équilibrage IP de serveur frontal nommé myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="e182f-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-220">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="e182f-221">Répertorie toutes les ressources IP frontale hello configurés pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="e182f-222">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-223">Supprime l’équilibrage tooload de hello frontal IP objet associé</span><span class="sxs-lookup"><span data-stu-id="e182f-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="e182f-224">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e182f-225">**Commandes toomanage des pools d’adresses principales d’un équilibrage de charge**</span><span class="sxs-lookup"><span data-stu-id="e182f-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e182f-226">Crée un pool d'adresses principales pour un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="e182f-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="e182f-227">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="e182f-228">Indique la plage du pool d'adresses IP principales pour un groupe de ressources spécifique</span><span class="sxs-lookup"><span data-stu-id="e182f-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="e182f-229">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="e182f-230">supprimer des livres-pool d’adresses réseau [options] < groupe de ressources >< lb-name ><name></span><span class="sxs-lookup"><span data-stu-id="e182f-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="e182f-231">Supprime la ressource de plage de pool hello back-end IP à partir de l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="e182f-232">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e182f-233">**Règles d’équilibrage de charge de toomanage des commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-234">Crée des règles d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-234">Create load balancer rules.</span></span>

<span data-ttu-id="e182f-235">Vous pouvez créer une règle d’équilibreur de charge la configuration de point de terminaison de serveur frontal hello pour l’équilibrage de charge hello et hello principal adresse pool plage tooreceive hello du trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="e182f-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="e182f-236">Paramètres incluent également les ports hello pour le point de terminaison de serveur frontal IP et ports pour la plage de pool adresse hello back-end.</span><span class="sxs-lookup"><span data-stu-id="e182f-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="e182f-237">Hello suivant montre comment toocreate un équilibreur de charge de règle, point de terminaison de serveur frontal hello tooport 80 à l’écoute le trafic de l’envoi tooport 8080 pour plage de pool hello principal adresse de réseau TCP et équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-238">Met à jour une règle d'équilibrage de charge existante définie dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="e182f-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="e182f-239">Bonjour l’exemple suivant, nous avons modifié le nom de la règle hello de mylbrule toomynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="e182f-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-240">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="e182f-241">Répertorie toutes les règles d'équilibrage de charge configurées pour un équilibrage de charge dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="e182f-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="e182f-242">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e182f-243">Supprime une règle d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="e182f-244">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e182f-245">**Équilibrage de charge de commandes toomanage les règles NAT de trafic entrant**</span><span class="sxs-lookup"><span data-stu-id="e182f-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-246">Crée une règle NAT entrante pour l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="e182f-247">Bonjour exemple suivant, nous avons créé une règle NAT de l’IP du serveur frontal (qui a déjà été définie à l’aide de la commande hello « ip frontale de réseau azure ») avec un port d’écoute entrant et le port de sortie cet équilibrage de charge hello utilise le trafic de réseau toosend hello.</span><span class="sxs-lookup"><span data-stu-id="e182f-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-248">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="e182f-249">Met à jour une règle NAT entrante existante.</span><span class="sxs-lookup"><span data-stu-id="e182f-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="e182f-250">Bonjour l’exemple suivant, nous avons modifié hello entrants du port d’écoute de too81 80.</span><span class="sxs-lookup"><span data-stu-id="e182f-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
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

<span data-ttu-id="e182f-251">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="e182f-252">Répertorie toutes les règles NAT entrantes pour un équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="e182f-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="e182f-253">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="e182f-254">Supprime une règle NAT pour l’équilibrage de charge de hello dans un groupe de ressources spécifique.</span><span class="sxs-lookup"><span data-stu-id="e182f-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="e182f-255">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="e182f-256">**Adresses ip publiques de toomanage commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="e182f-257">Crée une ressource IP publique.</span><span class="sxs-lookup"><span data-stu-id="e182f-257">Creates a public ip resource.</span></span> <span data-ttu-id="e182f-258">Vous créez la ressource d’adresse ip publique hello et associer le nom de domaine tooa.</span><span class="sxs-lookup"><span data-stu-id="e182f-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
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


<span data-ttu-id="e182f-259">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="e182f-260">Propriétés de hello mises à jour d’une ressource d’adresse ip publique existante.</span><span class="sxs-lookup"><span data-stu-id="e182f-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="e182f-261">Bonjour à l’exemple suivant, nous avons modifié les adresse IP publique hello de tooStatic dynamique.</span><span class="sxs-lookup"><span data-stu-id="e182f-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
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

<span data-ttu-id="e182f-262">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="e182f-263">network public-ip list [options] &lt;groupe-ressources&gt; Répertorie toutes les ressources IP publiques au sein d'un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="e182f-264">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="e182f-265">réseau public-ip afficher [options] < groupe de ressources ><name></span><span class="sxs-lookup"><span data-stu-id="e182f-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="e182f-266">Affiche les propriétés d’adresse IP publique pour une ressource IP publique au sein d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e182f-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
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

<span data-ttu-id="e182f-267">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="e182f-268">Supprime une ressource IP publique.</span><span class="sxs-lookup"><span data-stu-id="e182f-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="e182f-269">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="e182f-270">**Interfaces de commandes toomanage réseau**</span><span class="sxs-lookup"><span data-stu-id="e182f-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="e182f-271">Crée une ressource de l’interface réseau (NIC) qui peut être utilisé pour les équilibreurs de charge ou associer tooa Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e182f-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
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

<span data-ttu-id="e182f-272">Options de paramètre :</span><span class="sxs-lookup"><span data-stu-id="e182f-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="e182f-273">**Groupes de sécurité réseau commandes toomanage**</span><span class="sxs-lookup"><span data-stu-id="e182f-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="e182f-274">**Règles du groupe de sécurité commandes toomanage réseau**</span><span class="sxs-lookup"><span data-stu-id="e182f-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="e182f-275">**Commandes toomanage profil traffic manager**</span><span class="sxs-lookup"><span data-stu-id="e182f-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="e182f-276">**Commandes de points de terminaison toomanage traffic manager**</span><span class="sxs-lookup"><span data-stu-id="e182f-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="e182f-277">**Passerelles de réseau virtuel toomanage de commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="e182f-278">le fournisseur Azure : commandes toomanage inscriptions du fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="e182f-279">**Répertorier les fournisseurs actuellement enregistrés dans Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="e182f-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="e182f-280">**Afficher les détails sur hello a demandé l’espace de noms de fournisseur**</span><span class="sxs-lookup"><span data-stu-id="e182f-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="e182f-281">**Inscription du fournisseur avec un abonnement de hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="e182f-282">**Annuler l’inscription du fournisseur avec un abonnement de hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="e182f-283">ressource Azure : commandes toomanage vos ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="e182f-284">**Créer une ressource dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="e182f-285">**Mettre à jour une ressource dans un groupe de ressources sans aucun modèle ou paramètre**</span><span class="sxs-lookup"><span data-stu-id="e182f-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="e182f-286">**Ressources hello de listes**</span><span class="sxs-lookup"><span data-stu-id="e182f-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="e182f-287">**Obtenir une ressource au sein d'un groupe de ressources ou d'un abonnement**</span><span class="sxs-lookup"><span data-stu-id="e182f-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="e182f-288">**Supprimer une ressource dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="e182f-289">rôle Azure : commandes toomanage vos rôles Azure</span><span class="sxs-lookup"><span data-stu-id="e182f-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="e182f-290">**Obtenir toutes les définitions de rôles disponibles**</span><span class="sxs-lookup"><span data-stu-id="e182f-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="e182f-291">**Obtenir une définition de rôles disponible**</span><span class="sxs-lookup"><span data-stu-id="e182f-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="e182f-292">**Commandes toomanage votre attribution de rôle**</span><span class="sxs-lookup"><span data-stu-id="e182f-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="e182f-293">le stockage Azure : commandes toomanage vos objets de stockage</span><span class="sxs-lookup"><span data-stu-id="e182f-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="e182f-294">**Commandes toomanage vos comptes de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="e182f-295">**Commandes toomanage vos clés de compte de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="e182f-296">**Commandes tooshow votre chaîne de connexion de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="e182f-297">**Commandes toomanage vos conteneurs de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="e182f-298">**Commandes toomanage partagé des signatures d’accès de votre conteneur de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="e182f-299">**Commandes toomanage stockées les stratégies d’accès de votre conteneur de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="e182f-300">**Commandes toomanage vos objets BLOB de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="e182f-301">**Commandes toomanage vos opérations de copie d’objets blob**</span><span class="sxs-lookup"><span data-stu-id="e182f-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="e182f-302">**Signature d’accès partagé commandes toomanage de votre objet blob de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="e182f-303">**Commandes toomanage vos partages de fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="e182f-304">**Commandes toomanage vos fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="e182f-305">**Commandes toomanage votre répertoire de fichiers de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="e182f-306">**Commandes toomanage les files d’attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="e182f-307">**Commandes toomanage partagé des signatures d’accès de votre file d’attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="e182f-308">**Commandes toomanage stockées les stratégies d’accès de votre file d’attente de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="e182f-309">**Commandes toomanage vos propriétés de journalisation du stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="e182f-310">**Commandes toomanage vos propriétés de métriques de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="e182f-311">**Commandes toomanage vos tables de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="e182f-312">**Commandes toomanage partagé des signatures d’accès de votre table de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="e182f-313">**Commandes toomanage stockées les stratégies d’accès de votre table de stockage**</span><span class="sxs-lookup"><span data-stu-id="e182f-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="e182f-314">balise Azure : commandes toomanage votre balise du Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="e182f-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="e182f-315">**Ajouter une balise**</span><span class="sxs-lookup"><span data-stu-id="e182f-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="e182f-316">**Supprimer une balise entière ou une valeur de balise**</span><span class="sxs-lookup"><span data-stu-id="e182f-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="e182f-317">**Répertorie des informations de balise hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="e182f-318">**Obtenir une balise**</span><span class="sxs-lookup"><span data-stu-id="e182f-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="e182f-319">machine virtuelle Azure : commandes toomanage vos Machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e182f-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="e182f-320">**Créer une machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="e182f-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="e182f-321">**Créer une machine virtuelle avec les ressources par défaut**</span><span class="sxs-lookup"><span data-stu-id="e182f-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="e182f-322">À partir de la version 0.10 CLI, vous pouvez fournir un court alias tel que « UbuntuLTS » ou « Win2012R2Datacenter » en tant que hello `image-urn` pour certaines images Marketplace populaires.</span><span class="sxs-lookup"><span data-stu-id="e182f-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="e182f-323">Exécutez `azure help vm quick-create` pour voir les options.</span><span class="sxs-lookup"><span data-stu-id="e182f-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="e182f-324">En outre, en commençant par la version 0,10, `azure vm quick-create` utilise le stockage premium par défaut si elle est disponible dans la région de hello sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="e182f-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="e182f-325">**Répertorier les machines virtuelles hello dans un compte**</span><span class="sxs-lookup"><span data-stu-id="e182f-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="e182f-326">**Obtenir une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="e182f-327">**Supprimer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="e182f-328">**Arrêter une machine virtuelle au sein d'un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="e182f-329">**Redémarrer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="e182f-330">**Démarrer une machine virtuelle dans un groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="e182f-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="e182f-331">**Arrêter une machine virtuelle dans un Bonjour ressource de groupe et les versions des ressources de calcul**</span><span class="sxs-lookup"><span data-stu-id="e182f-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="e182f-332">**Répertorier les tailles disponibles des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="e182f-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="e182f-333">**Capturer hello machine virtuelle en tant qu’Image de système d’exploitation ou Image de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="e182f-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="e182f-334">**Définir l’état de hello VM tooGeneralized hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="e182f-335">**Obtenir la vue d’instance de la machine virtuelle de hello**</span><span class="sxs-lookup"><span data-stu-id="e182f-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="e182f-336">**Activez les vous tooreset accès Bureau à distance ou SSH sur un ordinateur virtuel et le tooreset hello mot de passe hello compte administrateur ou autorité sudo doté**</span><span class="sxs-lookup"><span data-stu-id="e182f-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="e182f-337">**Mettre à jour une machine virtuelle avec de nouvelles données**</span><span class="sxs-lookup"><span data-stu-id="e182f-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="e182f-338">**Commandes toomanage vos disques de données de Machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="e182f-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="e182f-339">**Extensions de ressource de commandes toomanage machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="e182f-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="e182f-340">**Commandes toomanage votre Machine virtuelle de Docker**</span><span class="sxs-lookup"><span data-stu-id="e182f-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="e182f-341">**Images de machine virtuelle toomanage de commandes**</span><span class="sxs-lookup"><span data-stu-id="e182f-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
