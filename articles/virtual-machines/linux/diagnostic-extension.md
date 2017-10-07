---
title: "Calcul d’aaaAzure - Extension Diagnostics Linux | Documents Microsoft"
description: "Mode tooconfigure hello métriques de toocollect Azure Linux Diagnostic Extension (SCÉNARISTE) et de consigner les événements dans les machines virtuelles Linux s’exécutant dans Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="8e754-103">Utilisez l’Extension Diagnostics Linux toomonitor métriques et journaux</span><span class="sxs-lookup"><span data-stu-id="8e754-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="8e754-104">Ce document décrit la version 3.0 de hello Extension Diagnostics Linux.</span><span class="sxs-lookup"><span data-stu-id="8e754-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e754-105">Pour plus d’informations sur la version 2.3 et les versions antérieures, consultez [ce document](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="8e754-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="8e754-106">Introduction</span><span class="sxs-lookup"><span data-stu-id="8e754-106">Introduction</span></span>

<span data-ttu-id="8e754-107">Hello Extension Diagnostics Linux permet à une utilisateur Moniteur hello l’intégrité d’un VM Linux en cours d’exécution sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="8e754-108">Il a hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="8e754-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="8e754-109">Collecte les métriques de performances système hello machine virtuelle et les stocke dans une table spécifique dans un compte de stockage désignées.</span><span class="sxs-lookup"><span data-stu-id="8e754-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="8e754-110">Récupère les journaux d’événements syslog et les stocke dans une table spécifique dans hello désigné du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e754-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="8e754-111">Permet aux utilisateurs toocustomize hello les métriques des données qui sont collectées et téléchargées.</span><span class="sxs-lookup"><span data-stu-id="8e754-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="8e754-112">Permet aux utilisateurs toocustomize hello syslog et des niveaux de gravité des événements qui sont collectées et téléchargées.</span><span class="sxs-lookup"><span data-stu-id="8e754-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="8e754-113">Permet aux utilisateurs tooupload journal spécifié fichiers tooa désigné stockage table.</span><span class="sxs-lookup"><span data-stu-id="8e754-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="8e754-114">Prend en charge l’envoi des métriques de journal des événements tooarbitrary EventHub points de terminaison et et les objets BLOB d’au format JSON Bonjour désigné compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e754-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="8e754-115">Cette extension fonctionne avec les deux modèles de déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="8e754-116">Extension de hello lors de l’installation dans votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8e754-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="8e754-117">Vous pouvez activer cette extension à l’aide des applets de commande PowerShell Azure hello, scripts CLI d’Azure ou les modèles de déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="8e754-118">Pour plus d’informations, consultez [Fonctionnalités des extensions](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="8e754-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="8e754-119">Hello portail Azure ne peut pas être utilisé tooenable ou configurer SCÉNARISTE 3.0.</span><span class="sxs-lookup"><span data-stu-id="8e754-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="8e754-120">Au lieu de cela, il installe et configure la version 2.3.</span><span class="sxs-lookup"><span data-stu-id="8e754-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="8e754-121">Alertes et des graphiques de portail azure fonctionnent avec des données à partir de deux versions d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="8e754-122">Ces instructions d’installation et un [exemple de configuration téléchargeable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurent l’extension de diagnostic Linux 3.0 pour :</span><span class="sxs-lookup"><span data-stu-id="8e754-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="8e754-123">capture et magasin hello mêmes métriques comme ont été fournies par SCÉNARISTE 2.3 ;</span><span class="sxs-lookup"><span data-stu-id="8e754-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="8e754-124">capturer un ensemble utile de métriques de système de fichier, nouveau tooLAD 3.0 ;</span><span class="sxs-lookup"><span data-stu-id="8e754-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="8e754-125">capturer la collection de syslog par défaut hello activée par SCÉNARISTE 2.3 ;</span><span class="sxs-lookup"><span data-stu-id="8e754-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="8e754-126">Activer hello expérience du portail Azure pour les graphiques et la génération d’alertes sur des métriques de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8e754-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="8e754-127">configuration de téléchargeable Hello est juste un exemple ; Modifiez-le toosuit vos propres besoins.</span><span class="sxs-lookup"><span data-stu-id="8e754-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8e754-128">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8e754-128">Prerequisites</span></span>

* <span data-ttu-id="8e754-129">**Agent Azure Linux version 2.2.0 ou ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="8e754-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="8e754-130">La plupart des images de la galerie Linux de machines virtuelles Azure incluent la version 2.2.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8e754-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="8e754-131">Exécutez `/usr/sbin/waagent -version` tooconfirm hello version est installée sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="8e754-132">Si hello machine virtuelle exécute une ancienne version de l’agent invité de hello, procédez comme [ces instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate il.</span><span class="sxs-lookup"><span data-stu-id="8e754-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="8e754-133">**Interface de ligne de commande Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e754-133">**Azure CLI**.</span></span> <span data-ttu-id="8e754-134">[Configurer hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environnement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8e754-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="8e754-135">Hello wget commande, si vous ne l’avez déjà : exécuter `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="8e754-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="8e754-136">Un abonnement Azure et un stockage existant compte qu’il contient les données de salutation toostore.</span><span class="sxs-lookup"><span data-stu-id="8e754-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="8e754-137">Exemple d’installation</span><span class="sxs-lookup"><span data-stu-id="8e754-137">Sample installation</span></span>

<span data-ttu-id="8e754-138">Renseignez les paramètres corrects de hello sur hello trois premières lignes, puis exécuter ce script en tant que racine :</span><span class="sxs-lookup"><span data-stu-id="8e754-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="8e754-139">URL de Hello pour la configuration d’exemple hello et son contenu, est toochange de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8e754-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="8e754-140">Téléchargez une copie du fichier JSON de paramètres de portail hello et personnaliser en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8e754-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="8e754-141">Les modèles ou l’automation que vous construisez doit utiliser votre propre copie au lieu de télécharger cette URL à chaque fois.</span><span class="sxs-lookup"><span data-stu-id="8e754-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="8e754-142">Mise à jour des paramètres d’extension hello</span><span class="sxs-lookup"><span data-stu-id="8e754-142">Updating hello extension settings</span></span>

<span data-ttu-id="8e754-143">Une fois que vous avez modifié les paramètres de votre protégé ou Public, déployez-les toohello machine virtuelle en exécutant hello même commande.</span><span class="sxs-lookup"><span data-stu-id="8e754-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="8e754-144">Si rien modifié dans les paramètres de hello, paramètres de hello mis à jour sont envoyées toohello extension.</span><span class="sxs-lookup"><span data-stu-id="8e754-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="8e754-145">SCÉNARISTE recharge la configuration de hello et redémarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="8e754-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="8e754-146">Migration à partir de versions précédentes de l’extension de hello</span><span class="sxs-lookup"><span data-stu-id="8e754-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="8e754-147">version la plus récente de l’extension de hello Hello est **3.0**.</span><span class="sxs-lookup"><span data-stu-id="8e754-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="8e754-148">**Les anciennes versions (2.x) sont dépréciées, et leur publication peut cesser le 31 juillet 2018 ou après**.</span><span class="sxs-lookup"><span data-stu-id="8e754-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e754-149">Cette extension présente la configuration de toohello de modifications avec rupture d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="8e754-150">Une telle modification sécurité de hello tooimprove d’extension de hello ; Par conséquent, descendante compatibilité avec 2.x Échec de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="8e754-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="8e754-151">En outre, hello Extension de serveur de publication pour cette extension est différent à publisher hello pour les versions 2.x hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="8e754-152">toomigrate de 2.x toothis nouvelle version de l’extension de hello, vous devez désinstaller ancienne extension de hello (sous l’ancien nom du serveur de publication hello), puis installez la version 3 d’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="8e754-153">Recommandations :</span><span class="sxs-lookup"><span data-stu-id="8e754-153">Recommendations:</span></span>

* <span data-ttu-id="8e754-154">Installez l’extension de hello avec mise à niveau de version mineure automatique activée.</span><span class="sxs-lookup"><span data-stu-id="8e754-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="8e754-155">Sur le modèle de déploiement classique de machines virtuelles, spécifiez « 3.* » en tant que version de hello si vous installez extension hello via Azure-XPLAT-CLI ou Powershell.</span><span class="sxs-lookup"><span data-stu-id="8e754-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="8e754-156">Modèle de machines virtuelles sur le déploiement d’Azure Resource Manager, incluez ' « autoUpgradeMinorVersion » : true' dans le modèle de déploiement d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="8e754-157">Utilisez un compte de stockage nouveau ou différent pour l’extension de diagnostic Linux 3.0.</span><span class="sxs-lookup"><span data-stu-id="8e754-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="8e754-158">Il existe plusieurs petites incompatibilités entre l’extension de diagnostic Linux 2.3 et l’extension de diagnostic Linux 3.0, qui rendent problématique le partage d’un compte :</span><span class="sxs-lookup"><span data-stu-id="8e754-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="8e754-159">L’extension de diagnostic Linux 3.0 stocke les événements Syslog dans une table avec un nom différent.</span><span class="sxs-lookup"><span data-stu-id="8e754-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="8e754-160">chaînes de counterSpecifier de Hello pour `builtin` métriques diffèrent dans SCÉNARISTE 3.0.</span><span class="sxs-lookup"><span data-stu-id="8e754-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="8e754-161">Paramètres protégés</span><span class="sxs-lookup"><span data-stu-id="8e754-161">Protected settings</span></span>

<span data-ttu-id="8e754-162">Cet ensemble d’informations de configuration contient des informations sensibles qui doivent être protégées d’une exposition publique, par exemple les informations d’identification de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e754-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="8e754-163">Ces paramètres sont transmis tooand stockée par extension hello sous forme chiffrée.</span><span class="sxs-lookup"><span data-stu-id="8e754-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="8e754-164">Nom</span><span class="sxs-lookup"><span data-stu-id="8e754-164">Name</span></span> | <span data-ttu-id="8e754-165">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-165">Value</span></span>
---- | -----
<span data-ttu-id="8e754-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="8e754-166">storageAccountName</span></span> | <span data-ttu-id="8e754-167">nom Hello hello du compte de stockage dans lequel les données sont écrites par l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="8e754-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="8e754-168">storageAccountEndPoint</span></span> | <span data-ttu-id="8e754-169">point de terminaison (facultatif) hello identification cloud hello dans le hello compte de stockage existe.</span><span class="sxs-lookup"><span data-stu-id="8e754-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="8e754-170">Si ce paramètre est absent, SCÉNARISTE par défaut toohello cloud public Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="8e754-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="8e754-171">toouse un compte de stockage dans Azure situés en Allemagne, Azure Government ou Azure Chine, définissez cette valeur en conséquence.</span><span class="sxs-lookup"><span data-stu-id="8e754-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="8e754-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="8e754-172">storageAccountSasToken</span></span> | <span data-ttu-id="8e754-173">Un [jeton compte SAP](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) pour les services Blob et de Table (`ss='bt'`), toocontainers applicable et les objets (`srt='co'`), qui accorde ajouter, créer, répertorier, mettre à jour et d’autorisations en écriture (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="8e754-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="8e754-174">Faire *pas* inclure hello début-point d’interrogation ( ?).</span><span class="sxs-lookup"><span data-stu-id="8e754-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="8e754-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="8e754-175">mdsdHttpProxy</span></span> | <span data-ttu-id="8e754-176">(facultatif) HTTP proxy informations nécessaires tooenable hello extension tooconnect toohello spécifié le compte de stockage et de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8e754-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="8e754-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="8e754-177">sinksConfig</span></span> | <span data-ttu-id="8e754-178">(facultatif) Détails des autres destinations toowhich mesures et les événements peuvent être remis.</span><span class="sxs-lookup"><span data-stu-id="8e754-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="8e754-179">Hello des détails spécifiques chaque récepteur de données pris en charge par l’extension de hello sont décrites dans les sections hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="8e754-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="8e754-180">Vous pouvez aisément construire le jeton SAS de hello requis via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="8e754-181">Sélectionnez toowhich de compte de stockage à usage général hello souhaité hello extension toowrite</span><span class="sxs-lookup"><span data-stu-id="8e754-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="8e754-182">Sélectionnez « Signature d’accès partagé » à partir de la partie des paramètres hello du menu de gauche hello</span><span class="sxs-lookup"><span data-stu-id="8e754-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="8e754-183">Vérifiez les sections appropriées hello comme décrites précédemment</span><span class="sxs-lookup"><span data-stu-id="8e754-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="8e754-184">Cliquez sur le bouton de « Générer SAS » hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-184">Click hello "Generate SAS" button.</span></span>

![image](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="8e754-186">Hello de copie généré SAS dans le champ de storageAccountSasToken hello ; supprimer hello-interrogation de début (« ? »).</span><span class="sxs-lookup"><span data-stu-id="8e754-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="8e754-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="8e754-187">sinksConfig</span></span>

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

<span data-ttu-id="8e754-188">Cette section facultative définit autres destinations extension de hello toowhich envoie des informations de hello qu'il collecte.</span><span class="sxs-lookup"><span data-stu-id="8e754-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="8e754-189">tableau de « sink » Hello contient un objet pour chaque récepteur de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8e754-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="8e754-190">Hello attribut « type » détermine hello autres attributs dans l’objet de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="8e754-191">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-191">Element</span></span> | <span data-ttu-id="8e754-192">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-192">Value</span></span>
------- | -----
<span data-ttu-id="8e754-193">name</span><span class="sxs-lookup"><span data-stu-id="8e754-193">name</span></span> | <span data-ttu-id="8e754-194">Chaîne utilisée récepteur de toothis toorefer ailleurs dans la configuration de l’extension hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="8e754-195">type</span><span class="sxs-lookup"><span data-stu-id="8e754-195">type</span></span> | <span data-ttu-id="8e754-196">type Hello du récepteur en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="8e754-196">hello type of sink being defined.</span></span> <span data-ttu-id="8e754-197">Détermine les hello autres valeurs (le cas échéant) dans les instances de ce type.</span><span class="sxs-lookup"><span data-stu-id="8e754-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="8e754-198">La version 3.0 de hello Extension Diagnostics Linux prend en charge deux types de récepteur : EventHub et JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="8e754-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="8e754-199">récepteur d’EventHub Hello</span><span class="sxs-lookup"><span data-stu-id="8e754-199">hello EventHub sink</span></span>

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

<span data-ttu-id="8e754-200">« sasURL » Hello contient hello URL complète, y compris le jeton SAS, pourquoi données toowhich de concentrateur d’événements doit être publiée.</span><span class="sxs-lookup"><span data-stu-id="8e754-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="8e754-201">SCÉNARISTE requiert une SAP une stratégie qui active la revendication d’envoi hello d’affectation de noms.</span><span class="sxs-lookup"><span data-stu-id="8e754-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="8e754-202">Exemple :</span><span class="sxs-lookup"><span data-stu-id="8e754-202">An example:</span></span>

* <span data-ttu-id="8e754-203">Créer un espace de noms Event Hub appelé `contosohub`</span><span class="sxs-lookup"><span data-stu-id="8e754-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="8e754-204">Créer un concentrateur d’événements dans l’espace de noms hello appelé`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="8e754-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="8e754-205">Créer une stratégie d’accès partagé sur hello concentrateur d’événements nommé `writer` qu’Active hello revendication d’envoi</span><span class="sxs-lookup"><span data-stu-id="8e754-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="8e754-206">Si vous avez créé une SAP de bonne jusqu'à minuit UTC sur 1 janvier 2018, la valeur de sasURL hello peut être :</span><span class="sxs-lookup"><span data-stu-id="8e754-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="8e754-207">Pour plus d’informations sur la génération de jetons SAS pour les Event Hubs, consultez [cette page web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e754-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="8e754-208">récepteur de JsonBlob Hello</span><span class="sxs-lookup"><span data-stu-id="8e754-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="8e754-209">Données dirigées tooa JsonBlob récepteur est stocké dans des objets BLOB dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="8e754-210">Chaque instance de l’extension de diagnostic Linux crée un objet blob toutes les heures pour chaque nom de récepteur.</span><span class="sxs-lookup"><span data-stu-id="8e754-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="8e754-211">Chaque objet blob contient toujours un tableau JSON syntaxiquement valide de l’objet.</span><span class="sxs-lookup"><span data-stu-id="8e754-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="8e754-212">Nouvelles entrées sont ajoutées atomiquement toohello tableau.</span><span class="sxs-lookup"><span data-stu-id="8e754-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="8e754-213">Objets BLOB sont stockés dans un conteneur avec hello même nom comme récepteur de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="8e754-214">Hello des règles de stockage Azure pour les noms de conteneur d’objets blob s’appliquent à des noms de toohello des récepteurs de JsonBlob : entre 3 et 63 caractères ASCII alphanumériques de minuscules ou des tirets.</span><span class="sxs-lookup"><span data-stu-id="8e754-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="8e754-215">Paramètres publics</span><span class="sxs-lookup"><span data-stu-id="8e754-215">Public settings</span></span>

<span data-ttu-id="8e754-216">Cette structure contient différents blocs de paramètres qui contrôlent les informations hello collectées par l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="8e754-217">Chaque paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="8e754-217">Each setting is optional.</span></span> <span data-ttu-id="8e754-218">Si vous spécifiez `ladCfg`, vous devez aussi spécifier `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="8e754-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="8e754-219">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-219">Element</span></span> | <span data-ttu-id="8e754-220">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-220">Value</span></span>
------- | -----
<span data-ttu-id="8e754-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="8e754-221">StorageAccount</span></span> | <span data-ttu-id="8e754-222">nom Hello hello du compte de stockage dans lequel les données sont écrites par l’extension de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="8e754-223">Doit être hello même nom que celui qu’est spécifiée dans hello [paramètres protégés par](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8e754-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="8e754-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="8e754-224">mdsdHttpProxy</span></span> | <span data-ttu-id="8e754-225">(facultatif) Identique à celui inclus hello [paramètres protégés par](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8e754-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="8e754-226">valeur de publique Hello est remplacée par valeur privé de hello, si définie.</span><span class="sxs-lookup"><span data-stu-id="8e754-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="8e754-227">Placer les paramètres de proxy qui contiennent une clé secrète, par exemple un mot de passe, Bonjour [paramètres protégés par](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8e754-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="8e754-228">les éléments restants Hello sont décrites en détail dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="8e754-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="8e754-229">ladCfg</span></span>

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

<span data-ttu-id="8e754-230">Cette collecte de données facultatif structure contrôles hello de mesures et les journaux toohello de remise des données de service et tooother Azure métriques récepteurs.</span><span class="sxs-lookup"><span data-stu-id="8e754-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="8e754-231">Vous devez spécifier `performanceCounters` ou `syslogEvents`, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="8e754-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="8e754-232">Vous devez spécifier hello `metrics` structure.</span><span class="sxs-lookup"><span data-stu-id="8e754-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="8e754-233">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-233">Element</span></span> | <span data-ttu-id="8e754-234">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-234">Value</span></span>
------- | -----
<span data-ttu-id="8e754-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="8e754-235">eventVolume</span></span> | <span data-ttu-id="8e754-236">(facultatif) Contrôles hello nombre de partitions créées au sein de la table de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="8e754-237">Doit être `"Large"`, `"Medium"` ou `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="8e754-238">Si non spécifié, la valeur par défaut de hello est `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="8e754-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="8e754-239">sampleRateInSeconds</span></span> | <span data-ttu-id="8e754-240">intervalle par défaut de hello (facultatif) entre la collection de brute (non agrégée).</span><span class="sxs-lookup"><span data-stu-id="8e754-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="8e754-241">taux d’échantillonnage Hello plus petit pris en charge est de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="8e754-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="8e754-242">Si non spécifié, la valeur par défaut de hello est `15`.</span><span class="sxs-lookup"><span data-stu-id="8e754-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="8e754-243">Mesures</span><span class="sxs-lookup"><span data-stu-id="8e754-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="8e754-244">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-244">Element</span></span> | <span data-ttu-id="8e754-245">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-245">Value</span></span>
------- | -----
<span data-ttu-id="8e754-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="8e754-246">resourceId</span></span> | <span data-ttu-id="8e754-247">ID de ressource Azure Resource Manager Hello de hello machine virtuelle ou d’échelle de machines virtuelles hello définie hello toowhich que machine virtuelle appartient.</span><span class="sxs-lookup"><span data-stu-id="8e754-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="8e754-248">Ce paramètre doit être également spécifiée si n’importe quel récepteur JsonBlob est utilisé dans la configuration de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="8e754-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="8e754-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="8e754-250">Hello fréquence à laquelle les métriques d’agrégation toobe calculées et transférées tooAzure métriques, exprimée sous la forme d’un intervalle de temps est un 8601.</span><span class="sxs-lookup"><span data-stu-id="8e754-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="8e754-251">période de transfert plus petit Hello est de 60 secondes, autrement dit, PT1M.</span><span class="sxs-lookup"><span data-stu-id="8e754-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="8e754-252">Vous devez spécifier au moins une scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="8e754-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="8e754-253">Exemples de hello métriques spécifiés dans la section des compteurs de performance hello sont collectées toutes les 15 secondes ou à des taux d’échantillonnage hello explicitement définie pour le compteur de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="8e754-254">Si plusieurs fréquences scheduledTransferPeriod apparaissent (comme dans l’exemple de hello), chaque agrégation est calculée indépendamment.</span><span class="sxs-lookup"><span data-stu-id="8e754-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="8e754-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="8e754-255">performanceCounters</span></span>

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

<span data-ttu-id="8e754-256">Collection de hello des métriques de contrôles de cette section facultative.</span><span class="sxs-lookup"><span data-stu-id="8e754-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="8e754-257">Exemples brutes sont agrégées pour chaque [scheduledTransferPeriod](#metrics) tooproduce ces valeurs :</span><span class="sxs-lookup"><span data-stu-id="8e754-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="8e754-258">mean</span><span class="sxs-lookup"><span data-stu-id="8e754-258">mean</span></span>
* <span data-ttu-id="8e754-259">minimum</span><span class="sxs-lookup"><span data-stu-id="8e754-259">minimum</span></span>
* <span data-ttu-id="8e754-260">maximum</span><span class="sxs-lookup"><span data-stu-id="8e754-260">maximum</span></span>
* <span data-ttu-id="8e754-261">dernière valeur collectée</span><span class="sxs-lookup"><span data-stu-id="8e754-261">last-collected value</span></span>
* <span data-ttu-id="8e754-262">nombre d’échantillons bruts utilisé agrégat de hello toocompute</span><span class="sxs-lookup"><span data-stu-id="8e754-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="8e754-263">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-263">Element</span></span> | <span data-ttu-id="8e754-264">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-264">Value</span></span>
------- | -----
<span data-ttu-id="8e754-265">sinks</span><span class="sxs-lookup"><span data-stu-id="8e754-265">sinks</span></span> | <span data-ttu-id="8e754-266">(facultatif) Une liste séparée par des virgules des noms des récepteurs toowhich que SCÉNARISTE envoie les résultats de mesure agrégées.</span><span class="sxs-lookup"><span data-stu-id="8e754-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="8e754-267">Toutes les mesures agrégées sont publiées tooeach répertorié récepteur.</span><span class="sxs-lookup"><span data-stu-id="8e754-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="8e754-268">Consultez [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="8e754-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="8e754-269">Exemple : `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="8e754-270">type</span><span class="sxs-lookup"><span data-stu-id="8e754-270">type</span></span> | <span data-ttu-id="8e754-271">Identifie hello réelle du fournisseur de métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="8e754-272">class</span><span class="sxs-lookup"><span data-stu-id="8e754-272">class</span></span> | <span data-ttu-id="8e754-273">Avec « counter », identifie le métrique spécifique de hello au sein de l’espace de noms du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="8e754-274">counter</span><span class="sxs-lookup"><span data-stu-id="8e754-274">counter</span></span> | <span data-ttu-id="8e754-275">Avec « classe », identifie le métrique spécifique de hello au sein de l’espace de noms du fournisseur hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="8e754-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="8e754-276">counterSpecifier</span></span> | <span data-ttu-id="8e754-277">Identifie les mesures spécifiques de hello au sein de l’espace de noms de métriques de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="8e754-278">condition</span><span class="sxs-lookup"><span data-stu-id="8e754-278">condition</span></span> | <span data-ttu-id="8e754-279">(facultatif) Applique de sélectionne une instance spécifique de la métrique de hello hello objet toowhich ou sélectionne hello d’agrégation sur toutes les instances de cet objet.</span><span class="sxs-lookup"><span data-stu-id="8e754-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="8e754-280">Pour plus d’informations, consultez hello [ `builtin` définitions de métrique](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="8e754-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="8e754-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="8e754-281">sampleRate</span></span> | <span data-ttu-id="8e754-282">EST l’intervalle 8601 qui définit les taux de hello collecte des échantillons brutes pour cette métrique.</span><span class="sxs-lookup"><span data-stu-id="8e754-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="8e754-283">Si non définie, intervalle de collecte hello a la valeur par valeur hello de [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="8e754-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="8e754-284">taux d’échantillonnage pris en charge le plus court de Hello est de 15 secondes (PT15S).</span><span class="sxs-lookup"><span data-stu-id="8e754-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="8e754-285">unité</span><span class="sxs-lookup"><span data-stu-id="8e754-285">unit</span></span> | <span data-ttu-id="8e754-286">Doit être une des chaînes suivantes : « Count », « Bytes », « Seconds », « Percent », « CountPerSecond », « BytesPerSecond », « Millisecond ».</span><span class="sxs-lookup"><span data-stu-id="8e754-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="8e754-287">Définit l’unité hello pour métrique de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="8e754-288">Consommateurs de données de hello collectée s’attendre hello collectées toomatch de valeurs de données de cette unité.</span><span class="sxs-lookup"><span data-stu-id="8e754-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="8e754-289">L’extension de diagnostic Linux ignore ce champ.</span><span class="sxs-lookup"><span data-stu-id="8e754-289">LAD ignores this field.</span></span>
<span data-ttu-id="8e754-290">displayName</span><span class="sxs-lookup"><span data-stu-id="8e754-290">displayName</span></span> | <span data-ttu-id="8e754-291">Hello étiquette (dans le langage de hello spécifié par les paramètres régionaux associé de hello) toobe attaché toothis des données dans Azure métriques.</span><span class="sxs-lookup"><span data-stu-id="8e754-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="8e754-292">L’extension de diagnostic Linux ignore ce champ.</span><span class="sxs-lookup"><span data-stu-id="8e754-292">LAD ignores this field.</span></span>

<span data-ttu-id="8e754-293">counterSpecifier de Hello est un identificateur arbitraire.</span><span class="sxs-lookup"><span data-stu-id="8e754-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="8e754-294">Les consommateurs de métriques, telles que hello graphiques portail Azure et alerte de fonctionnalité, utilisent counterSpecifier comme hello « clé » qui identifie une mesure ou une instance d’une métrique.</span><span class="sxs-lookup"><span data-stu-id="8e754-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="8e754-295">Pour les métriques `builtin`, nous vous recommandons d’utiliser des valeurs pour counterSpecifier qui commencent par `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="8e754-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="8e754-296">Si vous collectez une instance spécifique d’une mesure, nous vous recommandons de que vous joignez identificateur hello de valeur de counterSpecifier toohello hello instance.</span><span class="sxs-lookup"><span data-stu-id="8e754-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="8e754-297">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="8e754-297">Some examples:</span></span>

* <span data-ttu-id="8e754-298">`/builtin/Processor/PercentIdleTime` : Temps d’inactivité moyen pour tous les cœurs</span><span class="sxs-lookup"><span data-stu-id="8e754-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="8e754-299">`/builtin/Disk/FreeSpace(/mnt)`-Espace pour le système de fichiers/mnt hello</span><span class="sxs-lookup"><span data-stu-id="8e754-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="8e754-300">`/builtin/Disk/FreeSpace` : Espace libre moyen pour tous les systèmes de fichiers montés</span><span class="sxs-lookup"><span data-stu-id="8e754-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="8e754-301">SCÉNARISTE, ni hello portail Azure attend hello counterSpecifier valeur toomatch n’importe quel modèle.</span><span class="sxs-lookup"><span data-stu-id="8e754-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="8e754-302">Soyez cohérent dans la façon dont vous construisez les valeurs de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="8e754-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="8e754-303">Lorsque vous spécifiez `performanceCounters`, SCÉNARISTE écrit toujours table tooa de données dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="8e754-304">Vous pouvez avoir hello même les données écrites tooJSON BLOB et/ou les concentrateurs d’événements, mais vous ne pouvez pas désactiver le stockage table tooa de données.</span><span class="sxs-lookup"><span data-stu-id="8e754-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="8e754-305">Toutes les instances de hello extension diagnostic configurée toouse hello compte de stockage de même nom et le point de terminaison ajoutent leur toohello métriques et les journaux même table.</span><span class="sxs-lookup"><span data-stu-id="8e754-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="8e754-306">Si vous écrivent trop grand nombre de machines virtuelles toohello même partition de table, Azure peut accélérer écrit toothat partition.</span><span class="sxs-lookup"><span data-stu-id="8e754-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="8e754-307">eventVolume Hello définissant les causes entrées toobe réparties sur 1 (petit), 10 (moyen) ou 100 (grand) différentes partitions.</span><span class="sxs-lookup"><span data-stu-id="8e754-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="8e754-308">En règle générale, « Moyenne » est suffisante tooensure trafic n’est pas limité.</span><span class="sxs-lookup"><span data-stu-id="8e754-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="8e754-309">fonctionnalité de métriques de Azure Hello Hello portail Azure utilise des données de hello dans cette graphiques tooproduce de table ou les alertes de tootrigger.</span><span class="sxs-lookup"><span data-stu-id="8e754-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="8e754-310">nom de la table Hello est la concaténation de hello de ces chaînes :</span><span class="sxs-lookup"><span data-stu-id="8e754-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="8e754-311">Hello « scheduledTransferPeriod » pour hello agrégées des valeurs stockées dans la table de hello</span><span class="sxs-lookup"><span data-stu-id="8e754-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="8e754-312">Une date, dans l’écran hello « AAAAMMJJ », ce qui modifie tous les 10 jours</span><span class="sxs-lookup"><span data-stu-id="8e754-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="8e754-313">Exemples : `WADMetricsPT1HP10DV2S20170410` et `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="8e754-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="8e754-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="8e754-314">syslogEvents</span></span>

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

<span data-ttu-id="8e754-315">Cette section facultative contrôle collection hello de journaux d’événements à partir de syslog.</span><span class="sxs-lookup"><span data-stu-id="8e754-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="8e754-316">Si la section de hello est omise, les événements syslog ne sont pas capturés du tout.</span><span class="sxs-lookup"><span data-stu-id="8e754-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="8e754-317">Hello syslogEventConfiguration comporte une entrée pour chaque fonction syslog dignes d’intérêt.</span><span class="sxs-lookup"><span data-stu-id="8e754-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="8e754-318">Si minSeverity est « NONE » pour une installation donnée, ou si cette fonctionnalité n’apparaît pas du tout dans l’élément de hello, aucun événement à partir de cette fonctionnalité n’est capturées.</span><span class="sxs-lookup"><span data-stu-id="8e754-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="8e754-319">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-319">Element</span></span> | <span data-ttu-id="8e754-320">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-320">Value</span></span>
------- | -----
<span data-ttu-id="8e754-321">sinks</span><span class="sxs-lookup"><span data-stu-id="8e754-321">sinks</span></span> | <span data-ttu-id="8e754-322">Une liste séparée par des virgules des noms des récepteurs toowhich de journal des événements sont publiés.</span><span class="sxs-lookup"><span data-stu-id="8e754-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="8e754-323">Tous les événements de journal correspondant à des restrictions de hello dans syslogEventConfiguration sont publiées tooeach répertorié récepteur.</span><span class="sxs-lookup"><span data-stu-id="8e754-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="8e754-324">Exemple : « EHforsyslog »</span><span class="sxs-lookup"><span data-stu-id="8e754-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="8e754-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="8e754-325">facilityName</span></span> | <span data-ttu-id="8e754-326">Nom de fonction Syslog (comme « LOG\_USER » ou « LOG\_LOCAL0 »).</span><span class="sxs-lookup"><span data-stu-id="8e754-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="8e754-327">Voir « installation » hello section hello [page de manuel syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour la liste complète hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="8e754-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="8e754-328">minSeverity</span></span> | <span data-ttu-id="8e754-329">Niveau de gravité Syslog (comme « LOG\_ERR » ou « LOG\_INFO »).</span><span class="sxs-lookup"><span data-stu-id="8e754-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="8e754-330">Consultez la section « niveau » de hello Hello [page de manuel syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour la liste complète hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="8e754-331">extension de Hello capture la fonctionnalité de toohello événements envoyés à ou ci-dessus hello spécifié au niveau.</span><span class="sxs-lookup"><span data-stu-id="8e754-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="8e754-332">Lorsque vous spécifiez `syslogEvents`, SCÉNARISTE écrit toujours table tooa de données dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="8e754-333">Vous pouvez avoir hello même les données écrites tooJSON BLOB et/ou les concentrateurs d’événements, mais vous ne pouvez pas désactiver le stockage table tooa de données.</span><span class="sxs-lookup"><span data-stu-id="8e754-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="8e754-334">Hello partitionnement le comportement de cette table est hello identique à celle décrite pour `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="8e754-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="8e754-335">nom de la table Hello est la concaténation de hello de ces chaînes :</span><span class="sxs-lookup"><span data-stu-id="8e754-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="8e754-336">Une date, dans l’écran hello « AAAAMMJJ », ce qui modifie tous les 10 jours</span><span class="sxs-lookup"><span data-stu-id="8e754-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="8e754-337">Exemples : `LinuxSyslog20170410` et `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="8e754-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="8e754-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="8e754-338">perfCfg</span></span>

<span data-ttu-id="8e754-339">Cette section facultative contrôle l’exécution des requêtes [OMI](https://github.com/Microsoft/omi) arbitraires.</span><span class="sxs-lookup"><span data-stu-id="8e754-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="8e754-340">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-340">Element</span></span> | <span data-ttu-id="8e754-341">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-341">Value</span></span>
------- | -----
<span data-ttu-id="8e754-342">namespace</span><span class="sxs-lookup"><span data-stu-id="8e754-342">namespace</span></span> | <span data-ttu-id="8e754-343">espace de noms OMI de hello (facultatif) dans le hello requête doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="8e754-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="8e754-344">Si non spécifié, valeur par défaut de hello est « racine/scx », implémentée par hello [System Center inter-plateformes fournisseurs](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="8e754-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="8e754-345">query</span><span class="sxs-lookup"><span data-stu-id="8e754-345">query</span></span> | <span data-ttu-id="8e754-346">Hello OMI requête toobe doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="8e754-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="8e754-347">table</span><span class="sxs-lookup"><span data-stu-id="8e754-347">table</span></span> | <span data-ttu-id="8e754-348">table de stockage Azure hello (facultatif), Bonjour désigné du compte de stockage (voir [paramètres protégés par](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="8e754-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="8e754-349">frequency</span><span class="sxs-lookup"><span data-stu-id="8e754-349">frequency</span></span> | <span data-ttu-id="8e754-350">nombre de hello (facultatif) de secondes entre chaque exécution de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="8e754-351">La valeur par défaut est 300 (5 minutes). La valeur minimale est de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="8e754-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="8e754-352">sinks</span><span class="sxs-lookup"><span data-stu-id="8e754-352">sinks</span></span> | <span data-ttu-id="8e754-353">(facultatif) Une liste séparée par des virgules des noms des résultats des mesures supplémentaires récepteurs toowhich exemple brut doit être publiée.</span><span class="sxs-lookup"><span data-stu-id="8e754-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="8e754-354">Aucune agrégation de ces exemples brutes n’est calculée par extension de hello ou par les métriques de Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="8e754-355">Vous devez spécifier « table » ou « sinks », ou les deux.</span><span class="sxs-lookup"><span data-stu-id="8e754-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="8e754-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="8e754-356">fileLogs</span></span>

<span data-ttu-id="8e754-357">Hello de contrôles capturer des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="8e754-357">Controls hello capture of log files.</span></span> <span data-ttu-id="8e754-358">SCÉNARISTE capture les nouvelles lignes de texte qu’ils sont écrits toohello fichier et écrit les lignes tootable et/ou les récepteurs spécifiés (JsonBlob ou EventHub).</span><span class="sxs-lookup"><span data-stu-id="8e754-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="8e754-359">Élément</span><span class="sxs-lookup"><span data-stu-id="8e754-359">Element</span></span> | <span data-ttu-id="8e754-360">Valeur</span><span class="sxs-lookup"><span data-stu-id="8e754-360">Value</span></span>
------- | -----
<span data-ttu-id="8e754-361">file</span><span class="sxs-lookup"><span data-stu-id="8e754-361">file</span></span> | <span data-ttu-id="8e754-362">chemin d’accès complet Hello de toobe de fichier journal hello observé et capturées.</span><span class="sxs-lookup"><span data-stu-id="8e754-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="8e754-363">chemin d’accès Hello doit désigner un fichier unique ; Il ne peut pas nommer un répertoire ou contenir des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="8e754-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="8e754-364">table</span><span class="sxs-lookup"><span data-stu-id="8e754-364">table</span></span> | <span data-ttu-id="8e754-365">table de stockage Azure hello (facultatif), dans le stockage hello désigné (comme spécifié dans la configuration de hello protégé), dans les nouvelles lignes du compte hello « fin » du fichier de hello est écrits.</span><span class="sxs-lookup"><span data-stu-id="8e754-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="8e754-366">sinks</span><span class="sxs-lookup"><span data-stu-id="8e754-366">sinks</span></span> | <span data-ttu-id="8e754-367">(facultatif) Une liste séparée par des virgules de noms de lignes de journal supplémentaires récepteurs toowhich envoyé.</span><span class="sxs-lookup"><span data-stu-id="8e754-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="8e754-368">Vous devez spécifier « table » ou « sinks », ou les deux.</span><span class="sxs-lookup"><span data-stu-id="8e754-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="8e754-369">Mesures prises en charge par le fournisseur de builtin hello</span><span class="sxs-lookup"><span data-stu-id="8e754-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="8e754-370">fournisseur de métrique builtin Hello est une source de métriques plus intéressantes tooa large ensemble d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8e754-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="8e754-371">Ces métriques se répartissent en cinq classes principales :</span><span class="sxs-lookup"><span data-stu-id="8e754-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="8e754-372">Processeur</span><span class="sxs-lookup"><span data-stu-id="8e754-372">Processor</span></span>
* <span data-ttu-id="8e754-373">Mémoire</span><span class="sxs-lookup"><span data-stu-id="8e754-373">Memory</span></span>
* <span data-ttu-id="8e754-374">Réseau</span><span class="sxs-lookup"><span data-stu-id="8e754-374">Network</span></span>
* <span data-ttu-id="8e754-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="8e754-375">Filesystem</span></span>
* <span data-ttu-id="8e754-376">Disque</span><span class="sxs-lookup"><span data-stu-id="8e754-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="8e754-377">métriques de Builtin pour hello classe du processeur</span><span class="sxs-lookup"><span data-stu-id="8e754-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="8e754-378">Hello classe du processeur de métriques fournit des informations sur l’utilisation du processeur Bonjour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8e754-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="8e754-379">Lors de l’agrégation des pourcentages, hello résulte moyenne de hello toutes les unités centrales.</span><span class="sxs-lookup"><span data-stu-id="8e754-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="8e754-380">Dans une machine virtuelle avec deux cœurs, si un seul cœur était occupé à 100 % et hello autres 100 % inactif, hello signalé que percentidletime serait 50.</span><span class="sxs-lookup"><span data-stu-id="8e754-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="8e754-381">Si chaque noyau a 50 % de disponibilité pour hello même période, hello signalé le résultat est également 50.</span><span class="sxs-lookup"><span data-stu-id="8e754-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="8e754-382">Quatre principaux de machine virtuelle, avec un seul cœur 100 % occupé et hello autres inactif, hello signalé que percentidletime serait 75.</span><span class="sxs-lookup"><span data-stu-id="8e754-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="8e754-383">counter</span><span class="sxs-lookup"><span data-stu-id="8e754-383">counter</span></span> | <span data-ttu-id="8e754-384">Signification</span><span class="sxs-lookup"><span data-stu-id="8e754-384">Meaning</span></span>
------- | -------
<span data-ttu-id="8e754-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="8e754-385">PercentIdleTime</span></span> | <span data-ttu-id="8e754-386">Pourcentage de temps au cours de la fenêtre d’agrégation hello que processeurs sont exécutaient boucle inactive du noyau hello</span><span class="sxs-lookup"><span data-stu-id="8e754-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="8e754-387">percentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="8e754-387">PercentProcessorTime</span></span> | <span data-ttu-id="8e754-388">Pourcentage de temps passé à exécuter un thread actif</span><span class="sxs-lookup"><span data-stu-id="8e754-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="8e754-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="8e754-389">PercentIOWaitTime</span></span> | <span data-ttu-id="8e754-390">Pourcentage de temps d’attente des toocomplete des opérations d’e/s</span><span class="sxs-lookup"><span data-stu-id="8e754-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="8e754-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="8e754-391">PercentInterruptTime</span></span> | <span data-ttu-id="8e754-392">Pourcentage de temps passé à exécuter des interruptions matérielles/logicielles et des appels DPC (appels de procédure différés)</span><span class="sxs-lookup"><span data-stu-id="8e754-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="8e754-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="8e754-393">PercentUserTime</span></span> | <span data-ttu-id="8e754-394">De temps au cours de la fenêtre d’agrégation hello, pourcentage de hello de temps passé dans utilisateur plus au niveau de priorité normale</span><span class="sxs-lookup"><span data-stu-id="8e754-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="8e754-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="8e754-395">PercentNiceTime</span></span> | <span data-ttu-id="8e754-396">De temps, hello le pourcentage de temps passé à basse priorité (nice)</span><span class="sxs-lookup"><span data-stu-id="8e754-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="8e754-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="8e754-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="8e754-398">De temps, hello le pourcentage de temps passé en mode privilégié (noyau)</span><span class="sxs-lookup"><span data-stu-id="8e754-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="8e754-399">Hello tout d’abord quatre compteurs doivent additionner too100 %.</span><span class="sxs-lookup"><span data-stu-id="8e754-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="8e754-400">Hello dernière trois compteurs également somme too100 % ; ils subdivisent somme hello PercentProcessorTime PercentIOWaitTime et PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="8e754-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="8e754-401">tooobtain une seule mesure agrégée sur tous les processeurs, définissez `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="8e754-402">tooobtain une métrique pour un processeur spécifique, telles que le deuxième processeur logique hello de quatre principaux de machine virtuelle, définissez `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="8e754-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="8e754-403">Numéros des processeurs logiques sont dans la plage de hello `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="8e754-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="8e754-404">métriques de Builtin pour hello classe de mémoire</span><span class="sxs-lookup"><span data-stu-id="8e754-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="8e754-405">Hello classe de mémoire de métriques fournit des informations sur l’utilisation de mémoire, la pagination et le remplacement.</span><span class="sxs-lookup"><span data-stu-id="8e754-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="8e754-406">counter</span><span class="sxs-lookup"><span data-stu-id="8e754-406">counter</span></span> | <span data-ttu-id="8e754-407">Signification</span><span class="sxs-lookup"><span data-stu-id="8e754-407">Meaning</span></span>
------- | -------
<span data-ttu-id="8e754-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="8e754-408">AvailableMemory</span></span> | <span data-ttu-id="8e754-409">Mémoire physique disponible en Mio</span><span class="sxs-lookup"><span data-stu-id="8e754-409">Available physical memory in MiB</span></span>
<span data-ttu-id="8e754-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="8e754-410">PercentAvailableMemory</span></span> | <span data-ttu-id="8e754-411">Mémoire physique disponible sous forme de pourcentage de la mémoire totale</span><span class="sxs-lookup"><span data-stu-id="8e754-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="8e754-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="8e754-412">UsedMemory</span></span> | <span data-ttu-id="8e754-413">Mémoire physique utilisée (Mio)</span><span class="sxs-lookup"><span data-stu-id="8e754-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="8e754-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="8e754-414">PercentUsedMemory</span></span> | <span data-ttu-id="8e754-415">Mémoire physique utilisée sous forme de pourcentage de la mémoire totale</span><span class="sxs-lookup"><span data-stu-id="8e754-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="8e754-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="8e754-416">PagesPerSec</span></span> | <span data-ttu-id="8e754-417">Pagination totale (lecture/écriture)</span><span class="sxs-lookup"><span data-stu-id="8e754-417">Total paging (read/write)</span></span>
<span data-ttu-id="8e754-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="8e754-418">PagesReadPerSec</span></span> | <span data-ttu-id="8e754-419">Pages lues dans le magasin de stockage (fichier d’échange, fichier programme, fichier mappé, etc.)</span><span class="sxs-lookup"><span data-stu-id="8e754-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="8e754-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="8e754-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="8e754-421">Stocker les pages écrites toobacking (fichier d’échange, fichier mappé, etc.).</span><span class="sxs-lookup"><span data-stu-id="8e754-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="8e754-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="8e754-422">AvailableSwap</span></span> | <span data-ttu-id="8e754-423">Espace d’échange non utilisé (Mio)</span><span class="sxs-lookup"><span data-stu-id="8e754-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="8e754-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="8e754-424">PercentAvailableSwap</span></span> | <span data-ttu-id="8e754-425">Espace d’échange non utilisé sous forme de pourcentage de l’espace d’échange total</span><span class="sxs-lookup"><span data-stu-id="8e754-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="8e754-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="8e754-426">UsedSwap</span></span> | <span data-ttu-id="8e754-427">Espace d’échange utilisé (Mio)</span><span class="sxs-lookup"><span data-stu-id="8e754-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="8e754-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="8e754-428">PercentUsedSwap</span></span> | <span data-ttu-id="8e754-429">Espace d’échange utilisé sous forme de pourcentage de l’espace d’échange total</span><span class="sxs-lookup"><span data-stu-id="8e754-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="8e754-430">Cette classe de métriques n’a qu’une seule instance.</span><span class="sxs-lookup"><span data-stu-id="8e754-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="8e754-431">attribut de « condition » Hello possède pas de paramètres utiles et doit être omis.</span><span class="sxs-lookup"><span data-stu-id="8e754-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="8e754-432">métriques de Builtin pour hello classe du réseau</span><span class="sxs-lookup"><span data-stu-id="8e754-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="8e754-433">Hello classe réseau de métriques fournit des informations sur l’activité du réseau sur une interface réseau depuis le démarrage.</span><span class="sxs-lookup"><span data-stu-id="8e754-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="8e754-434">L’extension de diagnostic Linux n’expose pas de métriques de la bande passante, qui peuvent être récupérées à partir des métriques de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="8e754-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="8e754-435">compteur</span><span class="sxs-lookup"><span data-stu-id="8e754-435">counter</span></span> | <span data-ttu-id="8e754-436">Signification</span><span class="sxs-lookup"><span data-stu-id="8e754-436">Meaning</span></span>
------- | -------
<span data-ttu-id="8e754-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="8e754-437">BytesTransmitted</span></span> | <span data-ttu-id="8e754-438">Nombre total d’octets envoyés depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-438">Total bytes sent since boot</span></span>
<span data-ttu-id="8e754-439">Octets reçus</span><span class="sxs-lookup"><span data-stu-id="8e754-439">BytesReceived</span></span> | <span data-ttu-id="8e754-440">Nombre total d’octets reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-440">Total bytes received since boot</span></span>
<span data-ttu-id="8e754-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="8e754-441">BytesTotal</span></span> | <span data-ttu-id="8e754-442">Nombre total d’octets envoyés ou reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="8e754-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="8e754-443">PacketsTransmitted</span></span> | <span data-ttu-id="8e754-444">Nombre total de paquets envoyés depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-444">Total packets sent since boot</span></span>
<span data-ttu-id="8e754-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="8e754-445">PacketsReceived</span></span> | <span data-ttu-id="8e754-446">Nombre total de paquets reçus depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-446">Total packets received since boot</span></span>
<span data-ttu-id="8e754-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="8e754-447">TotalRxErrors</span></span> | <span data-ttu-id="8e754-448">Nombre d’erreurs de réception depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-448">Number of receive errors since boot</span></span>
<span data-ttu-id="8e754-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="8e754-449">TotalTxErrors</span></span> | <span data-ttu-id="8e754-450">Nombre d’erreurs de transmission depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="8e754-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="8e754-451">TotalCollisions</span></span> | <span data-ttu-id="8e754-452">Nombre de collisions signalées par des ports réseau hello depuis le démarrage</span><span class="sxs-lookup"><span data-stu-id="8e754-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="8e754-453">Bien que cette classe soit instanciée, l’extension de diagnostic Linux ne prend pas en charge la capture de métriques réseau agrégées pour tous les périphériques réseau.</span><span class="sxs-lookup"><span data-stu-id="8e754-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="8e754-454">définir des métriques de hello tooobtain pour une interface spécifique, tel qu’eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="8e754-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="8e754-455">métriques de Builtin pour hello classe du système de fichiers</span><span class="sxs-lookup"><span data-stu-id="8e754-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="8e754-456">Hello classe de système de fichiers de métriques fournit des informations sur l’utilisation du système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="8e754-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="8e754-457">Valeurs absolues et le pourcentage sont signalés comme utilisateur ordinaire de tooan affichées (pas de racine).</span><span class="sxs-lookup"><span data-stu-id="8e754-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="8e754-458">counter</span><span class="sxs-lookup"><span data-stu-id="8e754-458">counter</span></span> | <span data-ttu-id="8e754-459">Signification</span><span class="sxs-lookup"><span data-stu-id="8e754-459">Meaning</span></span>
------- | -------
<span data-ttu-id="8e754-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="8e754-460">FreeSpace</span></span> | <span data-ttu-id="8e754-461">Espace disque disponible en octets</span><span class="sxs-lookup"><span data-stu-id="8e754-461">Available disk space in bytes</span></span>
<span data-ttu-id="8e754-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="8e754-462">UsedSpace</span></span> | <span data-ttu-id="8e754-463">Espace disque utilisé en octets</span><span class="sxs-lookup"><span data-stu-id="8e754-463">Used disk space in bytes</span></span>
<span data-ttu-id="8e754-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="8e754-464">PercentFreeSpace</span></span> | <span data-ttu-id="8e754-465">Pourcentage d’espace libre</span><span class="sxs-lookup"><span data-stu-id="8e754-465">Percentage free space</span></span>
<span data-ttu-id="8e754-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="8e754-466">PercentUsedSpace</span></span> | <span data-ttu-id="8e754-467">Pourcentage d’espace utilisé</span><span class="sxs-lookup"><span data-stu-id="8e754-467">Percentage used space</span></span>
<span data-ttu-id="8e754-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="8e754-468">PercentFreeInodes</span></span> | <span data-ttu-id="8e754-469">Pourcentage d’inodes non utilisés</span><span class="sxs-lookup"><span data-stu-id="8e754-469">Percentage of unused inodes</span></span>
<span data-ttu-id="8e754-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="8e754-470">PercentUsedInodes</span></span> | <span data-ttu-id="8e754-471">Pourcentage total d’inodes alloués (utilisés) pour tous les systèmes de fichiers</span><span class="sxs-lookup"><span data-stu-id="8e754-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="8e754-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-472">BytesReadPerSecond</span></span> | <span data-ttu-id="8e754-473">Octets lus par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-473">Bytes read per second</span></span>
<span data-ttu-id="8e754-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="8e754-475">Octets écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-475">Bytes written per second</span></span>
<span data-ttu-id="8e754-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-476">BytesPerSecond</span></span> | <span data-ttu-id="8e754-477">Octets lus ou écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-477">Bytes read or written per second</span></span>
<span data-ttu-id="8e754-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-478">ReadsPerSecond</span></span> | <span data-ttu-id="8e754-479">Opérations de lecture par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-479">Read operations per second</span></span>
<span data-ttu-id="8e754-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-480">WritesPerSecond</span></span> | <span data-ttu-id="8e754-481">Opérations d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-481">Write operations per second</span></span>
<span data-ttu-id="8e754-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-482">TransfersPerSecond</span></span> | <span data-ttu-id="8e754-483">Opérations de lecture ou d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-483">Read or write operations per second</span></span>

<span data-ttu-id="8e754-484">Les valeurs agrégées pour tous les systèmes de fichiers peuvent être obtenues en définissant `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="8e754-485">Les valeurs pour un système de fichiers monté spécifique, comme « / mnt », peuvent être obtenues en définissant `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="8e754-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="8e754-486">métriques de Builtin pour hello classe disque</span><span class="sxs-lookup"><span data-stu-id="8e754-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="8e754-487">Hello classe disque de métriques fournit des informations sur l’utilisation du disque.</span><span class="sxs-lookup"><span data-stu-id="8e754-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="8e754-488">Ces statistiques s’appliquent toohello intégralité du lecteur.</span><span class="sxs-lookup"><span data-stu-id="8e754-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="8e754-489">S’il existe plusieurs systèmes de fichiers sur un appareil, compteurs hello pour cet appareil sont en réalité, agrégés sur tous les.</span><span class="sxs-lookup"><span data-stu-id="8e754-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="8e754-490">counter</span><span class="sxs-lookup"><span data-stu-id="8e754-490">counter</span></span> | <span data-ttu-id="8e754-491">Signification</span><span class="sxs-lookup"><span data-stu-id="8e754-491">Meaning</span></span>
------- | -------
<span data-ttu-id="8e754-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-492">ReadsPerSecond</span></span> | <span data-ttu-id="8e754-493">Opérations de lecture par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-493">Read operations per second</span></span>
<span data-ttu-id="8e754-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-494">WritesPerSecond</span></span> | <span data-ttu-id="8e754-495">Opérations d’écriture par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-495">Write operations per second</span></span>
<span data-ttu-id="8e754-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-496">TransfersPerSecond</span></span> | <span data-ttu-id="8e754-497">Nombre total d’opérations par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-497">Total operations per second</span></span>
<span data-ttu-id="8e754-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="8e754-498">AverageReadTime</span></span> | <span data-ttu-id="8e754-499">Nombre moyen de secondes par opération de lecture</span><span class="sxs-lookup"><span data-stu-id="8e754-499">Average seconds per read operation</span></span>
<span data-ttu-id="8e754-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="8e754-500">AverageWriteTime</span></span> | <span data-ttu-id="8e754-501">Nombre moyen de secondes par opération d’écriture</span><span class="sxs-lookup"><span data-stu-id="8e754-501">Average seconds per write operation</span></span>
<span data-ttu-id="8e754-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="8e754-502">AverageTransferTime</span></span> | <span data-ttu-id="8e754-503">Nombre moyen de secondes par opération</span><span class="sxs-lookup"><span data-stu-id="8e754-503">Average seconds per operation</span></span>
<span data-ttu-id="8e754-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="8e754-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="8e754-505">Nombre moyen d’opérations disque en file d’attente</span><span class="sxs-lookup"><span data-stu-id="8e754-505">Average number of queued disk operations</span></span>
<span data-ttu-id="8e754-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="8e754-507">Nombre d’octets lus par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-507">Number of bytes read per second</span></span>
<span data-ttu-id="8e754-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8e754-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="8e754-509">Nombre d’octets écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-509">Number of bytes written per second</span></span>
<span data-ttu-id="8e754-510">Octets par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-510">BytesPerSecond</span></span> | <span data-ttu-id="8e754-511">Nombre d’octets lus ou écrits par seconde</span><span class="sxs-lookup"><span data-stu-id="8e754-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="8e754-512">Les valeurs agrégées pour tous les disques peuvent être obtenues en définissant `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="8e754-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="8e754-513">jeu d’informations tooget pour un périphérique spécifique (par exemple, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="8e754-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="8e754-514">Installation et configuration de l’extension de diagnostic Linux 3.0 via CLI</span><span class="sxs-lookup"><span data-stu-id="8e754-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="8e754-515">En supposant que vos paramètres protégés sont dans le fichier de hello PrivateConfig.json et vos informations de configuration publique est PublicConfig.json, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8e754-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="8e754-516">commande Hello suppose que vous utilisez le mode de gestion des ressources Azure hello (arm) de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="8e754-517">tooconfigure SCÉNARISTE pour le déploiement classique (ASM) VMs du modèle, trop de basculer le mode « asm » (`azure config mode asm`) et omettre le nom de groupe de ressources hello dans la commande hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="8e754-518">Pour plus d’informations, consultez hello [documentation relative à CLI inter-plateformes](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="8e754-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="8e754-519">Exemple de configuration de l’extension de diagnostic Linux 3.0</span><span class="sxs-lookup"><span data-stu-id="8e754-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="8e754-520">En fonction de hello précédant définitions, ici un exemple de configuration d’extension SCÉNARISTE 3.0 avec une explication.</span><span class="sxs-lookup"><span data-stu-id="8e754-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="8e754-521">tooapply cet exemple tooyour de cas, vous devez utiliser votre propre nom de compte de stockage, le compte jeton SAS et des jetons EventHubs SAS.</span><span class="sxs-lookup"><span data-stu-id="8e754-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="8e754-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="8e754-522">PrivateConfig.json</span></span>

<span data-ttu-id="8e754-523">Ces paramètres privés configurent :</span><span class="sxs-lookup"><span data-stu-id="8e754-523">These private settings configure:</span></span>

* <span data-ttu-id="8e754-524">un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="8e754-524">a storage account</span></span>
* <span data-ttu-id="8e754-525">un jeton SAS de compte correspondant</span><span class="sxs-lookup"><span data-stu-id="8e754-525">a matching account SAS token</span></span>
* <span data-ttu-id="8e754-526">plusieurs récepteurs (JsonBlob ou EventHubs avec des jetons SAS)</span><span class="sxs-lookup"><span data-stu-id="8e754-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="8e754-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="8e754-527">PublicConfig.json</span></span>

<span data-ttu-id="8e754-528">Ces paramètres publics font que l’extension de diagnostic Linux :</span><span class="sxs-lookup"><span data-stu-id="8e754-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="8e754-529">Télécharger les métriques pourcentage de temps de processeur et l’espace disque utilisé toohello `WADMetrics*` table</span><span class="sxs-lookup"><span data-stu-id="8e754-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="8e754-530">Télécharger les messages syslog fonctionnalité « utilisateur » et la gravité « info » toohello `LinuxSyslog*` table</span><span class="sxs-lookup"><span data-stu-id="8e754-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="8e754-531">Télécharger brutes OMI requête résultats (PercentProcessorTime et PercentIdleTime) toohello nommé `LinuxCPU` table</span><span class="sxs-lookup"><span data-stu-id="8e754-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="8e754-532">Télécharger les lignes ajoutées dans le fichier `/var/log/myladtestlog` toohello `MyLadTestLog` table</span><span class="sxs-lookup"><span data-stu-id="8e754-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="8e754-533">Dans chaque cas, les données sont également chargées dans :</span><span class="sxs-lookup"><span data-stu-id="8e754-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="8e754-534">Stockage d’objets Blob Azure (nom du conteneur est tel que défini dans le récepteur de JsonBlob hello)</span><span class="sxs-lookup"><span data-stu-id="8e754-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="8e754-535">Point de terminaison EventHubs (comme spécifié dans le récepteur de EventHubs hello)</span><span class="sxs-lookup"><span data-stu-id="8e754-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

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

<span data-ttu-id="8e754-536">Hello `resourceId` hello configuration doit correspondre aux que de l’échelle de machines virtuelles de machine virtuelle ou hello hello définie.</span><span class="sxs-lookup"><span data-stu-id="8e754-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="8e754-537">Métriques de plateforme Azure graphiques et d’alerte sait resourceId hello Hello ordinateur virtuel sur lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="8e754-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="8e754-538">Il attend des données de hello toofind pour votre machine virtuelle à l’aide de la clé de recherche hello resourceId hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="8e754-539">Si vous utilisez Azure mise à l’échelle, resourceId hello dans la configuration de mise à l’échelle hello doit correspondre à resourceId hello utilisé par SCÉNARISTE.</span><span class="sxs-lookup"><span data-stu-id="8e754-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="8e754-540">Hello resourceId est intégrée à des noms de hello de JsonBlobs écrits par SCÉNARISTE.</span><span class="sxs-lookup"><span data-stu-id="8e754-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="8e754-541">Affichage de vos données</span><span class="sxs-lookup"><span data-stu-id="8e754-541">View your data</span></span>

<span data-ttu-id="8e754-542">Utiliser des données de performances hello tooview portail Azure, ou définir des alertes :</span><span class="sxs-lookup"><span data-stu-id="8e754-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![image](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="8e754-544">Hello `performanceCounters` données sont toujours stockées dans une table de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="8e754-545">Les API Stockage Azure sont disponibles pour de nombreux langages et de nombreuses plateformes.</span><span class="sxs-lookup"><span data-stu-id="8e754-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="8e754-546">Données envoyées tooJsonBlob récepteurs sont stockées dans des objets BLOB dans le compte de stockage hello nommé Bonjour [paramètres protégés par](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8e754-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="8e754-547">Vous pouvez utiliser les données d’objet blob hello à l’aide des API de stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8e754-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="8e754-548">En outre, vous pouvez utiliser ces données de l’interface utilisateur outils tooaccess hello dans le stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="8e754-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="8e754-549">Explorateur de serveurs Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e754-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="8e754-550">[Explorateur de stockage Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Explorateur de stockage Azure").</span><span class="sxs-lookup"><span data-stu-id="8e754-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="8e754-551">Cet instantané d’une session de Microsoft Azure Storage Explorer affiche hello généré des tables de stockage Azure et les conteneurs à partir d’une extension SCÉNARISTE 3.0 correctement configurée sur une machine virtuelle de test.</span><span class="sxs-lookup"><span data-stu-id="8e754-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="8e754-552">image de Hello ne correspond pas exactement à hello [exemple de configuration SCÉNARISTE 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="8e754-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![image](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="8e754-554">Consultez hello pertinentes [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn comment tooconsume messages publiés tooan EventHubs point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8e754-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e754-555">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e754-555">Next steps</span></span>

* <span data-ttu-id="8e754-556">Créer des alertes de métriques dans [moniteur Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) pour vous collectez les mesures de hello.</span><span class="sxs-lookup"><span data-stu-id="8e754-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="8e754-557">Créez [des graphiques de surveillance](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) pour vos métriques.</span><span class="sxs-lookup"><span data-stu-id="8e754-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="8e754-558">Découvrez comment trop[créer un ensemble d’échelle de machine virtuelle](/azure/virtual-machines/linux/tutorial-create-vmss) à l’aide de votre échelle toocontrol de métriques.</span><span class="sxs-lookup"><span data-stu-id="8e754-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
