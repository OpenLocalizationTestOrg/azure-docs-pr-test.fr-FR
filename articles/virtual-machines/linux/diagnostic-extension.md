---
title: Calcul Azure - Extension de diagnostic Linux | Microsoft Docs
description: "Comment configurer l’extension de diagnostic Linux Azure pour collecter des métriques et consigner les événements provenant de machines virtuelles Linux qui s’exécutent dans Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="e0a0a-103">Utilisez l’extension de diagnostic Linux pour surveiller les métriques et les journaux</span><span class="sxs-lookup"><span data-stu-id="e0a0a-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="e0a0a-104">Ce document décrit la version 3.0 et les versions ultérieures de l’extension de diagnostic Linux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a0a-105">Pour plus d’informations sur la version 2.3 et les versions antérieures, consultez [ce document](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="e0a0a-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="e0a0a-106">Introduction</span></span>

<span data-ttu-id="e0a0a-107">L’extension de diagnostic Linux aide l’utilisateur à surveiller l’intégrité d’une machine virtuelle Linux s’exécutant sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="e0a0a-108">Elle présente les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-108">It has the following capabilities:</span></span>

* <span data-ttu-id="e0a0a-109">Elle collecte des métriques de performances du système auprès de la machine virtuelle et les stocke dans une table spécifique d’un compte de stockage désigné.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="e0a0a-110">Elle récupère les journaux d’événements Syslog et les stocke dans une table spécifique du compte de stockage désigné.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="e0a0a-111">Elle permet aux utilisateurs de personnaliser les métriques des données qui sont collectées et chargées.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="e0a0a-112">Elle permet aux utilisateurs de personnaliser les fonctions Syslog et les niveaux de gravité des événements qui sont collectés et chargés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="e0a0a-113">Elle permet aux utilisateurs de télécharger les fichiers journaux spécifiés dans la table de stockage désignée.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="e0a0a-114">Elle prend en charge l’envoi des métriques et des événements des journaux à des points de terminaison EventHub arbitraires et à des objets blob au format JSON dans le compte de stockage désigné.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="e0a0a-115">Cette extension fonctionne avec les deux modèles de déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="e0a0a-116">Installation de l’extension dans votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e0a0a-116">Installing the extension in your VM</span></span>

<span data-ttu-id="e0a0a-117">Vous pouvez activer cette extension via des applets de commande Azure PowerShell, des scripts Azure CLI ou des modèles de déploiement Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="e0a0a-118">Pour plus d’informations, consultez [Fonctionnalités des extensions](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="e0a0a-119">Le portail Azure ne peut pas être utilisé pour activer ou configurer l’extension de diagnostic Linux 3.0.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="e0a0a-120">Au lieu de cela, il installe et configure la version 2.3.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="e0a0a-121">Les graphes et les alertes du portail Azure fonctionnent avec les données provenant des deux versions de l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="e0a0a-122">Ces instructions d’installation et un [exemple de configuration téléchargeable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurent l’extension de diagnostic Linux 3.0 pour :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="e0a0a-123">Capturer et stocker les mêmes mesures que celles fournies par l’extension de diagnostic Linux 2.3</span><span class="sxs-lookup"><span data-stu-id="e0a0a-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="e0a0a-124">Capturer un ensemble utile de métriques du système de fichiers, nouveau dans l’extension de diagnostic Linux 3.0</span><span class="sxs-lookup"><span data-stu-id="e0a0a-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="e0a0a-125">Capturer la collection Syslog par défaut activée par l’extension de diagnostic Linux 2.3</span><span class="sxs-lookup"><span data-stu-id="e0a0a-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="e0a0a-126">Permettre l’utilisation du portail Azure pour les graphes et les alertes sur des métriques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="e0a0a-127">La configuration téléchargeable est seulement un exemple. Modifiez-la selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e0a0a-128">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e0a0a-128">Prerequisites</span></span>

* <span data-ttu-id="e0a0a-129">**Agent Azure Linux version 2.2.0 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="e0a0a-130">La plupart des images de la galerie Linux de machines virtuelles Azure incluent la version 2.2.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="e0a0a-131">Exécutez `/usr/sbin/waagent -version` pour vérifier la version installée sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="e0a0a-132">Si la machine virtuelle exécute une version antérieure de l’agent invité, suivez [ces instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) pour le mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="e0a0a-133">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-133">**Azure CLI**.</span></span> <span data-ttu-id="e0a0a-134">[Configurez l’environnement Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="e0a0a-135">Si vous n’avez pas déjà la commande wget : exécutez `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="e0a0a-136">Un abonnement Azure et un compte de stockage existants sont utilisés pour stocker les données.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="e0a0a-137">Exemple d’installation</span><span class="sxs-lookup"><span data-stu-id="e0a0a-137">Sample installation</span></span>

<span data-ttu-id="e0a0a-138">Renseignez les paramètres corrects sur les trois premières lignes puis exécutez ce script en tant que root :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="e0a0a-139">L’URL de l’exemple de configuration et son contenu sont susceptibles d’être modifiés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="e0a0a-140">Téléchargez une copie du fichier JSON des paramètres du portail et personnalisez-la en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="e0a0a-141">Les modèles ou l’automation que vous construisez doit utiliser votre propre copie au lieu de télécharger cette URL à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="e0a0a-142">Mise à jour les paramètres de l’extension</span><span class="sxs-lookup"><span data-stu-id="e0a0a-142">Updating the extension settings</span></span>

<span data-ttu-id="e0a0a-143">Une fois que vous avez modifié vos paramètres protégés ou publics, déployez-les sur la machine virtuelle en exécutant la même commande.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="e0a0a-144">Si quelque chose a changé dans les paramètres, les paramètres mis à jour sont envoyés à l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="e0a0a-145">L’extension de diagnostic Linux recharge la configuration et redémarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="e0a0a-146">Migration depuis des versions antérieures de l’extension</span><span class="sxs-lookup"><span data-stu-id="e0a0a-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="e0a0a-147">La dernière version de l’extension est **3.0**.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="e0a0a-148">**Les anciennes versions (2.x) sont dépréciées, et leur publication peut cesser le 31 juillet 2018 ou après**.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a0a-149">Cette extension introduit des changements majeurs à la configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="e0a0a-150">Une telle modification a été apportée pour améliorer la sécurité de l’extension. Par conséquent, la compatibilité descendante avec les versions 2.x n’a pas pu être conservée.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="e0a0a-151">En outre, l’éditeur d’extension pour cette extension est différent de l’éditeur pour les versions 2.x.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="e0a0a-152">Pour migrer de 2.x vers cette nouvelle version de l’extension, vous devez désinstaller l’ancienne extension (sous l’ancien nom de l’éditeur) puis installer la version 3 de l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="e0a0a-153">Recommandations :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-153">Recommendations:</span></span>

* <span data-ttu-id="e0a0a-154">Installez l’extension avec la mise à niveau automatique de version mineure activée.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="e0a0a-155">Sur les machines virtuelles du modèle de déploiement classique, spécifiez « 3.* » comme version si vous installez l’extension via Azure XPLAT CLI ou Powershell.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="e0a0a-156">Sur les machines virtuelles du modèle de déploiement Azure Resource Manager, incluez '"autoUpgradeMinorVersion": true' dans le modèle de déploiement des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="e0a0a-157">Utilisez un compte de stockage nouveau ou différent pour l’extension de diagnostic Linux 3.0.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="e0a0a-158">Il existe plusieurs petites incompatibilités entre l’extension de diagnostic Linux 2.3 et l’extension de diagnostic Linux 3.0, qui rendent problématique le partage d’un compte :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="e0a0a-159">L’extension de diagnostic Linux 3.0 stocke les événements Syslog dans une table avec un nom différent.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="e0a0a-160">Les chaînes counterSpecifier pour les métriques `builtin` diffèrent dans l’extension de diagnostic Linux 3.0.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="e0a0a-161">Paramètres protégés</span><span class="sxs-lookup"><span data-stu-id="e0a0a-161">Protected settings</span></span>

<span data-ttu-id="e0a0a-162">Cet ensemble d’informations de configuration contient des informations sensibles qui doivent être protégées d’une exposition publique, par exemple les informations d’identification de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="e0a0a-163">Ces paramètres sont transmis et stockés par l’extension sous une forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="e0a0a-164">Nom</span><span class="sxs-lookup"><span data-stu-id="e0a0a-164">Name</span></span> | <span data-ttu-id="e0a0a-165">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-165">Value</span></span>
---- | -----
<span data-ttu-id="e0a0a-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="e0a0a-166">storageAccountName</span></span> | <span data-ttu-id="e0a0a-167">Nom du compte de stockage dans lequel les données sont écrites par l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="e0a0a-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="e0a0a-168">storageAccountEndPoint</span></span> | <span data-ttu-id="e0a0a-169">(facultatif) Le point de terminaison identifiant le cloud dans lequel se trouve le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="e0a0a-170">Si ce paramètre est absent, l’extension de diagnostic Linux utilise par défaut le cloud public Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="e0a0a-171">Pour utiliser un compte de stockage Azure Allemagne, Azure Government ou Azure Chine, définissez cette valeur en conséquence.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="e0a0a-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="e0a0a-172">storageAccountSasToken</span></span> | <span data-ttu-id="e0a0a-173">[Jeton SAS de compte](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) pour les services Blob et Table (`ss='bt'`), applicables aux conteneurs et aux objets (`srt='co'`), qui accorde les autorisations de créer, répertorier, mettre à jour et écrire (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="e0a0a-174">*N’incluez pas* le point d’interrogation ( ?) du début.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="e0a0a-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="e0a0a-175">mdsdHttpProxy</span></span> | <span data-ttu-id="e0a0a-176">(facultatif) Informations du proxy HTTP nécessaires pour permettre à l’extension de se connecter au compte de stockage et au point de terminaison spécifiés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="e0a0a-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="e0a0a-177">sinksConfig</span></span> | <span data-ttu-id="e0a0a-178">(facultatif) Détails des destinations alternatives auxquelles les métriques et les événements peuvent délivrés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="e0a0a-179">Les détails spécifiques de chaque récepteur de données pris en charge par l’extension sont traités dans les sections qui suivent.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="e0a0a-180">Vous pouvez facilement construire le jeton SAS nécessaire via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="e0a0a-181">Sélectionnez le compte de stockage à usage général dans lequel vous voulez que l’extension écrive</span><span class="sxs-lookup"><span data-stu-id="e0a0a-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="e0a0a-182">Sélectionnez « Signature d’accès partagé » dans la partie Paramètres du menu de gauche</span><span class="sxs-lookup"><span data-stu-id="e0a0a-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="e0a0a-183">Rendez les sections appropriées comme décrit précédemment</span><span class="sxs-lookup"><span data-stu-id="e0a0a-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="e0a0a-184">Cliquez sur le bouton « Générer une signature d’accès partagé ».</span><span class="sxs-lookup"><span data-stu-id="e0a0a-184">Click the "Generate SAS" button.</span></span>

![image](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="e0a0a-186">Copiez la signature SAS générée dans le champ storageAccountSasToken et supprimez le premier d’interrogation (« ? ») du début.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="e0a0a-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="e0a0a-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="e0a0a-188">Cette section facultative définit les autres destinations auxquelles l’extension envoie les informations collectées.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="e0a0a-189">Le tableau « récepteur » contient un objet pour chaque récepteur de données supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="e0a0a-190">L’attribut « type » détermine les autres attributs de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="e0a0a-191">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-191">Element</span></span> | <span data-ttu-id="e0a0a-192">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-192">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-193">name</span><span class="sxs-lookup"><span data-stu-id="e0a0a-193">name</span></span> | <span data-ttu-id="e0a0a-194">Chaîne utilisée pour référencer ce récepteur ailleurs dans la configuration de l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="e0a0a-195">type</span><span class="sxs-lookup"><span data-stu-id="e0a0a-195">type</span></span> | <span data-ttu-id="e0a0a-196">Type du récepteur défini.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-196">The type of sink being defined.</span></span> <span data-ttu-id="e0a0a-197">Détermine les autres valeurs (le cas échéant) dans les instances de ce type.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="e0a0a-198">La version 3.0 de l’extension de diagnostic Linux prend en charge deux types de récepteur : EventHub et JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="e0a0a-199">Récepteur EventHub</span><span class="sxs-lookup"><span data-stu-id="e0a0a-199">The EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="e0a0a-200">L’entrée « sasURL » contient l’URL complète, incluant un jeton SAS, pour l’Event Hub sur lequel les données doivent être publiées.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="e0a0a-201">L’extension de diagnostic Linux nécessite une signature SAS nommant une stratégie qui permet l’envoi de revendication.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="e0a0a-202">Exemple :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-202">An example:</span></span>

* <span data-ttu-id="e0a0a-203">Créer un espace de noms Event Hub appelé `contosohub`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="e0a0a-204">Créer un Event Hub dans l’espace de noms appelé `syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="e0a0a-205">Créer une stratégie d’accès partagé sur l’Event Hub nommé `writer` qui permet l’envoi de revendication</span><span class="sxs-lookup"><span data-stu-id="e0a0a-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="e0a0a-206">Si vous avez créé une signature SAS valable jusqu’au 1er janvier 2018 à minuit (UTC), la valeur de sasURL doit être :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="e0a0a-207">Pour plus d’informations sur la génération de jetons SAS pour les Event Hubs, consultez [cette page web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="e0a0a-208">Récepteur JsonBlob</span><span class="sxs-lookup"><span data-stu-id="e0a0a-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="e0a0a-209">Les données dirigées vers un récepteur JsonBlob sont stockées dans des objets blob dans Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="e0a0a-210">Chaque instance de l’extension de diagnostic Linux crée un objet blob toutes les heures pour chaque nom de récepteur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="e0a0a-211">Chaque objet blob contient toujours un tableau JSON syntaxiquement valide de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="e0a0a-212">Les nouvelles entrées sont ajoutées au tableau de manière atomique.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="e0a0a-213">Les objets blob sont stockés dans un conteneur du même nom que le récepteur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="e0a0a-214">Les règles du Stockage Azure pour les noms de conteneur d’objets blob s’appliquent aux noms des récepteurs JsonBlob : entre 3 et 63 caractères ASCII alphanumériques minuscules ou des tirets.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="e0a0a-215">Paramètres publics</span><span class="sxs-lookup"><span data-stu-id="e0a0a-215">Public settings</span></span>

<span data-ttu-id="e0a0a-216">Cette structure contient différents blocs de paramètres qui contrôlent les informations collectées par l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="e0a0a-217">Chaque paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-217">Each setting is optional.</span></span> <span data-ttu-id="e0a0a-218">Si vous spécifiez `ladCfg`, vous devez aussi spécifier `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="e0a0a-219">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-219">Element</span></span> | <span data-ttu-id="e0a0a-220">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-220">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="e0a0a-221">StorageAccount</span></span> | <span data-ttu-id="e0a0a-222">Nom du compte de stockage dans lequel les données sont écrites par l’extension.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="e0a0a-223">Doit être le même nom que celui spécifié dans les [paramètres protégés](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="e0a0a-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="e0a0a-224">mdsdHttpProxy</span></span> | <span data-ttu-id="e0a0a-225">(facultatif) Comme dans les [paramètres protégés](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="e0a0a-226">La valeur publique est remplacée par la valeur privée si celle-ci est définie.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="e0a0a-227">Placez les paramètres de proxy qui contiennent un secret, comme un mot de passe, dans le [paramètres protégés](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="e0a0a-228">Les éléments restants sont décrits en détail dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="e0a0a-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="e0a0a-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="e0a0a-230">Cette structure facultative contrôle la collecte des métriques et des journaux pour les délivrer au service des métriques Azure et à d’autres récepteurs.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="e0a0a-231">Vous devez spécifier `performanceCounters` ou `syslogEvents`, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="e0a0a-232">Vous devez spécifier la structure `metrics`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="e0a0a-233">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-233">Element</span></span> | <span data-ttu-id="e0a0a-234">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-234">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="e0a0a-235">eventVolume</span></span> | <span data-ttu-id="e0a0a-236">(facultatif) Contrôle le nombre de partitions créées dans la table de stockage.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="e0a0a-237">Doit être `"Large"`, `"Medium"` ou `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="e0a0a-238">Si elle n’est pas spécifiée, la valeur par défaut est `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="e0a0a-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="e0a0a-239">sampleRateInSeconds</span></span> | <span data-ttu-id="e0a0a-240">(facultatif) Intervalle par défaut entre les collectes des métriques brutes (non agrégées).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="e0a0a-241">L’échantillonnage le plus petit pris en charge de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="e0a0a-242">Si elle n’est pas spécifiée, la valeur par défaut est `15`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="e0a0a-243">Mesures</span><span class="sxs-lookup"><span data-stu-id="e0a0a-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="e0a0a-244">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-244">Element</span></span> | <span data-ttu-id="e0a0a-245">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-245">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="e0a0a-246">resourceId</span></span> | <span data-ttu-id="e0a0a-247">L’ID de ressource Azure Resource Manager de la machine virtuelle ou du groupe de machines virtuelles identiques auquel la machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="e0a0a-248">Ce paramètre doit également être spécifié si un récepteur JsonBlob est utilisé dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="e0a0a-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="e0a0a-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="e0a0a-250">La fréquence à laquelle les métriques agrégées doivent être calculées et transférées vers les métriques Azure, exprimée sous la forme d’un intervalle de temps IS 8601.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="e0a0a-251">La périodicité de transfert la plus petite est de 60 secondes, c’est-à-dire PT1M.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="e0a0a-252">Vous devez spécifier au moins une scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="e0a0a-253">Des échantillons des métriques spécifiées dans la section performanceCounters sont collectés toutes les 15 secondes ou selon le taux d’échantillonnage défini explicitement pour le compteur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="e0a0a-254">Si plusieurs fréquences scheduledTransferPeriod apparaissent (comme dans l’exemple), chaque agrégation est calculée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="e0a0a-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="e0a0a-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="e0a0a-256">Cette section facultative contrôle la collecte des métriques.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="e0a0a-257">Les échantillons bruts sont agrégés pour chaque [scheduledTransferPeriod](#metrics) pour produire ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="e0a0a-258">mean</span><span class="sxs-lookup"><span data-stu-id="e0a0a-258">mean</span></span>
* <span data-ttu-id="e0a0a-259">minimum</span><span class="sxs-lookup"><span data-stu-id="e0a0a-259">minimum</span></span>
* <span data-ttu-id="e0a0a-260">maximum</span><span class="sxs-lookup"><span data-stu-id="e0a0a-260">maximum</span></span>
* <span data-ttu-id="e0a0a-261">dernière valeur collectée</span><span class="sxs-lookup"><span data-stu-id="e0a0a-261">last-collected value</span></span>
* <span data-ttu-id="e0a0a-262">nombre d’échantillons bruts utilisés pour calculer l’agrégation</span><span class="sxs-lookup"><span data-stu-id="e0a0a-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="e0a0a-263">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-263">Element</span></span> | <span data-ttu-id="e0a0a-264">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-264">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-265">sinks</span><span class="sxs-lookup"><span data-stu-id="e0a0a-265">sinks</span></span> | <span data-ttu-id="e0a0a-266">(facultatif) Liste séparée par des virgules des noms des récepteurs auquel l’extension de diagnostic Linux envoie les résultats des métriques agrégées.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="e0a0a-267">Toutes les métriques agrégées sont publiées sur chaque récepteur répertorié.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="e0a0a-268">Consultez [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="e0a0a-269">Exemple : `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="e0a0a-270">type</span><span class="sxs-lookup"><span data-stu-id="e0a0a-270">type</span></span> | <span data-ttu-id="e0a0a-271">Identifie le fournisseur réel de la mesure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="e0a0a-272">class</span><span class="sxs-lookup"><span data-stu-id="e0a0a-272">class</span></span> | <span data-ttu-id="e0a0a-273">Avec « counter », identifie la métrique spécifique au sein de l’espace de noms du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="e0a0a-274">counter</span><span class="sxs-lookup"><span data-stu-id="e0a0a-274">counter</span></span> | <span data-ttu-id="e0a0a-275">Avec « class », identifie la métrique spécifique au sein de l’espace de noms du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="e0a0a-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="e0a0a-276">counterSpecifier</span></span> | <span data-ttu-id="e0a0a-277">Identifie la métrique spécifique au sein de l’espace de noms des métriques Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="e0a0a-278">condition</span><span class="sxs-lookup"><span data-stu-id="e0a0a-278">condition</span></span> | <span data-ttu-id="e0a0a-279">(facultatif) Sélectionne une instance spécifique de l’objet auquel s’applique la métrique ou sélectionne l’agrégation sur toutes les instances de cet objet.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="e0a0a-280">Pour plus d’informations, consultez les [ `builtin` définitions des métriques](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="e0a0a-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="e0a0a-281">sampleRate</span></span> | <span data-ttu-id="e0a0a-282">Intervalle IS 8601 qui définit la fréquence à laquelle des échantillons bruts sont collectés pour cette métrique.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="e0a0a-283">S’il n’est pas défini, l’intervalle de collecte est défini par la valeur de [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="e0a0a-284">L’échantillonnage le plus court pris en charge est de 15 secondes (PT15S).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="e0a0a-285">unité</span><span class="sxs-lookup"><span data-stu-id="e0a0a-285">unit</span></span> | <span data-ttu-id="e0a0a-286">Doit être une des chaînes suivantes : « Count », « Bytes », « Seconds », « Percent », « CountPerSecond », « BytesPerSecond », « Millisecond ».</span><span class="sxs-lookup"><span data-stu-id="e0a0a-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="e0a0a-287">Définit l’unité pour la métrique.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-287">Defines the unit for the metric.</span></span> <span data-ttu-id="e0a0a-288">Les consommateurs des données collectées attendent des valeurs de données collectées correspondant à cette unité.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="e0a0a-289">L’extension de diagnostic Linux ignore ce champ.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-289">LAD ignores this field.</span></span>
<span data-ttu-id="e0a0a-290">displayName</span><span class="sxs-lookup"><span data-stu-id="e0a0a-290">displayName</span></span> | <span data-ttu-id="e0a0a-291">Étiquette (dans la langue spécifiée par les paramètres régionaux associés) à attacher à ces données dans les métriques Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="e0a0a-292">L’extension de diagnostic Linux ignore ce champ.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-292">LAD ignores this field.</span></span>

<span data-ttu-id="e0a0a-293">counterSpecifier est un identificateur arbitraire.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="e0a0a-294">Les consommateurs de métriques, comme les fonctionnalités de graphe et d’alerte du portail Azure, utilisent counterSpecifier comme « clé » qui identifie une métrique ou une instance de métrique.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="e0a0a-295">Pour les métriques `builtin`, nous vous recommandons d’utiliser des valeurs pour counterSpecifier qui commencent par `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="e0a0a-296">Si vous collectez une instance spécifique d’une métrique, nous vous recommandons d’attacher l’identificateur de l’instance à la valeur de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="e0a0a-297">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-297">Some examples:</span></span>

* <span data-ttu-id="e0a0a-298">`/builtin/Processor/PercentIdleTime` : Temps d’inactivité moyen pour tous les cœurs</span><span class="sxs-lookup"><span data-stu-id="e0a0a-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="e0a0a-299">`/builtin/Disk/FreeSpace(/mnt)` : Espace libre pour le système de fichiers /mnt</span><span class="sxs-lookup"><span data-stu-id="e0a0a-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="e0a0a-300">`/builtin/Disk/FreeSpace` : Espace libre moyen pour tous les systèmes de fichiers montés</span><span class="sxs-lookup"><span data-stu-id="e0a0a-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="e0a0a-301">Ni l’extension de diagnostic Linux ni le portail Azure n’attendent un modèle particulier pour la valeur de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="e0a0a-302">Soyez cohérent dans la façon dont vous construisez les valeurs de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="e0a0a-303">Quand vous spécifiez `performanceCounters`, l’extension de diagnostic Linux écrit toujours les données dans une table de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="e0a0a-304">Les mêmes données peuvent être écrites dans des objets blob JSON et/ou des Event Hubs, mais vous ne pouvez pas désactiver le stockage des données dans une table.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="e0a0a-305">Toutes les instances de l’extension de diagnostic configuré pour utiliser le même nom et le même point de terminaison de compte de stockage ajoutent leurs mesures et leurs journaux à la même table.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="e0a0a-306">Si un trop grand nombre de machines virtuelles écrivent dans la même partition de table, Azure peut limiter les écritures sur cette partition.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="e0a0a-307">Le paramètre eventVolume permet de répartir les entrées entre 1 (Small), 10 (Medium) ou 100 (Large) partitions différentes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="e0a0a-308">En règle générale, « Medium » est suffisant pour que le trafic ne soit pas limité.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="e0a0a-309">La fonctionnalité des métriques Azure du portail Azure utilise les données de cette table pour produire des graphes ou déclencher des alertes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="e0a0a-310">Le nom de la table est la concaténation des chaînes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="e0a0a-311">« ScheduledTransferPeriod » pour les valeurs agrégées stockées dans la table</span><span class="sxs-lookup"><span data-stu-id="e0a0a-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="e0a0a-312">Une date, sous la forme « AAAAMMJJ », qui change tous les 10 jours</span><span class="sxs-lookup"><span data-stu-id="e0a0a-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="e0a0a-313">Exemples : `WADMetricsPT1HP10DV2S20170410` et `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="e0a0a-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="e0a0a-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="e0a0a-315">Cette section facultative contrôle la collecte des événements des journaux de Syslog.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="e0a0a-316">Si la section est omise, les événements Syslog ne sont pas capturés du tout.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="e0a0a-317">La collection syslogEventConfiguration a une entrée pour chaque fonction Syslog intéressante.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="e0a0a-318">Si minSeverity est défini sur « NONE » pour une fonction donnée ou si cette fonction n’apparaît pas du tout dans l’élément, aucun événement de cette fonction n’est capturé.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="e0a0a-319">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-319">Element</span></span> | <span data-ttu-id="e0a0a-320">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-320">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-321">sinks</span><span class="sxs-lookup"><span data-stu-id="e0a0a-321">sinks</span></span> | <span data-ttu-id="e0a0a-322">Une liste séparée par des virgules de noms de récepteurs sur lesquels des événements de journaux sont publiés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="e0a0a-323">Tous les événements de journaux correspondant aux restrictions de syslogEventConfiguration sont publiés sur chaque récepteur répertorié.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="e0a0a-324">Exemple : « EHforsyslog »</span><span class="sxs-lookup"><span data-stu-id="e0a0a-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="e0a0a-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="e0a0a-325">facilityName</span></span> | <span data-ttu-id="e0a0a-326">Nom de fonction Syslog (comme « LOG\_USER » ou « LOG\_LOCAL0 »).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="e0a0a-327">Consultez la section « facility » de la [page du manuel Syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour obtenir la liste complète.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="e0a0a-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="e0a0a-328">minSeverity</span></span> | <span data-ttu-id="e0a0a-329">Niveau de gravité Syslog (comme « LOG\_ERR » ou « LOG\_INFO »).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="e0a0a-330">Consultez la section « level » de la [page du manuel Syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour obtenir la liste complète.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="e0a0a-331">L’extension capture les événements envoyés à la fonction à un niveau supérieur ou égal au niveau spécifié.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="e0a0a-332">Quand vous spécifiez `syslogEvents`, l’extension de diagnostic Linux écrit toujours les données dans une table de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="e0a0a-333">Les mêmes données peuvent être écrites dans des objets blob JSON et/ou des Event Hubs, mais vous ne pouvez pas désactiver le stockage des données dans une table.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="e0a0a-334">Le comportement de partitionnement pour cette table est identique à celui décrit pour `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="e0a0a-335">Le nom de la table est la concaténation des chaînes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="e0a0a-336">Une date, sous la forme « AAAAMMJJ », qui change tous les 10 jours</span><span class="sxs-lookup"><span data-stu-id="e0a0a-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="e0a0a-337">Exemples : `LinuxSyslog20170410` et `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="e0a0a-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="e0a0a-338">perfCfg</span></span>

<span data-ttu-id="e0a0a-339">Cette section facultative contrôle l’exécution des requêtes [OMI](https://github.com/Microsoft/omi) arbitraires.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="e0a0a-340">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-340">Element</span></span> | <span data-ttu-id="e0a0a-341">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-341">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-342">namespace</span><span class="sxs-lookup"><span data-stu-id="e0a0a-342">namespace</span></span> | <span data-ttu-id="e0a0a-343">(facultatif) L’espace de noms OMI dans lequel la requête doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="e0a0a-344">Si elle n’est pas spécifiée, la valeur par défaut est « root/scx », implémentée par les [fournisseurs multiplateformes System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="e0a0a-345">query</span><span class="sxs-lookup"><span data-stu-id="e0a0a-345">query</span></span> | <span data-ttu-id="e0a0a-346">Requête OMI à exécuter.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-346">The OMI query to be executed.</span></span>
<span data-ttu-id="e0a0a-347">table</span><span class="sxs-lookup"><span data-stu-id="e0a0a-347">table</span></span> | <span data-ttu-id="e0a0a-348">(facultatif) La table de stockage Azure, dans le compte de stockage désigné (consultez [Paramètres protégés](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="e0a0a-349">frequency</span><span class="sxs-lookup"><span data-stu-id="e0a0a-349">frequency</span></span> | <span data-ttu-id="e0a0a-350">(facultatif) Le nombre de secondes entre chaque exécution de la requête.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="e0a0a-351">La valeur par défaut est 300 (5 minutes). La valeur minimale est de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="e0a0a-352">sinks</span><span class="sxs-lookup"><span data-stu-id="e0a0a-352">sinks</span></span> | <span data-ttu-id="e0a0a-353">(facultatif) Une liste séparée par des virgules de noms de récepteurs supplémentaires sur lesquels les résultats des échantillons bruts des métriques doivent être publiés.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="e0a0a-354">Aucune agrégation de ces échantillons bruts n’est calculée par l’extension ou par les métriques Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="e0a0a-355">Vous devez spécifier « table » ou « sinks », ou les deux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="e0a0a-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="e0a0a-356">fileLogs</span></span>

<span data-ttu-id="e0a0a-357">Contrôle la capture des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-357">Controls the capture of log files.</span></span> <span data-ttu-id="e0a0a-358">L’extension de diagnostic Linux capture les nouvelles lignes de texte au fil de leur écriture dans le fichier et les écrit dans des lignes de la table et/ou dans les récepteurs spécifiés (JsonBlob ou EventHub).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="e0a0a-359">Élément</span><span class="sxs-lookup"><span data-stu-id="e0a0a-359">Element</span></span> | <span data-ttu-id="e0a0a-360">Valeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-360">Value</span></span>
------- | -----
<span data-ttu-id="e0a0a-361">file</span><span class="sxs-lookup"><span data-stu-id="e0a0a-361">file</span></span> | <span data-ttu-id="e0a0a-362">Nom du chemin complet du fichier journal à surveiller et à capturer.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="e0a0a-363">Le nom du chemin doit désigner un seul fichier. Il ne peut pas nommer un répertoire ni contenir des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="e0a0a-364">table</span><span class="sxs-lookup"><span data-stu-id="e0a0a-364">table</span></span> | <span data-ttu-id="e0a0a-365">(facultatif) La table Stockage Azure, dans le compte de stockage désigné (tel que spécifié dans la configuration protégée), dans laquelle les nouvelles lignes de la « fin » du fichier sont écrites.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="e0a0a-366">sinks</span><span class="sxs-lookup"><span data-stu-id="e0a0a-366">sinks</span></span> | <span data-ttu-id="e0a0a-367">(facultatif) Une liste séparée par des virgules des noms des récepteurs supplémentaires auxquels les lignes des journaux sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="e0a0a-368">Vous devez spécifier « table » ou « sinks », ou les deux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="e0a0a-369">Métriques prises en charge par le fournisseur intégré</span><span class="sxs-lookup"><span data-stu-id="e0a0a-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="e0a0a-370">Le fournisseur de métriques intégré est une source de métriques parmi les plus intéressantes pour un large éventail d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="e0a0a-371">Ces métriques se répartissent en cinq classes principales :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="e0a0a-372">Processeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-372">Processor</span></span>
* <span data-ttu-id="e0a0a-373">Mémoire</span><span class="sxs-lookup"><span data-stu-id="e0a0a-373">Memory</span></span>
* <span data-ttu-id="e0a0a-374">Réseau</span><span class="sxs-lookup"><span data-stu-id="e0a0a-374">Network</span></span>
* <span data-ttu-id="e0a0a-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="e0a0a-375">Filesystem</span></span>
* <span data-ttu-id="e0a0a-376">Disque</span><span class="sxs-lookup"><span data-stu-id="e0a0a-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="e0a0a-377">métriques intégrées pour la classe Processeur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="e0a0a-378">La classe de métriques Processeur fournit des informations sur l’utilisation du processeur dans la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="e0a0a-379">Lors de l’agrégation de pourcentages, le résultat est la moyenne pour toutes les UC.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="e0a0a-380">Dans une machine virtuelle à deux cœurs, si un cœur a été occupé à 100 % et que l’autre a été inactif à 100 %, la valeur de PercentIdleTime serait ainsi 50.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="e0a0a-381">Si chaque cœur a été occupé à 50 % pour la même période, le résultat serait également 50.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="e0a0a-382">Dans une machine virtuelle à quatre cœurs, si un cœur a été occupé à 100 % et que les autres ont été inactifs, la valeur de PercentIdleTime serait 75.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="e0a0a-383">counter</span><span class="sxs-lookup"><span data-stu-id="e0a0a-383">counter</span></span> | <span data-ttu-id="e0a0a-384">Signification</span><span class="sxs-lookup"><span data-stu-id="e0a0a-384">Meaning</span></span>
------- | -------
<span data-ttu-id="e0a0a-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-385">PercentIdleTime</span></span> | <span data-ttu-id="e0a0a-386">Pourcentage de temps de la fenêtre d’agrégation pendant lequel les processeurs ont exécuté la boucle d’inactivité du noyau</span><span class="sxs-lookup"><span data-stu-id="e0a0a-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="e0a0a-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-387">PercentProcessorTime</span></span> | <span data-ttu-id="e0a0a-388">Pourcentage de temps passé à exécuter un thread actif</span><span class="sxs-lookup"><span data-stu-id="e0a0a-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="e0a0a-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-389">PercentIOWaitTime</span></span> | <span data-ttu-id="e0a0a-390">Pourcentage de temps passé à attendre la fin d’opérations d’E/S</span><span class="sxs-lookup"><span data-stu-id="e0a0a-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="e0a0a-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-391">PercentInterruptTime</span></span> | <span data-ttu-id="e0a0a-392">Pourcentage de temps passé à exécuter des interruptions matérielles/logicielles et des appels DPC (appels de procédure différés)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="e0a0a-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-393">PercentUserTime</span></span> | <span data-ttu-id="e0a0a-394">Pourcentage de temps passé pour l’utilisateur à une priorité supérieure à la normale, relativement au temps d’activité de la fenêtre d’agrégation</span><span class="sxs-lookup"><span data-stu-id="e0a0a-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="e0a0a-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-395">PercentNiceTime</span></span> | <span data-ttu-id="e0a0a-396">Pourcentage de temps passé à une priorité abaissée (commande nice), relativement au temps d’activité</span><span class="sxs-lookup"><span data-stu-id="e0a0a-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="e0a0a-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="e0a0a-398">Pourcentage de temps passé en mode privilégié (noyau), relativement au temps d’activité</span><span class="sxs-lookup"><span data-stu-id="e0a0a-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="e0a0a-399">La somme des quatre premiers compteurs doit être de 100 %.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="e0a0a-400">La somme des trois derniers compteurs est également de 100 %. Ils subdivisent la somme de PercentProcessorTime, PercentIOWaitTime et PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="e0a0a-401">Pour obtenir une seule métrique agrégée pour tous les processeurs, définissez `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="e0a0a-402">Pour obtenir une métrique pour un processeur spécifique, par exemple le deuxième processeur logique d’une machine virtuelle à quatre cœurs, définissez `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="e0a0a-403">Les numéros des processeurs logiques sont dans la plage `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="e0a0a-404">métriques intégrées pour la classe Mémoire</span><span class="sxs-lookup"><span data-stu-id="e0a0a-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="e0a0a-405">La classe de métriques Mémoire fournit des informations sur l’utilisation, la pagination et les échanges de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="e0a0a-406">counter</span><span class="sxs-lookup"><span data-stu-id="e0a0a-406">counter</span></span> | <span data-ttu-id="e0a0a-407">Signification</span><span class="sxs-lookup"><span data-stu-id="e0a0a-407">Meaning</span></span>
------- | -------
<span data-ttu-id="e0a0a-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="e0a0a-408">AvailableMemory</span></span> | <span data-ttu-id="e0a0a-409">Mémoire physique disponible en Mio</span><span class="sxs-lookup"><span data-stu-id="e0a0a-409">Available physical memory in MiB</span></span>
<span data-ttu-id="e0a0a-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="e0a0a-410">PercentAvailableMemory</span></span> | <span data-ttu-id="e0a0a-411">Mémoire physique disponible sous forme de pourcentage de la mémoire totale</span><span class="sxs-lookup"><span data-stu-id="e0a0a-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="e0a0a-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="e0a0a-412">UsedMemory</span></span> | <span data-ttu-id="e0a0a-413">Mémoire physique utilisée (Mio)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="e0a0a-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="e0a0a-414">PercentUsedMemory</span></span> | <span data-ttu-id="e0a0a-415">Mémoire physique utilisée sous forme de pourcentage de la mémoire totale</span><span class="sxs-lookup"><span data-stu-id="e0a0a-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="e0a0a-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="e0a0a-416">PagesPerSec</span></span> | <span data-ttu-id="e0a0a-417">Pagination totale (lecture/écriture)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-417">Total paging (read/write)</span></span>
<span data-ttu-id="e0a0a-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="e0a0a-418">PagesReadPerSec</span></span> | <span data-ttu-id="e0a0a-419">Pages lues dans le magasin de stockage (fichier d’échange, fichier programme, fichier mappé, etc.)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="e0a0a-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="e0a0a-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="e0a0a-421">Pages écrites dans le magasin de stockage (fichier d’échange, fichier mappé, etc.)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="e0a0a-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="e0a0a-422">AvailableSwap</span></span> | <span data-ttu-id="e0a0a-423">Espace d’échange non utilisé (Mio)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="e0a0a-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="e0a0a-424">PercentAvailableSwap</span></span> | <span data-ttu-id="e0a0a-425">Espace d’échange non utilisé sous forme de pourcentage de l’espace d’échange total</span><span class="sxs-lookup"><span data-stu-id="e0a0a-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="e0a0a-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="e0a0a-426">UsedSwap</span></span> | <span data-ttu-id="e0a0a-427">Espace d’échange utilisé (Mio)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="e0a0a-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="e0a0a-428">PercentUsedSwap</span></span> | <span data-ttu-id="e0a0a-429">Espace d’échange utilisé sous forme de pourcentage de l’espace d’échange total</span><span class="sxs-lookup"><span data-stu-id="e0a0a-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="e0a0a-430">Cette classe de métriques n’a qu’une seule instance.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="e0a0a-431">L’attribut « condition » n’a pas de paramètre utile et doit être omis.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="e0a0a-432">métriques intégrées pour la classe Réseau</span><span class="sxs-lookup"><span data-stu-id="e0a0a-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="e0a0a-433">La classe de métriques Réseau fournit des informations sur l’activité réseau sur une interface réseau individuelle depuis le démarrage.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="e0a0a-434">L’extension de diagnostic Linux n’expose pas de métriques de la bande passante, qui peuvent être récupérées à partir des métriques de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="e0a0a-435">compteur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-435">counter</span></span> | <span data-ttu-id="e0a0a-436">Signification</span><span class="sxs-lookup"><span data-stu-id="e0a0a-436">Meaning</span></span>
------- | -------
<span data-ttu-id="e0a0a-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="e0a0a-437">BytesTransmitted</span></span> | <span data-ttu-id="e0a0a-438">Nombre total d’octets envoyés depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-438">Total bytes sent since boot</span></span>
<span data-ttu-id="e0a0a-439">Octets reçus</span><span class="sxs-lookup"><span data-stu-id="e0a0a-439">BytesReceived</span></span> | <span data-ttu-id="e0a0a-440">Nombre total d’octets reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-440">Total bytes received since boot</span></span>
<span data-ttu-id="e0a0a-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="e0a0a-441">BytesTotal</span></span> | <span data-ttu-id="e0a0a-442">Nombre total d’octets envoyés ou reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="e0a0a-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="e0a0a-443">PacketsTransmitted</span></span> | <span data-ttu-id="e0a0a-444">Nombre total de paquets envoyés depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-444">Total packets sent since boot</span></span>
<span data-ttu-id="e0a0a-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="e0a0a-445">PacketsReceived</span></span> | <span data-ttu-id="e0a0a-446">Nombre total de paquets reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-446">Total packets received since boot</span></span>
<span data-ttu-id="e0a0a-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="e0a0a-447">TotalRxErrors</span></span> | <span data-ttu-id="e0a0a-448">Nombre d’erreurs de réception depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-448">Number of receive errors since boot</span></span>
<span data-ttu-id="e0a0a-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="e0a0a-449">TotalTxErrors</span></span> | <span data-ttu-id="e0a0a-450">Nombre d’erreurs de transmission depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="e0a0a-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="e0a0a-451">TotalCollisions</span></span> | <span data-ttu-id="e0a0a-452">Nombre de collisions signalées par les ports réseau depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="e0a0a-453">Bien que cette classe soit instanciée, l’extension de diagnostic Linux ne prend pas en charge la capture de métriques réseau agrégées pour tous les périphériques réseau.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="e0a0a-454">Pour obtenir les métriques pour une interface spécifique, comme eth0, définissez `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="e0a0a-455">métriques intégrées pour la classe Filesystem</span><span class="sxs-lookup"><span data-stu-id="e0a0a-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="e0a0a-456">La classe de métriques Filesystem fournit des informations sur l’utilisation du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="e0a0a-457">Les valeurs absolues et en pourcentage sont indiquées comme elles sont affichées pour un utilisateur ordinaire (non root).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="e0a0a-458">compteur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-458">counter</span></span> | <span data-ttu-id="e0a0a-459">Signification</span><span class="sxs-lookup"><span data-stu-id="e0a0a-459">Meaning</span></span>
------- | -------
<span data-ttu-id="e0a0a-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="e0a0a-460">FreeSpace</span></span> | <span data-ttu-id="e0a0a-461">Espace disque disponible en octets</span><span class="sxs-lookup"><span data-stu-id="e0a0a-461">Available disk space in bytes</span></span>
<span data-ttu-id="e0a0a-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="e0a0a-462">UsedSpace</span></span> | <span data-ttu-id="e0a0a-463">Espace disque utilisé en octets</span><span class="sxs-lookup"><span data-stu-id="e0a0a-463">Used disk space in bytes</span></span>
<span data-ttu-id="e0a0a-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="e0a0a-464">PercentFreeSpace</span></span> | <span data-ttu-id="e0a0a-465">Pourcentage d’espace libre</span><span class="sxs-lookup"><span data-stu-id="e0a0a-465">Percentage free space</span></span>
<span data-ttu-id="e0a0a-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="e0a0a-466">PercentUsedSpace</span></span> | <span data-ttu-id="e0a0a-467">Pourcentage d’espace utilisé</span><span class="sxs-lookup"><span data-stu-id="e0a0a-467">Percentage used space</span></span>
<span data-ttu-id="e0a0a-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="e0a0a-468">PercentFreeInodes</span></span> | <span data-ttu-id="e0a0a-469">Pourcentage d’inodes non utilisés</span><span class="sxs-lookup"><span data-stu-id="e0a0a-469">Percentage of unused inodes</span></span>
<span data-ttu-id="e0a0a-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="e0a0a-470">PercentUsedInodes</span></span> | <span data-ttu-id="e0a0a-471">Pourcentage total d’inodes alloués (utilisés) pour tous les systèmes de fichiers</span><span class="sxs-lookup"><span data-stu-id="e0a0a-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="e0a0a-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-472">BytesReadPerSecond</span></span> | <span data-ttu-id="e0a0a-473">Octets lus par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-473">Bytes read per second</span></span>
<span data-ttu-id="e0a0a-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="e0a0a-475">Octets écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-475">Bytes written per second</span></span>
<span data-ttu-id="e0a0a-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-476">BytesPerSecond</span></span> | <span data-ttu-id="e0a0a-477">Octets lus ou écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-477">Bytes read or written per second</span></span>
<span data-ttu-id="e0a0a-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-478">ReadsPerSecond</span></span> | <span data-ttu-id="e0a0a-479">Opérations de lecture par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-479">Read operations per second</span></span>
<span data-ttu-id="e0a0a-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-480">WritesPerSecond</span></span> | <span data-ttu-id="e0a0a-481">Opérations d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-481">Write operations per second</span></span>
<span data-ttu-id="e0a0a-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-482">TransfersPerSecond</span></span> | <span data-ttu-id="e0a0a-483">Opérations de lecture ou d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-483">Read or write operations per second</span></span>

<span data-ttu-id="e0a0a-484">Les valeurs agrégées pour tous les systèmes de fichiers peuvent être obtenues en définissant `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="e0a0a-485">Les valeurs pour un système de fichiers monté spécifique, comme « / mnt », peuvent être obtenues en définissant `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="e0a0a-486">métriques intégrées pour la classe Disque</span><span class="sxs-lookup"><span data-stu-id="e0a0a-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="e0a0a-487">La classe de métriques Disque fournit des informations sur l’utilisation du disque.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="e0a0a-488">Ces statistiques s’appliquent à la totalité du lecteur.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="e0a0a-489">S’il existe plusieurs systèmes de fichiers sur un périphérique, les compteurs pour ce périphérique sont agrégés pour tous les systèmes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="e0a0a-490">compteur</span><span class="sxs-lookup"><span data-stu-id="e0a0a-490">counter</span></span> | <span data-ttu-id="e0a0a-491">Signification</span><span class="sxs-lookup"><span data-stu-id="e0a0a-491">Meaning</span></span>
------- | -------
<span data-ttu-id="e0a0a-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-492">ReadsPerSecond</span></span> | <span data-ttu-id="e0a0a-493">Opérations de lecture par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-493">Read operations per second</span></span>
<span data-ttu-id="e0a0a-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-494">WritesPerSecond</span></span> | <span data-ttu-id="e0a0a-495">Opérations d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-495">Write operations per second</span></span>
<span data-ttu-id="e0a0a-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-496">TransfersPerSecond</span></span> | <span data-ttu-id="e0a0a-497">Nombre total d’opérations par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-497">Total operations per second</span></span>
<span data-ttu-id="e0a0a-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-498">AverageReadTime</span></span> | <span data-ttu-id="e0a0a-499">Nombre moyen de secondes par opération de lecture</span><span class="sxs-lookup"><span data-stu-id="e0a0a-499">Average seconds per read operation</span></span>
<span data-ttu-id="e0a0a-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-500">AverageWriteTime</span></span> | <span data-ttu-id="e0a0a-501">Nombre moyen de secondes par opération d’écriture</span><span class="sxs-lookup"><span data-stu-id="e0a0a-501">Average seconds per write operation</span></span>
<span data-ttu-id="e0a0a-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="e0a0a-502">AverageTransferTime</span></span> | <span data-ttu-id="e0a0a-503">Nombre moyen de secondes par opération</span><span class="sxs-lookup"><span data-stu-id="e0a0a-503">Average seconds per operation</span></span>
<span data-ttu-id="e0a0a-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="e0a0a-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="e0a0a-505">Nombre moyen d’opérations disque en file d’attente</span><span class="sxs-lookup"><span data-stu-id="e0a0a-505">Average number of queued disk operations</span></span>
<span data-ttu-id="e0a0a-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="e0a0a-507">Nombre d’octets lus par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-507">Number of bytes read per second</span></span>
<span data-ttu-id="e0a0a-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="e0a0a-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="e0a0a-509">Nombre d’octets écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-509">Number of bytes written per second</span></span>
<span data-ttu-id="e0a0a-510">Octets par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-510">BytesPerSecond</span></span> | <span data-ttu-id="e0a0a-511">Nombre d’octets lus ou écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="e0a0a-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="e0a0a-512">Les valeurs agrégées pour tous les disques peuvent être obtenues en définissant `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="e0a0a-513">Pour obtenir des informations pour un périphérique spécifique (par exemple /dev/sdf1), définissez `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="e0a0a-514">Installation et configuration de l’extension de diagnostic Linux 3.0 via CLI</span><span class="sxs-lookup"><span data-stu-id="e0a0a-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="e0a0a-515">En supposant que vos paramètres protégés sont dans le fichier PrivateConfig.json et que vos informations de configuration publique sont PublicConfig.json, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="e0a0a-516">La commande suppose que vous utilisez le mode Azure Resource Manager (arm) d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="e0a0a-517">Pour configurer l’extension de diagnostic Linux pour des machines virtuelles du modèle de déploiement classique (ASM), passez au mode « asm » (`azure config mode asm`) et omettez le nom du groupe de ressources dans la commande.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="e0a0a-518">Pour plus d’informations, consultez la [documentation relative à l’interface de ligne de commande multiplateforme](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="e0a0a-519">Exemple de configuration de l’extension de diagnostic Linux 3.0</span><span class="sxs-lookup"><span data-stu-id="e0a0a-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="e0a0a-520">Voici un exemple de configuration de l’extension de diagnostic Linux 3.0 basé sur les définitions précédentes, avec quelques explications.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="e0a0a-521">Pour appliquer cet exemple à votre cas, vous devez utiliser le nom de votre compte de stockage, votre jeton SAS de compte SAP et vos jetons SAS EventHubs.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="e0a0a-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="e0a0a-522">PrivateConfig.json</span></span>

<span data-ttu-id="e0a0a-523">Ces paramètres privés configurent :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-523">These private settings configure:</span></span>

* <span data-ttu-id="e0a0a-524">un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="e0a0a-524">a storage account</span></span>
* <span data-ttu-id="e0a0a-525">un jeton SAS de compte correspondant</span><span class="sxs-lookup"><span data-stu-id="e0a0a-525">a matching account SAS token</span></span>
* <span data-ttu-id="e0a0a-526">plusieurs récepteurs (JsonBlob ou EventHubs avec des jetons SAS)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="e0a0a-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="e0a0a-527">PublicConfig.json</span></span>

<span data-ttu-id="e0a0a-528">Ces paramètres publics font que l’extension de diagnostic Linux :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="e0a0a-529">Charge les métriques de pourcentage de temps processeur et d’espace disque utilisé dans la table `WADMetrics*`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="e0a0a-530">Charge les messages depuis la fonction Syslog « user » et le niveau de gravité « info » dans la table `LinuxSyslog*`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="e0a0a-531">Charge les résultats bruts des requêtes OMI (PercentProcessorTime et PercentIdleTime) dans la table nommée `LinuxCPU`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="e0a0a-532">Charge les lignes ajoutées au fichier `/var/log/myladtestlog` dans la table `MyLadTestLog`</span><span class="sxs-lookup"><span data-stu-id="e0a0a-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="e0a0a-533">Dans chaque cas, les données sont également chargées dans :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="e0a0a-534">Stockage Blob Azure (le nom du conteneur est celui qui est défini dans le récepteur JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="e0a0a-535">Point de terminaison EventHubs (comme spécifié dans le récepteur EventHubs)</span><span class="sxs-lookup"><span data-stu-id="e0a0a-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="e0a0a-536">Le `resourceId` dans la configuration doit correspondre à celui de la machine virtuelle ou du groupe de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="e0a0a-537">Les graphes et les alertes des métriques de la plateforme Azure connaissent le resourceId de la machine virtuelle sur laquelle vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="e0a0a-538">Ils s’attendent à trouver les données pour votre machine virtuelle en utilisant le resourceId comme clé de recherche.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="e0a0a-539">Si vous utilisez la mise à l’échelle automatique d’Azure, le resourceId dans la configuration de la mise à l’échelle automatique doit correspondre au resourceId utilisé par l’extension de diagnostic Linux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="e0a0a-540">Le resourceId est intégré dans les noms des récepteurs JsonBlob écrit par l’extension de diagnostic Linux.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="e0a0a-541">Affichage de vos données</span><span class="sxs-lookup"><span data-stu-id="e0a0a-541">View your data</span></span>

<span data-ttu-id="e0a0a-542">Utilisez le portail Azure pour afficher les données de performances ou pour définir des alertes :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-542">Use the Azure portal to view performance data or set alerts:</span></span>

![image](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="e0a0a-544">Les données `performanceCounters` sont toujours stockées dans une table de Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="e0a0a-545">Les API Stockage Azure sont disponibles pour de nombreux langages et de nombreuses plateformes.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="e0a0a-546">Les données envoyées aux récepteurs JsonBlob sont stockées dans des objets blob dans le compte de stockage nommé dans les [paramètres protégés](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="e0a0a-547">Vous pouvez consommer les données d’objet blob à l’aide des API de Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="e0a0a-548">Vous pouvez aussi utiliser ces outils d’interface utilisateur pour accéder aux données de Stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="e0a0a-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="e0a0a-549">Explorateur de serveurs Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="e0a0a-550">[Explorateur de stockage Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Explorateur de stockage Azure").</span><span class="sxs-lookup"><span data-stu-id="e0a0a-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="e0a0a-551">Cette capture instantanée d’une session de l’Explorateur de stockage Microsoft Azure montre les tables et les conteneurs Stockage Azure générés à partir d’une extension de diagnostic Linux 3.0 correctement configurée sur une machine virtuelle de test.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="e0a0a-552">L’image ne correspond pas exactement à [l’exemple de configuration de l’extension de diagnostic Linux 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="e0a0a-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![image](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="e0a0a-554">Consultez la [documentation EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) appropriée pour savoir comment consommer des messages publiés sur un point de terminaison EventHubs.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0a0a-555">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0a0a-555">Next steps</span></span>

* <span data-ttu-id="e0a0a-556">Créez des alertes de métrique dans [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) pour les métriques que vous collectez.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="e0a0a-557">Créez [des graphiques de surveillance](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) pour vos métriques.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="e0a0a-558">Découvrez comment [créer un groupe de machines virtuelles identiques](/azure/virtual-machines/linux/tutorial-create-vmss) en utilisant vos métriques pour contrôler la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="e0a0a-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
