---
title: aaaAzure chiffrement de disque pour Windows et les machines virtuelles IaaS Linux | Documents Microsoft
description: "Cet article offre une vue d’ensemble de Microsoft Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Chiffrement de disque Azure pour des machines virtuelles Windows et Linux IaaS
Microsoft Azure est tooensuring engage souveraineté de données de la confidentialité de vos données et vous permet de toocontrol votre Azure hébergé données via une gamme de technologies avancées tooencrypt, contrôler et gérer des clés de chiffrement, l’accès d’audit et de contrôle de données. Ainsi, les clients Azure hello flexibilité toochoose hello solution qui répond le mieux à leurs besoins. Dans ce document, nous allons tooa solution de nouvelle technologie « Chiffrement de disque Azure pour Windows et de Linux IaaS VM » toohelp protéger et sauvegarder votre toomeet données votre organisation engagements de conformité et de sécurité. papier de Hello fournit des instructions détaillées sur la fonctionnalités de chiffrement toouse hello disque Azure, y compris hello prise en charge des scénarios et des expériences utilisateur hello.

> [!NOTE]
> Certaines recommandations peuvent entraîner une augmentation de l’utilisation des données, des réseaux ou des ressources de calcul débouchant sur des coûts de licence ou d’abonnement supplémentaires.

## <a name="overview"></a>Vue d’ensemble
Azure Disk Encryption est une nouvelle fonctionnalité qui vous permet de chiffrer vos disques de machine virtuelle IaaS Windows et Linux. Le chiffrement des disques Azure s’appuie sur la norme industrielle de hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) la fonctionnalité de Windows et hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) fonctionnalité de chiffrement de volume tooprovide Linux pour hello du système d’exploitation et des disques de données hello. solution de Hello est intégrée à [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp contrôler et de gérer les clés de chiffrement de disque hello et les secrets dans votre abonnement de coffre de clés. solution de Hello garantit également que toutes les données sur les disques de machine virtuelle hello sont chiffrées au repos dans votre stockage Azure.

Azure Disk Encryption pour les machines virtuelles Iaas Windows et Linux est désormais à la **disponibilité générale** dans toutes les régions publiques Azure et les régions AzureGov pour les machines virtuelles standard et les machines virtuelles avec Stockage Premium.

### <a name="encryption-scenarios"></a>Scénarios de chiffrement
Hello solutions de chiffrement de disque Azure prend en charge hello client les scénarios suivants :

* Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels déjà chiffrés et de clés de chiffrement
* Activer le chiffrement sur les nouvelles machines virtuelles IaaS de créé à partir d’images de la galerie Azure hello pris en charge
* Activation du chiffrement sur des machines virtuelles IaaS existantes et fonctionnant dans Azure
* Désactivation du chiffrement sur les machines virtuelles IaaS Windows.
* Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux
* Activation du chiffrement des machines virtuelles avec disque managé
* Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante
* Sauvegarde et restauration de machines virtuelles chiffrées avec une clé de chiffrement de clé

solution de Hello prend en charge hello les scénarios suivants pour les machines virtuelles IaaS lorsqu’ils sont activés dans Microsoft Azure :

* Prise en main d’Azure Key Vault
* Machines virtuelles de niveau standard : [Machines virtuelles IaaS des séries A, D, DS, G, GS, F, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Activer le chiffrement sur Windows et les machines virtuelles IaaS Linux et machines virtuelles de disque géré à partir de hello pris en charge les images de la galerie Azure
* Désactivation du chiffrement des lecteurs de système d’exploitation et de données pour des machines virtuelles IaaS Windows et des machines virtuelles avec disque managé
* Désactivation du chiffrement des lecteurs de données pour des machines virtuelles IaaS Linux et des machines virtuelles avec disque managé
* Activation du chiffrement sur les machines virtuelles IaaS exécutant le système d’exploitation du client Windows.
* Activation du chiffrement sur les volumes avec chemins d’accès de montage.
* Activation du chiffrement sur des machines virtuelles Linux configurées avec une agrégation de disques (RAID) utilisant mdadm
* Activation du chiffrement sur des machines virtuelles Linux en utilisant LVM pour les disques de données
* Activation du chiffrement sur les machines virtuelles Windows configurées avec des espaces de stockage
* Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage non Premium chiffrée existante
* Toutes les régions publiques Azure et AzureGov sont prises en charge

solution de Hello ne prend pas en charge hello suivant des scénarios, les fonctionnalités et technologies :

* Machines virtuelles IaaS de niveau de base
* Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux
* La désactivation du chiffrement sur un lecteur de données si hello lecteur du système d’exploitation est chiffré pour les machines virtuelles Iaas Linux
* Machines virtuelles IaaS qui sont créés à l’aide de la méthode de création VM hello classique
* L’activation du chiffrement sur les images client personnalisées de machines virtuelles Iaas Windows et Linux n’est PAS prise en charge. L’activation du chiffrement sur des disques de système d’exploitation LVM Linux n’est pas prise en charge actuellement. Elles seront bientôt prise en charge.
* Intégration à votre service de gestion de clés local
* Azure Files (système de partage de fichiers), NFS (Network File System), volumes dynamiques et machines virtuelles Windows configurées avec des systèmes RAID logiciels
* Sauvegarde et restauration de machines virtuelles chiffrées sans clé de chiffrement de clé
* Mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée existante

> [!NOTE]
> Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello. Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK. KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle. Cette prise en charge sera bientôt disponible.
> La mise à jour des paramètres de chiffrement d’une machine virtuelle de stockage Premium chiffrée ne sont pas pris en charge. Cette prise en charge sera bientôt disponible.

### <a name="encryption-features"></a>Fonctionnalités de chiffrement
Lorsque vous activez et déployez le chiffrement de disque Azure pour les machines virtuelles Azure IaaS, hello fonctionnalités suivantes sont activées, selon la configuration de hello fournie :

* Chiffrement de volume de démarrage du système d’exploitation de hello volume tooprotect hello au repos dans votre espace de stockage
* Chiffrement des données des volumes tooprotect hello des volumes de données au repos dans votre espace de stockage
* La désactivation du chiffrement sur hello du système d’exploitation et les données des disques pour les machines virtuelles IaaS Windows
* La désactivation du chiffrement sur les données de salutation disques pour les machines virtuelles IaaS Linux (uniquement si le lecteur de système d’exploitation n’est pas chiffrée)
* Protection des clés de chiffrement hello et les clés secrètes dans votre abonnement de coffre de clés
* Rapports d’état de chiffrement hello Hello chiffré IaaS VM
* Suppression des paramètres de configuration de chiffrement de disque à partir de la machine virtuelle de hello IaaS
* Sauvegarde et restauration de machines virtuelles de chiffrées à l’aide du service de sauvegarde Azure hello

> [!NOTE]
> Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello. Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK. KEK est un paramètre facultatif permettant d’activer le chiffrement d’une machine virtuelle.

La solution Azure Disk Encryption pour les machines virtuelles IaaS Windows et Linux comprend :

* extension de chiffrement de disque Hello pour Windows.
* extension de chiffrement de disque Hello pour Linux.
* applets de commande PowerShell de chiffrement de disque Hello.
* Bonjour applets de commande Azure interface de ligne de commande (CLI) de chiffrement de disque.
* modèles Azure Resource Manager de chiffrement de disque Hello.

Hello solutions de chiffrement de disque Azure est prise en charge sur les machines virtuelles IaaS qui exécutent Windows ou le système d’exploitation Linux. Pour plus d’informations sur les systèmes d’exploitation hello pris en charge, consultez hello « conditions préalables » section.

> [!NOTE]
> Le chiffrement des disques de machine virtuelle avec Azure Disk Encryption est gratuit.

### <a name="value-proposition"></a>Proposition de valeur
Lorsque vous appliquez les solutions hello gestion du chiffrement de disque Azure, vous pouvez satisfaire hello suivant les besoins :

* Machines virtuelles IaaS sont sécurisés au repos, car vous pouvez utiliser le chiffrement standard technologie tooaddress sécurité et conformité besoins de l’organisation.
* Les machines virtuelles IaaS démarrent par le biais de stratégies et de clés contrôlées par les clients qui peuvent auditer leur utilisation dans le coffre de clés.

### <a name="encryption-workflow"></a>Workflow de chiffrement
chiffrement de disque tooenable pour Windows et les machines virtuelles Linux, procédez comme hello suivant :

1. Choisissez un scénario de chiffrement parmi hello précédant les scénarios de chiffrement.
2. Inclusion de chiffrement de disque tooenabling via le modèle de chiffrement de disque Azure Resource Manager hello, applets de commande PowerShell ou commande CLI et spécifier la configuration de chiffrement hello.

   * Pour le scénario de disque dur virtuel chiffrée client hello, téléchargez le compte de stockage de tooyour de disque dur virtuel hello chiffré et le coffre de clés tooyour matériel clé chiffrement hello. Ensuite, fournir hello cryptage configuration tooenable cryptage sur un VM IaaS nouvelle.
   * Pour les nouveaux ordinateurs virtuels qui sont créés à partir de hello Marketplace et des machines virtuelles existantes qui sont déjà en cours d’exécution dans Azure, permet le chiffrement de tooenable de configuration de chiffrement hello sur hello IaaS VM.

3. Grant toohello d’accès plateforme Azure tooread hello clé de chiffrement matériel (clés de chiffrement BitLocker pour les systèmes Windows) et le mot de passe Linux passe de votre coffre de clés tooenable sur hello IaaS VM.

4. Fournissez hello Azure Active Directory (Azure AD) application identité toowrite hello chiffrement tooyour matériel clé coffre de clés. Ainsi, le chiffrement sur hello IaaS VM pour les scénarios de hello mentionné à l’étape 2.

5. Azure met à jour le modèle de service de machine virtuelle hello avec le chiffrement et la configuration du coffre de clés hello et configure votre machine virtuelle chiffré.

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Workflow de déchiffrement
chiffrement de disque toodisable pour les machines virtuelles IaaS, hello complet suivant les étapes principales :

1. Choisissez toodisable chiffrement (déchiffrement) sur un VM IaaS en cours d’exécution dans Azure via le modèle de chiffrement de disque Azure Resource Manager hello ou des applets de commande PowerShell et spécifier la configuration du déchiffrement hello.

 Cette étape désactive le chiffrement de volume de données du système d’exploitation ou hello hello ou les deux sur hello machine virtuelle IaaS de Windows en cours d’exécution. Toutefois, comme indiqué dans la section précédente de hello, la désactivation du chiffrement de disque du système d’exploitation pour Linux n'est pas pris en charge. étape de déchiffrement Hello est autorisé uniquement pour les lecteurs de données sur les machines virtuelles Linux tant que disque de système d’exploitation hello n’est pas chiffré.
2. Les mises à jour Azure hello modèle de service de machine virtuelle, et hello IaaS VM est déchiffré. contenu Hello Hello machine virtuelle n’est plus chiffrés au repos.

> [!NOTE]
> opération de chiffrement de la désactiver Hello ne supprime pas votre clé coffre et hello chiffrement matériel de clé (clés de chiffrement BitLocker pour les systèmes Windows) ou une phrase secrète pour Linux.
 > La désactivation du chiffrement de disque de système d’exploitation pour Linux n’est pas prise en charge. étape de déchiffrement Hello est autorisé uniquement pour les lecteurs de données sur les machines virtuelles Linux.
La désactivation du chiffrement de disque de données pour Linux n’est pas prise en charge si hello lecteur du système d’exploitation est chiffré.

## <a name="prerequisites"></a>Composants requis
Avant d’activer le chiffrement de disque Azure sur les machines virtuelles Azure IaaS pour les scénarios de hello pris en charge qui sont présentés dans la section « Présentation » de hello, consultez hello suivant des conditions préalables :

* Vous devez disposer d’une ressource de toocreate un abonnement Azure actif dans Azure dans des régions hello pris en charge.
* Chiffrement de disque Azure est pris en charge sur hello des versions de Windows Server suivantes : Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.
* Hello suivant les versions du client Windows est pris en charge le chiffrement des disques Azure : client de Windows 10 et Windows 8.

> [!NOTE]
> Pour Windows Server 2008 R2, .NET Framework 4.5 doit être installé avant l’activation du chiffrement dans Azure. Vous pouvez l’installer à partir de la mise à jour Windows en installant la mise à jour facultative hello Microsoft .NET Framework 4.5.2 pour systèmes x64 64 de Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Chiffrement de disque Azure est prise en charge sur hello suivant la galerie Azure en fonction des distributions Linux server et les versions :

| Distribution Linux | Version | Type de volume pris en charge pour le chiffrement|
| --- | --- |--- |
| Ubuntu | 16.04-DAILY-LTS | Disque de système d’exploitation et de données |
| Ubuntu | 14.04.5-DAILY-LTS | Disque de système d’exploitation et de données |
| Ubuntu | 12.10 | Disque de données |
| Ubuntu | 12.04 | Disque de données |
| RHEL | 7.3 | Disque de système d’exploitation et de données |
| RHEL | 7,2 | Disque de système d’exploitation et de données |
| RHEL | 6,8 | Disque de système d’exploitation et de données |
| RHEL | 6.7 | Disque de données |
| CentOS | 7.3 | Disque de système d’exploitation et de données |
| CentOS | 7.2n | Disque de système d’exploitation et de données |
| CentOS | 6.8 | Disque de système d’exploitation et de données |
| CentOS | 7.1 | Disque de données |
| CentOS | 7.0 | Disque de données |
| CentOS | 6.7 | Disque de données |
| CentOS | 6.6 | Disque de données |
| CentOS | 6.5 | Disque de données |
| openSUSE | 13.2 | Disque de données |
| SLES | 12 SP1 | Disque de données |
| SLES | 12-SP1 (Premium) | Disque de données |
| SLES | HPC 12 | Disque de données |
| SLES | 11-SP4 (Premium) | Disque de données |
| SLES | 11 SP4 | Disque de données |

* Le chiffrement des disques Azure nécessite que votre coffre de clés et les machines virtuelles résident dans hello même région Azure et l’abonnement.

> [!NOTE]
> Configuration des ressources de hello dans des régions distinctes de provoque un échec de l’activation de fonctionnalité de chiffrement de disque Azure hello.

* tooset et configurer votre coffre de clés de chiffrement de disque Azure, consultez la section **définir installer et configurer votre coffre de clés de chiffrement de disque Azure** Bonjour *conditions préalables* section de cet article.
* tooset et configurer l’application Azure AD dans Azure Active directory pour le chiffrement du disque Azure, consultez la section **configurer application hello Azure AD dans Azure Active Directory** Bonjour *conditions préalables* section de cet article.
* tooset et configurer la stratégie d’accès de coffre de clés hello pour une application hello Azure AD, consultez la section **configurer la stratégie d’accès hello coffre de clés pour l’application hello Azure AD** Bonjour *conditions préalables* section de Cet article.
* tooprepare un disque dur virtuel déjà chiffrés de Windows, consultez la section **préparer un disque dur virtuel Windows déjà chiffrés** Bonjour *annexe*.
* tooprepare un VHD Linux déjà chiffrés, voir la section **préparer un VHD Linux déjà chiffrés** Bonjour *annexe*.
* Hello plateforme Azure a besoin de clés de chiffrement toohello accès ou les clés secrètes dans votre coffre de clés de toomake leur ordinateur de virtuel toohello disponibles lorsqu’il démarre et déchiffre le volume de l’ordinateur virtuel du système d’exploitation hello. plateforme de tooAzure autorisations toogrant, jeu hello **EnabledForDiskEncryption** propriété hello coffre de clés. Pour plus d’informations, consultez **définir installer et configurer votre coffre de clés de chiffrement de disque Azure** Bonjour annexe.
* Les URL de clé secrète de coffre de clés et de clé de chiffrement à clé (KEK) doivent être des versions gérées. Azure met en vigueur cette restriction de gestion de version. Pour secret valide et les URL de clés, consultez hello exemple suivant :

  * Exemple d’URL secrète valide : *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Exemple d’URL de clé de chiffrement à clé valide : *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk Encryption ne prend pas en charge l’intégration de numéros de port aux clés secrètes de coffre de clés et aux URL KEK. Pour obtenir des exemples d’URL de coffre de clés pris en charge et non pris en charge, voir hello :

  * URL de coffre de clés non acceptée : *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * URL de coffre de clés acceptée : *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* fonctionnalité de chiffrement de disque Azure hello tooenable, hello machines virtuelles IaaS doit respecter hello suivant les exigences de configuration de point de terminaison de réseau :
  * tooget un jeton tooconnect tooyour coffre de clés, hello IaaS VM doit être en mesure de tooconnect le point de terminaison Azure Active Directory tooan, \[login.microsoftonline.com\].
  * toowrite hello chiffrement clés tooyour coffre de clés, hello IaaS VM doit être le point de terminaison en mesure de tooconnect toohello coffre de clés.
  * Hello IaaS VM doit être le point de terminaison le stockage Azure de tooan tooconnect en mesure que les ordinateurs hôtes hello référentiel d’extensions Azure et un compte de stockage Azure que hôtes hello des fichiers de disque dur virtuel.

  > [!NOTE]
  > Si votre stratégie de sécurité limite l’accès à partir de machines virtuelles Azure toohello Internet, vous pouvez résoudre hello précédant l’URI et configurer un toohello de connectivité sortante tooallow règle spécifique des adresses IP.
  >
  >tooconfigure et accès Azure Key Vault derrière un pare-feu (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)

* Utilisez la version la plus récente du Kit de développement logiciel Azure PowerShell version tooconfigure chiffrement de disque Azure hello. Télécharger la version la plus récente de hello [Azure PowerShell version](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Azure Disk Encryption n’est pas pris en charge dans le [Kit de développement logiciel (SDK) Azure PowerShell version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Si vous recevez une erreur liés toousing Azure PowerShell 1.1.0, consultez [tooAzure Azure disque chiffrement erreur connexes PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun une commande CLI d’Azure et associez-le à votre abonnement Azure, vous devez d’abord installer CLI d’Azure :
  * tooinstall CLI d’Azure et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure CLI](../cli-install-nodejs.md).
  * toouse CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager, consultez [les commandes CLI d’Azure en mode de gestionnaire de ressources](../virtual-machines/azure-cli-arm-commands.md).

* Lors du chiffrement d’un disque géré, il est obligatoire tootake requis un instantané du disque de hello géré ou une sauvegarde de disque hello en dehors de chiffrement tooenabling préalable de chiffrement de disque Azure.  Sans une sauvegarde en place, tout échec inattendu au cours du chiffrement peut rendre les disque hello et l’ordinateur virtuel inaccessibles sans une option de récupération.  Set-AzureRmVMDiskEncryptionExtension ne pas actuellement sauvegarder disques gérés et génèrent une erreur si utilisé sur un disque géré, sauf si hello - skipVmBackup paramètre a été spécifié.  Ce paramètre est toouse unsafe, sauf si une sauvegarde a déjà été apportée en dehors de chiffrement de disque Azure.   Lorsque hello - skipVmBackup est précisé, applet de commande hello n’effectuera pas d’une sauvegarde de tooencryption préalable du disque hello géré.  Pour cette raison, il est considéré comme un toomake prérequis obligatoire vraiment besoin d’une sauvegarde de disque géré de hello que machine virtuelle est en place tooenabling préalable chiffrement de disque Azure en cas de récupération ultérieure.  
> [!NOTE]
 > paramètre de skipVmBackup - Hello ne doit jamais être utilisé sauf si une sauvegarde ou instantané a déjà été faite en dehors de chiffrement de disque Azure. 

* Hello solutions de chiffrement de disque Azure utilise le protecteur de clé externe hello BitLocker pour les machines virtuelles IaaS de Windows. Pour des machines virtuelles jointes au domaine, ne distribuez PAS de stratégies de groupe qui appliquent des protecteurs de Module de plateforme sécurisée (TPM). Pour plus d’informations sur la stratégie de groupe hello pour « Autoriser BitLocker sans un module de plateforme sécurisée compatible », consultez [référence de stratégie de groupe BitLocker](https://technet.microsoft.com/library/ee706521).
* Stratégie de BitLocker sur les ordinateurs virtuels de joints à un domaine avec la stratégie de groupe personnalisé doit inclure hello suivant paramètre : `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` chiffrement de disque Azure échoue lorsque les paramètres de stratégie de groupe personnalisé pour que Bitlocker sont incompatibles. Sur les ordinateurs qui n’avaient pas hello correct paramètre de stratégie, appliquer la stratégie de nouvelle hello, forçant hello nouvelle stratégie tooupdate (gpupdate.exe /force) et le redémarrage peut être nécessaire.  
* toocreate une application Azure AD, créez un coffre de clés, ou configurer un coffre de clés existant et activer le chiffrement, consultez hello [script PowerShell requis de chiffrement de disque Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* conditions préalables du chiffrement de disque tooconfigure à l’aide de hello CLI d’Azure, consultez [ce script Bash](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello Azure Backup service tooback haut et les machines virtuelles de restauration chiffrée, lorsque le chiffrement est activé avec le chiffrement du disque Azure, chiffrent vos machines virtuelles à l’aide de configuration de clé de chiffrement de disque Azure hello. Hello service de sauvegarde prend en charge les ordinateurs virtuels qui sont chiffrées à l’aide de la configuration de clés uniquement. Consultez [mode tooback configuration et restauration de chiffrement de machines virtuelles avec le chiffrement de sauvegarde Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Lors du chiffrement d’un volume de système d’exploitation Linux, notez qu’un redémarrage de l’ordinateur virtuel est actuellement requis à fin hello du processus de hello. Cela est possible via le portail de hello, powershell ou CLI.   progression de hello tootrack du chiffrement, interrogent régulièrement le message d’état hello retourné par Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.  Une fois que le chiffrement est terminé, message d’état hello hello retourné par cette commande indique cela.  Par exemple, « ProgressMessage : du disque du système d’exploitation a été chiffrée, redémarrez hello VM » à cette hello du point de machine virtuelle peut être redémarrée et utilisé.  

* Le chiffrement des disques Azure pour Linux nécessite des disques de données toohave un système de fichiers monté tooencryption préalable de Linux

* Récursive des disques de données montés ne sont pas pris en charge par hello chiffrement de disque Azure pour Linux. Par exemple, si hello système cible a été monté un disque sur /foo/bar et puis un autre sur /foo/bar/baz, chiffrement hello de /foo/bar/baz réussira, mais le chiffrement de barre/foo/échouera. 

* Chiffrement de disque Azure est uniquement pris en charge sur les images de la galerie Azure pris en charge que les conditions préalables hello susmentionnés. Images personnalisées du client ne sont pas pris en charge en raison des schémas de partition toocustom et les comportements de processus qui peuvent exister sur ces images. De plus, même les machines virtuelles d’image de galerie, qui initialement remplissaient les conditions préalables demandées, mais qui ont été modifiées depuis leur création, peuvent être incompatibles.  Pour que raison, hello suggéré procédure pour chiffrer un VM Linux est toostart à partir d’une image de galerie nettoyer, chiffrer hello machine virtuelle, puis ajoutez personnalisée de logiciels ou des données toohello machine virtuelle en fonction des besoins.  

> [!NOTE]
> Sauvegarde et restauration de machines virtuelles chiffrés est pris en charge uniquement pour les ordinateurs virtuels qui sont chiffrés avec une configuration de clés hello. Elles ne sont pas prises en charge pour les machines virtuelles chiffrées sans KEK. KEK est un paramètre facultatif qui active une machine virtuelle.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Configurer application Azure AD hello dans Azure Active Directory
Lorsque vous devez toobe chiffrement activé sur une machine virtuelle dans Azure, le chiffrement des disques Azure génère et écrit le coffre de clés hello chiffrement clés tooyour. La gestion des clés de chiffrement dans votre coffre de clés nécessite l’authentification Azure AD.

Une application Azure AD doit donc être créée à cet effet. Vous trouverez des instructions détaillées pour l’inscription d’une application de section de « Obtenir une identité pour hello Application » hello de billet de blog hello [le coffre de clés Azure - étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Cet article contient également plusieurs exemples utiles sur l’installation et la configuration de votre coffre de clés. Pour l’authentification, vous pouvez utiliser soit l’authentification par clé secrète de client, soit l’authentification Azure AD par certificat de client.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Authentification par clé secrète de client pour Azure AD
les sections Hello qui suivent peuvent vous aider à configurer une authentification basée sur une clé secrète du client pour Azure AD.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Créer une application Azure AD à l’aide d’Azure PowerShell
Utilisez hello suivant toocreate d’applet de commande PowerShell une application Azure AD :

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId est hello Azure AD ClientID et $aadClientSecret est la clé secrète du client hello que vous devez utiliser tooenable ultérieure le chiffrement des disques Azure. Protéger la question secrète du client hello Azure AD en conséquence.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Configuration d’ID de client hello Azure AD et la clé secrète à partir de hello portail Azure classic
Vous pouvez également configurer votre ID client Azure AD et la clé secrète à l’aide de hello [portail Azure classic]( https://manage.windowsazure.com). tooperform cette tâche, procédez comme hello suivant :

1. Cliquez sur hello **Active Directory** onglet.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Cliquez sur **ajouter une Application**et puis type hello nom de l’application.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Cliquez sur le bouton de flèche hello, puis configurez les propriétés de l’application hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Cliquez sur case à cocher hello dans hello inférieure gauche toofinish. page de configuration d’application Hello s’affiche, et ID de client Azure AD hello s’affiche en bas de hello de page de hello.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Enregistrer la clé secrète du client hello Azure AD en cliquant sur hello **enregistrer** bouton. Notez la clé secrète du client dans la zone de texte hello clés hello Azure AD. Prenez soin de bien la sauvegarder.

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Hello précédant le flux n’est pas pris en charge sur hello portail Azure classic.

##### <a name="use-an-existing-application"></a>Utiliser une application existante
tooexecute hello suivant de commandes, d’obtenir et utiliser hello [module PowerShell Azure AD](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Hello les commandes suivantes doivent être exécutées à partir d’une nouvelle fenêtre PowerShell. N’utilisez pas d’Azure PowerShell ou commandes de hello Azure Resource Manager fenêtre tooexecute hello. Nous recommandons cette approche, car ces applets de commande sont dans le module MSOnline de hello ou Azure AD PowerShell.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Authentification par certificat pour Azure AD
> [!NOTE]
> L’authentification par certificat Azure AD n’est actuellement pas prise en charge sur les machines virtuelles Linux.

Hello les sections suivantes indiquent comment tooconfigure une authentification basée sur certificat pour Azure AD.

##### <a name="create-an-azure-ad-application"></a>Créer une application Azure AD
toocreate une application Azure AD, exécutez hello suivant d’applets de commande PowerShell :

> [!NOTE]
> Remplacez hello suit `yourpassword` avec votre mot de passe sécurisé et le mot de passe de sauvegarde hello de chaîne.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Une fois que vous avez terminé cette étape, téléchargez un coffre de clés tooyour de fichier PFX et activer hello accès stratégie nécessaires toodeploy que tooa certificat machine virtuelle.

##### <a name="use-an-existing-azure-ad-application"></a>Utiliser une application Azure AD existante
Si vous configurez l’authentification par certificat pour une application existante, utilisez les applets de commande PowerShell hello indiqué ici. Être tooexecute vraiment à partir d’une nouvelle fenêtre PowerShell.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Une fois que vous avez terminé cette étape, téléchargez un coffre de clés tooyour de fichier PFX et activer la stratégie d’accès hello toodeploy hello certificat tooa machine virtuelle que nécessaire.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Télécharger un coffre de clés tooyour de fichier PFX
Pour obtenir une explication détaillée de ce processus, consultez [hello Blog de l’équipe officiel Azure Key Vault](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Toutefois, hello suivant d’applets de commande PowerShell est nécessaire pour la tâche hello. Être tooexecute que les à partir de la console Azure PowerShell.

> [!NOTE]
> Remplacez hello suit `yourpassword` avec votre mot de passe sécurisé et le mot de passe de sauvegarde hello de chaîne.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Déployer un certificat dans votre tooan de coffre de clés existant de machine virtuelle
Après avoir terminé le téléchargement hello PFX, déployez un certificat dans hello tooan de coffre de clés existant de machine virtuelle avec les éléments suivants de hello :
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Configurer la stratégie d’accès hello coffre de clés pour l’application hello Azure AD
Votre application Azure AD a besoin de clés de droits tooaccess hello ou des clés secrètes dans le coffre hello. Hello d’utilisation [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) applet de commande toogrant autorisations toohello application, en utilisant les ID de client hello (qui a été générée lors de l’application hello a été inscrit) comme hello _– ServicePrincipalName_ valeur du paramètre. toolearn plus, consultez hello billet de blog [le coffre de clés Azure - étape par étape](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Voici un exemple de comment tooperform cette tâche PowerShell :

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Le chiffrement des disques Azure nécessite que vous hello tooconfigure suite de l’application de client accès stratégies tooyour Azure AD : _WrapKey_ et _définir_ autorisations.

## <a name="terminology"></a>Terminologie
toounderstand certains des termes courants de hello utilisé par cette technologie, hello utilisez terminologie tableau suivant :

| Terminologie | Définition |
| --- | --- |
| Azure AD | Azure AD est [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Un compte Azure AD est requis pour l’authentification, le stockage et l’extraction des clés secrètes d’un coffre de clés. |
| coffre de clés Azure | Key Vault est un service de gestion de clés de chiffrement basé sur des modules de sécurité matériels FIPS (Federal Information Processing Standards) qui vous permet de protéger vos clés de chiffrement et les clés secrètes sensibles. Pour plus d’informations, consultez la documentation relative à [Key Vault](https://azure.microsoft.com/services/key-vault/). |
| ARM | Azure Resource Manager |
| BitLocker |[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) est une secteur d’activité Windows volume technologie de chiffrement utilisée par un chiffrement de disque tooenable sur les machines virtuelles IaaS Windows. |
| BEK | Les clés de chiffrement BitLocker sont le volume de démarrage utilisé tooencrypt hello du système d’exploitation et les volumes de données. les clés BitLocker Hello sont sauvegardés dans un coffre de clés en tant que clés secrètes. |
| Interface de ligne de commande | Voir [Interface de ligne de commande Azure](../cli-install-nodejs.md). |
| DM-Crypt |[Exploration de données-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) sous-système de chiffrement de disque basés sur Linux, transparent hello qui a utilisé un chiffrement de disque tooenable sur les machines virtuelles IaaS Linux. |
| KEK | Clé de chiffrement est hello clé asymétrique (RSA 2048) que vous pouvez utiliser tooprotect ou encapsuler le code secret hello. Vous pouvez fournir une clé protégée par le module HSM ou une clé protégée par le logiciel. Pour plus d’informations, consultez la documentation relative à [Azure Key Vault](https://azure.microsoft.com/services/key-vault/). |
| Applets de commande PS | Voir [Applets de commande Azure PowerShell](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Créer et configurer votre coffre de clés pour Azure Disk Encryption
Le chiffrement des disques Azure permet de protéger les clés de chiffrement de disque hello et les clés secrètes dans votre coffre de clés. tooset de votre coffre de clés de chiffrement de disque Azure, hello terminé les étapes dans chacune des hello les sections suivantes.

#### <a name="create-a-key-vault"></a>Création d’un coffre de clés
toocreate un coffre de clés, utilisez une des options suivantes de hello :

* [Modèle Resource Manager « 101-Key-Vault-Create »](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Applets de commande Key Vault Azure PowerShell](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* Comment trop[sécuriser votre coffre de clés](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Si vous avez déjà configuré un coffre de clés pour votre abonnement, ignorer la section suivante de toohello.

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Configurer une clé de chiffrement à clé (facultatif)
Si vous souhaitez toouse une clés pour une couche supplémentaire de sécurité pour les clés de chiffrement BitLocker hello, ajoutez un coffre de clés tooyour de clés. Hello d’utilisation [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate de l’applet de commande une clé de chiffrement dans le coffre de clés hello. Vous pouvez également importer une clé de chiffrement à clé à partir de votre module de sécurité matériel de gestion des clés locales. Pour plus d’informations, consultez la [Documentation relative à Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Vous pouvez ajouter hello veillent en accédant tooAzure Gestionnaire de ressources ou à l’aide de l’interface de coffre de clés.

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Définir des autorisations d’accès au coffre de clés
Hello plateforme Azure a besoin de clés de chiffrement toohello accès ou les clés secrètes dans votre coffre de clés de toomake les toohello disponible machine virtuelle pour le démarrage et le déchiffrement des volumes de hello. toogrant autorisations toohello plateforme Azure, jeu hello **EnabledForDiskEncryption** propriété dans la clé de hello coffre à l’aide d’applet de commande PowerShell de coffre de clés hello :

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Vous pouvez également définir hello **EnabledForDiskEncryption** propriété en visitant hello [Explorateur de ressources Azure](https://resources.azure.com).

Comme mentionné précédemment, vous devez définir hello **EnabledForDiskEncryption** propriété sur votre coffre de clés. Dans le cas contraire, le déploiement de hello échoue.

Vous pouvez définir des stratégies d’accès pour votre application Azure AD à partir de l’interface du coffre de clés hello, comme illustré ici :

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Sur hello **des stratégies d’accès avancé** onglet, vérifiez que votre coffre de clés est activé pour le chiffrement du disque Azure :

![Coffre de clés Azure](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Scénarios de déploiement de chiffrement de disque et expériences utilisateur
Vous pouvez activer plusieurs scénarios de chiffrement de disque, et les étapes de hello peuvent varier en fonction toohello scénario. Hello sections suivantes couvrent les scénarios de hello plus en détail.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Activer le chiffrement sur les nouvelles machines virtuelles IaaS qui sont créés à partir de hello Marketplace
Vous pouvez activer le chiffrement de disque sur virtuelle IaaS Windows à partir de hello Marketplace dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.

2. Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur un VM IaaS nouvelle.

> [!NOTE]
> Ce modèle crée un nouveau chiffrées Windows VM qui utilise l’image de la galerie hello Windows Server 2012.

Vous pouvez activer le chiffrement de disque sur une nouvelle machine virtuelle IaaS RedHat Linux 7.2 avec une baie RAID-0 de 200 Go à l’aide de ce [modèle Resource Manager](https://aka.ms/fde-rhel). Après avoir déployé le modèle de hello, vérifier état du chiffrement hello machine virtuelle à l’aide de hello `Get-AzureRmVmDiskEncryptionStatus` applet de commande, comme décrit dans [lecteur de chiffrement du système d’exploitation sur un VM Linux en cours d’exécution](#encrypting-os-drive-on-a-running-linux-vm). Lorsque les ordinateurs hello retourne l’état _VMRestartPending_, redémarrez hello machine virtuelle.

Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources hello pour les nouvelles machines virtuelles à partir du scénario de Marketplace hello à l’aide d’ID de client Azure AD :

| Paramètre | Description |
| --- | --- |
| adminUsername | Nom d’utilisateur administrateur pour l’ordinateur virtuel de hello. |
| adminPassword | Mot de passe administrateur pour l’ordinateur virtuel de hello. |
| newStorageAccountName | Nom de toostore de compte de stockage hello du système d’exploitation et des disques durs virtuels de données. |
| vmSize | Taille de machine virtuelle de hello. Actuellement, seules les séries A, D et G standard sont prises en charge. |
| virtualNetworkName | Nom de réseau virtuel que hello VM NIC de hello doit appartenir au. |
| subnetName | Nom du sous-réseau hello Bonjour réseau virtuel que hello VM NIC doit appartenir au. |
| AADClientID | ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour. |
| AADClientSecret | Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour. |
| keyVaultURL | URL de la clé de hello coffre que BitLocker clé doit être téléchargée dans hello. Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker (facultatif). |
| keyVaultResourceGroup | Groupe de ressources de coffre de clés hello. |
| vmName | Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur. |

> [!NOTE]
> _KeyEncryptionKeyURL_ est un paramètre facultatif. Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (mot de passe secret) dans votre coffre de clés.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>Activation du chiffrement sur de nouvelles machines virtuelles IaaS créées à partir de disques durs virtuels chiffrés par le client et de clés de chiffrement
Dans ce scénario, vous pouvez activer le chiffrement à l’aide des commandes CLI, applets de commande PowerShell ou modèle du Gestionnaire de ressources hello. Hello sections suivantes expliquent dans le modèle de gestionnaire de ressources de hello détail supérieur et les commandes CLI.

Suivez les instructions de hello à partir d’une de ces sections pour la préparation d’images déjà chiffrés qui peuvent être utilisés dans Azure. Après la création d’image de hello, vous pouvez utiliser les étapes de hello dans hello suivant section toocreate une machine virtuelle de Azure chiffré.

* [Préparer un disque dur virtuel Windows déjà chiffré](#preparing-a-pre-encrypted-windows-vhd)
* [Préparer un disque dur virtuel Linux déjà chiffré](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>À l’aide du modèle de gestionnaire de ressources hello
Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.

2. Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello nouvelle IaaS VM.

Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources hello pour votre disque dur virtuel chiffrée :

| Paramètre | Description |
| --- | --- |
| newStorageAccountName | Nom de hello de toostore de compte de stockage hello chiffré de disque dur virtuel du système d’exploitation. Ce compte de stockage doit déjà avoir été créé dans hello même groupe de ressources et le même emplacement que hello machine virtuelle. |
| osVhdUri | URI de hello disque dur virtuel du système d’exploitation à partir du compte de stockage hello. |
| osType | Type de système d’exploitation (Windows/Linux). |
| virtualNetworkName | Nom de réseau virtuel que hello VM NIC de hello doit appartenir au. Hello nom doit ont déjà été créé dans hello même groupe de ressources et le même emplacement que hello machine virtuelle. |
| subnetName | Nom du sous-réseau hello sur hello réseau virtuel que hello VM NIC doit appartenir au. |
| vmSize | Taille de machine virtuelle de hello. Actuellement, seules les séries A, D et G standard sont prises en charge. |
| keyVaultResourceID | Hello ResourceID qui identifie la ressource du coffre de clés hello dans Azure Resource Manager. Vous pouvez l’obtenir à l’aide de l’applet de commande PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | URL de la clé de chiffrement de disque hello qui est défini dans le coffre de clés hello. |
| keyVaultKekUrl | URL de la clé de chiffrement à clé hello pour chiffrer la clé de chiffrement de disque hello généré. |
| vmName | Nom de hello IaaS VM. |

#### <a name="using-powershell-cmdlets"></a>Utilisation d’applets de commande PowerShell
Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée à l’aide d’applet de commande PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>Utilisation des commandes CLI
chiffrement de disque tooenable pour ce scénario à l’aide des commandes CLI, hello suivant :

1. Définissez des stratégies d’accès dans votre coffre de clés :

   * Ensemble hello **EnabledForDiskEncryption** indicateur :

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. chiffrement tooenable sur une machine virtuelle existante ou en cours d’exécution, type :

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenez l’état de chiffrement :

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Activer le chiffrement sur des machines virtuelles IaaS Windows existantes/en cours de fonctionnement dans Azure
Dans ce scénario, vous pouvez activer le chiffrement à l’aide des commandes CLI, applets de commande PowerShell ou modèle du Gestionnaire de ressources hello. Hello sections suivantes expliquent en détail comment tooenable à l’aide de hello modèle du Gestionnaire de ressources et les commandes CLI.

#### <a name="using-hello-resource-manager-template"></a>À l’aide du modèle de gestionnaire de ressources hello
Vous pouvez activer le chiffrement de disque sur existant ou en exécutant des machines virtuelles IaaS de Windows dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.

2. Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello existant ou en cours d’exécution IaaS VM.

Hello tableau suivant répertorie les paramètres du modèle de gestionnaire de ressources hello pour existant ou en exécutant des ordinateurs virtuels qui utilisent un ID de client Azure AD :

| Paramètre | Description |
| --- | --- |
| AADClientID | ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello. |
| AADClientSecret | Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello. |
| keyVaultName | Nom de clé de hello coffre que BitLocker clé doit être téléchargée dans hello. Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker. Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste de hello UseExistingKek de liste déroulante. Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek de hello, vous devez entrer hello _keyEncryptionKeyURL_ valeur. |
| volumeType | Type de volume que l’opération de chiffrement hello est effectuée sur. Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_. |
| sequenceVersion | Version de la séquence de hello BitLocker opération. Incrémenter ce numéro de version, chaque fois qu’une opération de chiffrement de disque est exécutée sur hello même machine virtuelle. |
| vmName | Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur. |

> [!NOTE]
> _KeyEncryptionKeyURL_ est un paramètre facultatif. Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (secret de chiffrement BitLocker) dans le coffre de clés hello.

#### <a name="using-powershell-cmdlets"></a>Utilisation d’applets de commande PowerShell
Pour plus d’informations sur l’activation du chiffrement avec un chiffrement de disque Azure à l’aide des applets de commande PowerShell, consultez les billets de blog hello [Explorer le chiffrement de disque Azure avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer de chiffrement de disque Azure avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>Utilisation des commandes CLI
chiffrement tooenable sur existant ou en cours d’exécution IaaS Windows VM dans Azure à l’aide des commandes CLI, hello suivant :

1. stratégies d’accès tooset hello coffre de clés :
   * Ensemble hello **EnabledForDiskEncryption** indicateur :

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. chiffrement tooenable sur une machine virtuelle au existant ou en cours d’exécution :

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. état du chiffrement tooget :

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Activer le chiffrement sur une machine virtuelle IaaS Linux existante ou en cours d’exécution dans Azure
Vous pouvez activer le chiffrement de disque sur une version existante ou en cours d’exécution IaaS Linux machine virtuelle dans Azure à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Cliquez sur **déployer tooAzure** sur le modèle de démarrage rapide Azure de hello, entrez la configuration de chiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.

2. Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur hello existant ou en cours d’exécution IaaS VM.

Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources pour existant ou en exécutant des ordinateurs virtuels qui utilisent un ID de client Azure AD :

| Paramètre | Description |
| --- | --- |
| AADClientID | ID client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets toohello. |
| AADClientSecret | Question secrète du client de l’application hello Azure AD avec le coffre de clés autorisations toowrite secrets tooyour. |
| keyVaultName | Nom de clé de hello coffre que BitLocker clé doit être téléchargée dans hello. Vous pouvez l’obtenir à l’aide de l’applet de commande hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | URL de la clé de chiffrement hello est utilisé tooencrypt hello générée clé BitLocker. Ce paramètre est facultatif si vous sélectionnez **nokek** dans la liste de hello UseExistingKek de liste déroulante. Si vous sélectionnez **kek** dans la liste déroulante UseExistingKek de hello, vous devez entrer hello _keyEncryptionKeyURL_ valeur. |
| volumeType | Type de volume que l’opération de chiffrement hello est effectuée sur. Les valeurs valides prises en charge sont _Système d’exploitation_ ou _Tous_ (pour RHEL 7.2, CentOS 7.2 et Ubuntu 16.04) et _Données_ (pour toutes les autres distributions). |
| sequenceVersion | Version de la séquence de hello BitLocker opération. Incrémenter ce numéro de version, chaque fois qu’une opération de chiffrement de disque est exécutée sur hello même machine virtuelle. |
| vmName | Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur. |
| passPhrase | Tapez une phrase secrète forte en tant que clé de chiffrement de données hello. |

> [!NOTE]
> _KeyEncryptionKeyURL_ est un paramètre facultatif. Vous pouvez mettre votre propre clé de chiffrement de clés toofurther sauvegarde hello données (mot de passe secret) dans votre coffre de clés.

#### <a name="cli-commands"></a>Commandes CLI
Vous pouvez activer le chiffrement de disque sur votre disque dur virtuel chiffrée en installant et utilisant hello [commande CLI](../cli-install-nodejs.md). chiffrement tooenable sur existant ou en exécutant les machines virtuelles Linux IaaS dans Azure à l’aide des commandes CLI, hello suivant :

1. Définir des stratégies d’accès dans le coffre de clés hello :

 * Ensemble hello **EnabledForDiskEncryption** indicateur :

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * Jeu d’autorisations tooAzure AD application toowrite secrets tooyour coffre de clés :

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. chiffrement tooenable sur une machine virtuelle au existant ou en cours d’exécution :

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Obtenez l’état de chiffrement :

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. le chiffrement sur une machine virtuelle à partir de votre disque dur virtuel chiffrée, hello utilisez paramètres avec hello suivants tooenable `azure vm create` commande :
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Obtenir l’état de chiffrement hello d’une VM IaaS chiffrée
Vous pouvez obtenir l’état du chiffrement hello à l’aide du Gestionnaire de ressources Azure, [applets de commande PowerShell](/powershell/azure/overview), ou des commandes CLI. Hello les sections suivantes explique comment toouse hello portail Azure classic et tooget des commandes CLI hello état du chiffrement.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Obtenir l’état de chiffrement de hello d’une machine virtuelle de Windows chiffrées à l’aide du Gestionnaire de ressources Azure
Vous pouvez obtenir état du chiffrement hello Hello IaaS VM à partir du Gestionnaire de ressources Azure de manière hello suivante :

1. Connectez-vous à toohello [portail Azure classic](https://portal.azure.com/), puis cliquez sur **virtuels** dans le volet gauche de hello toosee un récapitulatif des ordinateurs virtuels de hello dans votre abonnement. Vous pouvez filtrer la vue des machines virtuelles hello en sélectionnant le nom de l’abonnement hello Bonjour **abonnement** liste déroulante.

2. En haut de hello Hello **virtuels** , cliquez sur **colonnes**.

3. Sur hello **choisissez colonne** panneau, sélectionnez **chiffrement de disque**, puis cliquez sur **mise à jour**. Vous devez voir État de chiffrement hello chiffrement de disque colonne affichant hello _activé_ ou _pas activé_ pour chaque machine virtuelle, comme indiqué dans la figure suivante de hello :

 ![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Obtenir l’état du chiffrement hello d’un chiffrée (Windows/Linux) IaaS VM à l’aide d’applet de commande PowerShell de chiffrement de disque hello
Vous pouvez obtenir l’état du chiffrement hello Hello IaaS VM à partir de l’applet de commande PowerShell de chiffrement de disque hello `Get-AzureRmVMDiskEncryptionStatus`. paramètres de chiffrement tooget hello pour votre machine virtuelle, entrez hello qui suit :

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Vous pouvez inspecter la sortie hello de _Get-AzureRmVMDiskEncryptionStatus_ pour le chiffrement de clé URL.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Hello OSVolumeEncrypted et les valeurs des paramètres DataVolumesEncrypted sont définies too_Encrypted_, ce qui indique que les deux volumes sont chiffrées à l’aide du chiffrement de disque Azure. Pour plus d’informations sur l’activation du chiffrement avec un chiffrement de disque Azure à l’aide des applets de commande PowerShell, consultez les billets de blog hello [Explorer le chiffrement de disque Azure avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) et [Explorer de chiffrement de disque Azure avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> Sur les machines virtuelles Linux, il prend trois minutes toofour hello `Get-AzureRmVMDiskEncryptionStatus` état de chiffrement d’applet de commande tooreport hello.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Obtenir l’état du chiffrement hello Hello IaaS VM à partir de la commande CLI de chiffrement de disque hello
Vous pouvez obtenir l’état du chiffrement hello Hello IaaS VM à l’aide des commandes CLI de chiffrement de disque hello `azure vm show-disk-encryption-status`. paramètres de chiffrement tooget hello pour votre machine virtuelle, entrez votre session CLI d’Azure :

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Désactivation du chiffrement sur une machine virtuelle IaaS Windows en cours d’exécution
Vous pouvez désactiver le chiffrement sur un ordinateur virtuel IaaS de Linux ou Windows en cours d’exécution via le modèle de chiffrement de disque Azure Resource Manager hello ou des applets de commande PowerShell et configuration de déchiffrement hello.

##### <a name="windows-vm"></a>Machine virtuelle Windows
étape de chiffrement de la désactivation de Hello désactive le chiffrement de hello du système d’exploitation, le volume de données hello ou les deux sur hello machine virtuelle IaaS de Windows en cours d’exécution. Vous ne peut pas désactiver le volume du système d’exploitation hello et laisser le volume de données hello chiffré. Lors de l’étape de chiffrement de la désactiver hello est effectuée, modèle de déploiement classique Azure hello met à jour le modèle de service de machine virtuelle hello, et hello machine virtuelle IaaS de Windows est déchiffré. contenu Hello Hello machine virtuelle n’est plus chiffrés au repos. le déchiffrement de Hello ne supprime pas votre clé coffre et hello chiffrement matériel de clé (clés de chiffrement BitLocker pour Windows et le mot de passe pour Linux).

##### <a name="linux-vm"></a>Machine virtuelle Linux
étape de chiffrement de la désactivation de Hello désactive le chiffrement de volume de données hello hello machine virtuelle IaaS de Linux en cours d’exécution. Cette étape fonctionne uniquement si le disque du système d’exploitation hello n’est pas chiffré.

> [!NOTE]
> La désactivation du chiffrement sur le disque du système d’exploitation hello n’est pas autorisée sur les machines virtuelles Linux.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution
Vous pouvez désactiver le chiffrement de disque sur les machines virtuelles IaaS Windows en cours d’exécution à l’aide de hello [modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. Sur le modèle de hello Azure de démarrage rapide, cliquez sur **déployer tooAzure**, entrez la configuration du déchiffrement hello sur hello **paramètres** panneau, puis cliquez sur **OK**.

2. Sélectionnez l’abonnement de hello, groupe de ressources, emplacement du groupe de ressources, juridiques et contrat, puis cliquez sur **créer** tooenable le chiffrement sur un VM IaaS nouvelle.

Pour les machines virtuelles Linux, vous pouvez désactiver le chiffrement à l’aide de hello [désactiver le chiffrement sur un VM Linux en cours d’exécution](https://aka.ms/decrypt-linuxvm) modèle.

Hello tableau suivant répertorie les paramètres de modèle de gestionnaire de ressources pour la désactivation du chiffrement sur un VM IaaS en cours d’exécution :

| Paramètre | Description |
| --- | --- |
| vmName | Nom de machine virtuelle qui hello l’opération de chiffrement de hello est toobe effectuée sur.
| volumeType | Type de volume sur lequel l’opération de déchiffrement est effectuée. Les valeurs valides sont _Système d’exploitation_, _Données_ et _Tous_. Vous ne pouvez pas désactiver le chiffrement sur le volume du système d’exploitation Windows IaaS VM/de démarrage en cours d’exécution sans la désactivation du chiffrement sur hello _données_ volume. Notez également que la désactivation du chiffrement sur le disque du système d’exploitation hello n’est pas autorisée sur les machines virtuelles Linux. |
| sequenceVersion | Version de la séquence de hello BitLocker opération. Incrémenter ce numéro de version, chaque fois qu’une opération de déchiffrement de disque est exécutée sur hello même machine virtuelle. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Désactivation du chiffrement sur une machine virtuelle IaaS existante ou en cours d’exécution
chiffrement toodisable sur une VM IaaS existant ou en cours d’exécution à l’aide d’applet de commande PowerShell hello, consultez [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Cette applet de commande prend en charge les machines virtuelles Linux et Windows. le chiffrement toodisable, il installe une extension sur l’ordinateur virtuel de hello. Si hello _nom_ paramètre n’est pas spécifié, une extension avec le nom par défaut de hello _AzureDiskEncryption pour Windows machines virtuelles_ est créé.

Sur les machines virtuelles Linux, hello AzureDiskEncryptionForLinux extension est utilisée.

> [!NOTE]
> Cette applet de commande redémarre l’ordinateur virtuel de hello.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Activer le chiffrement sur une machine virtuelle IaaS pré-chiffrée avec un disque managé Azure
Utilisez hello ARM de disque géré Azure modèle toocreate une VM chiffrée à partir d’un disque dur virtuel déjà chiffré à l’aide du modèle de hello ARM située   
[Créer un disque managé chiffré à partir d’un disque dur virtuel/bjet blob de stockage pré-chiffré] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Activer le chiffrement sur une nouvelle machine virtuelle IaaS Linux avec disque managé Azure
Utilisez hello ARM de disque géré Azure modèle toocreate chiffrées d’une nouvelle machine virtuelle IaaS de Linux à l’aide du modèle d’ARM hello situé   
[Déploiement de RHEL 7.2 avec un chiffrement de disque complet] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Activer le chiffrement sur une nouvelle machine virtuelle IaaS Windows avec disque managé Azure
 Utilisez hello ARM de disque géré Azure modèle toocreate chiffrées d’une nouvelle machine virtuelle IaaS de Linux à l’aide du modèle d’ARM hello situé   
 [Créer une machine virtuelle avec disque managé IaaS Windows chiffré à partir d’une image de la galerie] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Il est obligatoire toosnapshot et/ou sauvegarde un disque géré basée et instance de machine virtuelle en dehors de tooenabling préalable chiffrement de disque Azure.  Un instantané de disque géré de hello peut provenir de portail de hello ou Azure Backup peut être utilisé.  Sauvegardes de vous assurer qu’une option de récupération est possible dans les cas de hello de toute défaillance inattendue pendant le chiffrement.  Une fois qu’une sauvegarde est effectuée, applet de commande hello AzureRmVMDiskEncryptionExtension de jeu peut être utilisé tooencrypt géré disques en spécifiant le paramètre - skipVmBackup de hello.  Cette commande échoue sur les machines virtuelles de disques gérés tant qu’une sauvegarde n’a pas été effectuée et que ce paramètre n’a pas été spécifié.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Mettre à jour les paramètres de chiffrement d’une machine virtuelle non Premium chiffrée existante
  Utilisez hello disque Azure chiffrement pris en charge des interfaces existantes pour l’exécution de machine virtuelle [applets de commande PS, modèles CLI ou ARM] tooupdate paramètres de chiffrement hello comme client AAD ID/secret, clé de cryptage [KEK], clé de chiffrement BitLocker pour la machine virtuelle Windows ou le mot de passe Paramètre de chiffrement de mise à jour etc. de machine virtuelle Linux hello est pris en charge uniquement pour les machines virtuelles soutenus par un stockage non-premium. Il n’est PAS pris en charge pour des machines virtuelles s’appuyant sur un stockage Premium.

## <a name="appendix"></a>Annexe
### <a name="connect-tooyour-subscription"></a>Se connecter tooyour abonnement
Avant de continuer, examinez hello *conditions préalables* dans cet article. Après avoir vérifié que toutes les conditions préalables sont remplies, connexion tooyour abonnement de manière hello suivante :

1. Démarrez une session Azure PowerShell et connectez-vous tooyour compte Azure avec hello de commande suivante :

    `Login-AzureRmAccount`

2. Si vous avez plusieurs abonnements et que vous souhaitez les un toouse toospecify, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :

    `Get-AzureRmSubscription`

3. toospecify hello abonnement toouse, type :

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. tooverify que l’abonnement hello configuré est correct, tapez :

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure chiffrement de disque applets de commande sont installés, type :

    `Get-command *diskencryption*`

6. Hello suivant sortie confirme que l’installation de chiffrement de disque de Azure PowerShell hello :

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Préparer un disque dur virtuel Windows déjà chiffré
les sections Hello qui suivent sont nécessaire tooprepare un disque dur virtuel Windows déjà chiffrés pour le déploiement sous la forme d’un disque dur virtuel chiffré dans Azure IaaS. Utilisez hello informations tooprepare et démarrer une nouvelle machine virtuelle (disque dur virtuel Windows) sur Azure Site Recovery ou sur Azure.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Mettre à jour le groupe stratégie tooallow non TPM pour la protection du système d’exploitation
Configurer le paramètre de stratégie de groupe BitLocker hello **le chiffrement de lecteur BitLocker**, que vous trouverez sous **stratégie ordinateur Local** > **Configuration de l’ordinateur**  >  **Modèles d’administration** > **composants Windows**. Modifier ce paramètre trop**lecteurs de système d’exploitation** > **exiger une authentification supplémentaire au démarrage** > **Autoriser BitLocker sans un module de plateforme sécurisée compatible**, comme illustré dans la figure suivante de hello :

![Microsoft Antimalware dans Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>Installer les composants de fonctionnalité BitLocker
Pour Windows Server 2012 et versions ultérieures, utilisez hello de commande suivante :

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Pour Windows Server 2008 R2, utilisez hello de commande suivante :

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Préparer le volume du système d’exploitation hello pour BitLocker à l’aide`bdehdcfg`
toocompress hello partition du système d’exploitation et préparer l’ordinateur de hello pour BitLocker, exécutez hello de commande suivante :

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>Protéger le volume du système d’exploitation hello à l’aide de BitLocker
Hello d’utilisation [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) chiffrement tooenable de commande sur le volume de démarrage hello à l’aide d’un protecteur de clé externe. Placez également clé externe de hello (fichier .bek) sur un disque externe hello ou un volume. Le chiffrement est activé sur le volume de système de démarrage hello hello prochain redémarrage.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> Préparer hello machine virtuelle avec un disque dur virtuel données/ressources distinct pour l’obtention de clé externe de hello à l’aide de BitLocker.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Chiffrement d’un lecteur du système d’exploitation sur une machine virtuelle Linux en cours d’exécution
Chiffrement d’un lecteur du système d’exploitation sur un VM Linux en cours d’exécution est pris en charge sur hello suivant distributions :

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>Configuration requise pour le chiffrement du lecteur du système d’exploitation

* Hello machine virtuelle doit être créé à partir d’une image Marketplace hello dans Azure Resource Manager.
* Machine virtuelle Azure au moins 4 Go de RAM (la taille recommandée est de 7 Go).
* (Pour RHEL et CentOS) Désactivez SELinux. toodisable SELinux, consultez « 4.4.2. La désactivation de SELinux « Bonjour [Guide l’utilisateur SELinux et d’administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) sur hello machine virtuelle.
* Après avoir désactivé SELinux, redémarrez hello VM au moins une fois.

##### <a name="steps"></a>Étapes
1. Créer une machine virtuelle à l’aide d’une des distributions hello spécifiées précédemment.

 Pour CentOS 7.2, le chiffrement du lecteur du système d’exploitation est pris en charge via une image spécifique. toouse cette image, spécifiez « 7.2n » comme hello référence (SKU) lorsque vous créez hello machine virtuelle :
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Configurer les besoins de tooyour conséquente hello machine virtuelle. Si vous vous apprêtez à tooencrypt tous les lecteurs hello (système d’exploitation + données), les lecteurs de données hello besoin toobe spécifié et montable dans/etc/fstab.

 > [!NOTE]
 > Utilisez UUID =... toospecify lecteurs de données dans/etc/fstab au lieu de spécifier le nom de périphérique du bloc hello (par exemple, / dev/sdb1). Au cours du chiffrement, hello ordre des modifications de lecteurs sur hello machine virtuelle. Si votre machine virtuelle s’appuie sur un ordre spécifique de périphériques de bloc, il échouera toomount après chiffrement.

3. Déconnectez-vous de sessions SSH hello.

4. tooencrypt hello du système d’exploitation, spécifiez volumeType comme **tous les** ou **système d’exploitation** lorsque vous [activer le chiffrement](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Tous les processus d’espace utilisateur qui ne s’exécutent pas en tant que services `systemd` doivent être arrêtés avec un `SIGKILL`. Redémarrez hello machine virtuelle. Lorsque vous activez le chiffrement du lecteur du système d’exploitation sur une machine virtuelle en cours d’exécution, prévoyez un temps d’arrêt de la machine virtuelle.

5. Contrôlez régulièrement la progression hello du chiffrement à l’aide des instructions hello Bonjour [section suivante](#monitoring-os-encryption-progress).

6. Une fois que Get-AzureRmVmDiskEncryptionStatus affiche « VMRestartPending », redémarrez votre machine virtuelle en vous connectant tooit ou en utilisant le portail de hello, PowerShell ou CLI.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Avant de redémarrer, nous recommandons d’enregistrer [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) Hello machine virtuelle.

#### <a name="monitoring-os-encryption-progress"></a>Surveillance de la progression du chiffrement du système d’exploitation
Il existe trois façons de surveiller la progression du chiffrement du système d’exploitation :

* Hello d’utilisation `Get-AzureRmVmDiskEncryptionStatus` applet de commande et d’inspecter le champ de ProgressMessage hello :
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 Une fois hello VM atteint « A démarré le chiffrement du disque du système d’exploitation », il prend environ 40 minutes too50 sur un stockage Premium sauvegardé la machine virtuelle.

 En raison de [l’erreur #388](https://github.com/Azure/WALinuxAgent/issues/388) dans WALinuxAgent, `OsVolumeEncrypted` et `DataVolumesEncrypted` apparaissent comme `Unknown` dans certaines distributions. Ce problème est résolu automatiquement dans WALinuxAgent version 2.1.5 et ultérieure. Si vous voyez `Unknown` dans le résultat de hello, vous pouvez vérifier l’état de chiffrement de disque à l’aide de l’Explorateur de ressources Azure de hello.

 Accédez trop[Explorateur de ressources Azure](https://resources.azure.com/), puis développez cette hiérarchie dans le volet de sélection hello sur gauche :

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Bonjour InstanceView, faites défiler état du chiffrement toosee hello de vos lecteurs.

 ![Vue d’instance de machine virtuelle](./media/azure-security-disk-encryption/vm-instanceview.png)

* Recherchez les [diagnostics de démarrage](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Les messages à partir de l’extension de ADE de hello doivent avoir pour préfixe `[AzureDiskEncryption]`.

* Connectez-vous à toohello machine virtuelle via SSH, puis obtenir le journal à partir de l’extension hello :

    /var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 Il est recommandé que vous ne signez pas dans toohello machine virtuelle alors que le chiffrement du système d’exploitation est en cours d’exécution. Copier les journaux de hello uniquement lorsque hello deux autres méthodes ont échoué.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Préparer un disque dur virtuel Linux déjà chiffré
##### <a name="ubuntu-16"></a>Ubuntu 16
Configurer le chiffrement lors de l’installation de distribution hello de manière hello suivante :

1. Sélectionnez **configurer des volumes chiffrés** lorsque vous partitionnez les disques hello.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Créez un lecteur de démarrage séparé qui ne doit pas être chiffré. Chiffrez votre lecteur racine.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Indiquez une phrase secrète. Il s’agit de hello de mot de passe que vous téléchargez toohello coffre de clés.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Terminez le partitionnement.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Lorsque vous démarrez hello machine virtuelle et que vous êtes invité à entrer un mot de passe, utilisez hello de mot de passe entré à l’étape 3.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Préparer hello machine virtuelle pour le téléchargement dans Azure à l’aide [ces instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).

Configurer le chiffrement toowork avec Azure en procédant comme suit de hello :

1. Créer un fichier sous /usr/local/sbin/azure_crypt_key.sh, avec un contenu hello Bonjour script suivant. Payer une attention toohello KeyFileName, car il est le nom de fichier de mot de passe de hello utilisé par Azure.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Modifier la configuration de chiffrement hello dans *crypttab/etc/*. Il doit se présenter comme suit :
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Si vous modifiez *azure_crypt_key.sh* dans Windows et que vous copié tooLinux, exécutez `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Ajoutez les autorisations exécutable toohello script :
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Éditez */etc/initramfs-tools/modules* en ajoutant des lignes :
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Exécutez `update-initramfs -u -k all` tooupdate Bonjour initramfs toomake Bonjour `keyscript` prennent effet.

7. Vous pouvez désormais annuler le déploiement de hello machine virtuelle.

 ![Configuration d’Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Continuer l’étape suivante de toohello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.

##### <a name="opensuse-132"></a>openSUSE 13.2
chiffrement tooconfigure pendant l’installation de distribution de hello, procédez comme hello suivant :
1. Lorsque vous partitionnez les disques hello, sélectionnez **chiffrer un groupe de volumes**, puis entrez un mot de passe. Il s’agit d’un mot de passe hello que vous allez télécharger tooyour coffre de clés.

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Hello machine virtuelle à l’aide de votre mot de passe de démarrage.

 ![Configuration d’openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Préparation hello machine virtuelle pour le téléchargement tooAzure en suivant les instructions de hello dans [préparer un ordinateur virtuel SLES ou openSUSE Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).

toowork de chiffrement tooconfigure avec Azure, procédez comme hello suivant :
1. Modifier hello /etc/dracut.conf et ajoutez hello ligne suivante :
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Commentez les lignes en fin de hello Hello du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Ajouter hello ligne au début de hello de hello fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh suivante :
 ```
    DRACUT_SYSTEMD=0
 ```
Puis, remplacez toutes les occurrences de :
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
to:
```
    if [ 1 ]; then
```
4. Modifier /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et d’ajouter trop « appareil d’ouvrir LUKS # » :

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Exécutez `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. Maintenant vous pouvez annuler le déploiement de machine virtuelle hello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.

##### <a name="centos-7"></a>CentOS 7
chiffrement tooconfigure pendant l’installation de distribution de hello, procédez comme hello suivant :
1. Sélectionnez **Chiffrer mes données** lors du partitionnement des disques.

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Vérifiez que **Chiffrer** est sélectionné pour la partition racine.

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Indiquez une phrase secrète. Il s’agit de hello de mot de passe que vous allez télécharger tooyour coffre de clés.

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Lorsque vous démarrez hello machine virtuelle et que vous êtes invité à entrer un mot de passe, utilisez hello de mot de passe entré à l’étape 3.

 ![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Préparation hello machine virtuelle pour le téléchargement dans Azure à l’aide des instructions « CentOS 7.0 + » hello [préparer une machine virtuelle CentOS Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). N’exécutez pas encore étape de dernière hello (annulation d’approvisionnement hello machine virtuelle).

6. Maintenant vous pouvez annuler le déploiement de machine virtuelle hello et [télécharger votre disque dur virtuel](#upload-encrypted-vhd-to-an-azure-storage-account) dans Azure.

toowork de chiffrement tooconfigure avec Azure, procédez comme hello suivant :

1. Modifier hello /etc/dracut.conf et ajoutez hello ligne suivante :
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Commentez les lignes en fin de hello Hello du fichier /usr/lib/dracut/modules.d/90crypt/module-setup.sh :
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Ajouter hello ligne au début de hello de hello fichier /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh suivante :
```
    DRACUT_SYSTEMD=0
```
Puis, remplacez toutes les occurrences de :
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
to
```
    if [ 1 ]; then
```
4. Modifier /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh et l’ajouter après hello « appareil d’ouvrir LUKS # » :
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Exécutez hello « / usr/sbin/dracut - f - v « tooupdate hello initrd.

![Configuration de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Télécharger le compte de stockage Azure tooan disque dur virtuel chiffrée
Après l’activation d’un chiffrement BitLocker ou DM-Crypt, hello local chiffré compte de stockage de disque dur virtuel besoins toobe téléchargé tooyour.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Télécharger la clé secrète de chiffrement de disque hello pour hello déjà chiffrés VM tooyour coffre de clés
clé secrète de chiffrement de disque de Hello que vous avez obtenu précédemment doit être téléchargé en tant que secret dans votre coffre de clés. coffre de clés Hello doit toohave le chiffrement des disques et des autorisations activées pour votre client Azure AD.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>La clé secrète de chiffrement de disque non chiffré avec une clé de chiffrement à clé KEK
tooset secret hello dans votre coffre de clés, utilisez [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Si vous avez une machine virtuelle Windows, fichier de bek hello est encodé sous forme de chaîne base64 et puis téléchargé tooyour coffre de clés à l’aide de hello `Set-AzureKeyVaultSecret` applet de commande. Pour Linux, mot de passe hello est encodé sous forme de chaîne base64 de puis téléchargé toohello coffre de clés. En outre, assurez-vous que ce hello les étiquettes suivantes sont définies lorsque vous créez un code secret hello hello coffre de clés.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Hello d’utilisation `$secretUrl` à l’étape suivante de hello pour [attachement du disque du système d’exploitation de hello sans utiliser de clés](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>Disque chiffré avec une clé secrète de chiffrement de disque à clé KEK
Avant de télécharger le coffre de clés secrètes toohello hello, vous pouvez éventuellement le chiffrer à l’aide d’une clé de chiffrement. Retour à la ligne hello utilisation [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst chiffrer secret hello à l’aide de la clé de chiffrement à clé hello. sortie de cette opération de retour à la ligne Hello est une chaîne de URL encodée en base64, ce qui vous pouvez ensuite télécharger en tant que secret à l’aide de hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) applet de commande.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Utilisez `$KeyEncryptionKey` et `$secretUrl` à l’étape suivante de hello pour [attachement du disque hello du système d’exploitation à l’aide de clés](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>Spécifier une URL secrète lorsque vous attachez un lecteur de système d’exploitation
#### <a name="without-using-a-kek"></a>Sans utiliser de clé de chiffrement à clé KEK
Lorsque vous attachez un disque de hello du système d’exploitation, vous devez toopass `$secretUrl`. URL de Hello a été générée dans la section « secret de chiffrement de disque non chiffré avec une clés » de hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>À l’aide d’une clé de chiffrement à clé KEK
Lorsque vous attachez le disque de hello du système d’exploitation, passer `$KeyEncryptionKey` et `$secretUrl`. URL de Hello a été générée dans la section « secret de chiffrement de disque non chiffré avec une clés » de hello.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Télécharger ce guide
Vous pouvez télécharger ce guide hello [Galerie TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Pour plus d’informations
[Explorer Azure Disk Encryption avec Azure PowerShell - partie 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Explorer Azure Disk Encryption avec Azure PowerShell - partie 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
