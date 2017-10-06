---
title: "Sauvegarde Azure : Tooback utiliser PowerShell les charges de travail DPM | Documents Microsoft"
description: "Découvrez comment toodeploy et gérer la sauvegarde de Azure pour Data Protection Manager (DPM) à l’aide de PowerShell"
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
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="cc020-103">Déployer et gérer la sauvegarde tooAzure pour les serveurs Data Protection Manager (DPM) à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc020-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc020-104">ARM</span><span class="sxs-lookup"><span data-stu-id="cc020-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="cc020-105">Classique</span><span class="sxs-lookup"><span data-stu-id="cc020-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="cc020-106">Cet article explique comment toouse PowerShell tooback configurer et récupérer des données DPM à partir d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="cc020-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="cc020-107">Microsoft recommande d’utiliser des coffres Recovery Services pour tous les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="cc020-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="cc020-108">Si vous êtes un nouvel utilisateur de sauvegarde Azure, utilisez l’article hello, [déployer et gérer des tooAzure de données de Data Protection Manager à l’aide de PowerShell](backup-dpm-automation.md), de sorte que vous stockez vos données dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="cc020-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc020-109">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="cc020-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="cc020-110">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="cc020-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="cc020-111">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="cc020-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="cc020-112">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc020-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="cc020-113">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="cc020-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="cc020-114">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="cc020-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="cc020-115">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="cc020-116">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="cc020-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="cc020-117">Configurer l’environnement PowerShell de hello</span><span class="sxs-lookup"><span data-stu-id="cc020-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="cc020-118">Avant de pouvoir utiliser des sauvegardes de toomanage PowerShell à partir de Data Protection Manager tooAzure, vous devez toohave hello droite environnement PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cc020-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="cc020-119">Au début de hello de session de PowerShell hello, assurez-vous que vous exécutez hello suivant modules bon de commande tooimport hello et vous permettre d’applets de commande DPM toocorrectly référence hello :</span><span class="sxs-lookup"><span data-stu-id="cc020-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="cc020-120">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="cc020-120">Setup and Registration</span></span>
<span data-ttu-id="cc020-121">toobegin :</span><span class="sxs-lookup"><span data-stu-id="cc020-121">toobegin:</span></span>

1. <span data-ttu-id="cc020-122">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="cc020-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="cc020-123">Activer les applets de commande de sauvegarde Azure hello en basculant trop*AzureResourceManager* mode à l’aide de hello **Switch-AzureMode** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="cc020-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="cc020-124">Hello suivant le programme d’installation et tâches d’enregistrement peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="cc020-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="cc020-125">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="cc020-125">Create a backup vault</span></span>
* <span data-ttu-id="cc020-126">Installation de l’agent Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="cc020-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="cc020-127">L’inscription auprès de hello service Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cc020-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="cc020-128">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="cc020-128">Networking settings</span></span>
* <span data-ttu-id="cc020-129">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="cc020-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="cc020-130">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="cc020-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="cc020-131">Pour les clients à l’aide de la sauvegarde Azure pour hello première fois, vous devez tooregister hello Azure Backup fournisseur toobe utilisé avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="cc020-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="cc020-132">Cela est possible en exécutant hello de commande suivante : Register-AzureProvider - ProviderNamespace « Microsoft.Backup »</span><span class="sxs-lookup"><span data-stu-id="cc020-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="cc020-133">Vous pouvez créer un coffre de sauvegarde à l’aide de hello **New-AzureRMBackupVault** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="cc020-134">coffre de sauvegarde Hello est une ressource ARM, par conséquent, vous devez tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="cc020-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="cc020-135">Dans une console Azure PowerShell avec élévation de privilèges, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="cc020-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="cc020-136">Vous pouvez obtenir une liste de tous les coffres de sauvegarde hello dans un abonnement donné à l’aide de hello **Get-AzureRMBackupVault** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="cc020-137">Agent de sauvegarde Azure hello lors de l’installation sur un serveur DPM</span><span class="sxs-lookup"><span data-stu-id="cc020-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="cc020-138">Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="cc020-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="cc020-139">Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="cc020-140">Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="cc020-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="cc020-141">tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges **sur le serveur DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="cc020-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="cc020-142">Cette commande installe l’agent de hello avec toutes les options par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="cc020-143">installation de Hello prend quelques minutes en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="cc020-144">Si vous ne spécifiez pas hello */nu* hello d’option **mise à jour Windows** fenêtre s’ouvre à fin hello de toocheck d’installation hello pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="cc020-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="cc020-145">l’agent de Hello s’affichent dans la liste hello des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="cc020-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="cc020-146">liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="cc020-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="cc020-148">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="cc020-148">Installation options</span></span>
<span data-ttu-id="cc020-149">toosee tous hello options disponibles via hello de ligne de commande, utilisez les hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cc020-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="cc020-150">les options disponibles Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc020-150">hello available options include:</span></span>

| <span data-ttu-id="cc020-151">Option</span><span class="sxs-lookup"><span data-stu-id="cc020-151">Option</span></span> | <span data-ttu-id="cc020-152">Détails</span><span class="sxs-lookup"><span data-stu-id="cc020-152">Details</span></span> | <span data-ttu-id="cc020-153">Default</span><span class="sxs-lookup"><span data-stu-id="cc020-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc020-154">/q</span><span class="sxs-lookup"><span data-stu-id="cc020-154">/q</span></span> |<span data-ttu-id="cc020-155">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="cc020-155">Quiet installation</span></span> |- |
| <span data-ttu-id="cc020-156">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="cc020-156">/p:"location"</span></span> |<span data-ttu-id="cc020-157">Chemin d’accès toohello dossier d’installation de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="cc020-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="cc020-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="cc020-159">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="cc020-159">/s:"location"</span></span> |<span data-ttu-id="cc020-160">Chemin d’accès toohello dossier de cache de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="cc020-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="cc020-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="cc020-162">/m</span><span class="sxs-lookup"><span data-stu-id="cc020-162">/m</span></span> |<span data-ttu-id="cc020-163">Acceptation de la mise à jour tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="cc020-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="cc020-164">/nu</span><span class="sxs-lookup"><span data-stu-id="cc020-164">/nu</span></span> |<span data-ttu-id="cc020-165">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="cc020-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="cc020-166">/d</span><span class="sxs-lookup"><span data-stu-id="cc020-166">/d</span></span> |<span data-ttu-id="cc020-167">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="cc020-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="cc020-168">/ph</span><span class="sxs-lookup"><span data-stu-id="cc020-168">/ph</span></span> |<span data-ttu-id="cc020-169">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="cc020-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="cc020-170">/po</span><span class="sxs-lookup"><span data-stu-id="cc020-170">/po</span></span> |<span data-ttu-id="cc020-171">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="cc020-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="cc020-172">/pu</span><span class="sxs-lookup"><span data-stu-id="cc020-172">/pu</span></span> |<span data-ttu-id="cc020-173">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="cc020-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="cc020-174">/pw</span><span class="sxs-lookup"><span data-stu-id="cc020-174">/pw</span></span> |<span data-ttu-id="cc020-175">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="cc020-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="cc020-176">L’inscription auprès de hello service Azure Backup</span><span class="sxs-lookup"><span data-stu-id="cc020-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="cc020-177">Avant de pouvoir inscrire avec hello service Azure Backup, vous devez tooensure que hello [conditions préalables](backup-azure-dpm-introduction.md) sont remplies.</span><span class="sxs-lookup"><span data-stu-id="cc020-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="cc020-178">Vous devez respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc020-178">You must:</span></span>

* <span data-ttu-id="cc020-179">Avoir un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="cc020-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="cc020-180">Disposer d’un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="cc020-180">Have a backup vault</span></span>

<span data-ttu-id="cc020-181">informations d’identification d’archivage toodownload hello, exécutez hello **Get-AzureBackupVaultCredentials** applet de commande dans une console Azure PowerShell et le magasin dans un emplacement pratique comme * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="cc020-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="cc020-182">L’enregistrement machine hello avec le coffre de hello est effectuée à l’aide de hello [DPMCloudRegistration de début](https://technet.microsoft.com/library/jj612787) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="cc020-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="cc020-183">Cela inscrira hello nommé « TestingServer » le serveur DPM avec le coffre Microsoft Azure à l’aide de hello spécifié d’informations d’identification de coffre.</span><span class="sxs-lookup"><span data-stu-id="cc020-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc020-184">N’utilisez pas le fichier d’informations d’identification de chemins d’accès relatifs toospecify hello coffre.</span><span class="sxs-lookup"><span data-stu-id="cc020-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="cc020-185">Vous devez fournir un chemin d’accès absolu comme une applet de commande toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="cc020-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="cc020-186">Paramètres de la configuration initiale</span><span class="sxs-lookup"><span data-stu-id="cc020-186">Initial configuration settings</span></span>
<span data-ttu-id="cc020-187">Une fois hello serveur DPM est enregistré avec le coffre de sauvegarde Azure hello, il démarre avec les paramètres par défaut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="cc020-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="cc020-188">Ces paramètres d’abonnement incluent la mise en réseau, le chiffrement et hello zone de transit.</span><span class="sxs-lookup"><span data-stu-id="cc020-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="cc020-189">toobegin modification hello abonnement paramètres que vous devez toofirst obtenez un descripteur sur paramètres hello existants (par défaut) à l’aide de hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="cc020-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="cc020-190">Toutes les modifications sont apportées toothis local PowerShell objet ```$setting``` puis complet de l’objet hello est validée tooDPM et Azure Backup toosave les à l’aide de hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="cc020-191">Vous devez toouse hello ```–Commit``` tooensure indicateur qui hello les modifications sont conservées.</span><span class="sxs-lookup"><span data-stu-id="cc020-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="cc020-192">paramètres de Hello ne seront pas appliqués et utilisés par Azure Backup, sauf si la validation.</span><span class="sxs-lookup"><span data-stu-id="cc020-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="cc020-193">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="cc020-193">Networking</span></span>
<span data-ttu-id="cc020-194">Si la connexion de hello de hello DPM machine toohello service Azure Backup sur hello internet est via un serveur proxy, paramètres hello du serveur proxy doivent être fournis pour les sauvegardes toosucceed.</span><span class="sxs-lookup"><span data-stu-id="cc020-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="cc020-195">Il incombe à l’aide de hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` et hello ```ProxyPassword``` paramètres avec hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="cc020-196">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="cc020-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="cc020-197">L’utilisation de la bande passante peut également être contrôlée avec les options de ```-WorkHourBandwidth``` et ```-NonWorkHourBandwidth``` pour un ensemble donné de jours de semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="cc020-198">Dans cet exemple, nous ne fixons aucune limitation.</span><span class="sxs-lookup"><span data-stu-id="cc020-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="cc020-199">Configuration de la zone de transit hello</span><span class="sxs-lookup"><span data-stu-id="cc020-199">Configuring hello staging Area</span></span>
<span data-ttu-id="cc020-200">Bonjour Azure Backup agent en cours d’exécution sur le serveur DPM hello a besoin de stockage temporaire pour les données restaurées à partir du cloud de hello (zone de transit local).</span><span class="sxs-lookup"><span data-stu-id="cc020-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="cc020-201">Configurer la zone de transit à l’aide de hello hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande et hello ```-StagingAreaPath``` paramètre.</span><span class="sxs-lookup"><span data-stu-id="cc020-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="cc020-202">Dans l’exemple hello ci-dessus, la zone de transit hello sera définie trop*C:\StagingArea* dans l’objet de PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="cc020-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="cc020-203">Vérifiez que hello le dossier spécifié existe déjà, sinon la validation finale de paramètres d’abonnement hello hello échouera.</span><span class="sxs-lookup"><span data-stu-id="cc020-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="cc020-204">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="cc020-204">Encryption settings</span></span>
<span data-ttu-id="cc020-205">tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="cc020-206">phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="cc020-207">Il est important tookeep cette sécurisé des informations et sécuriser une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="cc020-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="cc020-208">Dans l’exemple hello ci-dessous, commande premier hello convertit la chaîne de hello ```passphrase123456789``` tooa sécurisée chaîne et lui affecte hello sécurisé toohello variable chaîne nommée ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="cc020-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="cc020-209">commande deuxième Hello définit la chaîne sécurisée de hello ```$Passphrase``` comme mot de passe hello pour le chiffrement des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="cc020-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="cc020-210">Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="cc020-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="cc020-211">Vous ne serez pas toorestore en mesure des données à partir d’Azure sans cette phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="cc020-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="cc020-212">À ce stade, vous aurait dû effectuer tous les toohello de modifications hello requis ```$setting``` objet.</span><span class="sxs-lookup"><span data-stu-id="cc020-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="cc020-213">N’oubliez pas de modifications de hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="cc020-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="cc020-214">Protéger les données tooAzure sauvegarde</span><span class="sxs-lookup"><span data-stu-id="cc020-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="cc020-215">Dans cette section, vous ajoutez un tooDPM de serveur de production et puis protégez hello toolocal DPM stockage et des données puis tooAzure sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="cc020-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="cc020-216">Dans les exemples hello, nous allons vous montrer comment tooback des fichiers et des dossiers.</span><span class="sxs-lookup"><span data-stu-id="cc020-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="cc020-217">Hello logique peut facilement être étendu toobackup n’importe quelle source de données pris en charge de DPM.</span><span class="sxs-lookup"><span data-stu-id="cc020-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="cc020-218">Toutes vos sauvegardes DPM sont régies par un groupe de protection constitué de quatre parties :</span><span class="sxs-lookup"><span data-stu-id="cc020-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="cc020-219">**Membres du groupe** est une liste de tous les objets protégeables hello (également appelé *sources de données* dans DPM) que vous souhaitez tooprotect Bonjour même groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="cc020-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="cc020-220">Par exemple, vous voudrez tooprotect production machines virtuelles dans un groupe de protection et de bases de données SQL Server dans un autre groupe de protection d’avoir différentes exigences de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="cc020-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="cc020-221">Avant que vous puissiez sauvegarder toute source de données sur un serveur de production, vous devez toomake hello que l’Agent DPM est installé sur le serveur de hello et est géré par DPM.</span><span class="sxs-lookup"><span data-stu-id="cc020-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="cc020-222">Suivez les étapes de hello pour [installation hello Agent DPM](https://technet.microsoft.com/library/bb870935.aspx) et en le liant toohello approprié du serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="cc020-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="cc020-223">**Méthode de protection des données** spécifie hello cible emplacements de sauvegarde - bande, disque et cloud.</span><span class="sxs-lookup"><span data-stu-id="cc020-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="cc020-224">Dans notre exemple, nous protégera données toohello local disque et toohello dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="cc020-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="cc020-225">A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prise et la fréquence à laquelle hello données doivent être synchronisées entre hello serveur DPM et le serveur de production hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="cc020-226">A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cc020-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="cc020-227">Création d’un groupe de protection</span><span class="sxs-lookup"><span data-stu-id="cc020-227">Creating a protection group</span></span>
<span data-ttu-id="cc020-228">Commencez par créer un nouveau groupe de Protection à l’aide de hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="cc020-229">Hello ci-dessus crée un groupe de Protection nommée *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="cc020-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="cc020-230">Ultérieures tooadd toohello à sauvegarde Azure cloud peut également être modifié à un groupe de protection existant.</span><span class="sxs-lookup"><span data-stu-id="cc020-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="cc020-231">Toutefois, toomake toutes les modifications toohello - groupe de Protection nouveau ou existant - nous avons besoin d’un handle de tooget sur un *modifiable* objet à l’aide de hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="cc020-232">Ajout de membres de groupe toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="cc020-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="cc020-233">Chaque Agent DPM sait liste hello de sources de données sur le serveur hello lequel il est installé.</span><span class="sxs-lookup"><span data-stu-id="cc020-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="cc020-234">tooadd un toohello de source de données groupe de Protection, hello toofirst des besoins de l’Agent DPM envoyer une liste de serveur DPM toohello arrière hello sources de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="cc020-235">Une ou plusieurs sources de données sont sélectionnées et ajoutées toohello groupe de Protection.</span><span class="sxs-lookup"><span data-stu-id="cc020-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="cc020-236">Hello PowerShell étapes nécessaires tooget atteindre sont :</span><span class="sxs-lookup"><span data-stu-id="cc020-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="cc020-237">Extraire une liste de tous les serveurs gérés par DPM via hello Agent DPM.</span><span class="sxs-lookup"><span data-stu-id="cc020-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="cc020-238">Choisissez un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="cc020-238">Choose a specific server.</span></span>
3. <span data-ttu-id="cc020-239">Extraire une liste de toutes les sources de données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="cc020-240">Choisissez une ou plusieurs sources de données et de les ajouter toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="cc020-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="cc020-241">Hello la liste des serveurs sur le hello Agent DPM est installé et est géré par le serveur DPM de hello est acquis par hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="cc020-242">Dans cet exemple, nous allons filtrer et configurer uniquement PS avec une sauvegarde nommée *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="cc020-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="cc020-243">Liste hello de sources de données d’extraire maintenant sur ```$server``` à l’aide de hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="cc020-244">Dans cet exemple, nous allons filtrage pour le volume de hello * D:\* que nous souhaitons tooconfigure pour la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="cc020-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="cc020-245">Cette source de données est ensuite ajouté toohello groupe de Protection à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="cc020-246">N’oubliez pas de toouse hello *modifable* objet du groupe de protection ```$MPG``` ajouts de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="cc020-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="cc020-247">Répétez cette étape autant de fois en fonction des besoins, jusqu'à ce que vous avez ajouté tous les hello choisi le groupe de protection toohello de sources de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="cc020-248">Vous pouvez également commencer par qu’une seule source de données et flux de travail hello complète pour la création de hello groupe de Protection et à un moment ultérieur ajouter plusieurs sources de données toohello groupe de Protection.</span><span class="sxs-lookup"><span data-stu-id="cc020-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="cc020-249">Méthode de protection des données en sélectionnant hello</span><span class="sxs-lookup"><span data-stu-id="cc020-249">Selecting hello data protection method</span></span>
<span data-ttu-id="cc020-250">Après ont ajouté les sources de données hello toohello groupe de Protection, hello prochaine étape consiste à l’aide de hello la méthode de protection hello toospecify [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="cc020-251">Dans cet exemple, hello groupe de Protection sera installé pour le disque local et de sauvegarde sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="cc020-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="cc020-252">Vous devez également datasource de hello toospecify que vous souhaitez toocloud tooprotect à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) applet de commande avec l’indicateur en ligne-.</span><span class="sxs-lookup"><span data-stu-id="cc020-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="cc020-253">Définition de la plage de rétention hello</span><span class="sxs-lookup"><span data-stu-id="cc020-253">Setting hello retention range</span></span>
<span data-ttu-id="cc020-254">Définir la rétention hello pour les points de sauvegarde hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="cc020-255">Il peut sembler rétention de hello impair tooset avant de la planification de sauvegarde hello a été définie, à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande définit automatiquement une planification de sauvegarde par défaut qui peut ensuite être modifiée.</span><span class="sxs-lookup"><span data-stu-id="cc020-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="cc020-256">Il est toujours possible tooset planification de sauvegarde hello en premier et hello après la période de rétention.</span><span class="sxs-lookup"><span data-stu-id="cc020-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="cc020-257">Dans l’exemple hello ci-dessous, hello définit des paramètres de rétention hello pour les sauvegardes sur disque.</span><span class="sxs-lookup"><span data-stu-id="cc020-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="cc020-258">Cela conservera sauvegardes pendant 10 jours, les données de synchronisation toutes les 6 heures entre le serveur de production hello et le serveur DPM hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="cc020-259">Hello ```SynchronizationFrequencyMinutes``` ne définit pas la fréquence à laquelle un point de sauvegarde est créé, mais comment souvent les données sont copiées toohello le serveur DPM ; ainsi, les sauvegardes ne deviennent trop volumineuses.</span><span class="sxs-lookup"><span data-stu-id="cc020-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="cc020-260">Pour les sauvegardes tooAzure (DPM fait référence toothese en tant que les sauvegardes en ligne) des plages de rétention hello peuvent être configurées pour [à long terme rétention à l’aide d’un schéma grand-père-Father-Son (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="cc020-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="cc020-261">Autrement dit, vous pouvez définir une stratégie de rétention combinée incluant des stratégies de rétention quotidiennes, hebdomadaires, mensuelles et annuelles.</span><span class="sxs-lookup"><span data-stu-id="cc020-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="cc020-262">Dans cet exemple, nous créer un tableau représentant le schéma de rétention complexes hello que nous souhaitons, puis configurez la durée de rétention hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="cc020-263">Planification de sauvegarde hello ensemble</span><span class="sxs-lookup"><span data-stu-id="cc020-263">Set hello backup schedule</span></span>
<span data-ttu-id="cc020-264">DPM définit automatiquement une planification de sauvegarde par défaut si vous spécifiez l’objectif de protection hello à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="cc020-265">les planifications par défaut toochange hello, utilisez hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) applet de commande suivie hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="cc020-266">Dans l’exemple hello ci-dessus, ```$onlineSch``` est un tableau qui contient la planification de protection en ligne existante hello pour hello groupe de Protection dans le schéma GFS hello avec quatre éléments :</span><span class="sxs-lookup"><span data-stu-id="cc020-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="cc020-267">```$onlineSch[0]```contiendra une planification quotidienne de hello</span><span class="sxs-lookup"><span data-stu-id="cc020-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="cc020-268">```$onlineSch[1]```contiendra hebdomadaire hello</span><span class="sxs-lookup"><span data-stu-id="cc020-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="cc020-269">```$onlineSch[2]```contiendra une planification mensuelle de hello</span><span class="sxs-lookup"><span data-stu-id="cc020-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="cc020-270">```$onlineSch[3]```contiendra la planification annuelle de hello</span><span class="sxs-lookup"><span data-stu-id="cc020-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="cc020-271">Si vous avez besoin de la planification hebdomadaire toomodify hello, vous devez toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="cc020-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="cc020-272">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="cc020-272">Initial backup</span></span>
<span data-ttu-id="cc020-273">Lorsque vous sauvegardez un datasource de hello première fois, DPM doit toocreate un réplica initial qui crée une copie de hello toobe de source de données protégée sur le volume du réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="cc020-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="cc020-274">Cette activité peuvent être planifiée pour une durée spécifique, ou peut être déclenchée manuellement, à l’aide de hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) applet de commande avec le paramètre hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="cc020-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="cc020-275">Modification de la taille de hello du réplica DPM et le volume des points de récupération</span><span class="sxs-lookup"><span data-stu-id="cc020-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="cc020-276">Vous pouvez également modifier la taille de hello du volume du réplica DPM, ainsi que l’aide de volume Shadow Copy [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) applet de commande comme hello exemple ci-dessous : $DS Get-DatasourceDiskAllocation - source de données Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuel - ReplicaArea (2 Go) - ShadowCopyArea (2 Go)</span><span class="sxs-lookup"><span data-stu-id="cc020-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="cc020-277">Validation hello change toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="cc020-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="cc020-278">Enfin, les modifications de hello doivent toobe validée que DPM puisse être sauvegarde hello par la nouvelle configuration de groupe de Protection hello.</span><span class="sxs-lookup"><span data-stu-id="cc020-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="cc020-279">Cette opération est effectuée à l’aide de hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="cc020-280">Afficher des points de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="cc020-280">View hello backup points</span></span>
<span data-ttu-id="cc020-281">Vous pouvez utiliser hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget de l’applet de commande une liste de tous les points de récupération pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="cc020-282">Dans cet exemple, nous allons :</span><span class="sxs-lookup"><span data-stu-id="cc020-282">In this example, we will:</span></span>

* <span data-ttu-id="cc020-283">extraction de toutes les pages hello sur le serveur DPM hello qui sera stocké dans un tableau```$PG```</span><span class="sxs-lookup"><span data-stu-id="cc020-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="cc020-284">obtenir toohello correspondante de sources de données hello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="cc020-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="cc020-285">obtenir tous les points de récupération hello pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="cc020-286">Restaurer des données protégées sur Azure</span><span class="sxs-lookup"><span data-stu-id="cc020-286">Restore data protected on Azure</span></span>
<span data-ttu-id="cc020-287">La restauration des données est une combinaison d'un objet ```RecoverableItem``` et d’un objet ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="cc020-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="cc020-288">Dans la section précédente de hello, nous avons obtenu une liste de points de sauvegarde hello pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="cc020-289">Dans l’exemple hello ci-dessous, nous allons montrer comment la machine virtuelle de toorestore Hyper-V à partir d’Azure Backup en combinant les points de sauvegarde avec hello cibler pour la récupération.</span><span class="sxs-lookup"><span data-stu-id="cc020-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="cc020-290">notamment :</span><span class="sxs-lookup"><span data-stu-id="cc020-290">This includes:</span></span>

* <span data-ttu-id="cc020-291">Création d’une option de récupération à l’aide de hello [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="cc020-292">Tableau de hello l’extraction des points de sauvegarde à l’aide de hello ```Get-DPMRecoveryPoint``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cc020-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="cc020-293">Choix d’un toorestore de point de sauvegarde à partir de.</span><span class="sxs-lookup"><span data-stu-id="cc020-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="cc020-294">commandes Hello peuvent facilement être étendus pour n’importe quel type de source de données.</span><span class="sxs-lookup"><span data-stu-id="cc020-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc020-295">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc020-295">Next steps</span></span>
* <span data-ttu-id="cc020-296">Pour plus d’informations sur Azure Backup pour DPM, consultez [Introduction tooDPM sauvegarde](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="cc020-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
