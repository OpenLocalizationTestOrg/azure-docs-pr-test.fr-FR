---
title: "tooback d’Azure Backup Server aaaUse portail classique de charges de travail tooAzure | Documents Microsoft"
description: "Assurez-vous que votre environnement est correctement préparé tooback des charges de travail à l’aide d’Azure Backup Server"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "serveur de sauvegarde Azure ; coffre de sauvegarde"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Préparation de tooback des charges de travail à l’aide d’Azure Backup Server
> [!div class="op_single_selector"]
> * [Azure Backup Server](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (Classic)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (Classic)](backup-azure-dpm-introduction-classic.md)
>
>

Cet article porte sur la préparation de votre tooback environnement des charges de travail à l’aide d’Azure Backup Server. Avec Azure Backup Server, vous pouvez protéger des charges de travail d’application telles que les machines virtuelles Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange et les clients Windows à partir d’une console unique :

> [!WARNING]
> Serveur de sauvegarde Azure hérite des fonctionnalités de hello de Data Protection Manager (DPM) pour la sauvegarde de la charge de travail. Vous trouverez des pointeurs documentation tooDPM pour certaines de ces fonctionnalités. Cependant, le serveur Microsoft Azure Backup ne fournit pas de protection sur bande et ne s’intègre pas à System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Machine Windows Server
![étape 1](./media/backup-azure-microsoft-azure-backup/step1.png)

première étape de Hello la route hello Azure Backup Server est toohave un ordinateur Windows Server.

| Lieu | Configuration minimale requise | Instructions supplémentaires |
| --- | --- | --- |
| Microsoft Azure |Machine virtuelle IaaS Azure<br><br>Standard A2 : 2 cœurs, 3,5 Go de RAM |Vous pouvez démarrer avec une simple image de la galerie de Windows Server 2012 R2 Datacenter. [La protection des charges de travail IaaS à l’aide d’Azure Backup Server (DPM)](https://technet.microsoft.com/library/jj852163.aspx) peut prendre plusieurs formes. Veillez à lire l’article de hello complètement avant de déployer l’ordinateur de hello. |
| Local |Machine virtuelle Hyper-V,<br> Machine virtuelle VMWare,<br> ou un hôte physique<br><br>2 cœurs et 4 Go de RAM |Vous pouvez dédupliquer le stockage DPM hello à l’aide de la déduplication de Windows Server. En savoir plus sur le fonctionnement du [DPM et de la déduplication](https://technet.microsoft.com/library/dn891438.aspx) en cas de déploiement sur des ordinateurs virtuels Hyper-V. |

> [!NOTE]
> Il est conseillé d’installer Azure Backup Server sur un ordinateur équipé de Windows Server 2012 R2 Datacenter. Un grand nombre de conditions préalables de hello sont traités automatiquement avec la version la plus récente du système d’exploitation de Windows hello hello.
>
>

Si vous envisagez de domaine de tooa toojoin Azure Backup Server, il est recommandé de joindre les serveurs physiques hello ou domaine toohello de machine virtuelle avant d’installer le logiciel de sauvegarde du serveur Azure hello. Le déplacement d’un serveur de sauvegarde Azure tooa nouveau domaine, après le déploiement, est *ne pas pris en charge*.

## <a name="2-backup-vault"></a>2. Archivage de sauvegarde
![étape 2](./media/backup-azure-microsoft-azure-backup/step2.png)

Si vous envoyez des données de sauvegarde tooAzure ou qu’il soit localement, hello Azure Backup Server doit être inscrit tooa coffre. Si vous êtes un nouvel utilisateur d’Azure Backup et que vous souhaitez toouse Azure Backup Server, consultez hello Azure portail version de cet article - [préparer tooback des charges de travail à l’aide d’Azure Backup Server](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>



## <a name="3-software-package"></a>3. Package logiciel
![étape 3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Téléchargement du package de logiciel hello
Informations d’identification toovault similaires, vous pouvez télécharger Microsoft Azure Backup pour des charges de travail à partir de hello **Page démarrage rapide** hello coffre de sauvegarde.

1. Cliquez sur **pour des charges de travail (tooCloud tooDisk de disque)**. Cette opération prendra page du centre de téléchargement toohello à partir de laquelle logiciel hello peut être téléchargé.

    ![Écran d’accueil Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Cliquez sur **Télécharger**.

    ![Centre de téléchargement 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Sélectionnez tous les fichiers hello et cliquez sur **suivant**. Téléchargement que tous hello fichiers provenant d’une page de téléchargement de Microsoft Azure Backup hello et place que tous les hello dans les fichiers hello même dossier.
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
2. Sur l’écran d’accueil hello, cliquez sur hello **suivant** bouton. Vous accéderez toohello *Prerequisite Checks* section. Dans cet écran, cliquez sur hello **vérifier** bouton toodetermine hello matérielle et logicielle requise pour Azure Backup Server ont été remplies. Si tous hello sont des conditions préalables sont remplies avec succès, vous verrez un message indiquant que l’ordinateur hello répond aux besoins de hello. Cliquez sur hello **suivant** bouton.

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

    étape suivante de Hello est tooconfigure hello Microsoft Azure Recovery Services Agent. Dans le cadre de la configuration de hello, vous aurez tooprovide votre hello coffre informations d’identification tooregister hello machine toohello coffre de sauvegarde. Elle fournit également une phrase secrète tooencrypt/decrypt hello les données envoyées entre Azure et votre environnement local. Vous pouvez automatiquement générer une phrase secrète ou fournir votre propre phrase secrète d’au minimum 16 caractères. Continuer avec l’Assistant de hello jusqu'à ce que l’agent de hello a été configuré.

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
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Serveur de sauvegarde Azure requiert service de sauvegarde Azure toohello de connectivité pour hello produit toowork avec succès. toovalidate si la machine de hello a hello connectivité tooAzure, utilisez hello ```Get-DPMCloudConnection``` applet de commande dans la console du serveur de sauvegarde Azure PowerShell hello. Si hello sortie de l’applet de commande hello est TRUE, puis il existe une connectivité, sinon il n’existe aucune connectivité.

Hello simultanément, hello abonnement Azure doit toobe dans un état sain. toofind état hello de votre abonnement et de toomanage il, ouvrez une session toohello [portal d’abonnement](https://account.windowsazure.com/Subscriptions).

Une fois que vous connaissez état hello hello connectivité Azure et hello abonnement Azure, vous pouvez utiliser la table hello ci-dessous toofind out impact de hello sur les fonctionnalités de sauvegarde/restauration hello offertes.

| État de la connectivité | Abonnement Azure | Sauvegarde tooAzure | Sauvegarde toodisk | Restauration à partir d’Azure | Restauration à partir d’un disque |
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
