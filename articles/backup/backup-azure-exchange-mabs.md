---
title: "aaaBack d’un tooAzure du serveur Exchange sauvegarde avec Azure Backup Server | Documents Microsoft"
description: "Découvrez comment tooback d’un tooAzure du serveur Exchange de sauvegarde à l’aide d’Azure Backup Server"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a>Sauvegarder un tooAzure du serveur Exchange sauvegarde avec Azure Backup Server
Cet article décrit comment tooback de Microsoft Azure Backup Server (MABS) tooconfigure d’un tooAzure de serveur Microsoft Exchange.  

## <a name="prerequisites"></a>Composants requis
Avant de continuer, assurez-vous que le serveur de sauvegarde Azure est [installé et prêt](backup-azure-microsoft-azure-backup.md).

## <a name="mabs-protection-agent"></a>Agent de protection du serveur de sauvegarde Azure
tooinstall hello MABS l’agent de protection sur le serveur Exchange de hello, procédez comme suit :

1. Assurez-vous que les pare-feux hello est correctement configurés. Consultez [configurer des exceptions de pare-feu pour l’agent de hello](https://technet.microsoft.com/library/Hh758204.aspx).
2. Installer l’agent de hello sur le serveur Exchange de hello en cliquant sur **Gestion > Agents > installer** dans la Console Administrateur de MABS. Consultez [installer l’agent de protection hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) pour obtenir des instructions détaillées.

## <a name="create-a-protection-group-for-hello-exchange-server"></a>Créer un groupe de protection pour Exchange server de hello
1. Dans la Console Administrateur de MABS de hello, cliquez sur **Protection**, puis cliquez sur **nouveau** sur Bonjour outil ruban tooopen Bonjour **créer un nouveau groupe de Protection** Assistant.
2. Sur hello **Bienvenue** écran de hello, cliquez sur Assistant **suivant**.
3. Sur hello **sélectionner le type de groupe de protection** , sélectionnez **serveurs** et cliquez sur **suivant**.
4. Base de données Sélectionnez hello Exchange server que vous souhaitez tooprotect, cliquez sur **suivant**.

   > [!NOTE]
   > Si vous protégez Exchange 2013, vérifiez hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).
   >
   >

    Bonjour l’exemple suivant, la base de données hello Exchange 2010 est sélectionné.

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. Sélectionnez la méthode de protection des données hello.

    Nom de groupe de protection hello et sélectionnez les deux hello options suivantes :

   * Je souhaite une protection à court terme à l’aide de Disque.
   * Je voudrais une protection en ligne.
6. Cliquez sur **Suivant**.
7. Sélectionnez hello **l’intégrité des données toocheck exécuter Eseutil** option si vous souhaitez que l’intégrité de hello toocheck des bases de données Exchange Server hello.

    Une fois que vous sélectionnez cette option, la vérification de cohérence de sauvegarde sur est exécutée MABS tooavoid hello d’e/s le trafic généré en exécutant hello **eseutil** commande sur le serveur Exchange de hello.

   > [!NOTE]
   > toouse cette option, vous devez copier hello Ese.dll et le répertoire C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello des fichiers Eseutil.exe sur le serveur d’AMC hello. Dans le cas contraire, hello l’erreur suivante est déclenchée :  
   > ![erreur eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)
   >
   >
8. Cliquez sur **Suivant**.
9. Base de données Sélectionnez hello pour **sauvegarde de copie**, puis cliquez sur **suivant**.

   > [!NOTE]
   > Si vous ne sélectionnez pas « Sauvegarde complète » pour au moins une copie DAG d’une base de données, les journaux ne seront pas tronqués.
   >
   >
10. Configurer les objectifs de hello pour **sauvegarde à court terme**, puis cliquez sur **suivant**.
11. Passez en revue l’espace disque disponible hello, puis cliquez sur **suivant**.
12. Sélectionnez heure hello à quels hello AMC serveur sera créé, la réplication initiale hello, puis cliquez sur **suivant**.
13. Sélectionnez les options de vérification de cohérence hello, puis cliquez sur **suivant**.
14. Choisissez hello la base de données que vous souhaitez tooback les tooAzure, puis cliquez sur **suivant**. Par exemple :

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. Définir la planification de hello pour **Azure Backup**, puis cliquez sur **suivant**. Par exemple :

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > Notez que les points de récupération en ligne sont basés sur des points de récupération complète express. Par conséquent, vous devez planifier un point de récupération hello après hello est spécifié pour hello express point de récupération complète.
    >
    >
16. Configurer la stratégie de rétention hello pour **Azure Backup**, puis cliquez sur **suivant**.
17. Choisissez une option de réplication en ligne, puis cliquez sur **Suivant**.

    Si vous avez une base de données volumineux, il peut prendre beaucoup de temps pour toobe sauvegarde initiale hello créée via le réseau de hello. tooavoid ce problème, vous pouvez créer une sauvegarde hors connexion.  

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. Confirmez les paramètres de hello, puis cliquez sur **créer un groupe**.
19. Cliquez sur **Fermer**.

## <a name="recover-hello-exchange-database"></a>Récupérer la base de données Exchange hello
1. toorecover une base de données Exchange, cliquez sur **récupération** Bonjour Console MABS administrateur.
2. Localisez la base de données Exchange hello que vous souhaitez toorecover.
3. Sélectionnez un point de récupération en ligne à partir de hello *temps de récupération* liste déroulante.
4. Cliquez sur **récupérer** toostart hello **Assistant récupération**.

Pour les points de récupération en ligne, il existe cinq types de récupération :

* **Récupérer l’emplacement du serveur Exchange toooriginal :** les données de salutation sera récupérée toohello d’origine Exchange server.
* **Récupérer la base de données tooanother sur un serveur Exchange :** les données de salutation seront récupérés tooanother de base de données sur un autre serveur Exchange.
* **Récupérer tooa de base de données de récupération :** les données de salutation seront récupéré tooan de base de données de récupération Exchange (RDB).
* **Copier le dossier réseau tooa :** les données de salutation sera récupérée tooa dossier du réseau.
* **Copiez tootape :** si vous avez une bibliothèque de bandes ou un lecteur de bande autonome attaché et configuré sur MABS, point de récupération hello seront copiés les bandes libres tooa.

    ![Choisir la réplication en ligne](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a>Étapes suivantes
* [Azure Backup - Forum Aux Questions](backup-azure-backup-faq.md)
