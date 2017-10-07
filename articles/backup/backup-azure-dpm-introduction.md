---
title: tooback DPM aaaUse portail tooAzure de charges de travail | Documents Microsoft
description: "Un toobacking introduction des serveurs DPM à l’aide du service de sauvegarde Azure hello"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: System Center Data Protection Manager, Data Protection Manager, sauvegarde DPM
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Préparation de tooback des tooAzure les charges de travail avec DPM
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (Classic)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Classic)](backup-azure-dpm-introduction-classic.md)
>
>

Cet article fournit une tooprotect de Microsoft Azure Backup introduction toousing vos serveurs de System Center Data Protection Manager (DPM) et les charges de travail. En le lisant, vous comprendrez :

* le fonctionnement de la sauvegarde du serveur Azure DPM ;
* conditions préalables de Hello tooachieve une meilleure expérience de sauvegarde
* Hello a rencontré des erreurs courantes et comment toodeal avec eux
* Scénarios pris en charge

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Cet article fournit des informations de hello et des procédures pour la restauration d’ordinateurs virtuels déployés à l’aide du modèle de gestionnaire de ressources hello.
>
>

System Center DPM sauvegarde les données des fichiers et des applications. Données sauvegardées tooDPM peuvent être stockées sur une bande, sur disque, ou sauvegardées tooAzure avec Microsoft Azure Backup. DPM interagit avec Azure Backup comme suit :

* **DPM déployé comme un serveur physique ou sur site virtual machine** : si DPM est déployé comme serveur physique ou comme machine virtuelle Hyper-V local vous pouvez sauvegarder des données tooa Services de récupération de coffre de plus de toodisk et sauvegarde sur bande.
* **DPM déployé comme une machine virtuelle Azure** : depuis la mise à jour 3 de System Center 2012 R2, DPM peut être déployé comme une machine virtuelle Azure. Si DPM est déployé comme une machine virtuelle Azure, que vous pouvez sauvegarder les données tooAzure disques attachés toohello une machine virtuelle Azure de DPM, ou vous pouvez décharger le stockage de données hello en le sauvegardant tooa de coffre Recovery Services.

## <a name="why-backup-from-dpm-tooazure"></a>Pourquoi sauvegarder à partir de DPM tooAzure ?
Hello entreprise de l’utilisation d’Azure Backup pour sauvegarder des serveurs DPM principaux avantages :

* Pour le déploiement du DPM local, vous pouvez utiliser Azure comme un tootape de déploiement autre toolong à long terme.
* Pour les déploiements DPM dans Azure, Azure Backup permet le stockage toooffload d’hello disque Azure, ce qui vous tooscale en stockant les données plus anciennes dans le coffre Recovery Services et les données sur le disque.

## <a name="prerequisites"></a>Composants requis
Préparez tooback Azure sauvegarde des données DPM comme suit :

1. **Créer un coffre Recovery Services** : créez un coffre dans le portail Azure.
2. **Télécharger les informations d’identification de coffre** : télécharger des informations d’identification hello que vous pouvez utiliser tooregister hello DPM server tooRecovery de coffre de Services.
3. **Installer hello Azure Backup Agent** : à partir de Azure Backup, installez l’agent de hello sur chaque serveur DPM.
4. **Inscrire le serveur de hello** : Register hello DPM serveur tooRecovery Services dans l’archivage.

### <a name="1-create-a-recovery-services-vault"></a>1. Créer un coffre Recovery Services
toocreate une récupération des services de coffre :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **Parcourir** et, dans la liste hello des ressources, tapez **Recovery Services**. Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée. Cliquez sur **Coffre Recovery Services**.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    liste de Hello des coffres des Services de récupération s’affiche.
3. Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.

    ![Créer un archivage de Recovery Services - Étape 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Pour **nom**, entrez un coffre de hello tooidentify nom convivial. nom de Hello doit toobe unique pour hello abonnement Azure. Tapez un nom contenant entre 2 et 50 caractères. Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.
5. Cliquez sur **abonnement** toosee hello liste abonnements. Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement. Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.
6. Cliquez sur **groupe de ressources** toosee hello la liste des groupes de ressources disponibles, ou cliquez sur **nouveau** toocreate un groupe de ressources. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Cliquez sur **emplacement** tooselect hello région pour le coffre hello.
8. Cliquez sur **Créer**. Il peut prendre un certain temps pour hello toobe créé de coffre de Services de récupération. Surveiller les notifications d’état hello dans hello supérieur droit dans le portail de hello.
   Une fois votre coffre est créé, il s’ouvre dans le portail de hello.

### <a name="set-storage-replication"></a>Définir la réplication du stockage
option de réplication de stockage Hello permet toochoose entre le stockage géo-redondant et le stockage localement redondant. Par défaut, votre archivage utilise un stockage géo-redondant. Laissez le stockage redondant toogeo option hello si c’est votre principal de la sauvegarde. Choisissez Stockage localement redondant si vous souhaitez une option plus économique, mais moins durable. En savoir plus sur [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage) des options de stockage Bonjour [vue d’ensemble de la réplication de stockage Azure](../storage/common/storage-redundancy.md).

paramètre de réplication de stockage tooedit hello :

1. Sélectionnez votre tableau de bord coffre tooopen hello coffre et le panneau des paramètres hello. Si hello **paramètres** panneau ne s’ouvre, cliquez sur **tous les paramètres** dans le tableau de bord coffre hello.
2. Sur hello **paramètres** panneau, cliquez sur **sauvegarde Infrastructure** > **Configuration de la sauvegarde** tooopen hello **Configurationdelasauvegarde** panneau. Sur hello **Configuration de la sauvegarde** panneau, choisissez l’option de réplication de stockage hello pour votre archivage.

    ![Liste des archivages de sauvegarde](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Après avoir choisi l’option de stockage hello pour votre archivage, vous êtes prêt tooassociate hello machine virtuelle avec le coffre de hello. association de hello toobegin, vous devez découvrir et inscrire hello des machines virtuelles.

### <a name="2-download-vault-credentials"></a>2. Télécharger les informations d'identification de coffre
fichier d’informations d’identification de coffre Hello est un certificat généré par le portail hello chaque coffre de sauvegarde. portail de Hello télécharge ensuite toohello de clé publique hello Access Control Service (ACS). clé privée de Hello du certificat de hello est effectuée utilisateur toohello disponibles dans le cadre du flux de travail hello qui est fournie sous la forme d’une entrée dans le workflow de l’inscription d’ordinateur hello. Cela permet d’authentifier hello machine toosend les données de sauvegarde tooan identifié coffre Bonjour service Azure Backup.

informations d’identification de coffre Hello sont utilisée uniquement pendant le flux de travail de l’inscription hello. Il est tooensure de responsabilité de l’utilisateur hello qui hello des informations d’identification de coffre fichier n’est pas compromis. S’il est compris entre les mains hello de n’importe quel utilisateur non autorisé, fichier d’informations d’identification de coffre hello peut être utilisé tooregister autres ordinateurs hello même coffre. Toutefois, comme les données de sauvegarde hello sont chiffrées à l’aide d’une phrase secrète qui appartient toohello client, les données de sauvegarde existantes ne peut pas être compromises. toomitigate ce problème, les informations d’identification de coffre sont définies tooexpire dans 48hrs. Vous pouvez télécharger des informations d’identification de coffre hello de services de récupération n’importe quel nombre de fois, mais uniquement hello dernière coffre d’informations d’identification est applicable au cours de flux de travail de l’inscription hello.

fichier d’informations d’identification de coffre Hello est téléchargé via un canal sécurisé à partir de hello portail Azure. Hello service Azure Backup n’a pas connaissance de la clé privée de hello du certificat de hello et la clé privée de hello n’est pas conservé dans le portail de hello ou un service de hello. Utilisez hello suivant les étapes toodownload hello coffre informations d’identification du fichier tooa ordinateur local.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Ouvrez toowhich Services de récupération de coffre toowhich vous souhaitez que l’ordinateur DPM tooregister.
3. Le panneau Paramètres s’ouvre par défaut. S’il est fermé, cliquez sur **paramètres** dans le panneau Paramètres hello coffre du tableau de bord tooopen. Dans le panneau Paramètres, cliquez sur **Propriétés**.

    ![Ouvrir le panneau de l’archivage](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. Dans la page de propriétés hello, cliquez sur **télécharger** sous **informations d’identification de la sauvegarde**. portail de Hello génère fichier d’informations d’identification du coffre de hello qui devient disponible en téléchargement.

    ![Télécharger](./media/backup-azure-dpm-introduction/vault-credentials.png)

portail de Hello générera une information d’identification de coffre à l’aide d’une combinaison de nom de l’archivage hello et hello date actuelle. Cliquez sur **enregistrer** toodownload hello coffre informations d’identification toohello du compte local télécharge le dossier ou sélectionnez Enregistrer sous à partir de hello enregistrer menu toospecify un emplacement pour les informations d’identification de coffre hello. Il occupera tooa minute hello toobe de fichier généré.

### <a name="note"></a>Remarque
* Vérifiez que ce fichier d’informations d’identification de coffre hello est enregistré dans un emplacement qui est accessible à partir de votre ordinateur. S’il est stocké dans un partage de fichier/SMB, recherchez les autorisations d’accès hello.
* fichier d’informations d’identification de coffre Hello est utilisé uniquement pendant le flux de travail de l’inscription hello.
* fichier d’informations d’identification de coffre Hello expire au bout de 48hrs et peut être téléchargé à partir du portail de hello.

### <a name="3-install-backup-agent"></a>3. Installer l’agent de sauvegarde
Après avoir créé le coffre de sauvegarde Azure hello, un agent doit être installé sur chacun de vos ordinateurs Windows (Windows Server, Windows client, serveur de System Center Data Protection Manager ou ordinateur du serveur de sauvegarde Azure) qui permet de sauvegarder des données et applications tooAzure.

1. Ouvrez toowhich Services de récupération de coffre toowhich vous souhaitez que l’ordinateur DPM tooregister.
2. Le panneau Paramètres s’ouvre par défaut. S’il est fermé, cliquez sur **paramètres** Panneau de paramètres tooopen hello. Dans le panneau Paramètres, cliquez sur **Propriétés**.

    ![Ouvrir le panneau de l’archivage](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. Dans la page Paramètres de hello, cliquez sur **télécharger** sous **Azure Backup Agent**.

    ![Télécharger](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Une fois que l’agent de hello est téléchargé, double-cliquez sur MARSAgentInstaller.exe toolaunch hello l’installation de hello Azure Backup agent. Choisissez le dossier d’installation hello et le dossier de travail requis pour l’agent de hello. emplacement de cache de Hello spécifié doit disposer de l’espace libre qui est au moins 5 % des données de sauvegarde hello.
4. Si vous utilisez un toohello tooconnect du serveur proxy internet, Bonjour **configuration Proxy** écran, entrez les détails du serveur proxy hello. Si vous utilisez un proxy authentifié, entrez les détails de nom et mot de passe utilisateur hello dans cet écran.
5. agent de sauvegarde Azure Hello installe .NET Framework 4.5 et Windows PowerShell (si elle n’est disponible) installation de hello toocomplete.
6. Une fois installé, l’agent de hello **fermer** fenêtre hello.

   ![fermez](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. trop**hello d’inscrire le serveur DPM** toohello coffre-fort, hello **gestion** onglet, cliquez sur **Online**. Sélectionnez ensuite **Inscription**. Hello Assistant d’enregistrement du programme d’installation s’ouvre.
8. Si vous utilisez un toohello tooconnect du serveur proxy internet, Bonjour **configuration Proxy** écran, entrez les détails du serveur proxy hello. Si vous utilisez un proxy authentifié, entrez les détails de nom et mot de passe utilisateur hello dans cet écran.

    ![Configuration du proxy](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. Dans l’écran informations d’identification de coffre hello, accédez à fichier tooand hello sélectionnez coffre informations d’identification qui a été téléchargée antérieurement.

    ![Informations d’identification du coffre](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    fichier d’informations d’identification de coffre Hello est valide uniquement pour 48 heures (après l’avoir téléchargée à partir du portail de hello). Si vous rencontrez une erreur dans cet écran (par exemple, « Archivage des informations d’identification de fichier fourni a expiré »), connexion toohello Azure portal et téléchargement hello coffre informations d’identification le fichier à nouveau.

    Vérifiez que ce fichier d’informations d’identification de coffre hello est disponible dans un emplacement qui est accessible par l’application d’installation de hello. Si vous rencontrez des erreurs connexes d’accès, informations d’identification du coffre copie hello tooa temporaire sur cet ordinateur et de recommencer l’opération de hello.

    Si vous rencontrez une erreur d’informations d’identification de coffre non valide (par exemple, « coffre non valide les informations d’identification fournies ») des fichiers de hello est endommagé ou ne pas avoir hello dernières informations d’identification associées au service de récupération hello. Recommencez l’opération hello après avoir téléchargé un nouveau fichier d’informations d’identification de coffre à partir du portail de hello. Cette erreur se produit généralement si l’utilisateur de hello clique sur hello **informations d’identification du coffre de téléchargement** option Bonjour portail Azure, de suite. Dans ce cas, uniquement hello deuxième coffre informations d’identification du fichier est valide.
10. l’utilisation de hello toocontrol de la bande passante réseau pendant le travail et les heures chômées, Bonjour **paramètre de limitation** écran, vous pouvez définir des limites de l’utilisation de la bande passante hello et définir un travail de hello et non liés au travail heures.

    ![Paramètre de limitation](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. Bonjour **paramètre du dossier récupération** écran, recherchez le dossier hello où les fichiers de hello téléchargés à partir d’Azure intermédiaire sera temporairement créé.

    ![Paramètre de dossier de récupération](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. Bonjour **paramètre de chiffrement** écran, vous pouvez générer un mot de passe ou fournissez une phrase secrète (16 caractères au minimum). N’oubliez pas de mot de passe toosave hello dans un emplacement sécurisé.

    ![Chiffrement](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Si hello le mot de passe est perdu ou oublié ; L’aide de Microsoft ne peut pas récupérer les données de sauvegarde hello. utilisateur final de Hello possède la phrase secrète de chiffrement hello et Microsoft n’a pas de visibilité hello de mot de passe utilisé par l’utilisateur final de hello. Enregistrez les fichiers hello dans un emplacement sécurisé comme requis pendant une opération de récupération.
    >
    >
13. Une fois que vous cliquez sur hello **inscrire** bouton, hello est inscrit correctement toohello coffre et que vous êtes maintenant prêt toostart sauvegarde tooMicrosoft Azure.
14. Lorsque vous utilisez Data Protection Manager, vous pouvez modifier les paramètres de hello spécifiées pendant le flux de travail de l’inscription hello en cliquant sur hello **configurer** option en sélectionnant **Online** sous hello  **Gestion** onglet.

## <a name="requirements-and-limitations"></a>Spécifications (et limitations)
* DPM peut s'exécuter en tant que serveur physique ou machine virtuelle Hyper-V installée sur System Center 2012 SP1 ou System Center 2012 R2. DPM peut également s'exécuter en tant que machine virtuelle Azure sur System Center 2012 R2 avec au moins le correctif cumulatif 3 pour DPM 2012 R2, ou en tant que machine virtuelle Windows dans VMWare sur System Center 2012 R2 avec au moins le correctif cumulatif 5.
* Si vous exécutez DPM avec System Center 2012 SP1, vous devez installer le correctif cumulatif 2 pour System Center Data Protection Manager SP1. Cela est nécessaire avant de pouvoir installer hello Azure Backup Agent.
* le serveur DPM Hello doit avoir Windows PowerShell et .net Framework 4.5 est installé.
* DPM peut sauvegarder la plupart des charges de travail tooAzure sauvegarde. Pour obtenir la liste complète de ce qui a pris en charge Voir hello Azure Backup prend en charge les éléments ci-dessous.
* Impossible de récupérer les données stockées dans Azure Backup avec l’option de « copier tootape » hello.
* Vous devez avoir un compte Azure avec fonctionnalité Azure Backup hello est activée. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. En savoir plus sur la [tarification d'Azure Backup](https://azure.microsoft.com/pricing/details/backup/).
* À l’aide d’Azure Backup nécessite hello toobe de l’Agent Azure Backup installé sur les serveurs hello souhaité tooback des. Chaque serveur doit avoir au moins 5 % de la taille de hello des données hello sont en cours de sauvegarde, disponible en tant qu’espace de stockage local. Par exemple, la sauvegarde de 100 Go de données nécessite un minimum de 5 Go d’espace libre dans l’emplacement de fichier temporaire hello.
* Bonjour, stockage d’archivage Azure, les données seront stockées. Il n’existe aucun montant de toohello limite de données, que vous pouvez sauvegarder le coffre Azure Backup tooan mais taille hello d’une source de données (par exemple un ordinateur virtuel ou une base de données) ne doit pas dépasser 54400 go.

Ces types de fichiers sont pris en charge pour tooAzure de sauvegarde :

* Chiffré (sauvegardes complètes uniquement)
* Compressé (sauvegardes incrémentielles prises en charge)
* Partiellement alloué (sauvegardes incrémentielles prises en charge)
* Compressé et partiellement alloué (traité comme partiellement alloué)

Et les types suivants ne sont pas pris en charge :

* Les serveurs sur des systèmes de fichiers respectant la casse ne sont pas pris en charge.
* Liens physiques (ignorés)
* Points d'analyse (ignorés)
* Chiffré et compressé (ignoré)
* Chiffré et partiellement alloué (ignoré)
* Flux compressé
* Flux partiellement alloué

> [!NOTE]
> À partir de System Center 2012 DPM avec SP1, vous pouvez sauvegarder des charges de travail protégés par tooAzure DPM à l’aide de Microsoft Azure Backup.
>
>
