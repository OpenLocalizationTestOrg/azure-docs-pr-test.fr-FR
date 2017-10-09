---
title: sauvegardes de Windows Server aaaUse PowerShell toomanage dans Azure | Documents Microsoft
description: "Déployez et gérez des sauvegardes Windows Server à l’aide de PowerShell."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="9e544-103">Déployer et gérer la sauvegarde tooAzure pour le Client Windows Server et Windows à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e544-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e544-104">ARM</span><span class="sxs-lookup"><span data-stu-id="9e544-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="9e544-105">Classique</span><span class="sxs-lookup"><span data-stu-id="9e544-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="9e544-106">Cet article explique comment tooback de PowerShell toouse Windows Server ou Windows workstation données tooa coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9e544-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="9e544-107">Microsoft recommande d’utiliser des coffres Recovery Services pour tous les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="9e544-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="9e544-108">Si vous êtes un nouvel utilisateur Azure Backup et que vous n’avez pas créé un coffre de sauvegarde dans votre abonnement, utilisez l’article hello, [déployer et gérer des tooAzure de données de Data Protection Manager à l’aide de PowerShell](backup-client-automation.md) afin de vous stockez vos données dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="9e544-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9e544-109">Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services.</span><span class="sxs-lookup"><span data-stu-id="9e544-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="9e544-110">Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="9e544-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="9e544-111">Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9e544-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="9e544-112">Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e544-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="9e544-113">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="9e544-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="9e544-114">Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.</span><span class="sxs-lookup"><span data-stu-id="9e544-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="9e544-115">Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="9e544-116">Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.</span><span class="sxs-lookup"><span data-stu-id="9e544-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="9e544-117">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e544-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="9e544-118">Azure PowerShell 1.0 a été publié en octobre 2015.</span><span class="sxs-lookup"><span data-stu-id="9e544-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="9e544-119">Cette version a réussi la mise en production hello 0.9.8 et résultant des modifications importantes, notamment dans le modèle de désignation hello d’applets de commande hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="9e544-120">Suivez d’applets de commande 1.0 hello modèle d’affectation de noms {verbe}-Azure Resource Manager {nom} ; alors que les noms de hello 0.9.8 n’incluent pas **Rm** (par exemple, New-AzureRmResourceGroup au lieu de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="9e544-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="9e544-121">Lorsque vous utilisez Azure PowerShell 0.9.8, vous devez d’abord activer le mode Gestionnaire de ressources hello en exécutant hello **Switch-AzureMode AzureResourceManager** commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="9e544-122">Cette commande n’est pas nécessaire dans les versions 1.0 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9e544-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="9e544-123">Si vous souhaitez toouse vos scripts écrits pour hello 0.9.8 environnement hello 1.0 ou ultérieure environnement, vous devez tester soigneusement les scripts hello dans un environnement de préproduction avant de les utiliser dans la production tooavoid impact inattendu.</span><span class="sxs-lookup"><span data-stu-id="9e544-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="9e544-124">[Télécharger la dernière version de PowerShell hello](https://github.com/Azure/azure-powershell/releases) (version minimale requise est : 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="9e544-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="9e544-125">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9e544-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="9e544-126">Pour les clients à l’aide de la sauvegarde Azure pour hello première fois, vous devez tooregister hello Azure Backup fournisseur toobe utilisé avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e544-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="9e544-127">Cela est possible en exécutant hello de commande suivante : Register-AzureProvider - ProviderNamespace « Microsoft.Backup »</span><span class="sxs-lookup"><span data-stu-id="9e544-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="9e544-128">Vous pouvez créer un coffre de sauvegarde à l’aide de hello **New-AzureRMBackupVault** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="9e544-129">coffre de sauvegarde Hello est une ressource ARM, par conséquent, vous devez tooplace dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9e544-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="9e544-130">Dans une console Azure PowerShell avec élévation de privilèges, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="9e544-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="9e544-131">Hello d’utilisation **Get-AzureRMBackupVault** les coffres de sauvegarde de hello toolist applet de commande dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e544-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="9e544-132">Installation de l’agent Azure Backup hello</span><span class="sxs-lookup"><span data-stu-id="9e544-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="9e544-133">Avant d’installer l’agent de sauvegarde Azure hello, vous devez le programme d’installation de toohave hello téléchargés et présent sur hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="9e544-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="9e544-134">Vous pouvez obtenir la version la plus récente du programme d’installation hello hello de hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou à partir de la page du tableau de bord du coffre de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="9e544-135">Enregistrer le programme d’installation de hello tooan les emplacement facilement accessible, tel que * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="9e544-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="9e544-136">tooinstall hello exécution de l’agent, hello suivant de commande dans une console PowerShell avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="9e544-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="9e544-137">Cette commande installe l’agent de hello avec toutes les options par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="9e544-138">installation de Hello prend quelques minutes en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="9e544-139">Si vous ne spécifiez pas hello */nu* option puis hello **mise à jour Windows** fenêtre s’ouvre à fin hello de toocheck d’installation hello pour les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="9e544-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="9e544-140">Une fois installé, l’agent de hello s’affichent dans la liste hello des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="9e544-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="9e544-141">liste de hello toosee des programmes installés, passez trop**le panneau de configuration** > **programmes** > **programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="9e544-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="9e544-143">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="9e544-143">Installation options</span></span>
<span data-ttu-id="9e544-144">toosee tous hello options disponibles via hello de ligne de commande, utilisez les hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e544-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="9e544-145">les options disponibles Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e544-145">hello available options include:</span></span>

| <span data-ttu-id="9e544-146">Option</span><span class="sxs-lookup"><span data-stu-id="9e544-146">Option</span></span> | <span data-ttu-id="9e544-147">Détails</span><span class="sxs-lookup"><span data-stu-id="9e544-147">Details</span></span> | <span data-ttu-id="9e544-148">Default</span><span class="sxs-lookup"><span data-stu-id="9e544-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9e544-149">/q</span><span class="sxs-lookup"><span data-stu-id="9e544-149">/q</span></span> |<span data-ttu-id="9e544-150">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="9e544-150">Quiet installation</span></span> |- |
| <span data-ttu-id="9e544-151">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="9e544-151">/p:"location"</span></span> |<span data-ttu-id="9e544-152">Chemin d’accès toohello dossier d’installation de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9e544-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="9e544-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="9e544-154">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="9e544-154">/s:"location"</span></span> |<span data-ttu-id="9e544-155">Chemin d’accès toohello dossier de cache de l’agent de sauvegarde Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="9e544-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="9e544-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="9e544-157">/m</span><span class="sxs-lookup"><span data-stu-id="9e544-157">/m</span></span> |<span data-ttu-id="9e544-158">Acceptation de la mise à jour tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="9e544-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="9e544-159">/nu</span><span class="sxs-lookup"><span data-stu-id="9e544-159">/nu</span></span> |<span data-ttu-id="9e544-160">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="9e544-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="9e544-161">/d</span><span class="sxs-lookup"><span data-stu-id="9e544-161">/d</span></span> |<span data-ttu-id="9e544-162">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="9e544-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="9e544-163">/ph</span><span class="sxs-lookup"><span data-stu-id="9e544-163">/ph</span></span> |<span data-ttu-id="9e544-164">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="9e544-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="9e544-165">/po</span><span class="sxs-lookup"><span data-stu-id="9e544-165">/po</span></span> |<span data-ttu-id="9e544-166">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="9e544-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="9e544-167">/pu</span><span class="sxs-lookup"><span data-stu-id="9e544-167">/pu</span></span> |<span data-ttu-id="9e544-168">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="9e544-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="9e544-169">/pw</span><span class="sxs-lookup"><span data-stu-id="9e544-169">/pw</span></span> |<span data-ttu-id="9e544-170">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="9e544-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="9e544-171">L’inscription auprès de hello service Azure Backup</span><span class="sxs-lookup"><span data-stu-id="9e544-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="9e544-172">Avant de pouvoir inscrire avec hello service Azure Backup, vous devez tooensure que hello [conditions préalables](backup-configure-vault.md) sont remplies.</span><span class="sxs-lookup"><span data-stu-id="9e544-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="9e544-173">Vous devez respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e544-173">You must:</span></span>

* <span data-ttu-id="9e544-174">Avoir un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="9e544-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="9e544-175">Disposer d’un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9e544-175">Have a backup vault</span></span>

<span data-ttu-id="9e544-176">informations d’identification d’archivage toodownload hello, exécutez hello **Get-AzureRMBackupVaultCredentials** applet de commande dans une console Azure PowerShell et le magasin dans un emplacement pratique comme * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="9e544-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="9e544-177">L’enregistrement machine hello avec le coffre de hello est effectuée à l’aide de hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="9e544-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="9e544-178">N’utilisez pas le fichier d’informations d’identification de chemins d’accès relatifs toospecify hello coffre.</span><span class="sxs-lookup"><span data-stu-id="9e544-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="9e544-179">Vous devez fournir un chemin d’accès absolu comme une applet de commande toohello d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9e544-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="9e544-180">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="9e544-180">Networking settings</span></span>
<span data-ttu-id="9e544-181">Lors de la connectivité hello Hello toohello qu'internet se fait via un serveur proxy d’ordinateur Windows, les paramètres de proxy hello peuvent également être fournies toohello agent.</span><span class="sxs-lookup"><span data-stu-id="9e544-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="9e544-182">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="9e544-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="9e544-183">L’utilisation de la bande passante peut également être contrôlée avec options hello ```work hour bandwidth``` et ```non-work hour bandwidth``` pour un ensemble donné de jours de semaine de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="9e544-184">Définition des détails de la bande passante et de proxy hello est effectuée à l’aide de hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="9e544-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="9e544-185">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="9e544-185">Encryption settings</span></span>
<span data-ttu-id="9e544-186">tooAzure de données de sauvegarde envoyées Hello sauvegarde est la confidentialité de hello tooprotect chiffré des données de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="9e544-187">phrase secrète de chiffrement Hello donnée hello « mot de passe » toodecrypt hello au moment de la restauration de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="9e544-188">Conserver les informations de mot de passe hello sûre et sécurisée une fois qu’elle est définie.</span><span class="sxs-lookup"><span data-stu-id="9e544-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="9e544-189">Vous ne serez pas toorestore en mesure des données à partir d’Azure sans cette phrase secrète.</span><span class="sxs-lookup"><span data-stu-id="9e544-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="9e544-190">Sauvegarde des fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="9e544-190">Back up files and folders</span></span>
<span data-ttu-id="9e544-191">Toutes les sauvegardes à partir de serveurs et clients Windows tooAzure sauvegarde sont régies par une stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e544-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="9e544-192">stratégie de Hello comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="9e544-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="9e544-193">A **planification de sauvegarde** qui spécifie quand les sauvegardes doivent toobe prises et synchronisé avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="9e544-194">A **planification de rétention** qui spécifie la durée pendant laquelle des points de récupération de hello tooretain dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9e544-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="9e544-195">Une **spécification d'inclusion/exclusion de fichier** qui dicte ce qui doit être sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="9e544-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="9e544-196">Dans ce document, comme nous automatisons la sauvegarde, nous supposons que rien n'a été configuré.</span><span class="sxs-lookup"><span data-stu-id="9e544-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="9e544-197">Nous commençons par créer une stratégie de sauvegarde à l’aide de hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) applet de commande et son utilisation.</span><span class="sxs-lookup"><span data-stu-id="9e544-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="9e544-198">À ce hello temps stratégie est vide et autres applets de commande sont nécessaire toodefine quels éléments seront inclus ou exclus, lorsque les sauvegardes sont exécutées et hello où les sauvegardes seront stockées.</span><span class="sxs-lookup"><span data-stu-id="9e544-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="9e544-199">Configuration de planification de sauvegarde hello</span><span class="sxs-lookup"><span data-stu-id="9e544-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="9e544-200">Hello tout d’abord de hello 3 parties d’une stratégie est hello planification de sauvegarde est créée à l’aide de hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="9e544-201">planification de sauvegarde Hello définit lorsque les sauvegardes doivent toobe prise.</span><span class="sxs-lookup"><span data-stu-id="9e544-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="9e544-202">Lors de la création d’une planification, vous devez toospecify 2 des paramètres d’entrée :</span><span class="sxs-lookup"><span data-stu-id="9e544-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="9e544-203">**Jours de semaine de hello** cette sauvegarde hello doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="9e544-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="9e544-204">Vous pouvez exécuter la tâche de sauvegarde hello sur une seule journée, ou tous les jours de semaine de hello ou n’importe quelle combinaison entre les deux.</span><span class="sxs-lookup"><span data-stu-id="9e544-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="9e544-205">**Heures de la journée de hello** quand la sauvegarde de hello doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="9e544-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="9e544-206">Vous pouvez définir des too3 différents moments de la journée hello déclenchement de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="9e544-207">Par exemple, vous pouvez configurer une stratégie de sauvegarde qui s'exécute à 16 h 00 chaque samedi et chaque dimanche.</span><span class="sxs-lookup"><span data-stu-id="9e544-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="9e544-208">planification de sauvegarde Hello doit toobe associé à une stratégie, et cela peut être obtenue à l’aide de hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="9e544-209">Configuration d'une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="9e544-209">Configuring a retention policy</span></span>
<span data-ttu-id="9e544-210">stratégie de rétention Hello définit la durée de récupération points créés à partir des travaux de sauvegarde sont conservés.</span><span class="sxs-lookup"><span data-stu-id="9e544-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="9e544-211">Lorsque vous créez une nouvelle stratégie de rétention à l’aide de hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) applet de commande, vous pouvez spécifier plusieurs hello jours pendant lesquels les points de récupération d’une sauvegarde de hello doivent toobe avec Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="9e544-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="9e544-212">exemple Hello ci-dessous définit une stratégie de rétention de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="9e544-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="9e544-213">Hello stratégie de rétention doit être associé à stratégie de principal de hello à l’aide d’applet de commande hello [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="9e544-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="9e544-214">Inclusion et exclusion de toobe de fichiers sauvegardé</span><span class="sxs-lookup"><span data-stu-id="9e544-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="9e544-215">Un ```OBFileSpec``` objet définit hello fichiers toobe inclus et exclu dans une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9e544-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="9e544-216">Il s’agit d’un ensemble de règles que les fichiers et dossiers sur un ordinateur protégés par étendue out hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="9e544-217">Vous pouvez avoir de nombreuses règles d'inclusion ou d’exclusion en fonction de vos besoins, et les associer à une stratégie.</span><span class="sxs-lookup"><span data-stu-id="9e544-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="9e544-218">Lorsque vous créez un objet OBFileSpec, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="9e544-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="9e544-219">Spécifiez hello toobe fichiers et dossiers inclus</span><span class="sxs-lookup"><span data-stu-id="9e544-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="9e544-220">Spécifiez hello toobe fichiers et dossiers exclu</span><span class="sxs-lookup"><span data-stu-id="9e544-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="9e544-221">Spécifiez la sauvegarde récursive de données dans un dossier (ou) si uniquement hello fichiers de niveau supérieur dans le dossier spécifié de hello doivent être sauvegardées jusqu'à.</span><span class="sxs-lookup"><span data-stu-id="9e544-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="9e544-222">Hello ce dernier est obtenue à l’aide d’indicateur de non récursives - hello dans la commande hello New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="9e544-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="9e544-223">Dans l’exemple hello ci-dessous, nous sauvegarder volume C: et D: et exclure les fichiers binaires du système d’exploitation hello dans le dossier de Windows hello et tous les dossiers temporaires.</span><span class="sxs-lookup"><span data-stu-id="9e544-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="9e544-224">toodo afin que nous allons créer deux spécifications de fichier à l’aide de hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) applet de commande - un pour inclusion et un pour l’exclusion.</span><span class="sxs-lookup"><span data-stu-id="9e544-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="9e544-225">Une fois les spécifications de fichier hello ont été créées, ils sont associés avec stratégie hello hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="9e544-226">Appliquer la stratégie de hello</span><span class="sxs-lookup"><span data-stu-id="9e544-226">Applying hello policy</span></span>
<span data-ttu-id="9e544-227">Maintenant, objet de stratégie de hello est terminée et a une planification de sauvegarde associée, la stratégie de rétention et une liste d’inclusion/exclusion de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9e544-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="9e544-228">Cette stratégie peut maintenant être validée pour Azure Backup toouse.</span><span class="sxs-lookup"><span data-stu-id="9e544-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="9e544-229">Avant d’appliquer hello nouvellement créé stratégie Assurez-vous qu’il n’y a aucune stratégie de sauvegarde existant associé avec le serveur de hello à l’aide de hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="9e544-230">Suppression de la stratégie de hello invitera à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="9e544-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="9e544-231">confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="9e544-232">Objet de stratégie de validation hello est effectuée à l’aide de hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="9e544-233">Une confirmation vous est également demandée.</span><span class="sxs-lookup"><span data-stu-id="9e544-233">This will also ask for confirmation.</span></span> <span data-ttu-id="9e544-234">confirmation de hello tooskip utiliser hello ```-Confirm:$false``` indicateur avec l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="9e544-235">Vous pouvez afficher les détails de hello hello existant stratégie de sauvegarde à l’aide de hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="9e544-236">Vous pouvez Explorer à l’aide des hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) applet de commande pour la planification de sauvegarde hello et hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) applet de commande pour les stratégies de rétention hello</span><span class="sxs-lookup"><span data-stu-id="9e544-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="9e544-237">Exécution d'une sauvegarde ad hoc</span><span class="sxs-lookup"><span data-stu-id="9e544-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="9e544-238">Une fois qu’une stratégie de sauvegarde a été définie hello sauvegardes par la planification de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="9e544-239">Déclenchement d’une sauvegarde ad hoc est également possible à l’aide de hello [OBBackup de début](https://technet.microsoft.com/library/hh770426) applet de commande :</span><span class="sxs-lookup"><span data-stu-id="9e544-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="9e544-240">Restauration des données à partir de Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="9e544-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="9e544-241">Cette section vous guidera tout au long des étapes hello pour automatiser la récupération des données à partir d’Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="9e544-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="9e544-242">Cette opération implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e544-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="9e544-243">Sélectionnez hello source volume</span><span class="sxs-lookup"><span data-stu-id="9e544-243">Pick hello source volume</span></span>
2. <span data-ttu-id="9e544-244">Choisissez un toorestore de point de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9e544-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="9e544-245">Choisissez un élément de toorestore</span><span class="sxs-lookup"><span data-stu-id="9e544-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="9e544-246">Processus de restauration hello déclencheur</span><span class="sxs-lookup"><span data-stu-id="9e544-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="9e544-247">Volume de prélèvement hello source</span><span class="sxs-lookup"><span data-stu-id="9e544-247">Picking hello source volume</span></span>
<span data-ttu-id="9e544-248">Dans l’ordre toorestore un élément à partir d’Azure Backup, vous devez d’abord source de hello tooidentify d’élément de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="9e544-249">Étant donné que nous allons l’exécution de commandes hello dans le contexte de hello d’un serveur Windows ou d’un client Windows, hello ordinateur est déjà identifié.</span><span class="sxs-lookup"><span data-stu-id="9e544-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="9e544-250">étape suivante de Hello pour identifier la source de hello est volume de hello tooidentify qui le contient.</span><span class="sxs-lookup"><span data-stu-id="9e544-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="9e544-251">Une liste des volumes ou des sources en cours de sauvegarde à partir de cet ordinateur peut être récupérée en exécutant hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="9e544-252">Cette commande retourne un tableau de toutes les sources de hello sauvegardés à partir de ce serveur/client.</span><span class="sxs-lookup"><span data-stu-id="9e544-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="9e544-253">Choix d’un toorestore de point de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9e544-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="9e544-254">Hello liste de points de sauvegarde peut être récupérée en exécutant hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="9e544-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="9e544-255">Dans notre exemple, nous allons choisir hello sauvegarde les plus récentes pour le volume source de hello *D:* et utilisez-le toorecover un fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="9e544-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="9e544-256">objet de Hello ```$rps``` est un tableau de points de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9e544-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="9e544-257">premier élément de Hello est plus récentes hello et Nième élément de hello est le point le plus ancien hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="9e544-258">toochoose hello les plus récentes, nous allons utiliser ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="9e544-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="9e544-259">Choix d’un élément de toorestore</span><span class="sxs-lookup"><span data-stu-id="9e544-259">Choosing an item toorestore</span></span>
<span data-ttu-id="9e544-260">tooidentify hello exact ou du fichier toorestore du dossier, récursive utiliser hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="9e544-261">Cette hiérarchie de dossiers de manière hello peut être parcourue uniquement à l’aide de hello ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="9e544-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="9e544-262">Dans cet exemple, si nous voulons que le fichier de hello toorestore *finances.xls* nous pouvons font référence à l’aide de cet objet de hello ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="9e544-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="9e544-263">Vous pouvez également rechercher des toorestore d’éléments à l’aide de hello ```Get-OBRecoverableItem``` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="9e544-264">Dans notre exemple, toosearch pour *finances.xls* nous aurions pu obtenir un descripteur sur un fichier hello en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="9e544-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="9e544-265">Processus de restauration hello déclenchement</span><span class="sxs-lookup"><span data-stu-id="9e544-265">Triggering hello restore process</span></span>
<span data-ttu-id="9e544-266">processus de restauration tootrigger hello, nous devons tout d’abord les options de récupération toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="9e544-267">Cela est possible à l’aide de hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="9e544-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="9e544-268">Pour cet exemple, supposons que nous souhaitons que les fichiers de hello toorestore trop*C:\temp*. Supposons également que nous souhaitons tooskip fichiers qui existent déjà sur le dossier de destination hello *C:\temp*. toocreate telle une option de récupération, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e544-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="9e544-269">Déclenchement de la restauration à l’aide de hello maintenant [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) commande hello sélectionné ```$item``` à partir de la sortie de hello Hello ```Get-OBRecoverableItem``` applet de commande :</span><span class="sxs-lookup"><span data-stu-id="9e544-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="9e544-270">Désinstallation de l’agent de sauvegarde Azure hello</span><span class="sxs-lookup"><span data-stu-id="9e544-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="9e544-271">Désinstaller l’agent de sauvegarde Azure hello est possible à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9e544-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="9e544-272">Désinstallation des fichiers binaires hello à partir de l’ordinateur de hello a certaines tooconsider conséquences :</span><span class="sxs-lookup"><span data-stu-id="9e544-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="9e544-273">Elle supprime le filtre de fichier hello à partir de l’ordinateur de hello et le suivi des modifications est arrêté.</span><span class="sxs-lookup"><span data-stu-id="9e544-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="9e544-274">Toutes les informations de stratégie sont supprimées de la machine de hello, mais les informations de stratégie hello continuent toobe stockée dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="9e544-275">Toutes les planifications de sauvegarde sont supprimées, et aucune autre sauvegarde n'est effectuée.</span><span class="sxs-lookup"><span data-stu-id="9e544-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="9e544-276">Toutefois, hello des données stockées dans le reste de Azure et sont conservées conformément aux paramètres de stratégie de rétention hello par vous.</span><span class="sxs-lookup"><span data-stu-id="9e544-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="9e544-277">Les points plus anciens deviennent automatiquement obsolètes.</span><span class="sxs-lookup"><span data-stu-id="9e544-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="9e544-278">Gestion à distance</span><span class="sxs-lookup"><span data-stu-id="9e544-278">Remote management</span></span>
<span data-ttu-id="9e544-279">Toute la gestion hello autour de l’agent de sauvegarde Azure hello, les stratégies et les sources de données peut être effectuée à distance via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e544-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="9e544-280">ordinateur Hello qui est géré à distance doit toobe correctement préparé.</span><span class="sxs-lookup"><span data-stu-id="9e544-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="9e544-281">Par défaut, hello service WinRM est configuré pour un démarrage manuel.</span><span class="sxs-lookup"><span data-stu-id="9e544-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="9e544-282">type de démarrage de Hello doit être défini trop*automatique* et hello service doit être démarré.</span><span class="sxs-lookup"><span data-stu-id="9e544-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="9e544-283">tooverify qui hello service WinRM est en cours d’exécution, la valeur de la propriété Status de hello hello doit être *en cours d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="9e544-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="9e544-284">PowerShell doit être configuré pour la communication à distance.</span><span class="sxs-lookup"><span data-stu-id="9e544-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="9e544-285">machine de Hello désormais peut être géré à distance, en commençant à partir de l’installation Bonjour de l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="9e544-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="9e544-286">Par exemple, hello script suivant copie de l’ordinateur distant hello agent toohello et l’installe.</span><span class="sxs-lookup"><span data-stu-id="9e544-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="9e544-287">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e544-287">Next steps</span></span>
<span data-ttu-id="9e544-288">Pour plus d’informations sur Sauvegarde Azure pour client/serveur Windows, consultez</span><span class="sxs-lookup"><span data-stu-id="9e544-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="9e544-289">Introduction tooAzure sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9e544-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="9e544-290">Sauvegarder des serveurs Windows</span><span class="sxs-lookup"><span data-stu-id="9e544-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
