---
title: 'Sauvegarde Azure : Utiliser PowerShell pour sauvegarder des charges de travail DPM | Microsoft Docs'
description: "Découvrez comment déployer et gérer Sauvegarde Azure pour Data Protection Manager (DPM) à l’aide de PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 943a12dcba49a114d206b9dab968da332ea99926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="84620-103">Déployer et gérer une sauvegarde vers Azure pour des serveurs Data Protection Manager (DPM) à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="84620-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="84620-104">ARM</span><span class="sxs-lookup"><span data-stu-id="84620-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="84620-105">Classique</span><span class="sxs-lookup"><span data-stu-id="84620-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="84620-106">Cet article explique comment utiliser PowerShell pour sauvegarder et récupérer des données DPM à partir d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="84620-106">This article explains how to use PowerShell to back up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="84620-107">Microsoft recommande d’utiliser des coffres Recovery Services pour tous les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="84620-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="84620-108">Si vous êtes un nouvel utilisateur de Sauvegarde Azure, appuyez-vous sur l’article [Déployer et gérer une sauvegarde vers Azure pour un serveur/client Windows à l’aide de PowerShell](backup-dpm-automation.md) pour stocker vos données dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="84620-108">If you are a new Azure Backup user, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84620-109">Vous pouvez désormais mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="84620-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="84620-110">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="84620-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="84620-111">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="84620-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="84620-112">À compter du 15 octobre 2017, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="84620-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="84620-113">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="84620-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="84620-114">tous les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="84620-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="84620-115">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="84620-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="84620-116">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="84620-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="84620-117">Configuration de l’environnement PowerShell</span><span class="sxs-lookup"><span data-stu-id="84620-117">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="84620-118">Avant de pouvoir utiliser PowerShell pour gérer les sauvegardes de Data Protection Manager vers Azure, vous devez disposer de l’environnement approprié dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84620-118">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you will need to have the right environment in PowerShell.</span></span> <span data-ttu-id="84620-119">Au début de la session PowerShell, veillez à exécuter la commande suivante pour importer les modules adéquats et avoir la possibilité de référencer correctement les applets de commande DPM :</span><span class="sxs-lookup"><span data-stu-id="84620-119">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="84620-120">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="84620-120">Setup and Registration</span></span>
<span data-ttu-id="84620-121">Pour commencer :</span><span class="sxs-lookup"><span data-stu-id="84620-121">To begin:</span></span>

1. <span data-ttu-id="84620-122">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="84620-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="84620-123">Activez les applets de commande Azure Backup en passant en mode *AzureResourceManager* via l’applet de commande **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="84620-123">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="84620-124">Les tâches de configuration et d’inscription ci-après peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="84620-124">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="84620-125">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="84620-125">Create a backup vault</span></span>
* <span data-ttu-id="84620-126">Installation de l'agent de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="84620-126">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="84620-127">Inscription auprès du service Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="84620-127">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="84620-128">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="84620-128">Networking settings</span></span>
* <span data-ttu-id="84620-129">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="84620-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="84620-130">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="84620-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="84620-131">Pour les clients utilisant Sauvegarde Azure pour la première fois, vous devez enregistrer le fournisseur Sauvegarde Azure à utiliser avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="84620-131">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="84620-132">Pour cela, exécutez la commande suivante : Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="84620-132">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="84620-133">Vous pouvez créer un coffre de sauvegarde en utilisant l’applet de commande **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="84620-133">You can create a new backup vault using the **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="84620-134">Le coffre de sauvegarde constituant une ressource ARM, vous devez le placer dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="84620-134">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="84620-135">Dans une console Azure PowerShell avec élévation de privilèges, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="84620-135">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="84620-136">Vous pouvez obtenir la liste de tous les coffres de sauvegarde d’un abonnement donné à l’aide de l’applet de commande **Get-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="84620-136">You can get a list of all the backup vaults in a given subscription using the **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="84620-137">Installation de l'agent de sauvegarde Azure sur un serveur DPM</span><span class="sxs-lookup"><span data-stu-id="84620-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="84620-138">Avant d’installer l'agent de sauvegarde Azure, vous devez avoir téléchargé le programme d’installation sur le serveur Windows.</span><span class="sxs-lookup"><span data-stu-id="84620-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="84620-139">Vous pouvez obtenir la dernière version du programme d’installation à partir du [Centre de téléchargement Microsoft](http://aka.ms/azurebackup_agent) ou de la page Tableau de bord du coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="84620-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="84620-140">Enregistrez le programme d’installation dans un emplacement auquel vous pouvez accéder facilement, par exemple *C:\Téléchargements\*.</span><span class="sxs-lookup"><span data-stu-id="84620-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="84620-141">Pour installer l’agent, exécutez la commande ci-après dans une console PowerShell avec élévation de privilèges **sur le serveur DPM**:</span><span class="sxs-lookup"><span data-stu-id="84620-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="84620-142">Cette opération installe l’agent avec les options par défaut.</span><span class="sxs-lookup"><span data-stu-id="84620-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="84620-143">L’installation s’effectue en arrière-plan et prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="84620-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="84620-144">Si vous ne spécifiez pas l’option */nu* , la fenêtre **Windows Update** s’ouvre à la fin de l’installation pour rechercher des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="84620-144">If you do not specify the */nu* option the **Windows Update** window will open at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="84620-145">L’agent apparaîtra dans la liste des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="84620-145">The agent will show in the list of installed programs.</span></span> <span data-ttu-id="84620-146">Pour afficher la liste des programmes installés, cliquez sur **Panneau de configuration** > **Programmes** > **Programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="84620-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="84620-148">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="84620-148">Installation options</span></span>
<span data-ttu-id="84620-149">Pour afficher toutes les options disponibles via la ligne de commande, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="84620-149">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="84620-150">Les options disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="84620-150">The available options include:</span></span>

| <span data-ttu-id="84620-151">Option</span><span class="sxs-lookup"><span data-stu-id="84620-151">Option</span></span> | <span data-ttu-id="84620-152">Détails</span><span class="sxs-lookup"><span data-stu-id="84620-152">Details</span></span> | <span data-ttu-id="84620-153">Default</span><span class="sxs-lookup"><span data-stu-id="84620-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="84620-154">/q</span><span class="sxs-lookup"><span data-stu-id="84620-154">/q</span></span> |<span data-ttu-id="84620-155">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="84620-155">Quiet installation</span></span> |- |
| <span data-ttu-id="84620-156">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="84620-156">/p:"location"</span></span> |<span data-ttu-id="84620-157">Chemin d’accès du dossier d’installation de l’agent de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="84620-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="84620-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="84620-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="84620-159">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="84620-159">/s:"location"</span></span> |<span data-ttu-id="84620-160">Chemin d’accès du dossier de cache de l’agent de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="84620-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="84620-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="84620-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="84620-162">/m</span><span class="sxs-lookup"><span data-stu-id="84620-162">/m</span></span> |<span data-ttu-id="84620-163">Abonnement à Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="84620-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="84620-164">/nu</span><span class="sxs-lookup"><span data-stu-id="84620-164">/nu</span></span> |<span data-ttu-id="84620-165">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="84620-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="84620-166">/d</span><span class="sxs-lookup"><span data-stu-id="84620-166">/d</span></span> |<span data-ttu-id="84620-167">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="84620-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="84620-168">/ph</span><span class="sxs-lookup"><span data-stu-id="84620-168">/ph</span></span> |<span data-ttu-id="84620-169">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="84620-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="84620-170">/po</span><span class="sxs-lookup"><span data-stu-id="84620-170">/po</span></span> |<span data-ttu-id="84620-171">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="84620-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="84620-172">/pu</span><span class="sxs-lookup"><span data-stu-id="84620-172">/pu</span></span> |<span data-ttu-id="84620-173">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="84620-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="84620-174">/pw</span><span class="sxs-lookup"><span data-stu-id="84620-174">/pw</span></span> |<span data-ttu-id="84620-175">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="84620-175">Proxy Password</span></span> |- |

### <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="84620-176">Inscription auprès du service Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="84620-176">Registering with the Azure Backup service</span></span>
<span data-ttu-id="84620-177">Avant de pouvoir vous inscrire auprès du service Sauvegarde Azure, vous devez vous assurer que les [prérequis](backup-azure-dpm-introduction.md) sont remplis.</span><span class="sxs-lookup"><span data-stu-id="84620-177">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="84620-178">Vous devez respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="84620-178">You must:</span></span>

* <span data-ttu-id="84620-179">Avoir un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="84620-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="84620-180">Disposer d’un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="84620-180">Have a backup vault</span></span>

<span data-ttu-id="84620-181">Pour télécharger les informations d’identification du coffre, exécutez l’applet de commande **Get-AzureBackupVaultCredentials** dans une console Azure PowerShell, puis stockez ces informations dans un emplacement pratique, tel que *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="84620-181">To download the vault credentials, run the **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="84620-182">L’inscription de l’ordinateur auprès du coffre s’effectue l’aide de l’applet de commande [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) :</span><span class="sxs-lookup"><span data-stu-id="84620-182">Registering the machine with the vault is done using the [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="84620-183">Cette opération inscrira le serveur DPM nommé « TestingServer » auprès de Microsoft Azure Vault à l’aide des informations d’identification de coffre.</span><span class="sxs-lookup"><span data-stu-id="84620-183">This will register the DPM Server named “TestingServer” with Microsoft Azure Vault using the specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84620-184">N’utilisez pas de chemins relatifs pour spécifier le fichier des informations d’identification du coffre.</span><span class="sxs-lookup"><span data-stu-id="84620-184">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="84620-185">Vous devez fournir un chemin absolu dans l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="84620-185">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="84620-186">Paramètres de la configuration initiale</span><span class="sxs-lookup"><span data-stu-id="84620-186">Initial configuration settings</span></span>
<span data-ttu-id="84620-187">Une fois que le serveur DPM est inscrit auprès du coffre de sauvegarde Azure, il démarre avec les paramètres d’abonnement par défaut.</span><span class="sxs-lookup"><span data-stu-id="84620-187">Once the DPM Server is registered with the Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="84620-188">Ces paramètres d’abonnement incluent la mise en réseau, le chiffrement et la zone intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="84620-188">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="84620-189">Avant de modifier les paramètres d’abonnement, vous devez obtenir les paramètres (par défaut) existants à l’aide de l’applet de commande [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="84620-189">To begin changing the subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="84620-190">Toutes les modifications sont apportées à cet objet PowerShell local ```$setting```. L’objet complet est ensuite validé vers DPM et la Sauvegarde Azure à des fins d’enregistrement à l’aide de l’applet de commande [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="84620-190">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="84620-191">Vous devez utiliser l’indicateur ```–Commit``` pour vous assurer que les modifications sont conservées.</span><span class="sxs-lookup"><span data-stu-id="84620-191">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="84620-192">Les paramètres ne sont pas appliqués ni utilisés par Sauvegarde Azure tant qu’ils ne sont pas validés.</span><span class="sxs-lookup"><span data-stu-id="84620-192">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="84620-193">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="84620-193">Networking</span></span>
<span data-ttu-id="84620-194">Si la connectivité entre l'ordinateur DPM et le service Sauvegarde Azure sur Internet est établie via un serveur proxy, les paramètres du serveur proxy doivent être fournis pour que les sauvegardes soient réussies.</span><span class="sxs-lookup"><span data-stu-id="84620-194">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for backups to succeed.</span></span> <span data-ttu-id="84620-195">Pour cela, utilisez les paramètres ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` et ```ProxyPassword``` avec l’applet de commande [DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="84620-195">This is done by using the ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="84620-196">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="84620-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="84620-197">L’utilisation de la bande passante peut également être contrôlée avec les options ```-WorkHourBandwidth``` et ```-NonWorkHourBandwidth```, certains jours de la semaine.</span><span class="sxs-lookup"><span data-stu-id="84620-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="84620-198">Dans cet exemple, nous ne fixons aucune limitation.</span><span class="sxs-lookup"><span data-stu-id="84620-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-the-staging-area"></a><span data-ttu-id="84620-199">Configuration de la zone intermédiaire</span><span class="sxs-lookup"><span data-stu-id="84620-199">Configuring the staging Area</span></span>
<span data-ttu-id="84620-200">L’agent de sauvegarde Azure en cours d’exécution sur le serveur DPM a besoin d’un stockage temporaire pour les données restaurées à partir du cloud (zone de transit locale).</span><span class="sxs-lookup"><span data-stu-id="84620-200">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="84620-201">Configurez la zone intermédiaire à l’aide de l’applet de commande [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) et du paramètre ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="84620-201">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="84620-202">Dans l’exemple ci-dessus, la zone intermédiaire est définie sur *C:\StagingArea* dans l’objet PowerShell ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="84620-202">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="84620-203">Assurez-vous que le dossier spécifié existe déjà, sinon la validation finale des paramètres d’abonnement échouera.</span><span class="sxs-lookup"><span data-stu-id="84620-203">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="84620-204">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="84620-204">Encryption settings</span></span>
<span data-ttu-id="84620-205">Les données sauvegardées envoyées à Sauvegarde Azure sont chiffrées pour garantir leur confidentialité.</span><span class="sxs-lookup"><span data-stu-id="84620-205">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="84620-206">Le mot de passe du chiffrement est le « mot de passe » permettant de déchiffrer les données lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="84620-206">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="84620-207">Il est important de conserver ces informations en lieu sûr après les avoir définies.</span><span class="sxs-lookup"><span data-stu-id="84620-207">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="84620-208">Dans l’exemple ci-dessous, la première commande convertit la chaîne de mot de passe ```passphrase123456789``` en une chaîne sécurisée et assigne la chaîne sécurisée à la variable nommée ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="84620-208">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="84620-209">La deuxième commande définit la chaîne sécurise dans ```$Passphrase``` en tant que mot de passe pour le chiffrement des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="84620-209">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="84620-210">Conservez les informations de phrase secrète en lieu sûr après les avoir définies.</span><span class="sxs-lookup"><span data-stu-id="84620-210">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="84620-211">Vous ne pourrez pas restaurer les données à partir d’Azure sans ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="84620-211">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="84620-212">À ce stade, vous devez avoir apporté toutes les modifications requises à l’objet ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="84620-212">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="84620-213">Pensez à valider les modifications.</span><span class="sxs-lookup"><span data-stu-id="84620-213">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="84620-214">Protection des données dans Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="84620-214">Protect data to Azure Backup</span></span>
<span data-ttu-id="84620-215">Dans cette section, vous allez ajouter un serveur de production à DPM, puis protéger les données sur le stockage DPM local, et enfin dans Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="84620-215">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="84620-216">Dans les exemples, nous vous montrerons comment sauvegarder des fichiers et des dossiers.</span><span class="sxs-lookup"><span data-stu-id="84620-216">In the examples we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="84620-217">La logique peut facilement être étendue pour sauvegarder toute source de données DPM prise en charge.</span><span class="sxs-lookup"><span data-stu-id="84620-217">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="84620-218">Toutes vos sauvegardes DPM sont régies par un groupe de protection constitué de quatre parties :</span><span class="sxs-lookup"><span data-stu-id="84620-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="84620-219">**Membres du groupe** est une liste de tous les objets pouvant être protégés (également appelés *Sources de données* dans DPM) que vous souhaitez protéger dans le même groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-219">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="84620-220">Par exemple, vous pouvez protéger les machines virtuelles de production dans un groupe de production et les bases de données SQL Server dans un autre groupe de protection, car leurs exigences de sauvegarde peuvent être différentes.</span><span class="sxs-lookup"><span data-stu-id="84620-220">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="84620-221">Avant de pouvoir sauvegarder une source de données sur un serveur de production, vous devez vérifier que l'agent DPM est installé sur le serveur de production et géré par DPM.</span><span class="sxs-lookup"><span data-stu-id="84620-221">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="84620-222">Suivez les étapes d’ [installation de l'agent DPM](https://technet.microsoft.com/library/bb870935.aspx) et de liaison de celui-ci au serveur DPM approprié.</span><span class="sxs-lookup"><span data-stu-id="84620-222">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="84620-223">**Méthode de protection des données** spécifie les emplacements de sauvegarde cibles (bande, disque ou cloud).</span><span class="sxs-lookup"><span data-stu-id="84620-223">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="84620-224">Dans notre exemple, nous protégerons les données sur le disque local et dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="84620-224">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="84620-225">Une **planification de sauvegarde** qui spécifie le moment où les sauvegardes doivent être effectuées et la fréquence de synchronisation des données entre le serveur DPM et le serveur de production.</span><span class="sxs-lookup"><span data-stu-id="84620-225">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="84620-226">Une **planification de rétention** qui spécifie la durée de rétention des points de récupération dans Azure.</span><span class="sxs-lookup"><span data-stu-id="84620-226">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="84620-227">Création d’un groupe de protection</span><span class="sxs-lookup"><span data-stu-id="84620-227">Creating a protection group</span></span>
<span data-ttu-id="84620-228">Commençons par créer un groupe de protection à l’aide de l’applet de commande [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="84620-228">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="84620-229">Celle-ci crée un groupe de protection nommé *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="84620-229">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="84620-230">Un groupe de protection existant peut également être modifié ultérieurement pour ajouter la sauvegarde vers le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="84620-230">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="84620-231">Toutefois, pour apporter des modifications au groupe de protection (nouveau ou existant), nous avons besoin d’obtenir un objet *modifiable* à l'aide de l’applet de commande [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="84620-231">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="84620-232">Ajout de membres au groupe de protection</span><span class="sxs-lookup"><span data-stu-id="84620-232">Adding group members to the Protection Group</span></span>
<span data-ttu-id="84620-233">Chaque agent DPM connaît la liste des sources de données sur le serveur sur lequel il est installé.</span><span class="sxs-lookup"><span data-stu-id="84620-233">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="84620-234">Pour ajouter une source de données au groupe de Protection, l'agent DPM doit renvoyer tout d'abord une liste des sources de données au serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="84620-234">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="84620-235">Une ou plusieurs sources de données sont sélectionnées, puis ajoutées au groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-235">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="84620-236">Les étapes PowerShell requises sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="84620-236">The PowerShell steps needed to get achieve this are:</span></span>

1. <span data-ttu-id="84620-237">Extrayez une liste de tous les serveurs gérés par DPM via l'agent DPM.</span><span class="sxs-lookup"><span data-stu-id="84620-237">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="84620-238">Choisissez un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="84620-238">Choose a specific server.</span></span>
3. <span data-ttu-id="84620-239">Extrayez une liste de toutes les sources de données sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="84620-239">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="84620-240">Choisissez une ou plusieurs sources de données et ajoutez-les au groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-240">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="84620-241">Vous pouvez obtenir la liste des serveurs sur lesquels l’agent DPM est installé et géré par le serveur DPM à l'aide de l’applet de commande [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="84620-241">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="84620-242">Dans cet exemple, nous allons filtrer et configurer uniquement PS avec une sauvegarde nommée *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="84620-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="84620-243">Extrayez à présent la liste des sources de données sur ```$server``` à l’aide de l’applet de commande [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="84620-243">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="84620-244">Dans cet exemple, nous filtrons le volume *D:\* que nous voulons configurer pour une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="84620-244">In this example we are filtering for the volume *D:\* which we want to configure for backup.</span></span> <span data-ttu-id="84620-245">Cette source de données est ensuite ajoutée au groupe de protection à l’aide de l’applet de commande [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="84620-245">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="84620-246">Veillez à utiliser l’objet de groupe de protection *modifiable* ```$MPG``` pour effectuer les ajouts.</span><span class="sxs-lookup"><span data-stu-id="84620-246">Remember to use the *modifable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="84620-247">Répétez cette étape autant de fois que nécessaire, jusqu'à ce que vous ayez ajouté toutes les sources de données choisies au groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-247">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="84620-248">Vous pouvez également commencer avec une seule source de données, puis terminer le flux de travail de création du groupe de protection, avant d’ajouter ultérieurement d’autres sources de données au groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-248">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="84620-249">Sélection de la méthode de protection des données</span><span class="sxs-lookup"><span data-stu-id="84620-249">Selecting the data protection method</span></span>
<span data-ttu-id="84620-250">Une fois que les sources de données ont été ajoutées au groupe de protection, l'étape suivante consiste à spécifier la méthode de protection à l'aide de l’applet de commande [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="84620-250">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="84620-251">Dans cet exemple, le groupe de protection est configuré pour une sauvegarde sur le disque local et dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="84620-251">In this example, the Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="84620-252">Vous devez également spécifier la source de données que vous souhaitez protéger sur le cloud à l’aide de l’applet de commande [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) avec l’indicateur Online.</span><span class="sxs-lookup"><span data-stu-id="84620-252">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="84620-253">Définition de la plage de rétention</span><span class="sxs-lookup"><span data-stu-id="84620-253">Setting the retention range</span></span>
<span data-ttu-id="84620-254">Définissez la rétention pour les points de sauvegarde à l'aide de l’applet de commande [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="84620-254">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="84620-255">Bien que cela puisse sembler étrange de définir la rétention avant la planification de sauvegarde, l’utilisation de l’applet de commande ```Set-DPMPolicyObjective``` définit automatiquement une planification de sauvegarde par défaut qui peut ensuite être modifiée.</span><span class="sxs-lookup"><span data-stu-id="84620-255">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="84620-256">Il est toujours possible de définir la planification de sauvegarde avant la stratégie de rétention.</span><span class="sxs-lookup"><span data-stu-id="84620-256">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="84620-257">Dans l'exemple ci-dessous, l'applet de commande définit les paramètres de rétention pour les sauvegardes sur disque.</span><span class="sxs-lookup"><span data-stu-id="84620-257">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="84620-258">Cela permet de conserver les sauvegardes pendant 10 jours, et de synchroniser les données toutes les 6 heures entre le serveur de production et le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="84620-258">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="84620-259">```SynchronizationFrequencyMinutes``` ne définit pas la fréquence à laquelle un point de sauvegarde est créé, mais la fréquence de copie des données sur le serveur DPM. Cela évite que les sauvegardes soient trop volumineuses.</span><span class="sxs-lookup"><span data-stu-id="84620-259">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="84620-260">Pour les sauvegardes vers Azure (qui sont désignées par « sauvegardes en ligne » dans DPM), les plages de rétention peuvent être configurées pour [une rétention à long terme à l'aide d'un schéma GFS (Grandfather-Father-Son)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="84620-260">For backups going to Azure (DPM refers to these as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="84620-261">Autrement dit, vous pouvez définir une stratégie de rétention combinée incluant des stratégies de rétention quotidiennes, hebdomadaires, mensuelles et annuelles.</span><span class="sxs-lookup"><span data-stu-id="84620-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="84620-262">Dans cet exemple, nous créons un tableau qui représente le schéma de rétention complexe souhaité, puis configurons la plage de rétention à l'aide de l’applet de commande [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="84620-262">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="84620-263">Définition de la planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="84620-263">Set the backup schedule</span></span>
<span data-ttu-id="84620-264">DPM définit automatiquement la planification de sauvegarde par défaut si vous spécifiez l'objectif de protection à l'aide de l’applet de commande ```Set-DPMPolicyObjective``` .</span><span class="sxs-lookup"><span data-stu-id="84620-264">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="84620-265">Pour modifier les planifications par défaut, utilisez l’applet de commande [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) suivie de l’applet de commande [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="84620-265">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="84620-266">Dans l'exemple ci-dessus, ```$onlineSch``` est un tableau avec quatre éléments qui contient la planification de protection en ligne existante pour le groupe de protection dans le schéma GFS :</span><span class="sxs-lookup"><span data-stu-id="84620-266">In the example above, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="84620-267">```$onlineSch[0]``` contient la planification quotidienne.</span><span class="sxs-lookup"><span data-stu-id="84620-267">```$onlineSch[0]``` will contain the daily schedule</span></span>
2. <span data-ttu-id="84620-268">```$onlineSch[1]``` contient la planification hebdomadaire.</span><span class="sxs-lookup"><span data-stu-id="84620-268">```$onlineSch[1]``` will contain the weekly schedule</span></span>
3. <span data-ttu-id="84620-269">```$onlineSch[2]``` contient la planification mensuelle.</span><span class="sxs-lookup"><span data-stu-id="84620-269">```$onlineSch[2]``` will contain the monthly schedule</span></span>
4. <span data-ttu-id="84620-270">```$onlineSch[3]``` contient la planification annuelle.</span><span class="sxs-lookup"><span data-stu-id="84620-270">```$onlineSch[3]``` will contain the yearly schedule</span></span>

<span data-ttu-id="84620-271">Par conséquent, si vous devez modifier la planification hebdomadaire, vous devez faire référence à ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="84620-271">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="84620-272">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="84620-272">Initial backup</span></span>
<span data-ttu-id="84620-273">Lorsque vous sauvegardez la source de données pour la première fois, DPM doit créer un réplica initial qui crée une copie de la source de données à protéger sur le volume du réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="84620-273">When backing up a datasource for the first time, DPM needs to create an initial replica which will create a copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="84620-274">Cette activité peut être planifiée pour une heure spécifique, ou peut être déclenchée manuellement à l’aide de l’applet de commande [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) avec le paramètre ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="84620-274">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="84620-275">Modification de la taille de réplica DPM et volume du point de récupération</span><span class="sxs-lookup"><span data-stu-id="84620-275">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="84620-276">Vous pouvez également modifier la taille du volume de réplica DPM, ainsi que du volume de clichés instantanés à l’aide de l’applet de commande [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) comme dans l’exemple ci-dessous : Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="84620-276">You can also change the size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="84620-277">Validation des modifications dans le groupe de protection</span><span class="sxs-lookup"><span data-stu-id="84620-277">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="84620-278">Pour terminer, les modifications doivent être validées avant que DPM puisse effectuer la sauvegarde conformément à la nouvelle configuration du groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="84620-278">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="84620-279">Pour ce faire, utilisez l’applet de commande [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="84620-279">This is done using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="84620-280">Affichage des points de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="84620-280">View the backup points</span></span>
<span data-ttu-id="84620-281">Vous pouvez utiliser l’applet de commande [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) pour obtenir la liste de tous les points de récupération d’une source de données.</span><span class="sxs-lookup"><span data-stu-id="84620-281">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="84620-282">Dans cet exemple, nous allons :</span><span class="sxs-lookup"><span data-stu-id="84620-282">In this example, we will:</span></span>

* <span data-ttu-id="84620-283">extraire tous les groupes de protection sur le serveur DPM pour les stocker dans un tableau ```$PG```</span><span class="sxs-lookup"><span data-stu-id="84620-283">fetch all the PGs on the DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="84620-284">obtenir les sources de données correspondant à ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="84620-284">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="84620-285">obtenir tous les points de récupération pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="84620-285">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="84620-286">Restaurer des données protégées sur Azure</span><span class="sxs-lookup"><span data-stu-id="84620-286">Restore data protected on Azure</span></span>
<span data-ttu-id="84620-287">La restauration des données est une combinaison d'un objet ```RecoverableItem``` et d’un objet ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="84620-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="84620-288">Dans la section précédente, nous avions une liste des points de sauvegarde pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="84620-288">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="84620-289">Dans l'exemple ci-dessous, nous démontrons comment restaurer une machine virtuelle Hyper-V à partir de Sauvegarde Azure en combinant les points de sauvegarde avec la cible pour la récupération.</span><span class="sxs-lookup"><span data-stu-id="84620-289">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="84620-290">notamment :</span><span class="sxs-lookup"><span data-stu-id="84620-290">This includes:</span></span>

* <span data-ttu-id="84620-291">Création d’une option de récupération à l’aide de l’applet de commande [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592).</span><span class="sxs-lookup"><span data-stu-id="84620-291">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="84620-292">Extraction du tableau de points de sauvegarde à l'aide de l’applet de commande ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="84620-292">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="84620-293">Choix d’un point de sauvegarde à partir duquel effectuer la restauration.</span><span class="sxs-lookup"><span data-stu-id="84620-293">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="84620-294">Les commandes peuvent facilement être étendues à n'importe quel type de source de données.</span><span class="sxs-lookup"><span data-stu-id="84620-294">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84620-295">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84620-295">Next steps</span></span>
* <span data-ttu-id="84620-296">Pour en savoir plus sur Sauvegarde Azure pour DPM, consultez [Présentation des sauvegardes DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="84620-296">For more information about Azure Backup for DPM see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
