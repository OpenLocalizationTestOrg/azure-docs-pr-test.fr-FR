---
title: tooback de PowerShell aaaUse de Windows Server tooAzure | Documents Microsoft
description: "Découvrez comment toodeploy et gérer la sauvegarde Azure à l’aide de PowerShell"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="37764-103">Déployer et gérer la sauvegarde tooAzure pour le Client Windows Server et Windows à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="37764-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37764-104">ARM</span><span class="sxs-lookup"><span data-stu-id="37764-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="37764-105">Classique</span><span class="sxs-lookup"><span data-stu-id="37764-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="37764-106">Cet article vous montre comment toouse PowerShell pour configurer la sauvegarde Azure sur Windows Server ou d’un client Windows et la gestion de sauvegarde et restauration.</span><span class="sxs-lookup"><span data-stu-id="37764-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="37764-107">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="37764-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="37764-108">Cet article se concentre sur hello Azure Resource Manager (ARM) et hello applets de commande PowerShell de sauvegarde en ligne MS activer toouse un coffre Recovery Services dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="37764-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="37764-109">Azure PowerShell 1.0 a été publié en octobre 2015.</span><span class="sxs-lookup"><span data-stu-id="37764-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="37764-110">Cette version a réussi la mise en production hello 0.9.8 et résultant des modifications importantes, notamment dans le modèle de désignation hello d’applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="37764-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="37764-111">Suivez d’applets de commande 1.0 hello modèle d’affectation de noms {verbe}-Azure Resource Manager {nom} ; alors que les noms de hello 0.9.8 n’incluent pas **Rm** (par exemple, New-AzureRmResourceGroup au lieu de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="37764-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="37764-112">Lorsque vous utilisez Azure PowerShell 0.9.8, vous devez d’abord activer le mode Gestionnaire de ressources hello en exécutant hello **Switch-AzureMode AzureResourceManager** commande.</span><span class="sxs-lookup"><span data-stu-id="37764-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="37764-113">Cette commande n’est pas nécessaire dans les versions 1.0 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="37764-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="37764-114">Si vous souhaitez toouse vos scripts écrits pour hello 0.9.8 environnement hello 1.0 ou ultérieure environnement, doit mettre à jour et de tester scrupuleusement les scripts hello dans un environnement de préproduction avant de les utiliser dans la production tooavoid impact inattendu.</span><span class="sxs-lookup"><span data-stu-id="37764-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="37764-115">[Télécharger la dernière version de PowerShell hello](https://github.com/Azure/azure-powershell/releases) (version minimale requise est : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="37764-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="37764-116">Créer un coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="37764-116">Create a recovery services vault</span></span>
<span data-ttu-id="37764-117">Hello suit vous guide lors de la création d’un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="37764-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="37764-118">Un coffre Recovery Services diffère d’un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="37764-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="37764-119">Si vous utilisez Azure Backup pour hello première fois, vous devez utiliser hello **Register-AzureRMResourceProvider** fournisseur de Service de récupération Azure hello applet de commande tooregister avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="37764-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="37764-120">Hello coffre Recovery Services est une ressource ARM, vous devez donc tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="37764-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="37764-121">Vous pouvez utiliser un groupe de ressources existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="37764-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="37764-122">Lorsque vous créez un nouveau groupe de ressources, spécifiez le nom de hello et un emplacement pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="37764-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="37764-123">Hello d’utilisation **New-AzureRmRecoveryServicesVault** nouveau coffre d’applet de commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="37764-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="37764-124">Veillez à toospecify hello même emplacement pour le coffre hello que celui utilisé pour le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="37764-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="37764-125">Spécifiez le type hello de toouse de redondance de stockage ; Vous pouvez utiliser [stockage localement redondant (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [stockage redondant de géo-réplication (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="37764-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="37764-126">Hello suivant montre testVault hello BackupStorageRedundancy - option est la valeur tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="37764-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="37764-127">Nombreuses applets de commande Azure Backup nécessitent l’objet de coffre Recovery Services hello en tant qu’entrée.</span><span class="sxs-lookup"><span data-stu-id="37764-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="37764-128">Pour cette raison, il est pratique toostore hello Services de récupération de sauvegarde coffre objet dans une variable.</span><span class="sxs-lookup"><span data-stu-id="37764-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="37764-129">Affichage des coffres de hello dans un abonnement</span><span class="sxs-lookup"><span data-stu-id="37764-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="37764-130">Utilisez **Get-AzureRmRecoveryServicesVault** liste de hello tooview de tous les coffres dans l’abonnement actif de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="37764-131">Vous pouvez utiliser cette toocheck commande qu’un nouvel archivage a été créé ou toosee les coffres sont disponibles dans l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="37764-132">Exécutez la commande hello **Get-AzureRmRecoveryServicesVault**, et tous les archivages dans l’abonnement de hello sont répertoriés.</span><span class="sxs-lookup"><span data-stu-id="37764-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="37764-133">Installation de l’agent Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="37764-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="37764-134">Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="37764-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="37764-135">Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de Services de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="37764-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="37764-136">Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="37764-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="37764-137">Ou bien, utilisez PowerShell tooget hello Téléchargeur d’installation :</span><span class="sxs-lookup"><span data-stu-id="37764-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="37764-138">tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="37764-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="37764-139">Cette commande installe l’agent de hello avec toutes les options par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="37764-140">installation de Hello prend quelques minutes en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="37764-141">Si vous ne spécifiez pas hello */nu* option puis hello **mise à jour Windows** fenêtre s’ouvre à fin hello de toocheck d’installation hello pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="37764-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="37764-142">Une fois installé, l’agent de hello s’affichent dans la liste hello des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="37764-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="37764-143">liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="37764-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="37764-145">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="37764-145">Installation options</span></span>
<span data-ttu-id="37764-146">toosee tous hello options disponibles via hello de ligne de commande, utilisez les hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="37764-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="37764-147">les options disponibles Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="37764-147">hello available options include:</span></span>

| <span data-ttu-id="37764-148">Option</span><span class="sxs-lookup"><span data-stu-id="37764-148">Option</span></span> | <span data-ttu-id="37764-149">Détails</span><span class="sxs-lookup"><span data-stu-id="37764-149">Details</span></span> | <span data-ttu-id="37764-150">Default</span><span class="sxs-lookup"><span data-stu-id="37764-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="37764-151">/q</span><span class="sxs-lookup"><span data-stu-id="37764-151">/q</span></span> |<span data-ttu-id="37764-152">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="37764-152">Quiet installation</span></span> |- |
| <span data-ttu-id="37764-153">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="37764-153">/p:"location"</span></span> |<span data-ttu-id="37764-154">Chemin d’accès toohello dossier d’installation de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37764-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="37764-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="37764-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="37764-156">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="37764-156">/s:"location"</span></span> |<span data-ttu-id="37764-157">Chemin d’accès toohello dossier de cache de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37764-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="37764-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="37764-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="37764-159">/m</span><span class="sxs-lookup"><span data-stu-id="37764-159">/m</span></span> |<span data-ttu-id="37764-160">Acceptation de la mise à jour tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="37764-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="37764-161">/nu</span><span class="sxs-lookup"><span data-stu-id="37764-161">/nu</span></span> |<span data-ttu-id="37764-162">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="37764-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="37764-163">/d</span><span class="sxs-lookup"><span data-stu-id="37764-163">/d</span></span> |<span data-ttu-id="37764-164">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="37764-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="37764-165">/ph</span><span class="sxs-lookup"><span data-stu-id="37764-165">/ph</span></span> |<span data-ttu-id="37764-166">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="37764-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="37764-167">/po</span><span class="sxs-lookup"><span data-stu-id="37764-167">/po</span></span> |<span data-ttu-id="37764-168">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="37764-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="37764-169">/pu</span><span class="sxs-lookup"><span data-stu-id="37764-169">/pu</span></span> |<span data-ttu-id="37764-170">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="37764-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="37764-171">/pw</span><span class="sxs-lookup"><span data-stu-id="37764-171">/pw</span></span> |<span data-ttu-id="37764-172">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="37764-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="37764-173">L’enregistrement de Windows Server ou Windows client machine tooa coffre Recovery Services</span><span class="sxs-lookup"><span data-stu-id="37764-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="37764-174">Une fois que vous avez créé le coffre Recovery Services hello, téléchargez l’agent plus récent hello et les informations d’identification de coffre hello et stockez-le dans un emplacement pratique comme C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="37764-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="37764-175">Sur hello Windows Server ou l’ordinateur client de Windows, exécutez hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) machine de hello tooregister applet de commande avec le coffre de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="37764-176">Cela et les autres applets de commande utilisés pour la sauvegarde, sont d’un module MSONLINE hello quels hello Mars l’ajouté en tant que partie du processus d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="37764-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="37764-177">programme d’installation de l’Agent Hello ne met pas à jour hello $Env : variable PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="37764-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="37764-178">Cela signifie que le chargement automatique du module échoue.</span><span class="sxs-lookup"><span data-stu-id="37764-178">This means module auto-load fails.</span></span> <span data-ttu-id="37764-179">tooresolve ce que vous pouvez effectuer les suivant hello :</span><span class="sxs-lookup"><span data-stu-id="37764-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="37764-180">Ou bien, vous pouvez charger manuellement le module de hello dans votre script comme suit :</span><span class="sxs-lookup"><span data-stu-id="37764-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="37764-181">Une fois que vous chargez des applets de commande de sauvegarde en ligne hello, vous inscrivez les informations d’identification de coffre hello :</span><span class="sxs-lookup"><span data-stu-id="37764-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="37764-182">N’utilisez pas le fichier d’informations d’identification de chemins d’accès relatifs toospecify hello coffre.</span><span class="sxs-lookup"><span data-stu-id="37764-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="37764-183">Vous devez fournir un chemin d’accès absolu comme une applet de commande toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="37764-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="37764-184">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="37764-184">Networking settings</span></span>
<span data-ttu-id="37764-185">Lors de la connectivité hello Hello toohello qu'internet se fait via un serveur proxy d’ordinateur Windows, les paramètres de proxy hello peuvent également être fournies toohello agent.</span><span class="sxs-lookup"><span data-stu-id="37764-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="37764-186">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="37764-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="37764-187">L’utilisation de la bande passante peut également être contrôlée avec options hello ```work hour bandwidth``` et ```non-work hour bandwidth``` pour un ensemble donné de jours de semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="37764-188">Définition des détails de la bande passante et de proxy hello est effectuée à l’aide de hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="37764-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="37764-189">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="37764-189">Encryption settings</span></span>
<span data-ttu-id="37764-190">tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="37764-191">phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="37764-192">Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="37764-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="37764-193">Vous ne sont pas être toorestore en mesure des données à partir d’Azure sans cette phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="37764-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="37764-194">Sauvegarde des fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="37764-194">Back up files and folders</span></span>
<span data-ttu-id="37764-195">Toutes les sauvegardes sur les serveurs et clients Windows tooAzure sauvegarde sont régies par une stratégie.</span><span class="sxs-lookup"><span data-stu-id="37764-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="37764-196">stratégie de Hello comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="37764-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="37764-197">A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prises et synchronisé avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="37764-198">A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.</span><span class="sxs-lookup"><span data-stu-id="37764-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="37764-199">Une **spécification d'inclusion/exclusion de fichier** qui dicte ce qui doit être sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="37764-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="37764-200">Dans ce document, comme nous automatisons la sauvegarde, nous supposons que rien n'a été configuré.</span><span class="sxs-lookup"><span data-stu-id="37764-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="37764-201">Nous commençons par créer une stratégie de sauvegarde à l’aide de hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="37764-202">À ce hello temps stratégie est vide et autres applets de commande sont nécessaire toodefine quels éléments seront inclus ou exclus, lorsque les sauvegardes sont exécutées et hello où les sauvegardes seront stockées.</span><span class="sxs-lookup"><span data-stu-id="37764-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="37764-203">Configuration de planification de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="37764-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="37764-204">Hello tout d’abord de hello 3 parties d’une stratégie est hello planification de sauvegarde est créée à l’aide de hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="37764-205">planification de sauvegarde Hello définit lorsque les sauvegardes doivent toobe prise.</span><span class="sxs-lookup"><span data-stu-id="37764-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="37764-206">Lors de la création d’une planification, vous devez toospecify 2 des paramètres d’entrée :</span><span class="sxs-lookup"><span data-stu-id="37764-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="37764-207">**Jours de semaine de hello** cette sauvegarde hello doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="37764-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="37764-208">Vous pouvez exécuter la tâche de sauvegarde hello sur une seule journée, ou tous les jours de semaine de hello ou n’importe quelle combinaison entre les deux.</span><span class="sxs-lookup"><span data-stu-id="37764-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="37764-209">**Heures de la journée de hello** quand la sauvegarde de hello doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="37764-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="37764-210">Vous pouvez définir des too3 différents moments de la journée hello déclenchement de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="37764-211">Par exemple, vous pouvez configurer une stratégie de sauvegarde qui s'exécute à 16 h 00 chaque samedi et chaque dimanche.</span><span class="sxs-lookup"><span data-stu-id="37764-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="37764-212">planification de sauvegarde Hello doit toobe associé à une stratégie, et cela peut être obtenue à l’aide de hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="37764-213">Configuration d'une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="37764-213">Configuring a retention policy</span></span>
<span data-ttu-id="37764-214">stratégie de rétention Hello définit la durée de récupération points créés à partir des travaux de sauvegarde sont conservés.</span><span class="sxs-lookup"><span data-stu-id="37764-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="37764-215">Lorsque vous créez une nouvelle stratégie de rétention à l’aide de hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) applet de commande, vous pouvez spécifier plusieurs hello jours pendant lesquels les points de récupération d’une sauvegarde de hello doivent toobe avec Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="37764-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="37764-216">exemple Hello ci-dessous définit une stratégie de rétention de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="37764-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="37764-217">Hello stratégie de rétention doit être associé à stratégie de principal de hello à l’aide d’applet de commande hello [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="37764-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="37764-218">Inclusion et exclusion de toobe de fichiers sauvegardé</span><span class="sxs-lookup"><span data-stu-id="37764-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="37764-219">Un ```OBFileSpec``` objet définit hello fichiers toobe inclus et exclu dans une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="37764-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="37764-220">Il s’agit d’un ensemble de règles que les fichiers et dossiers sur un ordinateur protégés par étendue out hello.</span><span class="sxs-lookup"><span data-stu-id="37764-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="37764-221">Vous pouvez avoir de nombreuses règles d'inclusion ou d’exclusion en fonction de vos besoins, et les associer à une stratégie.</span><span class="sxs-lookup"><span data-stu-id="37764-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="37764-222">Lorsque vous créez un objet OBFileSpec, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="37764-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="37764-223">Spécifiez hello toobe fichiers et dossiers inclus</span><span class="sxs-lookup"><span data-stu-id="37764-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="37764-224">Spécifiez hello toobe fichiers et dossiers exclu</span><span class="sxs-lookup"><span data-stu-id="37764-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="37764-225">Spécifiez la sauvegarde récursive de données dans un dossier (ou) si uniquement hello fichiers de niveau supérieur dans le dossier spécifié de hello doivent être sauvegardées jusqu'à.</span><span class="sxs-lookup"><span data-stu-id="37764-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="37764-226">Hello ce dernier est obtenue à l’aide d’indicateur de non récursives - hello dans la commande hello New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="37764-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="37764-227">Dans l’exemple hello ci-dessous, nous sauvegarder volume C: et D: et exclure les fichiers binaires du système d’exploitation hello dans le dossier de Windows hello et tous les dossiers temporaires.</span><span class="sxs-lookup"><span data-stu-id="37764-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="37764-228">toodo afin que nous allons créer deux spécifications de fichier à l’aide de hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) applet de commande - un pour inclusion et un pour l’exclusion.</span><span class="sxs-lookup"><span data-stu-id="37764-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="37764-229">Une fois les spécifications de fichier hello ont été créées, ils sont associés avec stratégie hello hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a><span data-ttu-id="37764-230">Appliquer la stratégie de hello</span><span class="sxs-lookup"><span data-stu-id="37764-230">Applying hello policy</span></span>
<span data-ttu-id="37764-231">Maintenant, objet de stratégie de hello est terminée et a une planification de sauvegarde associée, la stratégie de rétention et une liste d’inclusion/exclusion de fichiers.</span><span class="sxs-lookup"><span data-stu-id="37764-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="37764-232">Cette stratégie peut maintenant être validée pour Azure Backup toouse.</span><span class="sxs-lookup"><span data-stu-id="37764-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="37764-233">Avant d’appliquer hello nouvellement créé stratégie Assurez-vous qu’il n’y a aucune stratégie de sauvegarde existant associé avec le serveur de hello à l’aide de hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="37764-234">Suppression de la stratégie de hello invitera à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="37764-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="37764-235">confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="37764-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="37764-236">Objet de stratégie de validation hello est effectuée à l’aide de hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="37764-237">Une confirmation vous est également demandée.</span><span class="sxs-lookup"><span data-stu-id="37764-237">This will also ask for confirmation.</span></span> <span data-ttu-id="37764-238">confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="37764-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="37764-239">Vous pouvez afficher les détails de hello hello existant stratégie de sauvegarde à l’aide de hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="37764-240">Vous pouvez Explorer à l’aide des hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) applet de commande pour la planification de sauvegarde hello et hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) applet de commande pour les stratégies de rétention hello</span><span class="sxs-lookup"><span data-stu-id="37764-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="37764-241">Exécution d'une sauvegarde ad hoc</span><span class="sxs-lookup"><span data-stu-id="37764-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="37764-242">Une fois qu’une stratégie de sauvegarde a été définie hello sauvegardes par la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="37764-243">Déclenchement d’une sauvegarde ad hoc est également possible à l’aide de hello [OBBackup de début](https://technet.microsoft.com/library/hh770426) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="37764-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="37764-244">Restauration des données à partir de Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="37764-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="37764-245">Cette section vous guidera tout au long des étapes hello pour automatiser la récupération des données à partir d’Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="37764-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="37764-246">Cette opération implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="37764-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="37764-247">Sélectionnez hello source volume</span><span class="sxs-lookup"><span data-stu-id="37764-247">Pick hello source volume</span></span>
2. <span data-ttu-id="37764-248">Choisissez un toorestore de point de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="37764-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="37764-249">Choisissez un élément de toorestore</span><span class="sxs-lookup"><span data-stu-id="37764-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="37764-250">Processus de restauration hello déclencheur</span><span class="sxs-lookup"><span data-stu-id="37764-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="37764-251">Volume de prélèvement hello source</span><span class="sxs-lookup"><span data-stu-id="37764-251">Picking hello source volume</span></span>
<span data-ttu-id="37764-252">Dans l’ordre toorestore un élément à partir d’Azure Backup, vous devez d’abord source de hello tooidentify d’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="37764-253">Étant donné que nous allons l’exécution de commandes hello dans le contexte de hello d’un serveur Windows ou d’un client Windows, hello ordinateur est déjà identifié.</span><span class="sxs-lookup"><span data-stu-id="37764-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="37764-254">étape suivante de Hello pour identifier la source de hello est volume de hello tooidentify qui le contient.</span><span class="sxs-lookup"><span data-stu-id="37764-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="37764-255">Une liste des volumes ou des sources en cours de sauvegarde à partir de cet ordinateur peut être récupérée en exécutant hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="37764-256">Cette commande retourne un tableau de toutes les sources de hello sauvegardés à partir de ce serveur/client.</span><span class="sxs-lookup"><span data-stu-id="37764-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="37764-257">Choix d’un point de sauvegarde à partir de quels toorestore</span><span class="sxs-lookup"><span data-stu-id="37764-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="37764-258">Récupérer une liste de points de sauvegarde en exécutant hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="37764-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="37764-259">Dans notre exemple, nous allons choisir hello sauvegarde les plus récentes pour le volume source de hello *D:* et utilisez-le toorecover un fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="37764-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="37764-260">objet de Hello ```$rps``` est un tableau de points de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="37764-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="37764-261">premier élément de Hello est plus récentes hello et Nième élément de hello est le point le plus ancien hello.</span><span class="sxs-lookup"><span data-stu-id="37764-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="37764-262">toochoose hello les plus récentes, nous allons utiliser ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="37764-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="37764-263">Choix d’un élément de toorestore</span><span class="sxs-lookup"><span data-stu-id="37764-263">Choosing an item toorestore</span></span>
<span data-ttu-id="37764-264">tooidentify hello exact ou du fichier toorestore du dossier, récursive utiliser hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="37764-265">Cette hiérarchie de dossiers de manière hello peut être parcourue uniquement à l’aide de hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="37764-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="37764-266">Dans cet exemple, si nous voulons que le fichier de hello toorestore *finances.xls* nous pouvons font référence à l’aide de cet objet de hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="37764-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="37764-267">Vous pouvez également rechercher des toorestore d’éléments à l’aide de hello ```Get-OBRecoverableItem``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="37764-268">Dans notre exemple, toosearch pour *finances.xls* nous aurions pu obtenir un descripteur sur un fichier hello en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="37764-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="37764-269">Processus de restauration hello déclenchement</span><span class="sxs-lookup"><span data-stu-id="37764-269">Triggering hello restore process</span></span>
<span data-ttu-id="37764-270">processus de restauration tootrigger hello, nous devons tout d’abord les options de récupération toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="37764-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="37764-271">Cela est possible à l’aide de hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="37764-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="37764-272">Pour cet exemple, supposons que nous souhaitons que les fichiers de hello toorestore trop*C:\temp*. Supposons également que nous souhaitons tooskip fichiers qui existent déjà sur le dossier de destination hello *C:\temp*. toocreate telle une option de récupération, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="37764-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="37764-273">Maintenant déclencher le processus de restauration hello à l’aide de hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) commande hello sélectionné ```$item``` à partir de la sortie de hello Hello ```Get-OBRecoverableItem``` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="37764-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="37764-274">Désinstallation de l’agent de sauvegarde Azure hello</span><span class="sxs-lookup"><span data-stu-id="37764-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="37764-275">Désinstaller l’agent de sauvegarde Azure hello est possible à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="37764-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="37764-276">Désinstallation des fichiers binaires hello à partir de l’ordinateur de hello a certaines tooconsider conséquences :</span><span class="sxs-lookup"><span data-stu-id="37764-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="37764-277">Elle supprime le filtre de fichier hello à partir de l’ordinateur de hello et le suivi des modifications est arrêté.</span><span class="sxs-lookup"><span data-stu-id="37764-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="37764-278">Toutes les informations de stratégie sont supprimées de la machine de hello, mais les informations de stratégie hello continuent toobe stockée dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="37764-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="37764-279">Toutes les planifications de sauvegarde sont supprimées, et aucune autre sauvegarde n'est effectuée.</span><span class="sxs-lookup"><span data-stu-id="37764-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="37764-280">Toutefois, hello des données stockées dans le reste de Azure et sont conservées conformément aux paramètres de stratégie de rétention hello par vous.</span><span class="sxs-lookup"><span data-stu-id="37764-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="37764-281">Les points plus anciens deviennent automatiquement obsolètes.</span><span class="sxs-lookup"><span data-stu-id="37764-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="37764-282">Gestion à distance</span><span class="sxs-lookup"><span data-stu-id="37764-282">Remote management</span></span>
<span data-ttu-id="37764-283">Toute la gestion hello autour de l’agent de sauvegarde Azure hello, les stratégies et les sources de données peut être effectuée à distance via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37764-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="37764-284">ordinateur Hello qui est géré à distance doit toobe correctement préparé.</span><span class="sxs-lookup"><span data-stu-id="37764-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="37764-285">Par défaut, hello service WinRM est configuré pour un démarrage manuel.</span><span class="sxs-lookup"><span data-stu-id="37764-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="37764-286">type de démarrage de Hello doit être défini trop*automatique* et hello service doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="37764-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="37764-287">tooverify qui hello service WinRM est en cours d’exécution, la valeur de la propriété Status de hello hello doit être *en cours d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="37764-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="37764-288">PowerShell doit être configuré pour la communication à distance.</span><span class="sxs-lookup"><span data-stu-id="37764-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="37764-289">machine de Hello désormais peut être géré à distance, en commençant à partir de l’installation Bonjour de l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="37764-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="37764-290">Par exemple, hello script suivant copie de l’ordinateur distant hello agent toohello et l’installe.</span><span class="sxs-lookup"><span data-stu-id="37764-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="37764-291">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="37764-291">Next steps</span></span>
<span data-ttu-id="37764-292">Pour plus d’informations sur Sauvegarde Azure pour client/serveur Windows, consultez</span><span class="sxs-lookup"><span data-stu-id="37764-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="37764-293">Introduction tooAzure sauvegarde</span><span class="sxs-lookup"><span data-stu-id="37764-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="37764-294">Sauvegarder des serveurs Windows</span><span class="sxs-lookup"><span data-stu-id="37764-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
