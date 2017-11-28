---
title: Installation sans assistance du Serveur de sauvegarde Azure v2 | Microsoft Docs
description: "Utilisez un script PowerShell pour installer sans assistance le Serveur de sauvegarde Azure v2. Ce type d’installation est également appelé « installation silencieuse »."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="7c1db-104">Effectuer une installation sans assistance du Serveur de sauvegarde Azure v2</span><span class="sxs-lookup"><span data-stu-id="7c1db-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="7c1db-105">Découvrez comment effectuer une installation sans assistance du Serveur de sauvegarde Azure v2.</span><span class="sxs-lookup"><span data-stu-id="7c1db-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="7c1db-106">Ces étapes ne s’appliquent pas si vous installez le Serveur de sauvegarde Azure v1.</span><span class="sxs-lookup"><span data-stu-id="7c1db-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="7c1db-107">Installer le Serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="7c1db-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="7c1db-108">Sur le serveur hébergeant le Serveur de sauvegarde Azure v2, créez un fichier texte</span><span class="sxs-lookup"><span data-stu-id="7c1db-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="7c1db-109">(vous pouvez créer le fichier dans Bloc-notes ou dans un autre éditeur de texte). Enregistrez le fichier sous MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="7c1db-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="7c1db-110">Collez le code suivant dans le fichier MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="7c1db-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="7c1db-111">Remplacez le texte entre crochets (\< \>) par des valeurs de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="7c1db-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="7c1db-112">Voici un exemple de texte :</span><span class="sxs-lookup"><span data-stu-id="7c1db-112">The following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="7c1db-113">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="7c1db-113">Save the file.</span></span> <span data-ttu-id="7c1db-114">Ensuite, à une invite de commandes avec élévation de privilèges, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7c1db-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="7c1db-115">Vous pouvez utiliser les indicateurs suivants pour l’installation :</span><span class="sxs-lookup"><span data-stu-id="7c1db-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="7c1db-116">
**/f** : chemin d’accès du fichier .ini</span><span class="sxs-lookup"><span data-stu-id="7c1db-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="7c1db-117">
**/l** : chemin d’accès du journal</span><span class="sxs-lookup"><span data-stu-id="7c1db-117">
**/l**: Log path</span></span></br><span data-ttu-id="7c1db-118">
**/i** : chemin d’installation</span><span class="sxs-lookup"><span data-stu-id="7c1db-118">
**/i**: Installation path</span></span></br><span data-ttu-id="7c1db-119">
**/x** : chemin de désinstallation</span><span class="sxs-lookup"><span data-stu-id="7c1db-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="7c1db-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7c1db-120">Next steps</span></span>
<span data-ttu-id="7c1db-121">Après avoir installé le Serveur de sauvegarde, apprenez à préparer votre serveur ou commencez à protéger une charge de travail.</span><span class="sxs-lookup"><span data-stu-id="7c1db-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="7c1db-122">Préparer les charges de travail du Serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="7c1db-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="7c1db-123">Utiliser le Serveur de sauvegarde pour sauvegarder un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="7c1db-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="7c1db-124">Utiliser le serveur de sauvegarde pour sauvegarder SQL Server</span><span class="sxs-lookup"><span data-stu-id="7c1db-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="7c1db-125">Ajouter un stockage de sauvegarde moderne au Serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="7c1db-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
