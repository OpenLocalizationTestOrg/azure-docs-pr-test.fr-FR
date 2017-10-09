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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Effectuer une installation sans assistance du Serveur de sauvegarde Azure v2

Découvrez comment toorun une installation sans assistance d’Azure Backup Server v2. 

Ces étapes ne s’appliquent pas si vous installez le Serveur de sauvegarde Azure v1.

## <a name="install-backup-server-v2"></a>Installer le Serveur de sauvegarde v2

1. Sur le serveur hello qui héberge le serveur de sauvegarde Azure v2, créez un fichier texte. (Vous pouvez créer hello fichier dans le bloc-notes ou dans le texte d’un autre éditeur.) Enregistrez le fichier de hello sous MABSSetup.ini. 

2. Collez hello suivant de code dans un fichier MABSSetup.ini hello. Remplacer du texte hello hello crochets (\< \>) avec des valeurs à partir de votre environnement. Hello suivant le texte est un exemple :

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

3. Enregistrez le fichier de hello. Ensuite, à une invite de commandes avec élévation de privilèges sur le serveur d’installation Bonjour, entrez cette commande :

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Vous pouvez utiliser ces indicateurs pour l’installation de hello :</br>
**/f** : chemin d’accès du fichier .ini</br>
**/l** : chemin d’accès du journal</br>
**/i** : chemin d’installation</br>
**/x** : chemin de désinstallation</br>

## <a name="next-steps"></a>Étapes suivantes
Après avoir installé le serveur de sauvegarde, découvrez comment tooprepare votre serveur, ou pour commencer à protéger une charge de travail.

- [Préparer les charges de travail du serveur de sauvegarde](backup-azure-microsoft-azure-backup.md)
- [Utilisez tooback du serveur de sauvegarde d’un serveur VMware](backup-azure-backup-server-vmware.md)
- [Utilisez tooback de sauvegarde du serveur SQL Server](backup-azure-sql-mabs.md)
- [Ajouter le stockage de sauvegarde moderne tooBackup Server](backup-mabs-add-storage.md)
