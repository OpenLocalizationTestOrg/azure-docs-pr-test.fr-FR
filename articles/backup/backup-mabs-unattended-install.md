---
title: "installation d’aaaSilent d’Azure Backup Server v2 | Documents Microsoft"
description: "Utilisez un toosilently de script PowerShell installer Azure Backup Server v2. Ce type d’installation est également appelé « installation silencieuse »."
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
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="22ceb-104">Effectuer une installation sans assistance du Serveur de sauvegarde Azure v2</span><span class="sxs-lookup"><span data-stu-id="22ceb-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="22ceb-105">Découvrez comment toorun une installation sans assistance d’Azure Backup Server v2.</span><span class="sxs-lookup"><span data-stu-id="22ceb-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="22ceb-106">Ces étapes ne s’appliquent pas si vous installez le Serveur de sauvegarde Azure v1.</span><span class="sxs-lookup"><span data-stu-id="22ceb-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="22ceb-107">Installer le Serveur de sauvegarde v2</span><span class="sxs-lookup"><span data-stu-id="22ceb-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="22ceb-108">Sur le serveur hello qui héberge le serveur de sauvegarde Azure v2, créez un fichier texte.</span><span class="sxs-lookup"><span data-stu-id="22ceb-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="22ceb-109">(Vous pouvez créer hello fichier dans le bloc-notes ou dans le texte d’un autre éditeur.) Enregistrez le fichier de hello sous MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="22ceb-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="22ceb-110">Collez hello suivant de code dans un fichier MABSSetup.ini hello.</span><span class="sxs-lookup"><span data-stu-id="22ceb-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="22ceb-111">Remplacer du texte hello hello crochets (\< \>) avec des valeurs à partir de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="22ceb-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="22ceb-112">Hello suivant le texte est un exemple :</span><span class="sxs-lookup"><span data-stu-id="22ceb-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="22ceb-113">Enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="22ceb-113">Save hello file.</span></span> <span data-ttu-id="22ceb-114">Ensuite, à une invite de commandes avec élévation de privilèges sur le serveur d’installation Bonjour, entrez cette commande :</span><span class="sxs-lookup"><span data-stu-id="22ceb-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="22ceb-115">Vous pouvez utiliser ces indicateurs pour l’installation de hello :</span><span class="sxs-lookup"><span data-stu-id="22ceb-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="22ceb-116">
**/f** : chemin d’accès du fichier .ini</span><span class="sxs-lookup"><span data-stu-id="22ceb-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="22ceb-117">
**/l** : chemin d’accès du journal</span><span class="sxs-lookup"><span data-stu-id="22ceb-117">
**/l**: Log path</span></span></br><span data-ttu-id="22ceb-118">
**/i** : chemin d’installation</span><span class="sxs-lookup"><span data-stu-id="22ceb-118">
**/i**: Installation path</span></span></br><span data-ttu-id="22ceb-119">
**/x** : chemin de désinstallation</span><span class="sxs-lookup"><span data-stu-id="22ceb-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="22ceb-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="22ceb-120">Next steps</span></span>
<span data-ttu-id="22ceb-121">Après avoir installé le serveur de sauvegarde, découvrez comment tooprepare votre serveur, ou pour commencer à protéger une charge de travail.</span><span class="sxs-lookup"><span data-stu-id="22ceb-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="22ceb-122">Préparer les charges de travail du serveur de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="22ceb-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="22ceb-123">Utilisez tooback du serveur de sauvegarde d’un serveur VMware</span><span class="sxs-lookup"><span data-stu-id="22ceb-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="22ceb-124">Utilisez tooback de sauvegarde du serveur SQL Server</span><span class="sxs-lookup"><span data-stu-id="22ceb-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="22ceb-125">Ajouter le stockage de sauvegarde moderne tooBackup Server</span><span class="sxs-lookup"><span data-stu-id="22ceb-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
