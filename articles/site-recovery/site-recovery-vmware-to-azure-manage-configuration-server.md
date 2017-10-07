---
title: " Gérer un serveur de configuration dans Azure Site Recovery | Microsoft Docs"
description: "Cet article décrit comment tooset et gérer un serveur de Configuration."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a>Gérer un serveur de configuration

Configuration serveur agit en tant que coordinateur entre les services de récupération de Site de hello et votre infrastructure locale. Cet article décrit comment vous pouvez configurer, configurer et gérer hello serveur de Configuration.

## <a name="prerequisites"></a>Composants requis
Hello Voici tooset configuration requise de réseau d’un serveur de Configuration, logicielle et matérielle hello.

> [!NOTE]
> [Planification de la capacité](site-recovery-capacity-planner.md) est un tooensure étape importante déployer hello avec une configuration de serveur de Configuration qui convient le mieux vos exigences de charge. Pour en savoir plus, consultez la section [Exigences de dimensionnement d’un serveur de configuration](#sizing-requirements-for-a-configuration-server).

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a>Téléchargement du logiciel de serveur de Configuration hello
1. Ouvrez une session toohello tooyour portal et parcourir Azure coffre Recovery Services.
2. Parcourir trop**Infrastructure Site Recovery** > **serveurs de Configuration** (sous VMware pour les & ordinateurs physiques).

  ![Page Ajouter des serveurs](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. Cliquez sur hello **+ serveurs** bouton.
4. Sur hello **ajouter un serveur** , cliquez sur la clé d’inscription de hello téléchargement bouton toodownload hello. Vous avez besoin de cette clé pendant hello Configuration Server installation tooregister avec le service Azure Site Recovery.
5. Cliquez sur hello **téléchargement hello installation unifié de Microsoft Azure Site Recovery** lien toodownload hello version la plus récente du serveur de Configuration de hello.

  ![Page de téléchargement](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  Dernière version du serveur de Configuration de hello peut être téléchargée directement à partir de [page de téléchargement Microsoft Download Center](http://aka.ms/unifiedsetup)

## <a name="installing-and-registering-a-configuration-server-from-gui"></a>Installation et inscription d’un serveur de configuration à partir de l’interface graphique utilisateur
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a>Installation et inscription d’un serveur de configuration à l’aide de la ligne de commande

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a>Exemple d’utilisation
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a>Arguments de la ligne de commande du programme d’installation du serveur de configuration
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a>Créer un fichier d’informations d’identification de MySql
Le paramètre MySQLCredsFilePath prend un fichier en tant qu’entrée. Créer un fichier hello à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre d’entrée de MySQLCredsFilePath.
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a>Créer un fichier de configuration des paramètres de proxy
Le paramètre ProxySettingsFilePath prend un fichier en tant qu’entrée. Créer un fichier hello à l’aide de hello suivante, mettre en forme et passez-le en tant que paramètre d’entrée de ProxySettingsFilePath.

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a>Modification des paramètres de proxy du serveur de configuration
1. Connexion tooyour serveur de Configuration.
2. Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre.
3. Cliquez sur hello **inscription du coffre** onglet.
4. Télécharger un nouveau fichier d’inscription du coffre à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. Fournissez les détails du nouveau serveur Proxy de hello et cliquez sur hello **inscrire** bouton.
6. Ouvrez une fenêtre de commandes PowerShell administrateur.
7. Exécutez hello commande suivante
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  Si vous avez des serveurs de traitement de la montée en puissance parallèle attaché toothis serveur de Configuration, vous devez trop[corriger les paramètres de proxy hello sur tous les serveurs de processus de montée en puissance parallèle hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) dans votre déploiement.

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a>Réinscrire sur un serveur de Configuration avec hello même coffre Recovery Services
  1. Connexion tooyour serveur de Configuration.
  2. Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre bureau.
  3. Cliquez sur hello **inscription du coffre** onglet.
  4. Télécharger un nouveau fichier d’inscription à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.
        ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
  5. Fournir des détails du serveur Proxy hello et cliquez sur hello **inscrire** bouton.  
  6. Ouvrez une fenêtre de commandes PowerShell administrateur.
  7. Exécutez hello commande suivante

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  Si vous avez des serveurs de traitement de la montée en puissance parallèle attaché toothis serveur de Configuration, vous devez trop[réinscrire tous les serveurs de traitement de montée en puissance parallèle de hello](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) dans votre déploiement.

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a>Inscription d’un serveur de configuration auprès d’un autre coffre Recovery Services.
1. Connexion tooyour serveur de Configuration.
2. à partir d’une invite de commandes administrateur, exécutez la commande hello

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. Lancez cspsconfigtool.exe hello à l’aide du raccourci de hello sur votre.
4. Cliquez sur hello **inscription du coffre** onglet.
5. Télécharger un nouveau fichier d’inscription à partir du portail de hello et fournit en tant qu’outil de toohello d’entrée.

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. Fournir des détails du serveur Proxy hello et cliquez sur hello **inscrire** bouton.  
7. Ouvrez une fenêtre de commandes PowerShell administrateur.
8. Exécutez hello commande suivante
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a>Désaffectation d’un serveur de configuration
Vérifiez les éléments suivants de hello avant de commencer la mise hors service de votre serveur de Configuration.
1. Désactivez la protection de toutes les machines virtuelles relevant de ce serveur de configuration.
2. Dissociez toutes les stratégies de réplication à partir de hello serveur de Configuration.
3. Supprimer tous les hôtes de serveurs/vSphere vCenter qui sont associé toohello serveur de Configuration.

### <a name="delete-hello-configuration-server-from-azure-portal"></a>Supprimer hello serveur de Configuration à partir du portail Azure
1. Dans le portail Azure, accédez trop**Infrastructure Site Recovery** > **serveurs de Configuration** à partir du menu de coffre hello.
2. Cliquez sur hello serveur de Configuration que vous souhaitez toodecommission.
3. Dans la page des détails du serveur de Configuration hello, cliquez sur Supprimer hello.

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. Cliquez sur **Oui** tooconfirm la suppression hello du serveur de hello.

  >[!WARNING]
  Si vous disposez d’ordinateurs virtuels, les stratégies de réplication ou les hôtes de serveurs/vSphere vCenter associés à ce serveur de Configuration, vous ne pouvez pas supprimer les serveur hello. Supprimer ces entités avant d’essayer de coffre de hello toodelete.

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a>Désinstaller le logiciel de serveur de Configuration hello et ses dépendances
  > [!TIP]
  Si vous envisagez de nouveau tooreuse hello serveur de Configuration avec Azure Site Recovery, vous pouvez ignorer toostep 4 directement

1. Ouvrez une session sur le serveur de Configuration de toohello en tant qu’administrateur.
2. Ouvrez le Panneau de configuration > Programme > Désinstaller des programmes
3. Désinstaller des programmes hello Bonjour suivant séquence :
  * Agent Microsoft Azure Recovery Services
  * Service Mobilité/Serveur cible maître Microsoft Azure Site Recovery
  * Fournisseur Microsoft Azure Site Recovery
  * Serveur de configuration/Serveur de processus Microsoft Azure Site Recovery
  * Dépendances du serveur de configuration Microsoft Azure Site Recovery
  * MySQL Server 5.5
4. Exécutez hello suivant de commande à partir d’et invite de commandes d’administration.
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a>Renouveler les certificats SSL du serveur de configuration
Hello Configuration serveur possède un serveur Web intégré, qui orchestre les activités hello Hello Service mobilité, serveurs de traitement, et serveurs cibles maîtres connecté toohello serveur de Configuration. serveur Web du serveur de Configuration Hello utilise un tooauthenticate du certificat SSL à ses clients. Ce certificat a un délai d’expiration de trois ans et peut être renouvelé à tout moment à l’aide de hello suivant de méthode :

> [!WARNING]
L’expiration du certificat peut être appliquée uniquement sur les versions 9.4.XXXX.X ou supérieures. Mettre à niveau tous les composants d’Azure Site Recovery hello (serveur de Configuration, serveur de processus, serveur cible maître, Service mobilité) avant de démarrer le flux de travail hello renouveler les certificats.

1. On hello portail Azure, accédez tooyour coffre > Infrastructure Site Recovery > serveur de Configuration.
2. Cliquez sur le serveur de Configuration pour lesquels vous avez besoin toorenew hello hello certificat SSL.
3. Sous hello l’intégrité du serveur de Configuration, vous pouvez voir la date d’expiration hello pour hello certificat SSL.
4. Renouveler les certificats de hello en cliquant sur hello **renouveler les certificats** action, comme indiqué dans hello suivant image :

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a>Avertissement relatif à l’expiration du certificat SSL

> [!NOTE]
Hello validité du certificat SSL pour toutes les installations qui ont eu lieu avant mai 2016 a été définie tooone année. vous avez démarré l’affichage des notifications d’expiration de certificat s’affiche dans hello portail Azure.

1. Si le certificat SSL du serveur de Configuration hello va tooexpire Bonjour deux mois, service de hello démarre la notification des utilisateurs via le portail Azure Bonjour par courrier électronique (vous devez toobe abonné tooAzure Site Recovery notifications). Commencer à voir une bannière de notification sur la page de ressource du coffre hello.

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. Cliquez sur hello bannière tooget plus d’informations sur l’expiration du certificat hello.

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  Si un bouton **Mettre à niveau maintenant** s’affiche à la place d’un bouton **Renouveler maintenant**, Cela signifie qu’il n’y a certains composants de votre environnement qui n’ont pas encore été mis à niveau too9.4.xxxx.x ou versions ultérieures.

## <a name="sizing-requirements-for-a-configuration-server"></a>Exigences de dimensionnement d’un serveur de configuration

| **UC** | **Mémoire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées** |
| --- | --- | --- | --- | --- |
| 8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 GHz) |16 Go |300 Go |500 Go ou moins |Répliquez moins de 100 machines. |
| 12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz) |18 Go |600 Go |500 Go too1 to |Répliquez entre 100 et 150 machines. |
| 16 processeurs virtuels (2 sockets * 8 cœurs à 2,5 GHz) |32 Go |1 To |1 to too2 to |Répliquez entre 150 et 200 machines. |

  >[!TIP]
  Si vos données quotidiennes pendant dépasse 2 To, ou vous envisagez de tooreplicate plus de 200 machines virtuelles, il est recommandé de toodeploy processus supplémentaire serveurs tooload solde hello le trafic de réplication. Découvrez comment les serveurs de toodeploy processus de montée en puissance parallèle.


## <a name="common-issues"></a>Problèmes courants
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
