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
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="bf44d-103">Sauvegarder un tooAzure du serveur Exchange sauvegarde avec Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="bf44d-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="bf44d-104">Cet article décrit comment tooback de Microsoft Azure Backup Server (MABS) tooconfigure d’un tooAzure de serveur Microsoft Exchange.</span><span class="sxs-lookup"><span data-stu-id="bf44d-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bf44d-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf44d-105">Prerequisites</span></span>
<span data-ttu-id="bf44d-106">Avant de continuer, assurez-vous que le serveur de sauvegarde Azure est [installé et prêt](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="bf44d-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="bf44d-107">Agent de protection du serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="bf44d-107">MABS protection agent</span></span>
<span data-ttu-id="bf44d-108">tooinstall hello MABS l’agent de protection sur le serveur Exchange de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="bf44d-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="bf44d-109">Assurez-vous que les pare-feux hello est correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="bf44d-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="bf44d-110">Consultez [configurer des exceptions de pare-feu pour l’agent de hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf44d-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="bf44d-111">Installer l’agent de hello sur le serveur Exchange de hello en cliquant sur **Gestion > Agents > installer** dans la Console Administrateur de MABS.</span><span class="sxs-lookup"><span data-stu-id="bf44d-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="bf44d-112">Consultez [installer l’agent de protection hello MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="bf44d-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="bf44d-113">Créer un groupe de protection pour Exchange server de hello</span><span class="sxs-lookup"><span data-stu-id="bf44d-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="bf44d-114">Dans la Console Administrateur de MABS de hello, cliquez sur **Protection**, puis cliquez sur **nouveau** sur Bonjour outil ruban tooopen Bonjour **créer un nouveau groupe de Protection** Assistant.</span><span class="sxs-lookup"><span data-stu-id="bf44d-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="bf44d-115">Sur hello **Bienvenue** écran de hello, cliquez sur Assistant **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="bf44d-116">Sur hello **sélectionner le type de groupe de protection** , sélectionnez **serveurs** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="bf44d-117">Base de données Sélectionnez hello Exchange server que vous souhaitez tooprotect, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf44d-118">Si vous protégez Exchange 2013, vérifiez hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf44d-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="bf44d-119">Bonjour l’exemple suivant, la base de données hello Exchange 2010 est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="bf44d-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="bf44d-121">Sélectionnez la méthode de protection des données hello.</span><span class="sxs-lookup"><span data-stu-id="bf44d-121">Select hello data protection method.</span></span>

    <span data-ttu-id="bf44d-122">Nom de groupe de protection hello et sélectionnez les deux hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf44d-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="bf44d-123">Je souhaite une protection à court terme à l’aide de Disque.</span><span class="sxs-lookup"><span data-stu-id="bf44d-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="bf44d-124">Je voudrais une protection en ligne.</span><span class="sxs-lookup"><span data-stu-id="bf44d-124">I want online protection.</span></span>
6. <span data-ttu-id="bf44d-125">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-125">Click **Next**.</span></span>
7. <span data-ttu-id="bf44d-126">Sélectionnez hello **l’intégrité des données toocheck exécuter Eseutil** option si vous souhaitez que l’intégrité de hello toocheck des bases de données Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="bf44d-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="bf44d-127">Une fois que vous sélectionnez cette option, la vérification de cohérence de sauvegarde sur est exécutée MABS tooavoid hello d’e/s le trafic généré en exécutant hello **eseutil** commande sur le serveur Exchange de hello.</span><span class="sxs-lookup"><span data-stu-id="bf44d-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf44d-128">toouse cette option, vous devez copier hello Ese.dll et le répertoire C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin toohello des fichiers Eseutil.exe sur le serveur d’AMC hello.</span><span class="sxs-lookup"><span data-stu-id="bf44d-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="bf44d-129">Dans le cas contraire, hello l’erreur suivante est déclenchée :</span><span class="sxs-lookup"><span data-stu-id="bf44d-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="bf44d-130">![erreur eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="bf44d-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="bf44d-131">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-131">Click **Next**.</span></span>
9. <span data-ttu-id="bf44d-132">Base de données Sélectionnez hello pour **sauvegarde de copie**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf44d-133">Si vous ne sélectionnez pas « Sauvegarde complète » pour au moins une copie DAG d’une base de données, les journaux ne seront pas tronqués.</span><span class="sxs-lookup"><span data-stu-id="bf44d-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="bf44d-134">Configurer les objectifs de hello pour **sauvegarde à court terme**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="bf44d-135">Passez en revue l’espace disque disponible hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="bf44d-136">Sélectionnez heure hello à quels hello AMC serveur sera créé, la réplication initiale hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="bf44d-137">Sélectionnez les options de vérification de cohérence hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="bf44d-138">Choisissez hello la base de données que vous souhaitez tooback les tooAzure, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="bf44d-139">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bf44d-139">For example:</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="bf44d-141">Définir la planification de hello pour **Azure Backup**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="bf44d-142">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="bf44d-142">For example:</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="bf44d-144">Notez que les points de récupération en ligne sont basés sur des points de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="bf44d-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="bf44d-145">Par conséquent, vous devez planifier un point de récupération hello après hello est spécifié pour hello express point de récupération complète.</span><span class="sxs-lookup"><span data-stu-id="bf44d-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="bf44d-146">Configurer la stratégie de rétention hello pour **Azure Backup**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="bf44d-147">Choisissez une option de réplication en ligne, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="bf44d-148">Si vous avez une base de données volumineux, il peut prendre beaucoup de temps pour toobe sauvegarde initiale hello créée via le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="bf44d-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="bf44d-149">tooavoid ce problème, vous pouvez créer une sauvegarde hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bf44d-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="bf44d-151">Confirmez les paramètres de hello, puis cliquez sur **créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="bf44d-152">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="bf44d-153">Récupérer la base de données Exchange hello</span><span class="sxs-lookup"><span data-stu-id="bf44d-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="bf44d-154">toorecover une base de données Exchange, cliquez sur **récupération** Bonjour Console MABS administrateur.</span><span class="sxs-lookup"><span data-stu-id="bf44d-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="bf44d-155">Localisez la base de données Exchange hello que vous souhaitez toorecover.</span><span class="sxs-lookup"><span data-stu-id="bf44d-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="bf44d-156">Sélectionnez un point de récupération en ligne à partir de hello *temps de récupération* liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="bf44d-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="bf44d-157">Cliquez sur **récupérer** toostart hello **Assistant récupération**.</span><span class="sxs-lookup"><span data-stu-id="bf44d-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="bf44d-158">Pour les points de récupération en ligne, il existe cinq types de récupération :</span><span class="sxs-lookup"><span data-stu-id="bf44d-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="bf44d-159">**Récupérer l’emplacement du serveur Exchange toooriginal :** les données de salutation sera récupérée toohello d’origine Exchange server.</span><span class="sxs-lookup"><span data-stu-id="bf44d-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="bf44d-160">**Récupérer la base de données tooanother sur un serveur Exchange :** les données de salutation seront récupérés tooanother de base de données sur un autre serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="bf44d-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="bf44d-161">**Récupérer tooa de base de données de récupération :** les données de salutation seront récupéré tooan de base de données de récupération Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="bf44d-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="bf44d-162">**Copier le dossier réseau tooa :** les données de salutation sera récupérée tooa dossier du réseau.</span><span class="sxs-lookup"><span data-stu-id="bf44d-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="bf44d-163">**Copiez tootape :** si vous avez une bibliothèque de bandes ou un lecteur de bande autonome attaché et configuré sur MABS, point de récupération hello seront copiés les bandes libres tooa.</span><span class="sxs-lookup"><span data-stu-id="bf44d-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Choisir la réplication en ligne](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="bf44d-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf44d-165">Next steps</span></span>
* [<span data-ttu-id="bf44d-166">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="bf44d-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
