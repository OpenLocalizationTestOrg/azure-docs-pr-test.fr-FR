---
title: " Gérer un serveur de traitement de montée en puissance parallèle dans Azure Site Recovery | Microsoft Docs"
description: "Cet article décrit comment tooset configurer et gérer un serveur de traitement de montée en puissance parallèle dans Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a>Gérer un serveur de traitement de montée en puissance parallèle

Serveur de traitement de montée en puissance parallèle agit en tant que coordinateur pour un transfert de données entre les services de récupération de Site hello et votre infrastructure locale. Cet article explique comment installer, configurer et gérer un serveur de traitement de montée en puissance parallèle.

## <a name="prerequisites"></a>Composants requis
Hello Voici hello recommandé de matériel, logiciels et tooset de configuration requise de réseau d’un serveur de processus de montée en puissance parallèle.

> [!NOTE]
> [Planification de la capacité](site-recovery-capacity-planner.md) est un tooensure étape importante déployer hello serveur de traitement de montée en puissance parallèle avec une configuration qui convient le mieux vos exigences de charge. En savoir plus sur les [caractéristiques de mise à l’échelle pour un serveur de traitement de montée en puissance parallèle](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a>Téléchargement du logiciel de serveur de traitement de montée en puissance parallèle hello
1. Ouvrez une session toohello tooyour portal et parcourir Azure coffre Recovery Services.
2. Parcourir trop**Infrastructure Site Recovery** > **serveurs de Configuration** (sous VMware pour les & ordinateurs physiques).
3. Sélectionnez votre toodrill de serveur de configuration vers le bas dans la page des détails du serveur de configuration hello.
4. Cliquez sur hello **+ serveur de processus** bouton.
5. Bonjour **serveur ajouter** page, sélectionnez **une montée en puissance de déployer un serveur de processus locale** option hello **choisir où vous souhaitez toodeploy votre serveur de processus** liste déroulante.

  ![Page Ajouter des serveurs](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. Cliquez sur hello **téléchargement hello installation unifié de Microsoft Azure Site Recovery** lien toodownload hello version la plus récente de l’installation du serveur de processus hello montée en puissance parallèle.

  > [!WARNING]
  Hello version de votre serveur de traitement de montée en puissance parallèle doit être égale tooor inférieur à la version du serveur de Configuration hello en cours d’exécution dans votre environnement. Un moyen simple tooensure version de compatibilité est toouse hello mêmes bits du programme d’installation que vous avez récemment utilisé tooinstall/mettre à jour votre serveur de Configuration.

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a>Installation et inscription d’un serveur de traitement de montée en puissance parallèle à partir de l’interface graphique utilisateur
Si vous avez tooscale votre déploiement au-delà de 200 machines sources, ou un plan quotidien total évolution du taux de plus de 2 To, vous devez le volume de trafic de processus supplémentaire serveurs toohandle hello.

Vérifiez hello [dimensionner des recommandations pour les serveurs de processus](#size-recommendations-for-the-process-server), puis suivez ces tooset obtenir des instructions de configuration de serveur de processus hello. Après avoir configuré le serveur de hello, vous migrez source machines toouse il.

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a>Installation et inscription d’un serveur de traitement de montée en puissance parallèle à l’aide de la ligne de commande

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a>Exemple d’utilisation
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a>Arguments de la ligne de commande du programme d’installation du serveur de traitement de montée en puissance parallèle.
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a>Créer un fichier de configuration des paramètres de proxy
Le paramètre ProxySettingsFilePath prend un fichier en tant qu’entrée. Créer un fichier à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre ProxySettingsFilePath d’entrée.
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a>Modification des paramètres de proxy pour le serveur de traitement de montée en puissance parallèle
1. Connectez-vous à votre serveur de traitement de montée en puissance parallèle.
2. Ouvrez une fenêtre de commandes PowerShell administrateur.
3. Exécutez hello commande suivante
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. Ensuite parcourir le répertoire de toohello **%PROGRAMDATA%\ASR\Agent** et hello exécution de commande suivante
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a>Réinscription d’un serveur de traitement de montée en puissance parallèle
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* Ouvrez ensuite une invite de commandes administrateur.
* Parcourir le répertoire de toohello **%PROGRAMDATA%\ASR\Agent** et exécutez la commande hello

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a>Mise à niveau d’un serveur de traitement de montée en puissance parallèle
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a>Désaffectation d’un serveur de traitement de montée en puissance parallèle
1. Assurez-vous que :
  - État de la connexion du serveur de configuration affiche sous la forme **connecté** Bonjour portail Azure
  - Serveur de processus est toujours en mesure de toocommunicate avec le serveur de Configuration hello.
2. Ouvrez une session dans le serveur de processus toohello en tant qu’administrateur
3. Ouvrez le Panneau de configuration > Programme > Désinstaller des programmes
4. Désinstaller les programmes hello dans la séquence de hello étant donné ce qui suit :
  * Serveur de configuration Microsoft Azure Site Recovery/Serveur de traitement
  * Dépendances du serveur de configuration Microsoft Azure Site Recovery
  * Agent Microsoft Azure Recovery Services

Il peut prendre too15-up pour tooreflect de suppression de serveur de processus hello Bonjour portail Azure.

  > [!NOTE]
  Si le serveur de processus hello est toocommunicate impossible avec hello serveur de Configuration (état de la connexion dans le portail est déconnecté), vous devez toofollow hello suivant les étapes toopurge de hello serveur de Configuration.

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a>Désinscription d’un serveur de traitement de montée en puissance parallèle déconnecté d’un serveur de configuration

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a>Exigences de dimensionnement pour un serveur de traitement de montée en puissance parallèle

| **Serveur de traitement supplémentaire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées** |
| --- | --- | --- | --- |
|4 processeurs virtuels (2 sockets * 2 cœurs @ 2,5 GHz), 8 Go de mémoire |300 Go |250 Go ou moins |Répliquez 85 machines ou moins. |
|8 processeurs virtuels (2 sockets * 4 cœurs @ 2,5 GHz), 12 Go de mémoire |600 Go |250 Go too1 to |Répliquez entre 85 et 150 machines. |
|12 processeurs virtuels (2 sockets * 6 cœurs @ 2,5 GHz), 24 Go de mémoire |1 To |1 to too2 to |Répliquez entre 150 et 225 machines. |
