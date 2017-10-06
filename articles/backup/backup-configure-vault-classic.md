---
title: aaaBack des tooAzure serveur ou station de travail Windows (classique) | Documents Microsoft
description: "Sauvegarde Windows serveurs ou clients tooa coffre de sauvegarde dans Azure. Parcourez les principes de base pour la protection des fichiers et dossiers tooa coffre de sauvegarde à l’aide de l’agent de sauvegarde Azure hello."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: coffre de sauvegarde ; sauvegarder un serveur Windows ; sauvegarder windows ;
ms.assetid: 3b543bfd-8978-4f11-816a-0498fe14a8ba
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: c8f2a9bed1e5885f5c272c65b9282ededc05850a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-workstation-tooazure-using-hello-classic-portal"></a>Sauvegarder un tooAzure serveur ou station de travail Windows à l’aide du portail classique de hello
> [!div class="op_single_selector"]
> * [Portail classique](backup-configure-vault-classic.md)
> * [Portail Azure](backup-configure-vault.md)
>
>

Cet article traite des procédures hello que vous avez besoin de toofollow tooprepare votre environnement et que vous sauvegardez un tooAzure de Windows server (ou une station de travail). Il aborde également les considérations de déploiement de votre solution de sauvegarde. Si vous êtes intéressé par la première tentative Azure Backup pour hello, cet article vous guide rapidement dans les processus hello.

Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique. Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

## <a name="before-you-start"></a>Avant de commencer
tooback un serveur ou un client tooAzure, vous devez un compte Azure. Si vous n’en possédez pas, vous pouvez créer un [compte gratuit](https://azure.microsoft.com/free/) en quelques minutes.

## <a name="create-a-backup-vault"></a>Créer un coffre de sauvegarde
tooback des fichiers et dossiers à partir d’un serveur ou client, vous devez toocreate un coffre de sauvegarde dans la région de hello où vous souhaitez toostore hello données.

> [!IMPORTANT]
> À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique.
>
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> **Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell. <br/> **À compter du 1er novembre 2017** :
>- Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>


## <a name="download-hello-vault-credential-file"></a>Télécharger le fichier d’informations d’identification de coffre hello
ordinateur local, Hello doit toobe authentifiée avec un coffre de sauvegarde avant qu’il peut sauvegarder des données tooAzure. Grâce à l’authentification de Hello *informations d’identification de coffre*. fichier d’informations d’identification de coffre Hello est téléchargé via un canal sécurisé à partir du portail classique de hello. clé privée du certificat Hello n’est pas conservé dans le portail de hello ou un service de hello.

### <a name="toodownload-hello-vault-credential-file-tooa-local-machine"></a>toodownload hello coffre informations d’identification du fichier tooa ordinateur local
1. Dans le volet de navigation gauche hello, cliquez sur **Services de récupération**, puis sélectionnez le coffre de sauvegarde hello que vous avez créé.

    ![RI terminé](./media/backup-configure-vault-classic/rs-left-nav.png)
2. Dans la page de démarrage rapide de hello, cliquez sur **informations d’identification du coffre de téléchargement**.

   portail classique de Hello génère une information d’identification de coffre à l’aide d’une combinaison de nom de l’archivage hello et hello date actuelle. fichier d’informations d’identification de coffre Hello est utilisé uniquement pendant le flux de travail de l’inscription hello et expire au bout de 48 heures.

   fichier d’informations d’identification de coffre Hello peut être téléchargé à partir du portail de hello.
3. Cliquez sur **enregistrer** toodownload hello coffre informations d’identification du fichier toohello dossier Téléchargements du compte local de hello. Vous pouvez également sélectionner **enregistrer en tant que** de hello **enregistrer** menu toospecify un emplacement pour le fichier d’informations d’identification de coffre hello.

   > [!NOTE]
   > Assurez-vous que le fichier d’informations d’identification de coffre hello est enregistré dans un emplacement qui est accessible à partir de votre ordinateur. S’il est stocké dans un bloc de message de partage ou un serveur de fichiers, vérifiez que vous avez hello autorisations tooaccess il.
   >
   >

## <a name="download-install-and-register-hello-backup-agent"></a>Télécharger, installer et inscrire l’agent de sauvegarde hello
Après avoir créé le coffre de sauvegarde hello et téléchargez le fichier d’informations d’identification coffre hello, un agent doit être installé sur chacun de vos ordinateurs Windows.

### <a name="toodownload-install-and-register-hello-agent"></a>toodownload, installer et inscrire l’agent de hello
1. Cliquez sur **Services de récupération**, puis sélectionnez le coffre de sauvegarde hello que vous souhaitez tooregister avec un serveur.
2. Sur la page de démarrage rapide de hello, cliquez sur l’agent de hello **Agent pour Windows Server ou System Center Data Protection Manager ou Windows client**. Cliquez ensuite sur **Enregistrer**.

    ![Enregistrer l’agent](./media/backup-configure-vault-classic/agent.png)
3. Une fois hello MARSagentinstaller.exe fichier téléchargé, cliquez sur **exécuter** (ou double-cliquez sur **MARSAgentInstaller.exe** à partir de l’emplacement de hello enregistré).
4. Choisissez le dossier d’installation hello et le dossier de cache qui sont requis pour l’agent de hello, puis cliquez sur **suivant**. emplacement du cache Hello que vous spécifiez doit avoir tooat égal d’espace libre au moins 5 pour cent des données de sauvegarde hello.
5. Vous pouvez continuer tooconnect toohello Internet via les paramètres de proxy par défaut hello.             Si vous utilisez un toohello tooconnect du serveur proxy Internet, sur la page de Configuration du Proxy hello, sélectionnez hello **utiliser les paramètres de proxy personnalisés** case à cocher, puis entrez les détails du serveur proxy hello. Si vous utilisez un proxy authentifié, entrez les détails des nom et mot de passe utilisateur hello, puis cliquez sur **suivant**.
6. Cliquez sur **installer** installation de l’agent toobegin hello. l’agent de sauvegarde Hello installe .NET Framework 4.5 et Windows PowerShell (si elle n’est pas déjà installé) installation de hello toocomplete.
7. Une fois l’agent de hello est installé, cliquez sur **continuer tooRegistration** toocontinue un flux de travail hello.
8. Sur la page d’Identification de coffre hello, accédez à fichier tooand hello sélectionnez coffre d’informations d’identification que vous avez téléchargé précédemment.

    fichier d’informations d’identification de coffre Hello est valable uniquement des dernières 48 heures après que l’avoir téléchargée à partir du portail de hello. Si vous rencontrez une erreur sur cette page (par exemple, « informations d’identification coffre fichier fourni a expiré »), connectez-vous au portail de toohello et téléchargez à nouveau le fichier d’informations d’identification de coffre hello.

    Assurez-vous que le fichier d’informations d’identification de coffre hello est disponible dans un emplacement qui est accessible par l’application d’installation de hello. Si vous rencontrez des erreurs liées à l’accès, copiez hello coffre informations d’identification du fichier tooa emplacement temporaire sur hello même machine et recommencez l’opération de hello.

    Si vous rencontrez une erreur d’informations d’identification de coffre telles que « coffre non valide les informations d’identification fournies », fichier de hello est endommagé ou ne pas avoir hello dernières informations d’identification associées au service de récupération hello. Recommencez l’opération hello après avoir téléchargé un nouveau fichier d’informations d’identification de coffre à partir du portail de hello. Cette erreur peut également se produire si un utilisateur clique sur hello **informations d’identification du coffre de téléchargement** option plusieurs fois de suite. Dans ce cas, uniquement hello dernière coffre informations d’identification du fichier est valide.
9. Sur la page de paramètres de chiffrement de hello, vous pouvez générer un mot de passe ou fournissez une phrase secrète (avec un minimum de 16 caractères). N’oubliez pas de mot de passe toosave hello dans un emplacement sécurisé.
10. Cliquez sur **Terminer**. Hello Assistant Inscription de serveur inscrit les serveur hello avec sauvegarde.

    > [!WARNING]
    > Si vous perdez ou oubliez le mot de passe hello, Microsoft ne peut vous aider à récupérer les données de sauvegarde hello. Vous possédez hello phrase secrète de chiffrement, et Microsoft n’a pas de visibilité de la phrase secrète hello que vous utilisez. Enregistrez-le hello dans un emplacement sécurisé, car il sera nécessaire pendant une opération de récupération.
    >
    >

11. Une fois la clé de chiffrement hello est définie, laissez hello **lancer Microsoft Azure Recovery Services Agent** case à cocher, puis cliquez sur **fermer**.

## <a name="complete-hello-initial-backup"></a>Sauvegarde initiale de hello terminée
la sauvegarde initiale Hello inclut deux tâches principales :

* Création de planification de sauvegarde hello
* Sauvegarde de fichiers et dossiers pour hello première fois

Stratégie de sauvegarde hello après la sauvegarde initiale de hello, il crée des points de sauvegarde que vous pouvez utiliser si vous avez besoin des données de salutation toorecover. stratégie de sauvegarde Hello cela selon une planification hello que vous définissez.

### <a name="tooschedule-hello-backup"></a>sauvegarde de hello tooschedule
1. Ouvrez hello Microsoft Azure Backup agent. (Il s’ouvre automatiquement si vous avez laissé hello **lancer Microsoft Azure Recovery Services Agent** case à cocher activée lorsque vous avez fermé l’Assistant Inscription de serveur de hello.) Vous pouvez le trouver en recherchant **Microsoft Azure Backup**sur votre ordinateur.

    ![Lancez l’agent de sauvegarde Azure hello](./media/backup-configure-vault-classic/snap-in-search.png)
2. Dans l’agent de sauvegarde hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-configure-vault-classic/schedule-backup-close.png)
3. Sur hello mise en route de la page de hello Assistant Planification de sauvegarde, cliquez sur **suivant**.
4. Page de tooBackup hello sélectionner les éléments, cliquez sur **ajouter les éléments**.
5. Sélectionnez les fichiers de hello et dossiers que vous souhaitez tooback haut, puis cliquez sur **OK**.
6. Cliquez sur **Suivant**.
7. Sur hello **spécifier la planification de sauvegarde** , spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.

    Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.

    ![Éléments de sauvegarde de Windows Server](./media/backup-configure-vault-classic/specify-backup-schedule-close.png)

   > [!NOTE]
   > Pour plus d’informations sur comment toospecify hello planification de sauvegarde, voir l’article hello [tooreplace utilisez Azure Backup votre infrastructure de bande](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. Sur hello **sélectionner la stratégie de rétention** page, sélectionnez hello **stratégie de rétention** de copie de sauvegarde hello.

    stratégie de rétention Hello spécifie la durée hello pour lequel hello sauvegarde sera stockée. Plutôt que de simplement spécifier « stratégie plate » pour tous les points de sauvegarde, vous pouvez spécifier des stratégies de rétention différentes basées sur lors de la sauvegarde de hello se produit. Vous pouvez modifier toomeet de stratégies de rétention quotidienne, hebdomadaire, mensuel et annuel hello à vos besoins.
9. Sur la page Choisir un Type de sauvegarde initiale de hello, choisissez le type de sauvegarde initiale hello. Conservez l’option hello **automatiquement sur le réseau de hello** sélectionné, puis cliquez sur **suivant**.

    Vous pouvez sauvegarder automatiquement sur le réseau de hello, ou vous pouvez sauvegarder en mode hors connexion. reste Hello de cet article décrit le processus hello pour sauvegarder automatiquement. Si vous préférez toodo une sauvegarde hors connexion, consultez l’article de hello [workflow de sauvegarde en mode hors connexion dans Azure Backup](backup-azure-backup-import-export.md) pour plus d’informations.
10. Sur la page de Confirmation hello, passez en revue les informations de hello, puis cliquez sur **Terminer**.
11. Une fois l’Assistant de hello ait fini de créer la planification de sauvegarde hello, cliquez sur **fermer**.

### <a name="enable-network-throttling-optional"></a>Activer la limitation du réseau (facultatif)
l’agent de sauvegarde Hello fournit la limitation du réseau. La limitation contrôle l’utilisation de la bande passante réseau durant le transfert de données. Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic Internet. La limitation s’applique tooback des activités et de restauration.

**la limitation réseau tooenable**

1. Dans l’agent de sauvegarde hello, cliquez sur **modifier les propriétés**.

    ![Modifier les propriétés](./media/backup-configure-vault-classic/change-properties.png)
2. Sur hello **limitation** onglet, sélectionnez hello **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation** case à cocher.

    ![Limitation du réseau](./media/backup-configure-vault-classic/throttling-dialog.png)
3. Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.

    valeurs de la bande passante Hello commencent à 512 kilobits par seconde (Kbits/s) et peuvent atteindre la too1, 023 mégaoctets par seconde (Mbits/s). Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont des jours de travail pris en compte. Les heures non comprises dans les heures de travail définies sont considérées comme des heures chômées.
4. Cliquez sur **OK**.

### <a name="tooback-up-now"></a>tooback maintenant
1. Dans l’agent de sauvegarde hello, cliquez sur **sauvegarder maintenant** hello toocomplete initiale d’amorçage réseau hello.

    ![Sauvegarder Windows Server maintenant](./media/backup-configure-vault-classic/backup-now.png)
2. Sur la page de Confirmation hello, vérifier les paramètres hello qui hello Assistant sauvegarder maintenant utilisera tooback machine de hello. puis cliquez sur **Sauvegarder**.
3. Cliquez sur **fermer** Assistant de hello tooclose. Si vous procédez ainsi avant la fin du processus de sauvegarde hello, Assistant de hello continue toorun en arrière-plan de hello.

Une fois la sauvegarde initiale de hello est terminée, hello **fin du travail** état s’affiche dans la console de sauvegarde hello.

![RI terminé](./media/backup-configure-vault-classic/ircomplete.png)

## <a name="next-steps"></a>Étapes suivantes
* Ouvrir [gratuitement un compte Azure](https://azure.microsoft.com/free/).

Pour plus d’informations sur la sauvegarde des machines virtuelles ou d’autres charges de travail, consultez les références suivantes :

* [Sauvegarder des machines virtuelles IaaS](backup-azure-vms-prepare.md)
* [Sauvegarder tooAzure les charges de travail avec Microsoft Azure Backup Server](backup-azure-microsoft-azure-backup.md)
* [Sauvegarder tooAzure les charges de travail avec DPM](backup-azure-dpm-introduction.md)
