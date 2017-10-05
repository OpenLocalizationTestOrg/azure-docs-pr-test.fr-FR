---
title: "Utiliser PowerShell pour gérer les sauvegardes Windows Server dans Azure | Microsoft Docs"
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
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="81dc4-103">Déployer et gérer une sauvegarde vers Azure pour un serveur/client Windows à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="81dc4-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="81dc4-104">ARM</span><span class="sxs-lookup"><span data-stu-id="81dc4-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="81dc4-105">Classique</span><span class="sxs-lookup"><span data-stu-id="81dc4-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="81dc4-106">Cet article explique comment utiliser PowerShell pour sauvegarder des données Windows Server ou de station de travail Windows dans un coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="81dc4-107">Microsoft recommande d’utiliser des coffres Recovery Services pour tous les nouveaux déploiements.</span><span class="sxs-lookup"><span data-stu-id="81dc4-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="81dc4-108">Si vous êtes un nouvel utilisateur de la Sauvegarde Azure et que vous n’avez pas créé de coffre de sauvegarde dans votre abonnement, appuyez-vous sur l’article [Déployer et gérer une sauvegarde vers Azure pour un serveur/client Windows à l’aide de PowerShell](backup-client-automation.md) pour stocker vos données dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="81dc4-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="81dc4-109">Vous pouvez désormais mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="81dc4-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="81dc4-110">Pour en savoir plus, consultez l’article [Mettre à niveau un coffre de sauvegarde vers un coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="81dc4-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="81dc4-111">Microsoft vous recommande de mettre à niveau vos coffres de sauvegarde vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="81dc4-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="81dc4-112">À compter du 15 octobre 2017, vous ne pourrez plus vous servir de PowerShell pour créer des coffres de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="81dc4-113">**D’ici au 1er novembre 2017** :</span><span class="sxs-lookup"><span data-stu-id="81dc4-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="81dc4-114">tous les coffres de sauvegarde restants seront automatiquement mis à niveau vers des coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="81dc4-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="81dc4-115">Vous ne pourrez plus accéder à vos données de sauvegarde depuis le portail Classic.</span><span class="sxs-lookup"><span data-stu-id="81dc4-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="81dc4-116">Au lieu de cela, vous devrez utiliser le portail Azure pour accéder à ces données au sein de coffres Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="81dc4-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="81dc4-117">Installation d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81dc4-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="81dc4-118">Azure PowerShell 1.0 a été publié en octobre 2015.</span><span class="sxs-lookup"><span data-stu-id="81dc4-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="81dc4-119">Cette version, qui fait suite à la release 0.9.8, a introduit d’importantes modifications, en particulier dans le modèle de dénomination des applets de commande.</span><span class="sxs-lookup"><span data-stu-id="81dc4-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="81dc4-120">Les applets de commande version 1.0 suivent le modèle d’affectation de noms {verbe}-AzureRm{nom} ; les noms 0.9.8 n’incluent pas **Rm** (par exemple, New-AzureRmResourceGroup au lieu de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="81dc4-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="81dc4-121">Lorsque vous utilisez Azure PowerShell 0.9.8, vous devez d’abord activer le mode Resource Manager en exécutant la commande **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="81dc4-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="81dc4-122">Cette commande n’est pas nécessaire dans les versions 1.0 ou ultérieures.</span><span class="sxs-lookup"><span data-stu-id="81dc4-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="81dc4-123">Si vous souhaitez utiliser dans l’environnement 1.0 (ou ultérieur) des scripts écrits pour l’environnement 0.9.8, veillez à les tester dans un environnement de pré-production avant de les utiliser en production, ce afin d’éviter tout résultat inattendu.</span><span class="sxs-lookup"><span data-stu-id="81dc4-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="81dc4-124">[Téléchargez la dernière version de PowerShell](https://github.com/Azure/azure-powershell/releases) (version minimale requise : 1.0.0).</span><span class="sxs-lookup"><span data-stu-id="81dc4-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="81dc4-125">Créer un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="81dc4-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="81dc4-126">Pour les clients utilisant Sauvegarde Azure pour la première fois, vous devez enregistrer le fournisseur Sauvegarde Azure à utiliser avec votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="81dc4-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="81dc4-127">Pour cela, exécutez la commande suivante : Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="81dc4-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="81dc4-128">Vous pouvez créer un coffre de sauvegarde en utilisant l’applet de commande **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="81dc4-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="81dc4-129">Le coffre de sauvegarde constituant une ressource ARM, vous devez le placer dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="81dc4-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="81dc4-130">Dans une console Azure PowerShell avec élévation de privilèges, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="81dc4-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="81dc4-131">Utilisez l’applet de commande **Get-AzureRMBackupVault** pour répertorier les coffres de sauvegarde d’un abonnement.</span><span class="sxs-lookup"><span data-stu-id="81dc4-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="81dc4-132">Installation de l'agent Azure Backup</span><span class="sxs-lookup"><span data-stu-id="81dc4-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="81dc4-133">Avant d’installer l'agent Azure Backup, vous devez avoir téléchargé le programme d’installation sur le serveur Windows.</span><span class="sxs-lookup"><span data-stu-id="81dc4-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="81dc4-134">Vous pouvez obtenir la dernière version du programme d’installation à partir du [Centre de téléchargement Microsoft](http://aka.ms/azurebackup_agent) ou de la page Tableau de bord du coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="81dc4-135">Enregistrez le programme d’installation dans un emplacement auquel vous pouvez accéder facilement, par exemple *C:\Téléchargements\*.</span><span class="sxs-lookup"><span data-stu-id="81dc4-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="81dc4-136">Pour installer l’agent, exécutez la commande ci-après dans une console PowerShell avec élévation de privilèges :</span><span class="sxs-lookup"><span data-stu-id="81dc4-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="81dc4-137">Cette opération installe l’agent avec les options par défaut.</span><span class="sxs-lookup"><span data-stu-id="81dc4-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="81dc4-138">L’installation s’effectue en arrière-plan et prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="81dc4-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="81dc4-139">Si vous ne spécifiez pas l’option */nu* , la fenêtre **Windows Update** s’ouvrira à la fin de l’installation pour rechercher des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="81dc4-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="81dc4-140">Une fois installé, l’agent apparaît dans la liste des programmes installés.</span><span class="sxs-lookup"><span data-stu-id="81dc4-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="81dc4-141">Pour afficher la liste des programmes installés, cliquez sur **Panneau de configuration** > **Programmes** > **Programmes et fonctionnalités**.</span><span class="sxs-lookup"><span data-stu-id="81dc4-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agent installé](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="81dc4-143">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="81dc4-143">Installation options</span></span>
<span data-ttu-id="81dc4-144">Pour afficher toutes les options disponibles via la ligne de commande, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81dc4-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="81dc4-145">Les options disponibles incluent :</span><span class="sxs-lookup"><span data-stu-id="81dc4-145">The available options include:</span></span>

| <span data-ttu-id="81dc4-146">Option</span><span class="sxs-lookup"><span data-stu-id="81dc4-146">Option</span></span> | <span data-ttu-id="81dc4-147">Détails</span><span class="sxs-lookup"><span data-stu-id="81dc4-147">Details</span></span> | <span data-ttu-id="81dc4-148">Default</span><span class="sxs-lookup"><span data-stu-id="81dc4-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="81dc4-149">/q</span><span class="sxs-lookup"><span data-stu-id="81dc4-149">/q</span></span> |<span data-ttu-id="81dc4-150">Installation silencieuse</span><span class="sxs-lookup"><span data-stu-id="81dc4-150">Quiet installation</span></span> |- |
| <span data-ttu-id="81dc4-151">/p:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="81dc4-151">/p:"location"</span></span> |<span data-ttu-id="81dc4-152">Chemin d’accès du dossier d’installation de l’agent de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="81dc4-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="81dc4-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="81dc4-154">/s:"emplacement"</span><span class="sxs-lookup"><span data-stu-id="81dc4-154">/s:"location"</span></span> |<span data-ttu-id="81dc4-155">Chemin d’accès du dossier de cache de l’agent de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="81dc4-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="81dc4-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="81dc4-157">/m</span><span class="sxs-lookup"><span data-stu-id="81dc4-157">/m</span></span> |<span data-ttu-id="81dc4-158">Abonnement à Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="81dc4-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="81dc4-159">/nu</span><span class="sxs-lookup"><span data-stu-id="81dc4-159">/nu</span></span> |<span data-ttu-id="81dc4-160">Ne pas vérifier les mises à jour une fois l’installation terminée</span><span class="sxs-lookup"><span data-stu-id="81dc4-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="81dc4-161">/d</span><span class="sxs-lookup"><span data-stu-id="81dc4-161">/d</span></span> |<span data-ttu-id="81dc4-162">Désinstalle l’agent Microsoft Azure Recovery Services</span><span class="sxs-lookup"><span data-stu-id="81dc4-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="81dc4-163">/ph</span><span class="sxs-lookup"><span data-stu-id="81dc4-163">/ph</span></span> |<span data-ttu-id="81dc4-164">Adresse de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="81dc4-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="81dc4-165">/po</span><span class="sxs-lookup"><span data-stu-id="81dc4-165">/po</span></span> |<span data-ttu-id="81dc4-166">Numéro de port de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="81dc4-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="81dc4-167">/pu</span><span class="sxs-lookup"><span data-stu-id="81dc4-167">/pu</span></span> |<span data-ttu-id="81dc4-168">Nom d’utilisateur de l’hôte proxy</span><span class="sxs-lookup"><span data-stu-id="81dc4-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="81dc4-169">/pw</span><span class="sxs-lookup"><span data-stu-id="81dc4-169">/pw</span></span> |<span data-ttu-id="81dc4-170">Mot de passe du proxy</span><span class="sxs-lookup"><span data-stu-id="81dc4-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="81dc4-171">Inscription auprès du service Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="81dc4-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="81dc4-172">Avant de pouvoir vous inscrire auprès du service Sauvegarde Azure, vous devez vous assurer que les [prérequis](backup-configure-vault.md) sont remplis.</span><span class="sxs-lookup"><span data-stu-id="81dc4-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="81dc4-173">Vous devez respecter les consignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="81dc4-173">You must:</span></span>

* <span data-ttu-id="81dc4-174">Avoir un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="81dc4-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="81dc4-175">Disposer d’un coffre de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="81dc4-175">Have a backup vault</span></span>

<span data-ttu-id="81dc4-176">Pour télécharger les informations d’identification du coffre, exécutez l’applet de commande **Get-AzureRMBackupVaultCredentials** dans une console Azure PowerShell, puis stockez ces informations dans un emplacement pratique, tel que *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="81dc4-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="81dc4-177">L’inscription de la machine auprès du coffre s’effectue l’aide de la cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="81dc4-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="81dc4-178">N’utilisez pas de chemins relatifs pour spécifier le fichier des informations d’identification du coffre.</span><span class="sxs-lookup"><span data-stu-id="81dc4-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="81dc4-179">Vous devez fournir un chemin absolu dans l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="81dc4-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="81dc4-180">Paramètres de mise en réseau</span><span class="sxs-lookup"><span data-stu-id="81dc4-180">Networking settings</span></span>
<span data-ttu-id="81dc4-181">Lorsque l’ordinateur Windows accède à Internet via un serveur proxy, les paramètres proxy peuvent également être fournis à l’agent.</span><span class="sxs-lookup"><span data-stu-id="81dc4-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="81dc4-182">Dans cet exemple, il n’y a aucun serveur proxy. Nous effaçons donc explicitement toutes informations concernant un proxy.</span><span class="sxs-lookup"><span data-stu-id="81dc4-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="81dc4-183">L’utilisation de la bande passante peut également être contrôlée avec les options ```work hour bandwidth``` et ```non-work hour bandwidth```, certains jours de la semaine.</span><span class="sxs-lookup"><span data-stu-id="81dc4-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="81dc4-184">La définition des détails sur le proxy et la bande passante s’effectue à l’aide de l’applet de commande [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) :</span><span class="sxs-lookup"><span data-stu-id="81dc4-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="81dc4-185">Paramètres de chiffrement</span><span class="sxs-lookup"><span data-stu-id="81dc4-185">Encryption settings</span></span>
<span data-ttu-id="81dc4-186">Les données sauvegardées envoyées à Sauvegarde Azure sont chiffrées pour garantir leur confidentialité.</span><span class="sxs-lookup"><span data-stu-id="81dc4-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="81dc4-187">Le mot de passe du chiffrement est le « mot de passe » permettant de déchiffrer les données lors de la restauration.</span><span class="sxs-lookup"><span data-stu-id="81dc4-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="81dc4-188">Conservez les informations de phrase secrète en lieu sûr après les avoir définies.</span><span class="sxs-lookup"><span data-stu-id="81dc4-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="81dc4-189">Vous ne pourrez pas restaurer les données à partir d’Azure sans ce mot de passe.</span><span class="sxs-lookup"><span data-stu-id="81dc4-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="81dc4-190">Sauvegarde des fichiers et dossiers</span><span class="sxs-lookup"><span data-stu-id="81dc4-190">Back up files and folders</span></span>
<span data-ttu-id="81dc4-191">Toutes les sauvegardes de serveurs et clients Windows vers Azure Backup sont régies par une stratégie.</span><span class="sxs-lookup"><span data-stu-id="81dc4-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="81dc4-192">Cette dernière comprend trois parties :</span><span class="sxs-lookup"><span data-stu-id="81dc4-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="81dc4-193">Une **planification de sauvegarde** qui spécifie quand les sauvegardes doivent être établies et synchronisées avec le service.</span><span class="sxs-lookup"><span data-stu-id="81dc4-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="81dc4-194">Une **planification de rétention** qui spécifie la durée de rétention des points de récupération dans Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="81dc4-195">Une **spécification d'inclusion/exclusion de fichier** qui dicte ce qui doit être sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="81dc4-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="81dc4-196">Dans ce document, comme nous automatisons la sauvegarde, nous supposons que rien n'a été configuré.</span><span class="sxs-lookup"><span data-stu-id="81dc4-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="81dc4-197">Nous commençons par créer une stratégie de sauvegarde en utilisant l’applet de commande [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="81dc4-198">À ce stade, la stratégie est vide et les autres applets de commande sont nécessaires pour définir les éléments qui seront inclus ou exclus, le moment auquel les sauvegardes s'exécuteront et leur emplacement de stockage.</span><span class="sxs-lookup"><span data-stu-id="81dc4-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="81dc4-199">Configuration de la planification de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="81dc4-199">Configuring the backup schedule</span></span>
<span data-ttu-id="81dc4-200">La première des 3 parties d'une stratégie est la planification de sauvegarde, qui est créée à l'aide de l’applet de commande [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="81dc4-201">La planification de sauvegarde définit le moment où les sauvegardes doivent être effectuées.</span><span class="sxs-lookup"><span data-stu-id="81dc4-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="81dc4-202">Lors de la création d'une planification, vous devez spécifier 2 paramètres d'entrée :</span><span class="sxs-lookup"><span data-stu-id="81dc4-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="81dc4-203">**jours de la semaine** où la sauvegarde doit s'exécuter.</span><span class="sxs-lookup"><span data-stu-id="81dc4-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="81dc4-204">Vous pouvez exécuter le travail de sauvegarde une seule journée ou tous les jours de la semaine, ou une combinaison des deux.</span><span class="sxs-lookup"><span data-stu-id="81dc4-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="81dc4-205">**heures** où la sauvegarde doit être exécutée.</span><span class="sxs-lookup"><span data-stu-id="81dc4-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="81dc4-206">Vous pouvez définir jusqu'à 3 différentes heures pour le déclenchement de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="81dc4-207">Par exemple, vous pouvez configurer une stratégie de sauvegarde qui s'exécute à 16 h 00 chaque samedi et chaque dimanche.</span><span class="sxs-lookup"><span data-stu-id="81dc4-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="81dc4-208">La planification de sauvegarde doit être associée à une stratégie à l'aide de l’applet de commande [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="81dc4-209">Configuration d'une stratégie de rétention</span><span class="sxs-lookup"><span data-stu-id="81dc4-209">Configuring a retention policy</span></span>
<span data-ttu-id="81dc4-210">La stratégie de rétention définit la durée de conservation des points de récupération créés à partir des travaux de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="81dc4-211">Lorsque vous créez une stratégie de rétention à l'aide de l’applet de commande [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) , vous pouvez spécifier le nombre de jours pendant lesquels les points de récupération de sauvegarde doivent être conservés avec Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="81dc4-212">L'exemple suivant définit une stratégie de rétention de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="81dc4-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="81dc4-213">La stratégie de rétention doit être associée à la stratégie principale à l'aide de l'applet de commande [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="81dc4-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="81dc4-214">Inclusion et exclusion des fichiers à sauvegarder</span><span class="sxs-lookup"><span data-stu-id="81dc4-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="81dc4-215">Un objet ```OBFileSpec``` définit les fichiers à inclure et à exclure d'une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="81dc4-216">Il s'agit d'un ensemble de règles qui définissent l'étendue des fichiers et dossiers protégés sur un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="81dc4-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="81dc4-217">Vous pouvez avoir de nombreuses règles d'inclusion ou d’exclusion en fonction de vos besoins, et les associer à une stratégie.</span><span class="sxs-lookup"><span data-stu-id="81dc4-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="81dc4-218">Lorsque vous créez un objet OBFileSpec, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="81dc4-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="81dc4-219">Spécifier les fichiers et dossiers à inclure</span><span class="sxs-lookup"><span data-stu-id="81dc4-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="81dc4-220">Spécifier les fichiers et dossiers à exclure</span><span class="sxs-lookup"><span data-stu-id="81dc4-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="81dc4-221">Indiquer la sauvegarde récursive des données dans un dossier (ou) indiquer si seuls les fichiers de niveau supérieur du dossier spécifié doivent être sauvegardés</span><span class="sxs-lookup"><span data-stu-id="81dc4-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="81dc4-222">Dans le dernier cas, l’opération est effectuée à l’aide de l'indicateur -NonRecursive dans la commande New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="81dc4-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="81dc4-223">Dans l'exemple ci-dessous, nous sauvegardons les volumes C: et D: et excluons les fichiers binaires de système d'exploitation dans le dossier Windows et tous les dossiers temporaires.</span><span class="sxs-lookup"><span data-stu-id="81dc4-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="81dc4-224">Pour cela, nous allons créer deux spécifications de fichiers à l'aide de l’applet de commande [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) : une pour l’inclusion et une pour l’exclusion.</span><span class="sxs-lookup"><span data-stu-id="81dc4-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="81dc4-225">Une fois que les spécifications de fichiers ont été créées, elles sont associées à la stratégie à l'aide de l’applet de commande [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="81dc4-226">Application de la stratégie</span><span class="sxs-lookup"><span data-stu-id="81dc4-226">Applying the policy</span></span>
<span data-ttu-id="81dc4-227">L'objet de stratégie est à présent complet. Il est associé à une planification de sauvegarde, à une stratégie de rétention et à une liste d’inclusion/exclusion de fichiers.</span><span class="sxs-lookup"><span data-stu-id="81dc4-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="81dc4-228">Cette stratégie peut maintenant être validée à des fins d’utilisation par Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="81dc4-229">Avant d’appliquer la stratégie que vous venez de créer, vérifiez qu’aucune stratégie de sauvegarde existante n’est associée au serveur à l’aide de l’applet de commande [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415).</span><span class="sxs-lookup"><span data-stu-id="81dc4-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="81dc4-230">Lors de la suppression de la stratégie, vous êtes invité à confirmer l'opération.</span><span class="sxs-lookup"><span data-stu-id="81dc4-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="81dc4-231">Pour ignorer la confirmation, utilisez l’indicateur ```-Confirm:$false``` avec l'applet de commande.</span><span class="sxs-lookup"><span data-stu-id="81dc4-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="81dc4-232">La validation de l'objet de stratégie s'effectue à l'aide de l’applet de commande [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="81dc4-233">Une confirmation vous est également demandée.</span><span class="sxs-lookup"><span data-stu-id="81dc4-233">This will also ask for confirmation.</span></span> <span data-ttu-id="81dc4-234">Pour ignorer la confirmation, utilisez l’indicateur ```-Confirm:$false``` avec l'applet de commande.</span><span class="sxs-lookup"><span data-stu-id="81dc4-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="81dc4-235">Vous pouvez afficher les détails de la stratégie de sauvegarde existante à l'aide de l’applet de commande [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="81dc4-236">Vous pouvez afficher plus de détails à l’aide de l’applet de commande [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) pour la planification de sauvegarde et de l’applet de commande [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) pour les stratégies de rétention.</span><span class="sxs-lookup"><span data-stu-id="81dc4-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="81dc4-237">Exécution d'une sauvegarde ad hoc</span><span class="sxs-lookup"><span data-stu-id="81dc4-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="81dc4-238">Une fois qu'une stratégie de sauvegarde a été définie, les sauvegardes ont lieu selon la planification indiquée.</span><span class="sxs-lookup"><span data-stu-id="81dc4-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="81dc4-239">Le déclenchement d'une sauvegarde ad hoc est également possible à l'aide de l’applet de commande [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="81dc4-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="81dc4-240">Restauration des données à partir de Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="81dc4-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="81dc4-241">Cette section vous guide tout au long des étapes d'automatisation de la récupération des données à partir de Sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="81dc4-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="81dc4-242">Cette opération implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="81dc4-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="81dc4-243">Sélection du volume source</span><span class="sxs-lookup"><span data-stu-id="81dc4-243">Pick the source volume</span></span>
2. <span data-ttu-id="81dc4-244">Choix d’un point de sauvegarde à restaurer</span><span class="sxs-lookup"><span data-stu-id="81dc4-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="81dc4-245">Choix d’un élément à restaurer</span><span class="sxs-lookup"><span data-stu-id="81dc4-245">Choose an item to restore</span></span>
4. <span data-ttu-id="81dc4-246">Déclenchement du processus de restauration</span><span class="sxs-lookup"><span data-stu-id="81dc4-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="81dc4-247">Sélection du volume source</span><span class="sxs-lookup"><span data-stu-id="81dc4-247">Picking the source volume</span></span>
<span data-ttu-id="81dc4-248">Pour restaurer un élément à partir de Sauvegarde Azure, vous devez d'abord identifier la source associée.</span><span class="sxs-lookup"><span data-stu-id="81dc4-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="81dc4-249">Étant donné que nous exécutons les commandes dans le contexte d'un serveur ou d’un client Windows, l'ordinateur est déjà identifié.</span><span class="sxs-lookup"><span data-stu-id="81dc4-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="81dc4-250">L'étape suivante pour identifier la source consiste à identifier le volume qui la contient.</span><span class="sxs-lookup"><span data-stu-id="81dc4-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="81dc4-251">Vous pouvez récupérer la liste des volumes ou des sources en cours de sauvegarde à partir de cet ordinateur en exécutant l’applet de commande [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="81dc4-252">Cette commande renvoie un tableau de toutes les sources sauvegardées à partir de ce serveur/client.</span><span class="sxs-lookup"><span data-stu-id="81dc4-252">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="81dc4-253">Choix d’un point de sauvegarde à restaurer</span><span class="sxs-lookup"><span data-stu-id="81dc4-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="81dc4-254">Vous pouvez récupérer la liste des points de sauvegarde en exécutant l’applet de commande [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) avec les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="81dc4-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="81dc4-255">Dans notre exemple, nous allons sélectionner le dernier point de sauvegarde du volume source *D:* et l'utiliser pour récupérer un fichier spécifique.</span><span class="sxs-lookup"><span data-stu-id="81dc4-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="81dc4-256">L'objet ```$rps``` est un tableau de points de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="81dc4-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="81dc4-257">Le premier élément est le point le plus récent et le Nième élément est le point le plus ancien.</span><span class="sxs-lookup"><span data-stu-id="81dc4-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="81dc4-258">Pour choisir le point le plus récent, nous allons utiliser ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="81dc4-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="81dc4-259">Choix d’un élément à restaurer</span><span class="sxs-lookup"><span data-stu-id="81dc4-259">Choosing an item to restore</span></span>
<span data-ttu-id="81dc4-260">Pour identifier le fichier ou dossier exact à restaurer, utilisez de manière récursive l’applet de commande [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="81dc4-261">De cette façon, la hiérarchie de dossiers est accessible uniquement à l'aide de ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="81dc4-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="81dc4-262">Dans cet exemple, si vous souhaitez restaurer le fichier *finances.xls*, nous pouvons le référencer à l’aide de l’objet ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="81dc4-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="81dc4-263">Vous pouvez également rechercher des éléments à restaurer à l'aide de l’applet de commande ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="81dc4-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="81dc4-264">Dans notre exemple, pour rechercher le fichier *finances.xls* , nous pouvons trouver le fichier en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81dc4-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="81dc4-265">Déclenchement du processus de restauration</span><span class="sxs-lookup"><span data-stu-id="81dc4-265">Triggering the restore process</span></span>
<span data-ttu-id="81dc4-266">Pour déclencher le processus de restauration, nous devons d'abord spécifier les options de récupération.</span><span class="sxs-lookup"><span data-stu-id="81dc4-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="81dc4-267">Pour ce faire, utilisez l’applet de commande [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="81dc4-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="81dc4-268">Dans le cadre de cet exemple, supposons que vous souhaitez restaurer les fichiers dans *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="81dc4-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="81dc4-269">Supposons également que vous souhaitez ignorer les fichiers qui existent déjà dans le dossier de destination *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="81dc4-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="81dc4-270">Pour créer une telle option de récupération, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81dc4-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="81dc4-271">Déclenchez à présent la restauration à l’aide de la commande [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) dans l’élément ```$item``` sélectionné à partir de la sortie de l’applet de commande ```Get-OBRecoverableItem``` :</span><span class="sxs-lookup"><span data-stu-id="81dc4-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="81dc4-272">Désinstallation de l’agent Azure Backup</span><span class="sxs-lookup"><span data-stu-id="81dc4-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="81dc4-273">La désinstallation de l’agent de sauvegarde Azure peut être effectuée à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="81dc4-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="81dc4-274">La désinstallation des fichiers binaires de l'agent de l'ordinateur a certaines conséquences à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="81dc4-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="81dc4-275">Elle supprime le filtre de fichier de l'ordinateur et le suivi des modifications est arrêté.</span><span class="sxs-lookup"><span data-stu-id="81dc4-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="81dc4-276">Toutes les informations de stratégie sont supprimées de l'ordinateur, mais elles continuent à être stockées dans le service.</span><span class="sxs-lookup"><span data-stu-id="81dc4-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="81dc4-277">Toutes les planifications de sauvegarde sont supprimées, et aucune autre sauvegarde n'est effectuée.</span><span class="sxs-lookup"><span data-stu-id="81dc4-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="81dc4-278">Cependant, les données stockées dans Azure sont conservées selon la stratégie de rétention que vous avez définie.</span><span class="sxs-lookup"><span data-stu-id="81dc4-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="81dc4-279">Les points plus anciens deviennent automatiquement obsolètes.</span><span class="sxs-lookup"><span data-stu-id="81dc4-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="81dc4-280">Gestion à distance</span><span class="sxs-lookup"><span data-stu-id="81dc4-280">Remote management</span></span>
<span data-ttu-id="81dc4-281">L’intégralité de la gestion concernant l’agent de sauvegarde Azure, les stratégies et les sources de données peut être effectuée à distance par le biais de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81dc4-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="81dc4-282">L’ordinateur qui sera géré à distance doit être correctement préparé.</span><span class="sxs-lookup"><span data-stu-id="81dc4-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="81dc4-283">Par défaut, le service WinRM est configuré pour un démarrage manuel.</span><span class="sxs-lookup"><span data-stu-id="81dc4-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="81dc4-284">Le type de démarrage doit être défini sur *Automatique* et le service devrait être démarré.</span><span class="sxs-lookup"><span data-stu-id="81dc4-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="81dc4-285">Pour vérifier que le service WinRM est exécuté, la valeur de la propriété État devrait être défini sur *En cours d’exécution*.</span><span class="sxs-lookup"><span data-stu-id="81dc4-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="81dc4-286">PowerShell doit être configuré pour la communication à distance.</span><span class="sxs-lookup"><span data-stu-id="81dc4-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="81dc4-287">L’ordinateur peut maintenant être géré à distance, en commençant par l’installation de l’agent.</span><span class="sxs-lookup"><span data-stu-id="81dc4-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="81dc4-288">Par exemple, le script suivant copie et installe l’agent sur l’ordinateur distant.</span><span class="sxs-lookup"><span data-stu-id="81dc4-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="81dc4-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="81dc4-289">Next steps</span></span>
<span data-ttu-id="81dc4-290">Pour plus d’informations sur Sauvegarde Azure pour client/serveur Windows, consultez</span><span class="sxs-lookup"><span data-stu-id="81dc4-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="81dc4-291">Présentation de Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="81dc4-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="81dc4-292">Sauvegarder des serveurs Windows</span><span class="sxs-lookup"><span data-stu-id="81dc4-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
