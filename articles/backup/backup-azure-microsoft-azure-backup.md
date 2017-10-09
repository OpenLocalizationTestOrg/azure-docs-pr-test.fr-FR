---
title: "tooback d’Azure Backup Server aaaUse des charges de travail tooAzure | Documents Microsoft"
description: Utiliser Azure Backup Server tooprotect ou sauvegarder des charges de travail toohello portail Azure.
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: azure backup server; protect workloads; back up workloads
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Préparation de tooback des charges de travail à l’aide d’Azure Backup Server
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Cet article explique comment tooprepare tooback de votre environnement des charges de travail à l’aide d’Azure Backup Server. Le serveur de sauvegarde Azure vous permet de protéger des charges de travail d’application telles que des machines virtuelles Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange et des clients Windows à partir d’une console unique.

> [!NOTE]
> Serveur de sauvegarde Azure peut désormais protéger les machines virtuelles VMware et fournit des fonctionnalités de sécurité améliorées. Installer le produit de hello comme expliqué dans les sections hello ci-dessous ; appliquer la mise à jour 1 et hello plus récente d’Azure Backup Agent. toolearn en savoir plus sur la sauvegarde de serveurs VMware avec Azure Backup Server, consultez l’article hello, [tooback utilisez Azure Backup Server d’un serveur VMware](backup-azure-backup-server-vmware.md). toolearn sur les fonctionnalités de sécurité, consultez trop[documentation des fonctionnalités de sécurité de la sauvegarde Azure](backup-azure-security-feature.md).
>
>

Vous pouvez également protéger les charges de travail Iaas, telles que les machines virtuelles dans Azure.

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Cet article fournit des informations de hello et des procédures pour la restauration d’ordinateurs virtuels déployés à l’aide du modèle de gestionnaire de ressources hello.
>
>

Serveur de sauvegarde Azure une grande partie de la fonctionnalité de sauvegarde de la charge de travail hello hérite de Data Protection Manager (DPM). Cet article lie tooDPM documentation tooexplain hello certaines des fonctionnalités partagées. Bien que Azure Backup Server partage une grande partie de hello même fonctionnalité que DPM. N’est pas le cas du serveur de sauvegarde Azure sauvegarder tootape, ni s’intègre avec System Center.

## <a name="1-choose-an-installation-platform"></a>1. Choisir une plateforme d’installation
première étape de Hello la route hello Azure Backup Server est tooset d’un serveur Windows. Il peut s’agir d’un serveur local ou d’un serveur dans Azure.

### <a name="using-a-server-in-azure"></a>Utilisation d’un serveur dans Azure
Lors du choix d’un serveur pour l’exécution d’Azure Backup Server, il est recommandé de commencer par une image de la galerie de Windows Server 2012 R2 Datacenter. l’article Hello, [créer votre première machine virtuelle de Windows Bonjour Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), propose un didacticiel de mise en route avec hello recommandée de machine virtuelle dans Azure, même si vous n’avez jamais utilisé Azure avant. Hello recommandé configuration minimale requise pour hello serveur virtual machine (VM) doit être : A2 Standard avec deux cœurs et 3,5 Go de RAM.

La protection des charges de travail à l’aide d’Azure Backup Server peut prendre plusieurs formes. l’article Hello, [Install DPM as d’une machine virtuelle Azure](https://technet.microsoft.com/library/jj852163.aspx), permet d’expliquer ces nuances. Avant de déployer un ordinateur de hello, lisez cet article complètement.

### <a name="using-an-on-premises-server"></a>Utilisation d’un serveur local
Si vous ne souhaitez pas le serveur de base toorun hello dans Azure, vous pouvez exécuter le serveur de hello sur une machine virtuelle Hyper-V, un VM VMware ou un hôte physique. Hello recommandé la configuration minimale requise pour le matériel de serveur hello est deux cœurs et 4 Go de RAM. les systèmes d’exploitation Hello pris en charge sont répertoriés dans hello tableau suivant :

| Système d’exploitation | Plateforme | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 et derniers Service Packs |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 et derniers Service Packs |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 et derniers Service Packs |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 et derniers Service Packs |64 bits |Standard, Workgroup |

Vous pouvez dédupliquer le stockage DPM hello à l’aide de la déduplication de Windows Server. En savoir plus sur le fonctionnement du [DPM et de la déduplication](https://technet.microsoft.com/library/dn891438.aspx) en cas de déploiement sur des ordinateurs virtuels Hyper-V.

> [!NOTE]
> Serveur de sauvegarde Azure est conçue toorun sur un serveur dédié à fonction unique. Vous ne pouvez pas installer le serveur de sauvegarde Azure sur :
> - Un ordinateur servant de contrôleur de domaine
> - Un ordinateur sur le serveur d’applications hello rôle est installé
> - Un ordinateur qui est un serveur d’administration de System Center Operations Manager
> - Un ordinateur sur lequel Exchange Server s’exécute
> - Un ordinateur qui est un nœud d’un cluster

Toujours vous joindre Azure Backup Server tooa domaine. Si vous envisagez de domaine différent du tooa serveur hello toomove, il est recommandé que vous joignez un nouveau domaine hello server toohello avant d’installer le serveur de sauvegarde Azure. Déplacement d’un serveur de sauvegarde Azure existant de l’ordinateur tooa nouveau domaine après le déploiement est *ne pas pris en charge*.

## <a name="2-recovery-services-vault"></a>2. Coffre Recovery Services
Si vous envoyez des données de sauvegarde tooAzure ou qu’il soit localement, les logiciels hello doivent toobe connecté tooAzure. toobe plus spécifique, ordinateur de serveur de sauvegarde Azure hello doit toobe inscrit auprès d’un coffre de services de récupération.

toocreate une récupération des services de coffre :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **Parcourir** et, dans la liste hello des ressources, tapez **Recovery Services**. Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Cliquez sur **Coffre Recovery Services**.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    liste de Hello des coffres des Services de récupération s’affiche.
3. Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.

    ![Créer un archivage de Recovery Services - Étape 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Pour **nom**, entrez un coffre de hello tooidentify nom convivial. nom de Hello doit toobe unique pour hello abonnement Azure. Tapez un nom contenant entre 2 et 50 caractères. Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.
5. Cliquez sur **abonnement** toosee hello liste abonnements. Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement. Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.
6. Cliquez sur **groupe de ressources** toosee hello la liste des groupes de ressources disponibles, ou cliquez sur **nouveau** toocreate un groupe de ressources. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Cliquez sur **emplacement** tooselect hello région pour le coffre hello.
8. Cliquez sur **Créer**. Il peut prendre un certain temps pour hello toobe créé de coffre de Services de récupération. Surveiller les notifications d’état hello dans hello supérieur droit dans le portail de hello.
   Une fois votre coffre est créé, il s’ouvre dans le portail de hello.

### <a name="set-storage-replication"></a>Définir la réplication du stockage
option de réplication de stockage Hello permet toochoose entre le stockage géo-redondant et le stockage localement redondant. Par défaut, votre archivage utilise un stockage géo-redondant. Si ce coffre est votre coffre principal, laissez hello option ensemble toogeo redondante de stockage. Choisissez Stockage localement redondant si vous souhaitez une option plus économique, mais moins durable. En savoir plus sur [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage) des options de stockage Bonjour [vue d’ensemble de la réplication de stockage Azure](../storage/common/storage-redundancy.md).

paramètre de réplication de stockage tooedit hello :

1. Sélectionnez votre tableau de bord coffre tooopen hello coffre et le panneau des paramètres hello. Si hello **paramètres** panneau ne s’ouvre, cliquez sur **tous les paramètres** dans le tableau de bord coffre hello.
2. Sur hello **paramètres** panneau, cliquez sur **sauvegarde Infrastructure** > **Configuration de la sauvegarde** tooopen hello **Configurationdelasauvegarde** panneau. Sur hello **Configuration de la sauvegarde** panneau, choisissez l’option de réplication de stockage hello pour votre archivage.

    ![Liste des archivages de sauvegarde](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Après avoir choisi l’option de stockage hello pour votre archivage, vous êtes prêt tooassociate hello machine virtuelle avec le coffre de hello. association de hello toobegin, vous devez découvrir et inscrire hello des machines virtuelles.

## <a name="3-software-package"></a>3. Package logiciel
### <a name="downloading-hello-software-package"></a>Téléchargement du package de logiciel hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Si vous avez déjà ouvert un coffre Recovery Services, passez toostep 3. Si vous n’avez pas d’un coffre Recovery Services est ouvert, mais sont Bonjour portail Azure, dans le menu du Hub hello, cliquez sur **Parcourir**.

   * Dans la liste de hello des ressources, tapez **Recovery Services**.
   * Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

     ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     liste Hello des archivages de Recovery Services s’affiche.
   * À partir de la liste de hello des archivages de Recovery Services, sélectionnez un coffre.

     tableau de bord Hello coffre-fort sélectionné s’ouvre.

     ![Ouvrir le panneau de l’archivage](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Hello **paramètres** panneau s’ouvre par défaut. S’il est fermé, cliquez sur **paramètres** Panneau de paramètres tooopen hello.

    ![Ouvrir le panneau de l’archivage](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Cliquez sur **sauvegarde** Assistant de mise en route tooopen hello.

    ![Prise en main de la sauvegarde](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    Bonjour **mise en route de la sauvegarde** panneau s’ouvre, **sauvegarde objectifs** seront sélectionnés automatiquement.

    ![Backup-goals-default-opened](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. Bonjour **sauvegarde objectif** panneau, à partir de hello **votre charge de travail exécutant** menu, sélectionnez **local**.

    ![en local et charges de travail comme objectifs](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    À partir de hello **comment vous souhaitez toobackup ?** menu déroulant, les charges de travail hello Sélectionnez votre choix tooprotect à l’aide d’Azure Backup Server, puis cliquez sur **OK**.

    Hello **mise en route de la sauvegarde** Assistant commutateurs hello **Prepare infrastructure** tooback option des charges de travail tooAzure.

   > [!NOTE]
   > Si vous souhaitez uniquement tooback des fichiers et des dossiers, nous recommandons à l’aide de l’agent de sauvegarde Azure hello et en suivant les instructions de hello dans l’article hello, [tout d’abord rechercher : sauvegarder des fichiers et dossiers](backup-try-azure-backup-in-10-mins.md). Si vous vous apprêtez tooprotect plusieurs fichiers et dossiers ou vous envisagez de protection de hello tooexpand doit dans un avenir hello, sélectionnez ces charges de travail.
   >
   >

    ![Modification de l’Assistant Mise en route](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. Bonjour **Prepare infrastructure** panneau que s’ouvre, cliquez sur hello **télécharger** liens pour installer Azure Backup Server et les informations d’identification du coffre de téléchargement. Vous utilisez des informations d’identification de coffre hello pendant l’inscription du coffre Azure Backup Server toohello recovery services. les liens Hello prennent toohello centre de téléchargement où hello package logiciel peut être téléchargé.

    ![Préparer l’infrastructure pour Azure Backup Server](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Sélectionnez tous les fichiers hello et cliquez sur **suivant**. Téléchargement que tous hello fichiers provenant d’une page de téléchargement de Microsoft Azure Backup hello et place que tous les hello dans les fichiers hello même dossier.

    ![Centre de téléchargement 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Étant hello taille du téléchargement de tous les fichiers hello ensemble > 3G, minutes pour hello téléchargent sur un lien de téléchargement de 10 Mbits/s que peut prendre jusqu'à too60 toocomplete.

### <a name="extracting-hello-software-package"></a>Extraction du package de logiciel hello
Une fois que vous avez téléchargé tous les fichiers de hello, cliquez sur **MicrosoftAzureBackupInstaller.exe**. Ceci démarrera hello **Assistant Installation de Microsoft Azure sauvegarde** le programme d’installation de tooextract hello fichiers emplacement tooa que vous avez spécifié. Suivez les instructions de l’Assistant de hello et cliquez sur hello **extraire** bouton processus d’extraction de hello toobegin.

> [!WARNING]
> Au moins 4 Go d’espace libre est les fichiers d’installation requis tooextract hello.
>
>

![L’Assistant Installation de Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Une fois hello extraction terminée, hello de toolaunch case à cocher hello fraîchement extrait *setup.exe* toobegin l’installation de Microsoft Azure Backup Server, puis cliquez sur hello **Terminer** bouton.

### <a name="installing-hello-software-package"></a>Installation du package de logiciel hello
1. Cliquez sur **Microsoft Azure Backup** Assistant d’installation toolaunch hello.

    ![L’Assistant Installation de Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. Sur l’écran d’accueil hello, cliquez sur hello **suivant** bouton. Vous accéderez toohello *Prerequisite Checks* section. Dans cet écran, cliquez sur **vérifier** toodetermine si hello matérielle et logicielle requise pour Azure Backup Server ont été remplies. Si toutes les conditions préalables sont remplies avec succès, vous verrez un message indiquant que l’ordinateur hello répond aux besoins de hello. Cliquez sur hello **suivant** bouton.

    ![Azure Backup Server - Accueil et contrôle des conditions préalables requises](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Microsoft Azure Backup Server nécessite SQL Server Standard, et le package d’installation du serveur de sauvegarde Azure hello est fourni avec des fichiers binaires SQL Server appropriés de hello nécessités. Lorsque vous démarrez avec une nouvelle installation du serveur de sauvegarde Azure, vous devez choisir les option hello **installer de nouvelle Instance de SQL Server avec ce programme d’installation** et cliquez sur hello **vérifier et installer** bouton. Une fois les conditions préalables de hello sont correctement installés, cliquez sur **suivant**.

    ![Serveur de sauvegarde Azure - Vérification SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Si une défaillance se produit avec un ordinateur de hello recommandation toorestart, dans ce cas, cliquez sur **vérifier à nouveau**.

   > [!NOTE]
   > Azure Backup Server ne fonctionne pas avec une instance de serveur SQL distante. instance Hello utilisé par le serveur de sauvegarde Azure doit toobe local.
   >
   >
4. Fournir un emplacement pour l’installation de hello des fichiers du serveur Microsoft Azure Backup, puis cliquez sur **suivant**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    emplacement de fichier temporaire Hello est obligatoire pour tooAzure de sauvegarde. Vérifiez l’emplacement hello est au moins 5 % des données de salutation planifié toobe sauvegardée toohello cloud. Pour la protection des disques, des disques distincts doivent toobe configuré une fois hello installation terminée. Pour plus d’informations sur les pools de stockage, consultez [Configurer des pools de stockage et de stockage sur disque](https://technet.microsoft.com/library/hh758075.aspx).
5. Fournissez un mot de passe fort pour les comptes utilisateur locaux restreints et cliquez sur **Suivant**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Indiquez si vous souhaitez toouse *Microsoft Update* toocheck pour les mises à jour et cliquez sur **suivant**.

   > [!NOTE]
   > Nous vous conseillons Windows Update rediriger tooMicrosoft mise à jour, ce qui offre une sécurité et des mises à jour importantes pour Windows et d’autres produits tels que Microsoft Azure Backup Server.
   >
   >

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Hello de révision *résumé des paramètres* et cliquez sur **installer**.

    ![Microsoft Azure Backup PreReq2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. installation de Hello se produit en plusieurs phases. Bonjour phase de la première hello Microsoft Azure Recovery Services Agent est installé sur le serveur de hello. Assistant de Hello vérifie également pour la connectivité Internet. Si la connectivité Internet est disponible vous pouvez poursuivre l’installation, si ce n’est pas, vous devez tooprovide proxy détails tooconnect toohello Internet.

    étape suivante de Hello est tooconfigure hello Microsoft Azure Recovery Services Agent. Dans le cadre de la configuration de hello, vous devez tooprovide vos services de récupération coffre informations d’identification machine tooregister hello toohello coffre. Elle fournit également une phrase secrète tooencrypt/decrypt hello les données envoyées entre Azure et votre environnement local. Vous pouvez automatiquement générer une phrase secrète ou fournir votre propre phrase secrète d’au minimum 16 caractères. Continuer avec l’Assistant de hello jusqu'à ce que l’agent de hello a été configuré.

    ![PreReq2 de serveur de sauvegarde Azure](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Une fois l’inscription du serveur de Microsoft Azure Backup hello terminée avec succès, hello globale Assistant d’installation poursuit toohello installation et configuration de SQL Server et les composants du serveur de sauvegarde Azure hello. Une fois hello installation des composants SQL Server terminée, les composants du serveur de sauvegarde Azure hello sont installés.

    ![Azure Backup Server](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Lors de l’étape d’installation hello terminée, hello icônes du bureau du produit seront créées ainsi. Simplement double-cliquer sur le produit de hello icône toolaunch hello.

### <a name="add-backup-storage"></a>Ajouter de l’espace de stockage pour la sauvegarde
première copie de sauvegarde Hello est conservé sur le stockage attaché toohello machine du serveur de sauvegarde Azure. Pour plus d’informations sur l’ajout de disques, consultez la section [Configurer des pools de stockage et un disque de stockage](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Vous avez besoin de stockage de sauvegarde tooadd même si vous envisagez de toosend données tooAzure. Dans l’architecture actuelle hello du serveur de sauvegarde Azure, le coffre de sauvegarde Azure hello conserve hello *deuxième* copie des données hello pendant que le stockage local de hello conserve hello premier (et obligatoire) copie de sauvegarde.
>
>

## <a name="4-network-connectivity"></a>4. Connectivité réseau
Serveur de sauvegarde Azure requiert service de sauvegarde Azure toohello de connectivité pour hello produit toowork avec succès. toovalidate si la machine de hello a hello connectivité tooAzure, utilisez hello ```Get-DPMCloudConnection``` applet de commande dans la console du serveur de sauvegarde Azure PowerShell hello. Si hello sortie de l’applet de commande hello est TRUE, puis il existe une connectivité, sinon il n’existe aucune connectivité.

Hello simultanément, hello abonnement Azure doit toobe dans un état sain. toofind état hello de votre abonnement et de toomanage il, ouvrez une session toohello [portal d’abonnement](https://account.windowsazure.com/Subscriptions).

Une fois que vous connaissez état hello hello connectivité Azure et hello abonnement Azure, vous pouvez utiliser la table hello ci-dessous toofind out impact de hello sur les fonctionnalités de sauvegarde/restauration hello offertes.

| État de la connectivité | Abonnement Azure | Sauvegarder tooAzure | Sauvegarder toodisk | Restauration à partir d’Azure | Restauration à partir d’un disque |
| --- | --- | --- | --- | --- | --- |
| Connecté |Actif |Autorisé |Autorisé |Autorisé |Autorisé |
| Connecté |Expiré |Arrêté |Arrêté |Autorisé |Autorisé |
| Connecté |Approvisionnement annulé |Arrêté |Arrêté |Arrêté et points de restauration Azure supprimés |Arrêté |
| Connectivité perdue depuis > 15 jours |Actif |Arrêté |Arrêté |Autorisé |Autorisé |
| Connectivité perdue depuis > 15 jours |Expiré |Arrêté |Arrêté |Autorisé |Autorisé |
| Connectivité perdue depuis > 15 jours |Approvisionnement annulé |Arrêté |Arrêté |Arrêté et points de restauration Azure supprimés |Arrêté |

### <a name="recovering-from-loss-of-connectivity"></a>Récupération après la perte de connectivité
Si vous avez un pare-feu ou un proxy qui empêche l’accès tooAzure, vous devez hello toowhitelist suivant des adresses de domaine dans le profil de pare-feu/proxy hello :

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Une fois la connectivité tooAzure a été restaurée toohello Azure sauvegarde du serveur, les opérations hello qui peuvent être effectuées sont déterminées par hello état de l’abonnement Azure. tableau Hello ci-dessus a plus d’informations sur les opérations hello autorisées une fois que l’ordinateur de hello est « connecté ».

### <a name="handling-subscription-states"></a>Gestion des états d’abonnement
Il est possible tootake un abonnement Azure à partir d’un *expiré* ou *Deprovisioned* état toohello *Active* état. Toutefois cela a des conséquences sur le comportement du produit hello pendant que l’état de hello n’est pas *Active*:

* A *Deprovisioned* abonnement perd la fonctionnalité hello période pour laquelle il est annulé. Sur l’activation *Active*, fonctionnalités du produit de sauvegarde/restauration hello sont réactivée. les données de sauvegarde Hello sur le disque local hello peuvent également être récupérées si elle a été conservé avec une période de rétention suffisante. Toutefois, les données de sauvegarde hello dans Azure sont irrémédiablement perdues dès que l’abonnement de hello atteint hello *Deprovisioned* état.
* Un abonnement *Expiré* ne fonctionne plus tant qu’il n’a pas été *réactivé*. Toutes les sauvegardes planifiées pour la période de hello hello d’abonnement a été *expiré* ne s’exécutera pas.

## <a name="troubleshooting"></a>Résolution des problèmes
Si Microsoft Azure Backup server échoue avec des erreurs pendant la phase d’installation hello (ou de sauvegarde ou de restauration), consultez toothis [document de codes d’erreur](https://support.microsoft.com/kb/3041338) pour plus d’informations.
Vous pouvez également faire référence trop[Azure Backup liées à des questions fréquentes](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez obtenir des informations détaillées [préparation de votre environnement pour DPM](https://technet.microsoft.com/library/hh758176.aspx) sur site de Microsoft TechNet hello. Ce dernier contient également des informations relatives aux configurations prises en charge sur lesquelles Azure Backup Server peut être déployé et utilisé.

Vous pouvez utiliser ces toogain articles une meilleure compréhension de la protection de la charge de travail à l’aide de Microsoft Azure sauvegarde du serveur.

* [Sauvegarde SQL Server](backup-azure-backup-sql.md)
* [Sauvegarde de serveur SharePoint](backup-azure-backup-sharepoint.md)
* [Sauvegarde sur un autre serveur](backup-azure-alternate-dpm-server.md)
