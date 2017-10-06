---
title: aaaAzure sauvegarde - tooback utiliser PowerShell des charges de travail DPM | Documents Microsoft
description: "Découvrez comment toodeploy et gérer la sauvegarde de Azure pour Data Protection Manager (DPM) à l’aide de PowerShell"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="a24f9-103">Déployer et gérer la sauvegarde tooAzure pour les serveurs Data Protection Manager (DPM) à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a24f9-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a24f9-104">ARM</span><span class="sxs-lookup"><span data-stu-id="a24f9-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="a24f9-105">Classique</span><span class="sxs-lookup"><span data-stu-id="a24f9-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="a24f9-106">Cet article vous montre comment toouse PowerShell toosetup Azure Backup sur un serveur DPM et toomanage sauvegarde et de récupération.</span><span class="sxs-lookup"><span data-stu-id="a24f9-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="a24f9-107">Configurer l’environnement PowerShell de hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="a24f9-108">Avant de pouvoir utiliser des sauvegardes de toomanage PowerShell à partir de Data Protection Manager tooAzure, vous avez besoin d’environnement de droite hello toohave dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a24f9-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="a24f9-109">Au début de hello de session de PowerShell hello, assurez-vous que vous exécutez hello suivant modules bon de commande tooimport hello et vous permettre d’applets de commande DPM toocorrectly référence hello :</span><span class="sxs-lookup"><span data-stu-id="a24f9-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="a24f9-110">Installation et inscription</span><span class="sxs-lookup"><span data-stu-id="a24f9-110">Setup and Registration</span></span>
<span data-ttu-id="a24f9-111">toobegin :</span><span class="sxs-lookup"><span data-stu-id="a24f9-111">toobegin:</span></span>

1. <span data-ttu-id="a24f9-112">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="a24f9-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="a24f9-113">Activer les applets de commande de sauvegarde Azure hello en basculant trop*AzureResourceManager* mode à l’aide de hello **Switch-AzureMode** applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a24f9-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="a24f9-114">Hello suivant le programme d’installation et tâches d’enregistrement peuvent être automatisées avec PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a24f9-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="a24f9-115">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a24f9-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="a24f9-116">Installation de l’agent Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="a24f9-117">L’inscription auprès de hello service Azure Backup</span><span class="sxs-lookup"><span data-stu-id="a24f9-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="a24f9-118">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="a24f9-118">Networking settings</span></span>
* <span data-ttu-id="a24f9-119">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="a24f9-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="a24f9-120">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a24f9-120">Create a recovery services vault</span></span>
<span data-ttu-id="a24f9-121">Hello suit vous guide lors de la création d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="a24f9-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="a24f9-122">Un coffre Recovery Services diffère d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a24f9-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="a24f9-123">Si vous utilisez Azure Backup pour hello première fois, vous devez utiliser hello **Register-AzureRMResourceProvider** fournisseur de Service de récupération Azure hello applet de commande tooregister avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="a24f9-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="a24f9-124">Hello coffre Recovery Services est une ressource ARM, vous devez donc tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a24f9-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="a24f9-125">Vous pouvez utiliser un groupe de ressources existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="a24f9-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="a24f9-126">Lorsque vous créez un nouveau groupe de ressources, spécifiez le nom de hello et un emplacement pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="a24f9-127">Hello d’utilisation **New-AzureRmRecoveryServicesVault** toocreate de l’applet de commande un coffre.</span><span class="sxs-lookup"><span data-stu-id="a24f9-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="a24f9-128">Veillez à toospecify hello même emplacement pour le coffre hello que celui utilisé pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="a24f9-129">Spécifiez le type hello de toouse de redondance de stockage ; Vous pouvez utiliser [stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [stockage redondant de géo-réplication (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="a24f9-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="a24f9-130">Hello suivant montre testVault hello BackupStorageRedundancy - option est la valeur tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="a24f9-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="a24f9-131">Nombreuses applets de commande Azure Backup nécessitent l’objet de coffre Recovery Services hello en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="a24f9-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="a24f9-132">Pour cette raison, il est pratique toostore hello Services de récupération de sauvegarde coffre objet dans une variable.</span><span class="sxs-lookup"><span data-stu-id="a24f9-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="a24f9-133">Affichage des coffres de hello dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="a24f9-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="a24f9-134">Utilisez **Get-AzureRmRecoveryServicesVault** liste de hello tooview de tous les coffres dans l’abonnement actif de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="a24f9-135">Vous pouvez utiliser cette toocheck commande qu’un nouvel archivage a été créé ou toosee les coffres sont disponibles dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="a24f9-136">Exécutez la commande hello, Get-AzureRmRecoveryServicesVault, et tous les archivages dans l’abonnement de hello sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="a24f9-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="a24f9-137">Agent de sauvegarde Azure hello lors de l’installation sur un serveur DPM</span><span class="sxs-lookup"><span data-stu-id="a24f9-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="a24f9-138">Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a24f9-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="a24f9-139">Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de Services de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="a24f9-140">Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="a24f9-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="a24f9-141">tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges **sur le serveur DPM hello**:</span><span class="sxs-lookup"><span data-stu-id="a24f9-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="a24f9-142">Cette commande installe l’agent de hello avec toutes les options par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="a24f9-143">installation de Hello prend quelques minutes en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="a24f9-144">Si vous ne spécifiez pas hello */nu* hello d’option **mise à jour Windows** fenêtre s’ouvre à la fin de hello de toocheck d’installation hello pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="a24f9-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="a24f9-145">l’agent de Hello s’affiche dans la liste hello des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="a24f9-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="a24f9-146">liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="a24f9-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="a24f9-148">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="a24f9-148">Installation options</span></span>
<span data-ttu-id="a24f9-149">toosee toutes les options de hello disponibles via hello commandline, hello utilisation suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="a24f9-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="a24f9-150">les options disponibles Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a24f9-150">hello available options include:</span></span>

| <span data-ttu-id="a24f9-151">Option</span><span class="sxs-lookup"><span data-stu-id="a24f9-151">Option</span></span> | <span data-ttu-id="a24f9-152">Détails</span><span class="sxs-lookup"><span data-stu-id="a24f9-152">Details</span></span> | <span data-ttu-id="a24f9-153">Default</span><span class="sxs-lookup"><span data-stu-id="a24f9-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a24f9-154">/q</span><span class="sxs-lookup"><span data-stu-id="a24f9-154">/q</span></span> |<span data-ttu-id="a24f9-155">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="a24f9-155">Quiet installation</span></span> |- |
| <span data-ttu-id="a24f9-156">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="a24f9-156">/p:"location"</span></span> |<span data-ttu-id="a24f9-157">Chemin d’accès toohello dossier d’installation de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="a24f9-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="a24f9-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="a24f9-159">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="a24f9-159">/s:"location"</span></span> |<span data-ttu-id="a24f9-160">Chemin d’accès toohello dossier de cache de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="a24f9-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="a24f9-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="a24f9-162">/m</span><span class="sxs-lookup"><span data-stu-id="a24f9-162">/m</span></span> |<span data-ttu-id="a24f9-163">Acceptation de la mise à jour tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="a24f9-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="a24f9-164">/nu</span><span class="sxs-lookup"><span data-stu-id="a24f9-164">/nu</span></span> |<span data-ttu-id="a24f9-165">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="a24f9-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="a24f9-166">/d</span><span class="sxs-lookup"><span data-stu-id="a24f9-166">/d</span></span> |<span data-ttu-id="a24f9-167">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a24f9-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="a24f9-168">/ph</span><span class="sxs-lookup"><span data-stu-id="a24f9-168">/ph</span></span> |<span data-ttu-id="a24f9-169">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="a24f9-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="a24f9-170">/po</span><span class="sxs-lookup"><span data-stu-id="a24f9-170">/po</span></span> |<span data-ttu-id="a24f9-171">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="a24f9-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="a24f9-172">/pu</span><span class="sxs-lookup"><span data-stu-id="a24f9-172">/pu</span></span> |<span data-ttu-id="a24f9-173">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="a24f9-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="a24f9-174">/pw</span><span class="sxs-lookup"><span data-stu-id="a24f9-174">/pw</span></span> |<span data-ttu-id="a24f9-175">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="a24f9-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="a24f9-176">L’enregistrement DPM tooa coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="a24f9-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="a24f9-177">Une fois que vous avez créé le coffre Recovery Services hello, téléchargez l’agent plus récent hello et les informations d’identification de coffre hello et stockez-le dans un emplacement pratique comme C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="a24f9-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="a24f9-178">Sur le serveur DPM hello, exécutez hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) machine de hello tooregister applet de commande avec le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="a24f9-179">Paramètres de la configuration initiale</span><span class="sxs-lookup"><span data-stu-id="a24f9-179">Initial configuration settings</span></span>
<span data-ttu-id="a24f9-180">Une fois hello serveur DPM est enregistré avec hello de coffre Recovery Services, il commence par les paramètres par défaut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a24f9-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="a24f9-181">Ces paramètres d’abonnement incluent la mise en réseau, le chiffrement et hello zone de transit.</span><span class="sxs-lookup"><span data-stu-id="a24f9-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="a24f9-182">paramètres d’abonnement toochange vous devez toofirst obtenez un descripteur sur paramètres hello existants (par défaut) à l’aide de hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="a24f9-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="a24f9-183">Toutes les modifications sont apportées toothis local PowerShell objet ```$setting``` puis complet de l’objet hello est validée tooDPM et Azure Backup toosave les à l’aide de hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="a24f9-184">Vous devez toouse hello ```–Commit``` tooensure indicateur qui hello les modifications sont conservées.</span><span class="sxs-lookup"><span data-stu-id="a24f9-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="a24f9-185">paramètres de Hello ne seront pas appliqués et utilisés par Azure Backup, sauf si la validation.</span><span class="sxs-lookup"><span data-stu-id="a24f9-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="a24f9-186">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="a24f9-186">Networking</span></span>
<span data-ttu-id="a24f9-187">Si la connexion de hello de hello DPM machine toohello service Azure Backup sur hello internet est via un serveur proxy, paramètres hello du serveur proxy doivent être fournies pour les sauvegardes réussies.</span><span class="sxs-lookup"><span data-stu-id="a24f9-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="a24f9-188">Il incombe à l’aide de hello ```-ProxyServer```et ```-ProxyPort```, ```-ProxyUsername``` et hello ```ProxyPassword``` paramètres avec hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="a24f9-189">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="a24f9-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="a24f9-190">L’utilisation de la bande passante peut également être contrôlée avec les options de ```-WorkHourBandwidth``` et ```-NonWorkHourBandwidth``` pour un ensemble donné de jours de semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="a24f9-191">Dans cet exemple, nous ne fixons aucune limitation.</span><span class="sxs-lookup"><span data-stu-id="a24f9-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="a24f9-192">Configuration de la zone de transit hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-192">Configuring hello staging Area</span></span>
<span data-ttu-id="a24f9-193">Bonjour Azure Backup agent en cours d’exécution sur le serveur DPM hello a besoin de stockage temporaire pour les données restaurées à partir du cloud de hello (zone de transit local).</span><span class="sxs-lookup"><span data-stu-id="a24f9-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="a24f9-194">Configurer la zone de transit à l’aide de hello hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) applet de commande et hello ```-StagingAreaPath``` paramètre.</span><span class="sxs-lookup"><span data-stu-id="a24f9-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="a24f9-195">Dans l’exemple hello ci-dessus, la zone de transit hello sera définie trop*C:\StagingArea* dans l’objet de PowerShell hello ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="a24f9-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="a24f9-196">Vérifiez que hello le dossier spécifié existe déjà, sinon la validation finale de paramètres d’abonnement hello hello échouera.</span><span class="sxs-lookup"><span data-stu-id="a24f9-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="a24f9-197">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="a24f9-197">Encryption settings</span></span>
<span data-ttu-id="a24f9-198">tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="a24f9-199">phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="a24f9-200">Il est important tookeep cette sécurisé des informations et sécuriser une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="a24f9-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="a24f9-201">Dans l’exemple hello ci-dessous, commande premier hello convertit la chaîne de hello ```passphrase123456789``` tooa sécurisée chaîne et lui affecte hello sécurisé toohello variable chaîne nommée ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="a24f9-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="a24f9-202">commande deuxième Hello définit la chaîne sécurisée de hello ```$Passphrase``` comme mot de passe hello pour le chiffrement des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="a24f9-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="a24f9-203">Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="a24f9-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="a24f9-204">Vous ne serez pas toorestore en mesure des données à partir d’Azure sans cette phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="a24f9-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="a24f9-205">À ce stade, vous aurait dû effectuer tous les toohello de modifications hello requis ```$setting``` objet.</span><span class="sxs-lookup"><span data-stu-id="a24f9-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="a24f9-206">N’oubliez pas de modifications de hello toocommit.</span><span class="sxs-lookup"><span data-stu-id="a24f9-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="a24f9-207">Protéger les données tooAzure sauvegarde</span><span class="sxs-lookup"><span data-stu-id="a24f9-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="a24f9-208">Dans cette section, vous ajoutez un tooDPM de serveur de production et puis protégez hello toolocal DPM stockage et des données puis tooAzure sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a24f9-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="a24f9-209">Dans les exemples hello, nous allons vous montrer comment tooback des fichiers et des dossiers.</span><span class="sxs-lookup"><span data-stu-id="a24f9-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="a24f9-210">Hello logique peut facilement être étendu toobackup n’importe quelle source de données pris en charge de DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="a24f9-211">Toutes vos sauvegardes DPM sont régies par un groupe de protection constitué de quatre parties :</span><span class="sxs-lookup"><span data-stu-id="a24f9-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="a24f9-212">**Membres du groupe** est une liste de tous les objets protégeables hello (également appelé *sources de données* dans DPM) que vous souhaitez tooprotect Bonjour même groupe de protection.</span><span class="sxs-lookup"><span data-stu-id="a24f9-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="a24f9-213">Par exemple, vous voudrez tooprotect production machines virtuelles dans un groupe de protection et de bases de données SQL Server dans un autre groupe de protection d’avoir différentes exigences de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a24f9-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="a24f9-214">Avant que vous puissiez sauvegarder toute source de données sur un serveur de production, vous devez toomake hello que l’Agent DPM est installé sur le serveur de hello et est géré par DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="a24f9-215">Suivez les étapes de hello pour [installation hello Agent DPM](https://technet.microsoft.com/library/bb870935.aspx) et en le liant toohello approprié du serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="a24f9-216">**Méthode de protection des données** spécifie hello cible emplacements de sauvegarde - bande, disque et cloud.</span><span class="sxs-lookup"><span data-stu-id="a24f9-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="a24f9-217">Dans notre exemple, nous protégera données toohello local disque et toohello dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="a24f9-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="a24f9-218">A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prise et la fréquence à laquelle hello données doivent être synchronisées entre hello serveur DPM et le serveur de production hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="a24f9-219">A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f9-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="a24f9-220">Création d’un groupe de protection</span><span class="sxs-lookup"><span data-stu-id="a24f9-220">Creating a protection group</span></span>
<span data-ttu-id="a24f9-221">Commencez par créer un nouveau groupe de Protection à l’aide de hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="a24f9-222">Hello ci-dessus crée un groupe de Protection nommée *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="a24f9-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="a24f9-223">Ultérieures tooadd toohello à sauvegarde Azure cloud peut également être modifié à un groupe de protection existant.</span><span class="sxs-lookup"><span data-stu-id="a24f9-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="a24f9-224">Toutefois, toomake toutes les modifications toohello - groupe de Protection nouveau ou existant - nous avons besoin d’un handle de tooget sur un *modifiable* objet à l’aide de hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="a24f9-225">Ajout de membres de groupe toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="a24f9-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="a24f9-226">Chaque Agent DPM sait liste hello de sources de données sur le serveur hello lequel il est installé.</span><span class="sxs-lookup"><span data-stu-id="a24f9-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="a24f9-227">tooadd un toohello de source de données groupe de Protection, hello toofirst des besoins de l’Agent DPM envoyer une liste de serveur DPM toohello arrière hello sources de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="a24f9-228">Une ou plusieurs sources de données sont sélectionnées et ajoutées toohello groupe de Protection.</span><span class="sxs-lookup"><span data-stu-id="a24f9-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="a24f9-229">étapes de PowerShell Hello nécessaires tooachieve cela sont :</span><span class="sxs-lookup"><span data-stu-id="a24f9-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="a24f9-230">Extraire une liste de tous les serveurs gérés par DPM via hello Agent DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="a24f9-231">Choisissez un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="a24f9-231">Choose a specific server.</span></span>
3. <span data-ttu-id="a24f9-232">Extraire une liste de toutes les sources de données sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="a24f9-233">Choisissez une ou plusieurs sources de données et de les ajouter toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="a24f9-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="a24f9-234">Hello la liste des serveurs sur le hello Agent DPM est installé et est géré par le serveur DPM de hello est acquis par hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="a24f9-235">Dans cet exemple, nous allons filtrer et configurer uniquement PS avec une sauvegarde nommée *productionserver01* .</span><span class="sxs-lookup"><span data-stu-id="a24f9-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="a24f9-236">Liste hello de sources de données d’extraire maintenant sur ```$server``` à l’aide de hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="a24f9-237">Dans cet exemple, nous allons filtrage pour le volume de hello * D:\* que nous souhaitons tooconfigure pour la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a24f9-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="a24f9-238">Cette source de données est ensuite ajouté toohello groupe de Protection à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="a24f9-239">N’oubliez pas de toouse hello *modifiable* objet du groupe de protection ```$MPG``` ajouts de hello toomake.</span><span class="sxs-lookup"><span data-stu-id="a24f9-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="a24f9-240">Répétez cette étape autant de fois en fonction des besoins, jusqu'à ce que vous avez ajouté tous les hello choisi le groupe de protection toohello de sources de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="a24f9-241">Vous pouvez également commencer par qu’une seule source de données et flux de travail hello complète pour la création de hello groupe de Protection et à un moment ultérieur ajouter plusieurs sources de données toohello groupe de Protection.</span><span class="sxs-lookup"><span data-stu-id="a24f9-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="a24f9-242">Méthode de protection des données en sélectionnant hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-242">Selecting hello data protection method</span></span>
<span data-ttu-id="a24f9-243">Après ont ajouté les sources de données hello toohello groupe de Protection, hello prochaine étape consiste à l’aide de hello la méthode de protection hello toospecify [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="a24f9-244">Dans cet exemple, hello groupe de Protection est configurée pour le disque local et de sauvegarde sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="a24f9-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="a24f9-245">Vous devez également datasource de hello toospecify que vous souhaitez toocloud tooprotect à l’aide de hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) applet de commande avec l’indicateur en ligne-.</span><span class="sxs-lookup"><span data-stu-id="a24f9-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="a24f9-246">Définition de la plage de rétention hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-246">Setting hello retention range</span></span>
<span data-ttu-id="a24f9-247">Définir la rétention hello pour les points de sauvegarde hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="a24f9-248">Il peut sembler rétention de hello impair tooset avant de la planification de sauvegarde hello a été définie, à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande définit automatiquement une planification de sauvegarde par défaut qui peut ensuite être modifiée.</span><span class="sxs-lookup"><span data-stu-id="a24f9-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="a24f9-249">Il est toujours possible tooset planification de sauvegarde hello en premier et hello après la période de rétention.</span><span class="sxs-lookup"><span data-stu-id="a24f9-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="a24f9-250">Dans l’exemple hello ci-dessous, hello définit des paramètres de rétention hello pour les sauvegardes sur disque.</span><span class="sxs-lookup"><span data-stu-id="a24f9-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="a24f9-251">Cela conservera sauvegardes pendant 10 jours, les données de synchronisation toutes les 6 heures entre le serveur de production hello et le serveur DPM hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="a24f9-252">Hello ```SynchronizationFrequencyMinutes``` ne définit pas la fréquence à laquelle un point de sauvegarde est créé, mais la fréquence à laquelle les données sont copié toohello le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="a24f9-253">Ce paramètre évite que les sauvegardes soient trop volumineuses.</span><span class="sxs-lookup"><span data-stu-id="a24f9-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="a24f9-254">Pour les sauvegardes tooAzure (DPM fait référence toothem en tant que les sauvegardes en ligne) des plages de rétention hello peuvent être configurées pour [à long terme rétention à l’aide d’un schéma grand-père-Father-Son (GFS)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="a24f9-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="a24f9-255">Autrement dit, vous pouvez définir une stratégie de rétention combinée incluant des stratégies de rétention quotidiennes, hebdomadaires, mensuelles et annuelles.</span><span class="sxs-lookup"><span data-stu-id="a24f9-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="a24f9-256">Dans cet exemple, nous créer un tableau représentant le schéma de rétention complexes hello que nous souhaitons, puis configurez la durée de rétention hello à l’aide de hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="a24f9-257">Planification de sauvegarde hello ensemble</span><span class="sxs-lookup"><span data-stu-id="a24f9-257">Set hello backup schedule</span></span>
<span data-ttu-id="a24f9-258">DPM définit automatiquement une planification de sauvegarde par défaut si vous spécifiez l’objectif de protection hello à l’aide de hello ```Set-DPMPolicyObjective``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="a24f9-259">les planifications par défaut toochange hello, utilisez hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) applet de commande suivie hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="a24f9-260">Bonjour au-dessus de l’exemple, ```$onlineSch``` est un tableau qui contient la planification de protection en ligne existante hello pour hello groupe de Protection dans le schéma GFS hello avec quatre éléments :</span><span class="sxs-lookup"><span data-stu-id="a24f9-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="a24f9-261">```$onlineSch[0]```contient la planification quotidienne de hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="a24f9-262">```$onlineSch[1]```contient la planification hebdomadaire hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="a24f9-263">```$onlineSch[2]```contient la planification mensuelle de hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="a24f9-264">```$onlineSch[3]```contient la planification annuelle de hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="a24f9-265">Si vous avez besoin de la planification hebdomadaire toomodify hello, vous devez toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="a24f9-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="a24f9-266">Sauvegarde initiale</span><span class="sxs-lookup"><span data-stu-id="a24f9-266">Initial backup</span></span>
<span data-ttu-id="a24f9-267">Lorsque la sauvegarde un datasource de hello première fois, DPM doit crée réplica initial qui crée une copie complète de hello toobe de source de données protégée sur le volume du réplica DPM.</span><span class="sxs-lookup"><span data-stu-id="a24f9-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="a24f9-268">Cette activité peuvent être planifiée pour une durée spécifique, ou peut être déclenchée manuellement, à l’aide de hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) applet de commande avec le paramètre hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="a24f9-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="a24f9-269">Modification de la taille de hello du réplica DPM et le volume des points de récupération</span><span class="sxs-lookup"><span data-stu-id="a24f9-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="a24f9-270">Vous pouvez également modifier la taille du volume du réplica DPM et le volume de cliché instantané à l’aide de hello [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) applet de commande comme hello l’exemple suivant : Get-DatasourceDiskAllocation - source de données $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manuel - ReplicaArea (2 Go) - ShadowCopyArea (2 Go)</span><span class="sxs-lookup"><span data-stu-id="a24f9-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="a24f9-271">Validation hello change toohello groupe de Protection</span><span class="sxs-lookup"><span data-stu-id="a24f9-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="a24f9-272">Enfin, les modifications de hello doivent toobe validée que DPM puisse être sauvegarde hello par la nouvelle configuration de groupe de Protection hello.</span><span class="sxs-lookup"><span data-stu-id="a24f9-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="a24f9-273">Cela peut être obtenue à l’aide de hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="a24f9-274">Afficher des points de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="a24f9-274">View hello backup points</span></span>
<span data-ttu-id="a24f9-275">Vous pouvez utiliser hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget de l’applet de commande une liste de tous les points de récupération pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="a24f9-276">Dans cet exemple, nous allons :</span><span class="sxs-lookup"><span data-stu-id="a24f9-276">In this example, we will:</span></span>

* <span data-ttu-id="a24f9-277">FETCH tous hello pages sur le serveur DPM hello et stockées dans un tableau```$PG```</span><span class="sxs-lookup"><span data-stu-id="a24f9-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="a24f9-278">obtenir toohello correspondante de sources de données hello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="a24f9-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="a24f9-279">obtenir tous les points de récupération hello pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="a24f9-280">Restaurer des données protégées sur Azure</span><span class="sxs-lookup"><span data-stu-id="a24f9-280">Restore data protected on Azure</span></span>
<span data-ttu-id="a24f9-281">La restauration des données est une combinaison d'un objet ```RecoverableItem``` et d’un objet ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="a24f9-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="a24f9-282">Dans la section précédente de hello, nous avons obtenu une liste de points de sauvegarde hello pour une source de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="a24f9-283">Dans l’exemple hello ci-dessous, nous allons montrer comment la machine virtuelle de toorestore Hyper-V à partir d’Azure Backup en combinant les points de sauvegarde avec hello cibler pour la récupération.</span><span class="sxs-lookup"><span data-stu-id="a24f9-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="a24f9-284">Cet exemple inclut :</span><span class="sxs-lookup"><span data-stu-id="a24f9-284">This example includes:</span></span>

* <span data-ttu-id="a24f9-285">Création d’une option de récupération à l’aide de hello [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="a24f9-286">Tableau de hello l’extraction des points de sauvegarde à l’aide de hello ```Get-DPMRecoveryPoint``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a24f9-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="a24f9-287">Choix d’un toorestore de point de sauvegarde à partir de.</span><span class="sxs-lookup"><span data-stu-id="a24f9-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="a24f9-288">commandes Hello peuvent facilement être étendus pour n’importe quel type de source de données.</span><span class="sxs-lookup"><span data-stu-id="a24f9-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a24f9-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a24f9-289">Next steps</span></span>
* <span data-ttu-id="a24f9-290">Pour plus d’informations sur DPM tooAzure sauvegarde consultez [Introduction tooDPM sauvegarde](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="a24f9-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
